Wake-on-LAN (WOL) is a feature to switch on a computer via a network connection (be it the internet or intranet).

## Contents

*   [1 Hardware settings](#Hardware_settings)
*   [2 Software configuration](#Software_configuration)
    *   [2.1 netctl](#netctl)
    *   [2.2 systemd-networkd](#systemd-networkd)
    *   [2.3 systemd service](#systemd_service)
    *   [2.4 udev](#udev)
    *   [2.5 cron](#cron)
    *   [2.6 NetworkManager](#NetworkManager)
*   [3 Trigger a wake up](#Trigger_a_wake_up)
    *   [3.1 On the same LAN](#On_the_same_LAN)
    *   [3.2 With port forwarding](#With_port_forwarding)
    *   [3.3 Across the internet](#Across_the_internet)
*   [4 Miscellaneous](#Miscellaneous)
    *   [4.1 Battery draining problem](#Battery_draining_problem)
    *   [4.2 Example WOL script](#Example_WOL_script)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Realtek](#Realtek)
    *   [5.2 Suspend/Resume](#Suspend.2FResume)
*   [6 See also](#See_also)

## Hardware settings

The target computer's motherboard and [NIC](https://en.wikipedia.org/wiki/NIC "wikipedia:NIC") have to support Wake-on-LAN. Wireless cards do not support Wake-on-LAN, so the target computer has to be physically connected (i.e. by cable) to router or the source computer.

The Wake-on-LAN feature also has to be enabled in the PC's BIOS. Different motherboard manufactures use slightly different language for this feature. Look for terminology such as "PCI Power up", "Allow PCI wake up event" or "Boot from PCI/PCI-E".

It is known that some motherboards are affected by a nasty bug that causes reboots rather than shutdowns under certain situations (see [this](https://bbs.archlinux.org/viewtopic.php?id=173648) thread for example). To prevent this bug from surfacing, it is recommended to do the following on the target machine:

1.  Disable all references to "xHCI" as it pertains to USB settings.
2.  Disable EuP 2013 if it is explicitly an option.
3.  Optionally enable WOL for keyboard actions.

**Note:** There are mixed opinions as to the value of #3 above and it may be motherboard dependent.

## Software configuration

Depending on the hardware, the network drivers may have WOL switched off by default. To query this status or to change the settings, install [ethtool](https://www.archlinux.org/packages/?name=ethtool).

Query the network device via this command:

 `# ethtool net0 | grep Wake-on` 
```
        Supports Wake-on: pumbag
	Wake-on: d

```

The values define what activity to wake on: `d` (disabled), `p` (PHY activity), `u` (unicast activity), `m` (multicast activity), `b` (broadcast activity), `a` (ARP activity), and `g` (magic packet activity). The value of `g` is required for WOL to work.

To enable the WOL feature in the driver:

```
# ethtool -s net0 wol g

```

This command might not last beyond the next reboot, so it must be repeated via some mechanism. Common solutions are listed in the following subsections.

### netctl

If using netctl, one can make this setting persistent by adding the following the netctl profile:

 `/etc/netctl/*profile*`  `ExecUpPost='/usr/bin/ethtool -s net0 wol g'` 

### systemd-networkd

If [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") is used to setup machine's network then it is easy to enable Wake-On-Lan using `systemd.link` configuration. Add `WakeOnLan` option to the network link file:

 `/etc/systemd/network/50-wired.link` 
```
[Link]
WakeOnLan=magic
...
```

See [systemd-networkd#link files](/index.php/Systemd-networkd#link_files "Systemd-networkd") and `man systemd.link` for more information.

### systemd service

This is an equivalent of previous `systemd.link` option, but uses a standalone systemd service.

 `/etc/systemd/system/wol@.service` 
```
[Unit]
Description=Wake-on-LAN for %i
Requires=network.target
After=network.target

[Service]
ExecStart=/usr/bin/ethtool -s %i wol g
Type=oneshot

[Install]
WantedBy=multi-user.target
```

Alternatively install the [wol-systemd](https://aur.archlinux.org/packages/wol-systemd/) package.

Then activate this new service by [starting](/index.php/Starting "Starting") `wol@*interface*.service`.

### udev

[udev](/index.php/Udev "Udev") is capable of running any command as soon as a device is visible. The following rule will turn on WOL on all [network interfaces](/index.php/Network_interface "Network interface") whose name matches `enp*`:

 `/etc/udev/rules.d/99-wol.rules` 
```
ACTION=="add", SUBSYSTEM=="net", NAME=="enp*", RUN+="/usr/bin/ethtool -s $name wol g"

```

The `$name` placeholder will be replaced by the value of the `NAME` variable for the matched device.

**Note:** The name of the configuration file is important. Due to the introduction of [persistent device names](/index.php/Network_configuration#Device_names "Network configuration") in systemd v197, it is important that the rules matching a specific network interface are named lexicographically after `80-net-name-slot.rules`, so that they are applied after the devices gain the persistent names.

### cron

A command can be run each time the computer is (re)booted using "@reboot" in a crontab. First, make sure [cron](/index.php/Cron#Installation "Cron") is enabled, and then [edit a crontab](/index.php/Cron#Basic_commands "Cron") for the root user that contains the following line:

```
@reboot /usr/bin/ethtool -s [net-device] wol g

```

### NetworkManager

In version 1.0.6 NetworkManager [adds Wake-on-LAN controls](https://www.phoronix.com/scan.php?page=news_item&px=NetworkManager-WoL-Control). One way to enable Wake-on-LAN by magic packet is through nmcli.

First, search for the name of the wired connection:

 `# nmcli con show` 
```
NAME    UUID                                  TYPE            DEVICE
wired1  612e300a-c047-4adb-91e2-12ea7bfe214e  802-3-ethernet  enp0s25
```

By following, one can view current status of Wake-on-LAN settings:

 `# nmcli c show "wired1" | grep 802-3-ethernet.wake-on-lan` 
```
802-3-ethernet.wake-on-lan:             default
802-3-ethernet.wake-on-lan-password:    --
```

Enable Wake-on-LAN by magic packet on that connection:

```
# nmcli c modify "wired1" 802-3-ethernet.wake-on-lan magic

```

Then reboot, possibly two times.

## Trigger a wake up

To trigger WOL on a target machine, its MAC address and external or internal IP should be known.

To obtain the internal IP address and MAC address of the target computer, execute the following command:

 `$ ip addr` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
      valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host
      valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc fq_codel master br0 state UP group default qlen 1000
    link/ether **48:05:ca:09:0e:6a** brd ff:ff:ff:ff:ff:ff
    inet **192.168.1.20/24** brd 192.168.1.255 scope global br0
       valid_lft forever preferred_lft forever
    inet6 fe80::6a05:caff:fe09:e6a/64 scope link
       valid_lft forever preferred_lft forever

```

Here the internal IP address is `192.168.1.20` and the MAC address is `48:05:ca:09:0e:6a`.

One program able to send magic packets for WOL is [wol](https://www.archlinux.org/packages/?name=wol).

### On the same LAN

If you are connected directly to another computer through a network cable, or the traffic within a LAN is not firewalled, then using Wake-on-LAN should be very easy since there is no need to worry about port redirects.

In the simplest case the default broadcast address `255.255.255.255` is used:

```
$ wol *target_MAC_address*

```

To broadcast the magic packet only to a specific subnet or host, use the `-i` switch:

```
$ wol -i *target_IP* *target_MAC_address*

```

**Tip:** If you intend to continue using Wake-on-LAN, it is recommended to assign a static IP address to the target computer.

### With port forwarding

When the source and target computers are separated by a router, Wake-on-LAN can be used via [port forwarding](https://en.wikipedia.org/wiki/Port_forwarding "wikipedia:Port forwarding"). The router must be instructed to forward any signal heading for a specific port to the internal IP of the target PC. See for example [Firewalls](/index.php/Firewalls "Firewalls") for configuration details.

To trigger the wakeup:

```
$ wol -p *forwarded_port* -i *router_IP* *target_MAC_address*

```

In case of multiple computers behind the router, it is recommended to assign a different port forward to each target IP.

### Across the internet

The syntax needed in this case:

```
$ wol -p *target_port* -i *target_IP_or_hostname* *target_MAC_address*

```

*   Assuming that you know the external IP of the target machine, and that the [router ports](#With_port_forwarding) on both sides have been forwarding correctly, then this should be exactly as the syntax states.

Usually it is necessary to forward your wol port (typically UDP 9) to the broadcast address on your network, not to a particular IP. Most routers do not allow you to forward to broadcast, however if you can get shell access to your router (through telnet, ssh, serial cable, etc) you can implement this workaround:

```
$ ip neighbor add 192.168.1.254 lladdr FF:FF:FF:FF:FF:FF dev net0

```

(The above command assumes your network is 192.168.1.0/24 and use net0 as network interface). Now, forward UDP port 9 to 192.168.1.254\. This has worked for me on a Linksys WRT54G running Tomato, and on the Verizon FIOS ActionTec router.

For notes on how to do it on DD-WRT routers, see [this tutorial](http://www.dd-wrt.com/wiki/index.php/WOL#Remote_Wake_On_LAN_via_Port_Forwarding).

## Miscellaneous

### Battery draining problem

Some laptops have a battery draining problem after shutdown [[1]](http://ubuntuforums.org/archive/index.php/t-1729782.html). This might be caused by enabled WOL. To solve this problem, disable it by using ethtool as mentioned above.

```
# ethtool -s net0 wol d

```

### Example WOL script

Here is a script to automate WOL to several different machines:

```
#!/bin/bash

# definition of MAC addresses
monster=01:12:46:82:ab:4f
chronic=00:3a:53:21:bc:30
powerless=1a:32:41:02:29:92
ghost=01:1a:d2:56:6b:e6

while [ "$input1" != quit ]; do
echo "Which PC to wake?"
echo "p) powerless"
echo "m) monster"
echo "c) chronic"
echo "g) ghost"
echo "b) wake monster, wait 40sec, then wake chronic"
echo "q) quit and take no action"
read input1
  if [ $input1 == p ]; then
  /usr/bin/wol $powerless
  exit 1
fi

if [ $input1 == m ]; then
  /usr/bin/wol $monster
  exit 1
fi

if [ $input1 == c ]; then
  /usr/bin/wol $chronic
  exit 1
fi

# this line requires an IP address in /etc/hosts for ghost
# and should use wol over the internet provided that port 9
# is forwarded to ghost on ghost's router

if [ $input1 == g ]; then
  /usr/bin/wol -v -h -p 9 ghost $ghost
  exit 1
fi

if [ $input1 == b ]; then
  /usr/bin/wol $monster
  echo "monster sent, now waiting for 40sec then waking chronic"
  sleep 40
  /usr/bin/wol $chronic
  exit 1
fi

if [ $input1 == Q ] || [ $input1 == q ]; then
echo "later!"
exit 1
fi

done
echo  "this is the (quit) end!! c-ya!"

```

## Troubleshooting

### Realtek

Users with Realtek 8168 8169 8101 8111(C) based NICs (cards / and on-board) may notice a problem where the NIC seems to be disabled on boot and has no Link light. See [Network configuration#Realtek no link / WOL problem](/index.php/Network_configuration#Realtek_no_link_.2F_WOL_problem "Network configuration")

### Suspend/Resume

If the computer does not wake after suspend/hibernate when using [TLP](/index.php/TLP "TLP"), set the `WOL_DISABLE` value to `N` in `/etc/default/tlp`.

## See also

*   [Wake-On-Lan](http://www.depicus.com/wake-on-lan/woli.aspx)