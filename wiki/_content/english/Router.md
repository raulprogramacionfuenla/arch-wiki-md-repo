This article is a tutorial for turning a computer into an internet gateway/router. To strengthen its security it should not run **any** services available to the outside world. Towards the LAN, run only gateway specific services; especially do not run httpd, ftpd, samba, nfsd, etc. as those belong on a server in the LAN since they introduce security risks.

This article does not attempt to show how to set up a shared connection between two machines using cross-over cables. For a simple internet sharing solution, see [Internet sharing](/index.php/Internet_sharing "Internet sharing").

**Note:** Throughout the article, **intern0** and **extern0** are used as names for the network interfaces. The reasoning is further explained in [#Persistent interface naming](#Persistent_interface_naming).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Requirements](#Hardware_Requirements)
*   [2 Network interface configuration](#Network_interface_configuration)
    *   [2.1 Persistent interface naming](#Persistent_interface_naming)
    *   [2.2 IP configuration](#IP_configuration)
*   [3 ADSL connection/PPPoE](#ADSL_connection/PPPoE)
    *   [3.1 PPPoE configuration](#PPPoE_configuration)
*   [4 DNS and DHCP](#DNS_and_DHCP)
*   [5 Connection sharing](#Connection_sharing)
    *   [5.1 Connection sharing with shorewall](#Connection_sharing_with_shorewall)
    *   [5.2 Manual](#Manual)
*   [6 IPv6 tips](#IPv6_tips)
    *   [6.1 Unique Local Addresses](#Unique_Local_Addresses)
    *   [6.2 Global Unicast Addresses](#Global_Unicast_Addresses)
        *   [6.2.1 Static IPv6 prefix](#Static_IPv6_prefix)
        *   [6.2.2 Acquiring IPv6 prefix via DHCPv6-PD](#Acquiring_IPv6_prefix_via_DHCPv6-PD)
    *   [6.3 Router Advertisement and Stateless Autoconfiguration (SLAAC)](#Router_Advertisement_and_Stateless_Autoconfiguration_(SLAAC))
*   [7 Optional additions](#Optional_additions)
    *   [7.1 UPnP](#UPnP)
    *   [7.2 Remote administration](#Remote_administration)
    *   [7.3 Caching web proxy](#Caching_web_proxy)
    *   [7.4 Time server](#Time_server)
    *   [7.5 Content filtering](#Content_filtering)
    *   [7.6 Traffic shaping](#Traffic_shaping)
        *   [7.6.1 Traffic shaping with shorewall](#Traffic_shaping_with_shorewall)
*   [8 See also](#See_also)

## Hardware Requirements

*   At least 1 GB of hard drive space. The base install will take up around 500MB of space and if you want to use a caching web proxy, you will need to reserve space for the cache as well.
*   At least two physical network interfaces: a gateway connects two networks with each other (actually a router can be made using a single physical interface that underlays two [VLAN](/index.php/VLAN "VLAN") interfaces and is connected to a VLAN-aware switch, so-called router-on-a-stick configuration, but it is not covered in this article). You will need to be able to connect those networks to the same physical computer. One interface must connect to the external network, while the other connects to the internal network.
*   A hub, switch or UTP cable: You need a way to connect the other computers to the gateway

## Network interface configuration

### Persistent interface naming

Systemd automatically chooses unique interface names for all your interfaces. These are persistent and will not change when you reboot. However you might want to rename your interfaces e.g. in order to highlight their different networks to which they connect. Throughout the following sections of this guide, the convention stated below is used:

*   **intern0**: the network card connected to the LAN. On an actual computer it will probably have the name enp2s0, enp1s1, etc.
*   **extern0**: the network card connected to the external network (or WAN). It will probably have the name enp2s0, enp1s1, etc.

You may change the assigned names of your devices via a configuration file using [Systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") described in [Systemd-networkd#Renaming an interface](/index.php/Systemd-networkd#Renaming_an_interface "Systemd-networkd") or by a [udev](/index.php/Udev "Udev")-rule following [Network configuration#Change interface name](/index.php/Network_configuration#Change_interface_name "Network configuration"). Due to the example-rich nature of this article, you might want to choose the names above.

### IP configuration

Now you will need to configure the network interfaces. The best way to do so, is using [netctl](/index.php/Netctl "Netctl") profiles. You will need to create two profiles.

**Note:** If you will be connecting to the Internet only via PPPoE (you have one WAN port) you **do not need** to setup or enable the extern0-profile. See below for more information on configuring PPPoE.
 `/etc/netctl/extern0-profile` 
```
Description='Public Interface.'
Interface=extern0
Connection=ethernet
IP='dhcp'
```
 `/etc/netctl/intern0-profile` 
```
Description='Private Interface'
Interface=intern0
Connection=ethernet
IP='static'
Address=('10.0.0.1/24')
```

**Note:** The example configuration above assumes a full subnet. If you are building the gateway for a small amount of people, you will want to change the [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing "wikipedia:Classless Inter-Domain Routing") suffix to accommodate a smaller range. For example `/27` will give you `10.0.0.1` to `10.0.0.30`. There are many CIDR calculators, online and offline, for example [sipcalc](https://www.archlinux.org/packages/?name=sipcalc).

**Tip:** Use `SkipNoCarrier=yes` in the LAN profile to make sure the connection is enabled even when the guest on LAN is not yet up.

Next, we set up the interfaces with netctl:

```
# netctl enable extern0-profile
# netctl enable intern0-profile

```

## ADSL connection/PPPoE

Using rp-pppoe, we can connect an ADSL modem to the `extern0` interface of the firewall and have Arch manage the connection. Make sure to put the modem in *bridged* mode though (either half-bridge or RFC1483), otherwise, the modem will act as a router too. [Install](/index.php/Install "Install") the [rp-pppoe](https://www.archlinux.org/packages/?name=rp-pppoe) package.

It should be noted that if you use only PPPoE to connect to the internet (i.e. you do not have another WAN port, except for the one that connects to your modem) you do not need to set up the `extern0-profile` as the external pseudo-interface will be ppp0.

### PPPoE configuration

You can use netctl to setup the PPPoE connection. To get started, do

```
# cp /etc/netctl/examples/pppoe /etc/netctl/

```

and start editing. For the interface configuration, choose the interface that connects to the modem. If you only connect to the internet through PPPoE, this will probably be `extern0`. Fill in the rest of the fields with your ISP information. See the PPPoE section in the [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5) man page for more information on the fields.

## DNS and DHCP

We will use [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), a DNS and DHCP daemon for the LAN. It was specifically designed for small sites. [Install](/index.php/Install "Install") it with the [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package.

Dnsmasq needs to be configured to be a DHCP server with a configuration similar to the following:

 `/etc/dnsmasq.conf` 
```
interface=intern0 # make dnsmasq listen for requests only on intern0 (our LAN)
expand-hosts      # add a domain to simple hostnames in /etc/hosts
domain=foo.bar    # allow fully qualified domain names for DHCP hosts (needed when
                  # "expand-hosts" is used)
dhcp-range=10.0.0.2,10.0.0.255,255.255.255.0,1h # defines a DHCP-range for the LAN: 
                  # from 10.0.0.2 to .255 with a subnet mask of 255.255.255.0 and a
                  # DHCP lease of 1 hour (change to your own preferences)

```

Somewhere below, you will notice you can also add "static" DHCP leases, i.e. assign an IP-address to the MAC-address of a computer on the LAN. This way, whenever the computer requests a new lease, it will get the same IP. That is very useful for network servers with a DNS record. You can also deny certain MACs from obtaining an IP.

Now [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `dnsmasq.service`.

## Connection sharing

Time to tie the two network interfaces together.

### Connection sharing with shorewall

See [Shorewall](/index.php/Shorewall "Shorewall") for a detailed configuration guide.

### Manual

First of all, we need to allow packets to hop from one network interface to the other. See [Internet sharing#Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") for details.

In order for packets to be properly sent and received, it is necessary to translate the IP addresses between the outward facing network and the subnet used locally. The technique is called *masquerading* . We also need two forwarding rules to keep connections going and enable LAN to WAN forwarding. For this task, we are going to use [iptables](/index.php/Iptables "Iptables"):

 `/etc/iptables/iptables.rules` 
```
*nat
:PREROUTING ACCEPT [0:0]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -o extern0 -j MASQUERADE
COMMIT

*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i intern0 -o extern0 -j ACCEPT
COMMIT

```

If you're connecting via PPPoE, you'll also need to clamp mss to pmtu in order the prevent fragmentation from happening:

 `/etc/iptables/iptables.rules` 
```

*mangle
:PREROUTING ACCEPT [0:0]
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
-A FORWARD -o ppp0 -p tcp -m tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu
COMMIT

```

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `iptables.service`. The router should now be fully functional and route your traffic. However, since it is facing the public Internet, it makes sense to additionally secure it using a [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

## IPv6 tips

Useful reading: [IPv6](/index.php/IPv6 "IPv6") and the [wikipedia:IPv6](https://en.wikipedia.org/wiki/IPv6 "wikipedia:IPv6").

### Unique Local Addresses

You can use your router in IPv6 mode even if you do not have an IPv6 address from your ISP. Unless you disable IPv6, all interfaces should have been assigned a unique `fe80::/10` address.

For internal networking the block `fc00::/7` has been reserved. These addresses are guaranteed to be unique and non-routable from the open Internet. Addresses that belong to the `fc00::/7` block are called [Unique Local Addresses](https://en.wikipedia.org/wiki/Unique_local_address "wikipedia:Unique local address"). To get started [generate a ULA /64 block](http://www.simpledns.com/private-ipv6.aspx) to use in your network. For this example we will use `fd00:aaaa:bbbb:cccc::/64`. Firstly, we must assign a static IPv6 on the internal interface. Modify the `intern0-profile` we created above to include the following line:

```
 Address6=('fd00:aaaa:bbbb:cccc::1/64')

```

This will add the ULA to the internal interface. As far as the router goes, this is all you need to configure.

### Global Unicast Addresses

If your ISP or WAN network can access the IPv6 Internet, you can additionally assign global link addresses to your router and propagate them through [SLAAC](#Router_Advertisement_and_Stateless_Autoconfiguration_.28SLAAC.29) to your internal network. The global unicast prefix is usually either *static* or provided through *prefix delegation*.

#### Static IPv6 prefix

If your ISP has provided you with a static prefix, then edit `/etc/netctl/extern0-profile` and simply add the IPv6 and the IPv6 prefix (usually /64) you have been provided

```
 Address6=('2002:1:2:3:4:5:6:7/64')

```

You can use this in addition to the ULA address described above.

#### Acquiring IPv6 prefix via DHCPv6-PD

If your ISP handles IPv6 via prefix delegation, then you can follow the instructions in the [IPv6#Prefix delegation (DHCPv6-PD)](/index.php/IPv6#Prefix_delegation_(DHCPv6-PD) "IPv6") on how to properly configure your router. Following the conventions of this article, the WAN interface is `extern0` (or `ppp0` if you are connecting through PPPoE) and the LAN interface is `intern0`.

### Router Advertisement and Stateless Autoconfiguration (SLAAC)

To properly hand out IPv6s to the network clients, we will need to use an advertising daemon. Follow the details of the [main IPv6 article](/index.php/IPv6#For_gateways "IPv6") on how to set up `radvd`. According to this guide's convention, the LAN-facing interface is `intern0`. You can either advertise all prefixes or choose which prefixes will be assigned to the local network.

## Optional additions

### UPnP

The above configuration of shorewall does not include [UPnP](https://en.wikipedia.org/wiki/UPnP "wikipedia:UPnP") support. Use of UPnP is discouraged as it may make the gateway vulnerable to attacks from within the LAN. However, some applications require this to function correctly.

To enable UPnP on your router, you need to install an UPnP [Internet Gateway Device (IGD) protocol](https://en.wikipedia.org/wiki/Internet_Gateway_Device_Protocol "wikipedia:Internet Gateway Device Protocol") daemon. To get it, [install](/index.php/Install "Install") the [miniupnpd](https://www.archlinux.org/packages/?name=miniupnpd) package.

Read the [Shorewall guide on UPnP](http://www.shorewall.net/UPnP.html) for more information.

### Remote administration

[OpenSSH](/index.php/OpenSSH "OpenSSH") can be used to administer your router remotely. This is useful for running it in headless mode (no monitor or input devices).

### Caching web proxy

See [Squid](/index.php/Squid "Squid") or [Polipo](/index.php/Polipo "Polipo") for the setup of a web proxy to speed up browsing and/or adding an extra layer of security.

### Time server

To use the router as a time server, see [System time#Time synchronization](/index.php/System_time#Time_synchronization "System time") for available Network Time Protocol (NTP) server implementations.

Then, configure shorewall or iptables to allow NTP traffic in and out.

### Content filtering

Install and configure [DansGuardian](/index.php/DansGuardian "DansGuardian") or [Privoxy](/index.php/Privoxy "Privoxy") if you need a content filtering solution.

### Traffic shaping

Traffic shaping is very useful, especially when you are not the only one on the LAN. The idea is to assign a priority to different types of traffic. Interactive traffic (ssh, online gaming) probably needs the highest priority, while P2P traffic can do with the lowest. Then there is everything in between.

#### Traffic shaping with shorewall

See [Shorewall#Traffic shaping](/index.php/Shorewall#Traffic_shaping "Shorewall").

## See also

*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")