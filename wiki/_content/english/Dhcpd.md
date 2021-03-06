Related articles

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd")

dhcpd is the [Internet Systems Consortium](http://www.isc.org/downloads/dhcp/) DHCP Server. It is useful for instance on a machine acting as a router on a LAN.

**Note:** *dhcpd* (DHCP **(server)** daemon) is not the same as [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (DHCP **client** daemon).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Listening on only one interface](#Listening_on_only_one_interface)
        *   [3.1.1 Configuring dhcpd](#Configuring_dhcpd)
        *   [3.1.2 Service file](#Service_file)
    *   [3.2 Use for PXE](#Use_for_PXE)

## Installation

[Install](/index.php/Install "Install") the [dhcp](https://www.archlinux.org/packages/?name=dhcp) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

*dhcpd* includes two unit files `dhcpd4.service` and `dhcpd6.service`, which can be used to [control](/index.php/Enable "Enable") the daemon. They start the daemon on *all* [network interfaces](/index.php/Network_interfaces "Network interfaces") for IPv4 and IPv6 respectively. See [#Listening on only one interface](#Listening_on_only_one_interface) for an alternative.

## Configuration

Assign a static IPv4 address to the interface you want to use (in our examples we will use `eth0`). The first 3 bytes of this address cannot be exactly the same as those of another interface.

```
# ip link set up dev eth0
# ip addr add 139.96.30.100/24 dev eth0 # arbitrary address

```

**Tip:** Usually, the one of next three subnets is used for private networks, which are specially reserved and won't conflict with any host in the Internet:

*   `192.168/16` (subnet `192.168.0.0`, netmask `255.255.0.0`)
*   `172.16/12` (subnet `172.16.0.0`, netmask `255.240.0.0`)
*   `10/8` (for large networks; subnet `10.0.0.0`, netmask `255.0.0.0`)

See also [RFC 1918](http://www.ietf.org/rfc/rfc1918.txt).

To have your static ip assigned at boot, see [Network configuration#Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration").

The default `dhcpd.conf` contains many uncommented examples, so relocate it:

```
# cp /etc/dhcpd.conf.example /etc/dhcpd.conf

```

The minimal configuration file may look like:

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.4.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;
}

```

If you need to provide a fixed IP address for a single specific device, you can use the following syntax

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.4.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;

  host macbookpro{
   hardware ethernet 70:56:81:22:33:44;
   fixed-address 139.96.30.199;
  }
}

```

`domain-name-servers` option contains addresses of DNS servers which are supplied to clients. In our example we are using Google's public DNS servers. If you know a local DNS server (for example, provided by your ISP), you should use it. If you've configured your own DNS on a local machine, then use its address in your subnet (e. g. `139.96.30.100` in our example).

`subnet-mask` and `routers` defines a subnet mask and a list of available routers on the subnet. In most cases for small networks you can use `255.255.255.0` as a mask and specify an IP address of the machine on which you're configuring DHCP server as a router.

`subnet` blocks defines options for separate subnets, which are mapped to the network interfaces on which *dhcpd* is running. In our example this is one subnet `139.96.30.0/24` for single interface `eth0`, for which we defined the range of available IP addresses. Addresses from this range will be assigned to the connecting clients.

### Listening on only one interface

If your computer is already part of one or several networks, it could be a problem if your computer starts giving ip addresses to machines from the other networks. It can be done by either configuring dhcpd or starting it as a daemon with [systemctl](/index.php/Systemd#Using_units "Systemd").

#### Configuring dhcpd

In order to exclude an interface, you must create an empty declaration for the subnet that will be configured on that interface.

This is done by editing the configuration file (for example):

 `/etc/dhcpd.conf` 
```
# No DHCP service in DMZ network (192.168.2.0/24)
subnet 192.168.2.0 netmask 255.255.255.0 {
}

```

#### Service file

There is no service files provided by default to use *dhcpd* only on one interface so you need to create one:

 `/etc/systemd/system/dhcpd4@.service` 
```
[Unit]
Description=IPv4 DHCP server on %I
Wants=network.target
After=network.target

[Service]
Type=forking
PIDFile=/run/dhcpd4.pid
ExecStart=/usr/bin/dhcpd -4 -q -pf /run/dhcpd4.pid %I
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target

```

This is a template unit, which binds it to a particular interface, for example `dhcpd4@*eth0*.service` where *eth0* is an interface shown with `ip link`.

Sometimes we want to wait for the network to be configured, in this case the solution is to make service waits for network-online.target instead of network.target:

 `/etc/systemd/system/dhcpd4@.service` 
```
[Unit]
Wants=network-online.target
After=network-online.target

```

To have this working we have to enable another service to make it work:

```
# systemctl enable systemd-networkd-wait-online

```

### Use for PXE

PXE Configuration is done with the following two options:

 `/etc/dhcpd.conf` 
```
next-server 192.168.0.2;
filename "/pxelinux.0";

```

This section can either be in an entire `subnet` or just in a `host` definition. `next-server` is the IP of the TFTP Server, and `filename` is the filename of the image to boot. For more information see [PXE](/index.php/PXE "PXE").