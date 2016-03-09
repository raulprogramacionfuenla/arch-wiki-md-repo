[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) is a cross-platform [supplicant](https://en.wikipedia.org/wiki/Supplicant_(computer) with support for WEP, WPA and WPA2 ([IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i "wikipedia:IEEE 802.11i") / RSN (Robust Secure Network)). It is suitable for desktops, laptops and embedded systems.

*wpa_supplicant* is the IEEE 802.1X/WPA component that is used in the client stations. It implements key negotiation with a WPA authenticator and it controls the roaming and IEEE 802.11 authentication/association of the wireless driver.

## Contents

*   [1 Installation](#Installation)
*   [2 Overview](#Overview)
*   [3 Connecting with wpa_cli](#Connecting_with_wpa_cli)
*   [4 Connecting with wpa_passphrase](#Connecting_with_wpa_passphrase)
*   [5 Advanced usage](#Advanced_usage)
    *   [5.1 Configuration](#Configuration)
    *   [5.2 Connection](#Connection)
        *   [5.2.1 Manual](#Manual)
        *   [5.2.2 At boot (systemd)](#At_boot_.28systemd.29)
    *   [5.3 wpa_cli action script](#wpa_cli_action_script)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 nl80211 driver not supported on some hardware](#nl80211_driver_not_supported_on_some_hardware)
    *   [6.2 Problem with mounted network shares (cifs) and shutdown (Date: 1st Oct. 2015)](#Problem_with_mounted_network_shares_.28cifs.29_and_shutdown_.28Date:_1st_Oct._2015.29)
    *   [6.3 Password-related problems](#Password-related_problems)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) package.

Optionally also install [wpa_supplicant_gui](https://www.archlinux.org/packages/?name=wpa_supplicant_gui), which provides *wpa_gui*, a graphical front-end for *wpa_supplicant*.

## Overview

The first step to connect to an encrypted wireless network is having *wpa_supplicant* obtain authentication from a WPA authenticator. In order to do this, *wpa_supplicant* must be configured so that it will be able to submit the correct credentials to the authenticator.

Once the authentication is successful, it will be possible to connect to the network by normally obtaining an IP address by setting it manually with the [iproute2](/index.php/Core_utilities#ip "Core utilities") suite or using some networking program, like [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") or [dhcpcd](/index.php/Dhcpcd "Dhcpcd"), to configure an *interface* to obtain an IP address automatically via DHCP. See also the [wireless](/index.php/Wireless_network_configuration#Systemd_with_wpa_supplicant_and_static_IP "Wireless network configuration") and [wired](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") network configuration articles for methods and examples.

## Connecting with wpa_cli

This connection method allows scanning for the available networks, making use of *wpa_cli*, a command line tool which can be used to interactively configure *wpa_supplicant* at runtime. See [wpa_cli(8)](http://linux.die.net/man/8/wpa_cli) for details.

In order to use *wpa_cli*, a control interface must be specified for *wpa_supplicant*, and it must be given the rights to update the configuration. Do this by creating a minimal configuration file:

 `/etc/wpa_supplicant/example.conf` 
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Now start *wpa_supplicant* with:

```
# wpa_supplicant -B -i *interface* -c /etc/wpa_supplicant/example.conf

```

**Tip:** To discover your wireless network interface name, issue the `ip link` command.

At this point run:

```
# wpa_cli

```

This will present an interactive prompt (`>`), which has tab completion and descriptions of completed commands.

**Tip:** The default location of the control socket is `/var/run/wpa_supplicant/`, custom path can be set manually with the `-p` option to match the *wpa_supplicant* configuration. It is also possible to specify the interface to be configured with the `-i` option, otherwise the first found wireless interface managed by *wpa_supplicant* will be used.

Use the `scan` and `scan_results` commands to see the available networks:

```
> scan
OK
<3>CTRL-EVENT-SCAN-RESULTS
> scan_results
bssid / frequency / signal level / flags / ssid
00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MYSSID
11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ANOTHERSSID

```

To associate with `MYSSID`, add the network, set the credentials and enable it:

```
> add_network
0
> set_network 0 ssid "MYSSID"
> set_network 0 psk "passphrase"
> enable_network 0
<2>CTRL-EVENT-CONNECTED - Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]

```

If the SSID does not have password authentication, you must explicitly configure the network as keyless by replacing the command `set_network 0 psk "passphrase"` with `set_network 0 key_mgmt NONE`.

**Note:**

*   Each network is indexed numerically, so the first network will have index 0.
*   The [PSK](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") is computed from the *quoted* "passphrase" string, as also shown by the [wpa_passphrase](#Connecting_with_wpa_passphrase) command. Nonetheless, you can enter the PSK directly by passing it to `psk` *without* quotes.

Finally save this network in the configuration file:

```
> save_config
OK

```

Once association is complete, all that is left to do is obtain an IP address as indicated in the [#Overview](#Overview), for example:

```
# dhcpcd *interface*

```

## Connecting with wpa_passphrase

This connection method allows quickly connecting to a network whose SSID is already known, making use of *wpa_passphrase*, a command line tool which generates the minimal configuration needed by *wpa_supplicant*. For example:

 `$ wpa_passphrase MYSSID passphrase` 
```
network={
    ssid="MYSSID"
    #psk="passphrase"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

This means that *wpa_supplicant* can be associated with *wpa_passphrase* and simply started with:

```
# wpa_supplicant -B -i *interface* -c <(wpa_passphrase MYSSID passphrase)

```

**Note:** Because of the process substitution, you **cannot** run this command with [sudo](/index.php/Sudo "Sudo") - you will need a root shell. Just pre-pending *sudo* will lead to the following error:
```
Successfully initialized wpa_supplicant
Failed to open config file '/dev/fd/63', error: No such file or directory
Failed to read or parse configuration '/dev/fd/63'

```
See also [Help:Reading#Regular user or root](/index.php/Help:Reading#Regular_user_or_root "Help:Reading").

**Tip:**

*   Use quotes, if the input contains spaces. For example: `"secret passphrase"`
*   To discover your wireless network interface name, issue the `ip link` command.
*   Some unusually complex passphrases may require input from a file, e.g. `wpa_passphrase MYSSID < passphrase.txt`, or here strings, e.g. `wpa_passphrase MYSSID <<< "passphrase"`.

Finally, you should obtain an IP address as indicated in the [#Overview](#Overview), for example:

```
# dhcpcd *interface*

```

## Advanced usage

For networks of varying complexity, possibly employing extensive use of [EAP](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol "wikipedia:Extensible Authentication Protocol"), it will be useful to maintain a customised configuration file. For an overview of the configuration with examples, refer to [wpa_supplicant.conf(5)](http://linux.die.net/man/5/wpa_supplicant.conf); for details on all the supported configuration parameters, refer to the example file `/etc/wpa_supplicant/wpa_supplicant.conf`.

### Configuration

As is clear after reading [#Connecting with wpa_passphrase](#Connecting_with_wpa_passphrase), a basic configuration file can be generated with:

```
# wpa_passphrase MYSSID passphrase > /etc/wpa_supplicant/example.conf

```

This will only create a `network` section. A configuration file with some more common options may look like:

 `/etc/wpa_supplicant/example.conf` 
```
ctrl_interface=/var/run/wpa_supplicant
ctrl_interface_group=wheel
update_config=1
fast_reauth=1
ap_scan=1

network={
    ssid="MYSSID"
    psk=59e0d07fa4c7741797a4e394f38a5c321e3bed51d54ad5fcbd3f84bc7415d73d
}
```

The passphrase can alternatively be defined in clear text by enclosing it in quotes, if the resulting security problems are not of concern:

```
network={
    ssid="MYSSID"
    psk="passphrase"
}
```

If the network does not have a passphrase, e.g. a public Wi-Fi:

```
network={
    ssid="MYSSID"
    key_mgmt=NONE
}
```

Further `network` blocks may be added manually, or using *wpa_cli* as illustrated in [#Connecting with wpa_cli](#Connecting_with_wpa_cli). In order to use *wpa_cli*, a control interface must be set with the `ctrl_interface` option. Setting `ctrl_interface_group=wheel` allows users belonging to such group to execute *wpa_cli*. Also add `update_config=1` so that changes made with *wpa_cli* to `example.conf` can be saved.

`fast_reauth=1` and `ap_scan=1` are the *wpa_supplicant* options active globally at the time of writing. Whether you need them, or other global options too for that matter, depends on the type of network to connect to. If you need other global options, simply copy them over to the file from `/etc/wpa_supplicant/wpa_supplicant.conf`.

Alternatively, `wpa_cli set` can be used to see options' status or set new ones. Multiple network blocks may be appended to this configuration: the supplicant will handle association to and roaming between all of them. The strongest signal defined with a network block usually is connected to by default, one may define `priority=` to influence behaviour.

An advantage to be mentioned in using a customized configuration file at `/etc/wpa_supplicant/wpa_supplicant.conf` is that it is used by default by [dhcpcd](/index.php/Dhcpcd "Dhcpcd"). If you do so, you might want to make a backup of the original and delete the extensive network block examples in it. Otherwise, do not be surprised if your device suddenly connects to networks defined in them. In any case, changes to new versions of the configuration file should of course be [merged](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files").

**Tip:** To configure a network block to a hidden wireless *SSID*, which by definition will not turn up in a regular scan, the option `scan_ssid=1` has to be defined in the network block.

### Connection

#### Manual

First start *wpa_supplicant* command, whose most commonly used arguments are:

*   `-B` - Fork into background.
*   `-c *filename*` - Path to configuration file.
*   `-i *interface*` - Interface to listen on.
*   `-D *driver*` - Optionally specify the driver to be used. For a list of supported drivers see the output of `wpa_supplicant -h`.
    *   `nl80211` is the current standard, but not all wireless chip's modules support it.
    *   `wext` is currently deprecated, but still widely supported.

See [wpa_supplicant(8)](http://linux.die.net/man/8/wpa_supplicant) for the full argument list. For example:

```
# wpa_supplicant -B -i *interface* -c /etc/wpa_supplicant/example.conf

```

followed by a method to obtain an ip address manually as indicated in the [#Overview](#Overview), for example:

```
# dhcpcd *interface*

```

**Tip:** *dhcpcd* has a hook that can lauch *wpa_supplicant* implicitly, see [dhcpcd#10-wpa_supplicant](/index.php/Dhcpcd#10-wpa_supplicant "Dhcpcd").

#### At boot (systemd)

The *wpa_supplicant* package provides multiple [systemd](/index.php/Systemd "Systemd") service files:

*   `wpa_supplicant.service` - uses [D-Bus](/index.php/D-Bus "D-Bus"), recommended for [NetworkManager](/index.php/NetworkManager "NetworkManager") users.
*   `wpa_supplicant@.service` - accepts the interface name as an argument and starts the *wpa_supplicant* daemon for this interface. It reads the configuration file in `/etc/wpa_supplicant/wpa_supplicant-*interface*.conf`.
*   `wpa_supplicant-nl80211@.service` - also interface specific, but explicitly forces the `nl80211` driver (see below). The configuration file path is `/etc/wpa_supplicant/wpa_supplicant-nl80211-*interface*.conf`.
*   `wpa_supplicant-wired@.service` - also interface specific, uses the `wired` driver. The configuration file path is `/etc/wpa_supplicant/wpa_supplicant-wired-*interface*.conf`.

To enable wireless at boot, enable one of the services above on a particular wireless interface. For example:

```
# systemctl enable wpa_supplicant@*interface*

```

Now choose and [enable](/index.php/Enable "Enable") a service to obtain an ip address for the particular *interface* as indicated in the [#Overview](#Overview), for example:

```
# systemctl enable dhcpcd@*interface*

```

**Tip:** *dhcpcd* has a hook that can lauch *wpa_supplicant* implicitly, see [dhcpcd#10-wpa_supplicant](/index.php/Dhcpcd#10-wpa_supplicant "Dhcpcd").

### wpa_cli action script

*wpa_cli* can run in daemon mode and execute a specified script based on events from *wpa_supplicant*. Two events are supported: `CONNECTED` and `DISCONNECTED`. Some [environment variables](/index.php/Environment_variables "Environment variables") are available to the script, see [wpa_cli(8)](http://linux.die.net/man/8/wpa_cli) for details.

The following example will use [desktop notifications](/index.php/Desktop_notifications "Desktop notifications") to notify the user about the events:

```
#!/bin/bash

case "$2" in
    CONNECTED)
        notify-send "WPA supplicant: connection established";
        ;;
    DISCONNECTED)
        notify-send "WPA supplicant: connection lost";
        ;;
esac

```

Remember to make the script executable, then use the `-a` flag to pass the script path to *wpa_cli*:

```
$ wpa_cli -a */path/to/script*

```

## Troubleshooting

**Warning:** Make sure that you are **not** using the default configuration file at `/etc/wpa_supplicant/wpa_supplicant.conf`, which is filled with uncommented examples that will lead to lots of random errors in practice. This is a known packaging bug of the [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) package: [FS#40661](https://bugs.archlinux.org/task/40661).

### nl80211 driver not supported on some hardware

On some (especially old) hardware, *wpa_supplicant* may fail with the following error:

```
Successfully initialized wpa_supplicant
nl80211: Driver does not support authentication/association or connect commands
wlan0: Failed to initialize driver interface

```

This indicates that the standard `nl80211` driver does not support the given hardware. The deprecated `wext` driver might still support the device:

```
# wpa_supplicant -B -i wlan0 **-D wext** -c /etc/wpa_supplicant/example.conf

```

If the command works to connect, and the user wishes to use [systemd](/index.php/Systemd "Systemd") to manage the wireless connection, it is necessary to [edit](/index.php/Systemd#Editing_provided_units "Systemd") the `wpa_supplicant@.service` unit provided by the package and modify the `ExecStart` line accordingly:

 `/etc/systemd/system/wpa_supplicant@.service.d/wext.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/wpa_supplicant -c/etc/wpa_supplicant/wpa_supplicant-%I.conf -i%I **-Dwext**
```

### Problem with mounted network shares (cifs) and shutdown (Date: 1st Oct. 2015)

When you use **WPA supplicant** (wlan) to connect to your network you might have the problem that the shutdown takes a very long time. That is because systemd runs against a 3 minute timeout. The reason is that WPA supplicant is shut down to early and you do not have the network online when systemd tries to unmount your share(-s). As a workaround (fix) you can add the following settings to the `wpa_supplicant.service` file. This can be done by [Systemd#Drop-in snippets](/index.php/Systemd#Drop-in_snippets "Systemd"). The result looks like this:

 `/etc/systemd/system/wpa_supplicant.service.d/override.conf` 
```
[Unit]
After=dbus.service
Before=network.target
Wants=network.target

```

See more about this bug here: [https://github.com/systemd/systemd/issues/1435](https://github.com/systemd/systemd/issues/1435)

This bug is not fixed in version 2.3 of [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant). In version 2.5 they added `Before=network.target` and `Wants=network.target` but still miss `After=dbus.service`. So after an update to 2.5 you can remove the `Before=network.target` and `Wants=network.target` from your `/etc/systemd/system/wpa_supplicant.service.d/override.conf`. After this bug has been fixed you can just remove `/etc/systemd/system/wpa_supplicant.service.d/override.conf`.

### Password-related problems

[wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) may not work properly if directly passed via stdin particularly long or complex passphrases which include special characters. This may lead to errors such as `failed 4-way WPA handshake, PSK may be wrong` when launching [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant).

In order to solve this try using here strings `wpa_passphrase <MYSSID> <<< "<passphrase>"` or passing a file to the `-c` flag instead:

```
$ wpa_supplicant -i <interface> -c /etc/wpa_supplicant/wpa_supplicant.conf

```

In some instances it was found that storing the passphrase cleartext in the `psk` key of the `wpa_supplicant.conf` `network` block gave positive results (see [[1]](http://www.linuxquestions.org/questions/linux-wireless-networking-41/wpa-4-way-handshake-failed-843394/)). However, this approach is rather insecure. Using `wpa_cli` to create this file instead of manually writing it gives the best results most of the time and therefore is the recommended way to proceed.

## See also

*   [WPA Supplicant home](http://hostap.epitest.fi/wpa_supplicant/)
*   [wpa_cli usage examples](https://gist.github.com/buhman/7162560)
*   [wpa_supplicant(8)](http://linux.die.net/man/8/wpa_supplicant)
*   [wpa_supplicant.conf(5)](http://linux.die.net/man/5/wpa_supplicant.conf)
*   [wpa_cli(8)](http://linux.die.net/man/8/wpa_cli)
*   [Kernel.org wpa_supplicant documentation](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)