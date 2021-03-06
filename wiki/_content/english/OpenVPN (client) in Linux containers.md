Related articles

*   [AirVPN](/index.php/AirVPN "AirVPN")
*   [Docker](/index.php/Docker "Docker")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [OpenVPN](/index.php/OpenVPN "OpenVPN")
*   [OpenVPN (server) in Linux containers](/index.php/OpenVPN_(server)_in_Linux_containers "OpenVPN (server) in Linux containers")
*   [PeerGuardian_Linux](/index.php/PeerGuardian_Linux "PeerGuardian Linux")
*   [Systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [ufw](/index.php/Ufw "Ufw")

This article describes how to setup a [Linux Container](/index.php/Linux_Container "Linux Container") to run OpenVPN in client mode with a "kill switch" for secure/private internet use. Doing so offers a distinct advantage over using full-blown virtualization like [VirtualBox](/index.php/VirtualBox "VirtualBox") or [QEMU](/index.php/QEMU "QEMU") in that the resource overhead is minimal by comparison and able to run on low powered devices.

## Contents

*   [1 Container setup](#Container_setup)
    *   [1.1 LXC config](#LXC_config)
    *   [1.2 Needed packages within the container](#Needed_packages_within_the_container)
    *   [1.3 Package setup](#Package_setup)
        *   [1.3.1 OpenVPN](#OpenVPN)
            *   [1.3.1.1 Avoiding DNS leaks](#Avoiding_DNS_leaks)
        *   [1.3.2 ufw](#ufw)
        *   [1.3.3 pgl](#pgl)
*   [2 Test the service](#Test_the_service)

## Container setup

Basic setup and understanding of [Linux Containers](/index.php/Linux_Containers "Linux Containers") is required. This article assumes that readers have a base LXC setup operational. Newcomers to these are directed to the aforementioned article.

### LXC config

The container's config should be modified to include several key lines in order to both run OpenVPN and have internet programs (browsers, email clients, torrent clients, etc.) interact with the host system from within the LXC and from behind the VPN.

For the example, the lxc is named "playtime" and a full config is shown:

 `/var/lib/lxc/playtime/config` 
```
...

## for openvpn
lxc.mount.entry = /dev/net dev/net none bind,create=dir
lxc.cgroup.devices.allow = c 10:200 rwm

```

### Needed packages within the container

In addition to the base system, [openvpn](https://www.archlinux.org/packages/?name=openvpn) is required and available from the [official repositories](/index.php/Official_repositories "Official repositories"). A properly configured [firewall](/index.php/Firewall "Firewall") to run within the container is *highly* recommended. The role of the firewall within the container is two fold:

1.  Provide a functional "kill switch" to maintain privacy should the connection to the VPN fail.
2.  Keep nasty stuff out.

This guide uses [ufw](https://www.archlinux.org/packages/?name=ufw) which is very easy to configure, but other examples can certainly be used.

### Package setup

#### OpenVPN

Configuration of OpenVPN is beyond the scope of this article. Readers are encouraged to read the [OpenVPN](/index.php/OpenVPN "OpenVPN") article to properly setup the software for a given VPN provider. Note that many private VPN providers include links to directly download a properly configured openvpn.opvn profile unique to their particular service. For the purposes of this guide, `/etc/openvpn/client/myprofile.conf` will refer to that config.

Verify openvpn functionality within the container; [start](/index.php/Start "Start") openvpn via `openvpn-client@myprofile.service` and once satisfied [enable](/index.php/Enable "Enable") it to run at boot.

**Note:** Users running openvpn within an *unprivileged* container will need to create a custom systemd unit to start it within the container. Simply copy the package-provided `/usr/lib/systemd/system/openvpn-client@.service` to `/etc/systemd/system/openvpn-client@.service` and modify the new file commenting out the the line beginning with: `LimitNPROC...`

##### Avoiding DNS leaks

Users are highly encouraged to setup openvpn with to manage `/etc/resolv.conf` via the instructions in [OpenVPN#DNS](/index.php/OpenVPN#DNS "OpenVPN"). Failure to do so may lead to DNS leaks if the host's DNS server is specified in said file.

#### ufw

**Note:** The following applies to inside the container.

Configuration of [ufw](/index.php/Ufw "Ufw") is described in [OpenVPN#Firewall configuration](/index.php/OpenVPN#Firewall_configuration "OpenVPN"). Once modified as described, additional setup is simply to define the protocols to run (ssh, torrent, etc.) and also define the IP address or address range of the VPN provider. Again, these are available from the private providers.

**Note:** The following needs to be executed as the root user; the "#" sign prefixing these commands per standard wiki notation has been omitted to allow for a clean copy/paste into a terminal.

First setup the default deny policy and then allow whatever services are to pass though:

```
ufw default deny outgoing
ufw default deny incoming
ufw allow ssh
ufw allow 1194
ufw allow out 1194
ufw allow out on tun0 from any to any
ufw allow in on tun0 from any to any

```

Now add the VPN server IP addresses or ranges. Note two entries for each IP address is required. In the example below, only a single fictitious IP address is shown for illustrative purposes.

```
ufw allow in from 50.120.10.200 to any
ufw allow out from 50.121.10.200 to any

```

Finally, add the internal LAN IP range to allow access regardless of VPN connectivity:

```
ufw allow from 192.168.0.0/24

```

Start ufw and [enable](/index.php/Enable "Enable") `ufw.service` to start at boot.

```
# ufw enable

```

#### pgl

Additional protection can be had via using [pgl](/index.php/Pgl "Pgl") within the container. See: [PeerGuardian Linux#Running pgl from within a container](/index.php/PeerGuardian_Linux#Running_pgl_from_within_a_container "PeerGuardian Linux").

## Test the service

From within the running container, (connected via ssh or via `lxc-attach -n playtime`) test the setup by exporting a browser to the host's machine X server:

```
$ DISPLAY=:0 firefox

```

The result should be a firefox window in the host's X server with the title, "Mozilla Firefox (playtime)." A number of websites can be used to verify IP address and status of DNS entries. Once such site is [ipleak dot net](http://ipleak.net).

At this point, the IP and DNS entries corresponding to `/etc/openvpn/client/myprofile.conf` should be displayed.