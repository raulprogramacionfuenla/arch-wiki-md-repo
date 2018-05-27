[Openresolv](https://roy.marples.name/projects/openresolv) é um framework de gerenciamento de [resolv.conf](/index.php/Resolv.conf_(Portugu%C3%AAs) "Resolv.conf (Português)").

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [openresolv](https://www.archlinux.org/packages/?name=openresolv).

## Uso

Openresolv fornece [resolvconf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.8) e é configurado no `/etc/resolvconf.conf`. Veja [resolvconf.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.conf.5) para opções válidas.

A execução de `resolvconf -u` vai gerar `/etc/resolv.conf`.

## Usuários

Clientes DHCP autônomos:

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd") tem um *hook* que usa resolvconf se ele estiver instalado.

[Gerenciador de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede"):

*   [netctl](/index.php/Netctl "Netctl") (usado por padrão)
*   [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager")

Clientes [VPN](/index.php/VPN "VPN"):

*   [OpenVPN#DNS](/index.php/OpenVPN#DNS "OpenVPN")