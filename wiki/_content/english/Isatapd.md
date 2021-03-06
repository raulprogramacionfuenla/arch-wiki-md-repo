Related articles

*   [Daemon](/index.php/Daemon "Daemon")
*   [IPv6_-_6in4_Tunnel](/index.php/IPv6_-_6in4_Tunnel "IPv6 - 6in4 Tunnel")

[isatapd](http://www.saschahlusiak.de/linux/isatap.htm) is an [ISATAP](https://en.wikipedia.org/wiki/ISATAP "wikipedia:ISATAP") client. It is a daemon program to create and to maintain an ISATAP tunnel RFC 5214 in Linux.

## Installation

[Install](/index.php/Install "Install") the package [isatapd](https://www.archlinux.org/packages/?name=isatapd) from [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

The package add an rc.d script /etc/rc.d/isatapd to run isatapd as a system service. You need to modify it to set your router. Change the value of **ISATAPD_ROUTER** to the hostname of the router you want to use.

**Note:** The default value of **ISATAPD_ROUTER** is **isatap.tsinghua.edu.cn**. It's the router provided by Tsinghua University.

If you want to modify other options instead of using the default values, have a look at [the project's homepage](http://www.saschahlusiak.de/linux/isatap.htm) for further reference.

## Run

Start and enable isatapd systemd [service](/index.php/Systemd#Using_units "Systemd").