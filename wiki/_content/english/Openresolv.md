[Openresolv](https://roy.marples.name/projects/openresolv) is a [resolv.conf](/index.php/Resolv.conf "Resolv.conf") management framework.

## Installation

[Install](/index.php/Install "Install") the [openresolv](https://www.archlinux.org/packages/?name=openresolv) package.

## Usage

Openresolv provides [resolvconf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.8) and is configured in `/etc/resolvconf.conf`. See [resolvconf.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.conf.5) for supported options.

Running `resolvconf -u` will generate `/etc/resolv.conf`.

## Users

Stand-alone DHCP clients:

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd") has a hook which uses resolvconf if it is installed.

[Network manager](/index.php/Network_manager "Network manager"):

*   [netctl](/index.php/Netctl "Netctl") (used by default)
*   [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager")

[VPN](/index.php/VPN "VPN") clients:

*   [OpenVPN#DNS](/index.php/OpenVPN#DNS "OpenVPN")