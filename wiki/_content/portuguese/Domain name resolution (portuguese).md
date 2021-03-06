**Status de tradução:** Esse artigo é uma tradução de [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution"). Data da última tradução: 2019-01-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Domain_name_resolution&diff=0&oldid=562570) na versão em inglês.

Artigos relacionados

*   [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede")

Em geral, um [nome de domínio](https://en.wikipedia.org/wiki/pt:Dom%C3%ADnio "wikipedia:pt:Domínio") representa um endereço IP e está associado a ele no [Sistema de Nomes de Domínio](https://en.wikipedia.org/wiki/pt:Sistema_de_Nomes_de_Dom%C3%ADnio "wikipedia:pt:Sistema de Nomes de Domínio"), ou *Domain Name System* (DNS). Esse artigo explica como para configurar resolução de nome de domínio e resolver nomes de domínio.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Name Service Switch](#Name_Service_Switch)
    *   [1.1 Resolva um nome de domínio usando NSS](#Resolva_um_nome_de_domínio_usando_NSS)
*   [2 Resolvedor do glibc](#Resolvedor_do_glibc)
    *   [2.1 Sobrescrita do /etc/resolv.conf](#Sobrescrita_do_/etc/resolv.conf)
    *   [2.2 Limitar o tempo de pesquisa](#Limitar_o_tempo_de_pesquisa)
    *   [2.3 Pesquisa de hostname atrasada com IPv6](#Pesquisa_de_hostname_atrasada_com_IPv6)
    *   [2.4 Nomes de domínio local](#Nomes_de_domínio_local)
*   [3 Utilitários de pesquisa](#Utilitários_de_pesquisa)
*   [4 Desempenho de resolvedor](#Desempenho_de_resolvedor)
*   [5 Privacidade e segurança](#Privacidade_e_segurança)
*   [6 Serviços DNS de terceiros](#Serviços_DNS_de_terceiros)
*   [7 Servidores DNS](#Servidores_DNS)
    *   [7.1 Servidores apenas autoritativos](#Servidores_apenas_autoritativos)
*   [8 Veja também](#Veja_também)

## Name Service Switch

O recurso [Name Service Switch](https://en.wikipedia.org/wiki/pt:Name_Service_Switch "wikipedia:pt:Name Service Switch") (NSS) é parte da biblioteca C do GNU ([glibc](https://www.archlinux.org/packages/?name=glibc)) e apoia a API [getaddrinfo(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getaddrinfo.3), usada para resolver nomes de domínio. O NSS permite que bancos de dados do sistema sejam fornecidos por serviços separados, cuja ordem de pesquisa pode ser configurada pelo administrador no [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5). O banco de dados responsável pela resolução de nomes de domínio é o banco de dados *hosts*, para o qual a glibc oferece os seguintes serviços:

*   *file*: lê o arquivo `/etc/hosts`, veja [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)
*   *dns*: o [resolvedor do glibc](#Resolvedor_do_glibc) que lê `/etc/resolv.conf`, veja [resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5)

[Systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") fornece três serviços NSS para resolução de hostname:

*   [nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8) - um resolvedor de tronco de DNS em cache, descrito em [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   [nss-myhostname(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-myhostname.8) - fornece resolução de hostname sem ter que editar `/etc/hosts`, descrito em [Configuração de rede#Resolução de hostname local](/index.php/Configura%C3%A7%C3%A3o_de_rede#Resolução_de_hostname_local "Configuração de rede")
*   [nss-mymachines(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-mymachines.8) - fornece resolução de hostname para os nomes de contêineres locais de [systemd-machined(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-machined.8)

### Resolva um nome de domínio usando NSS

Bancos de dados NSS podem ser consultados com [getent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getent.1). Um nome de domínio pode ser resolvido por meio do NSS usando:

```
$ getent hosts *nome_domínio*

```

**Nota:** Enquanto a maioria dos programas resolve nomes de domínio usando NSS, alguns podem ler `/etc/resolv.conf` e/ou `/etc/hosts` diretamente. Veja [Configuração de rede#Resolução de hostname local](/index.php/Configura%C3%A7%C3%A3o_de_rede#Resolução_de_hostname_local "Configuração de rede").

## Resolvedor do glibc

O resolvedor do glibc lê `/etc/resolv.conf` para toda resolução para determinar os servidores de nome e opções para usar.

[resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5) lista servidores de nomes juntos com algumas opções de configuração.

Servidores de nome *(nameservers)* listados primeiros são tentados primeiro, até os três servidores podem ser listados. Linhas iniciando com um cerquilha (`#`) são ignoradas.

**Nota:** O resolvedor do glibc não faz cache de consultas. Para melhorar tempo de consulta, você pode configurar um resolvedor em cache. Veja [#Servidores DNS](#Servidores_DNS) para mais informações.

### Sobrescrita do /etc/resolv.conf

[Gerenciadores de rede](/index.php/Gerenciadores_de_rede "Gerenciadores de rede") tendem a sobrescrever `/etc/resolv.conf`, para particularidades veja a seção correspondente:

*   [dhcpcd#resolv.conf](/index.php/Dhcpcd#resolv.conf "Dhcpcd")
*   [netctl#resolv.conf](/index.php/Netctl#resolv.conf "Netctl")
*   [NetworkManager (Português)#resolv.conf](/index.php/NetworkManager_(Portugu%C3%AAs)#resolv.conf "NetworkManager (Português)")

Para evitar que programas sobrescrevam `/etc/resolv.conf`, você também pode protegê-lo contra gravação definindo o [atributo de arquivo](/index.php/Atributos_de_arquivo "Atributos de arquivo") imutável:

```
# chattr +i /etc/resolv.conf

```

**Dica:** Se você quiser que vários processos escrevam no `/etc/resolv.conf`, você pode usar [resolvconf](/index.php/Resolvconf_(Portugu%C3%AAs) "Resolvconf (Português)").

### Limitar o tempo de pesquisa

Se você for confrontado com uma consulta de hostname muito longa (seja no [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou enquanto navega), frequentemente ajuda a definir um pequeno tempo limite após o qual um servidor de nomes alternativo é usado. Para fazer isso, coloque o seguinte em `/etc/resolv.conf`:

```
options timeout:1

```

### Pesquisa de hostname atrasada com IPv6

Se você tiver um atraso de 5 segundos ao resolver os hostname, isso pode ser devido a um mau comportamento do servidor DNS/Firewall e somente dando uma resposta a uma solicitação paralela A e AAAA.[[1]](https://udrepper.livejournal.com/20948.html) Você pode corrigir isso configurando a seguinte opção no `/etc/resolv.conf`:

```
options single-request

```

### Nomes de domínio local

Se você quiser usar o hostname de máquinas locais sem os nomes de domínio totalmente qualificados, adicione uma linha ao `/etc/resolv.conf` com o domínio local, como:

```
domain exemplo.com.br

```

Dessa forma, você pode se referir a hosts locais como `maquinaprincipal1.exemplo.com.brm` como simplesmente `maquinaprincipal1` ao usar o comando *ssh*, mas o comando *drill* ainda requer os nomes de domínio totalmente qualificados para realizar pesquisas.

## Utilitários de pesquisa

Para consultar servidores DNS específicos e registros DNS/[DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)"), você pode usar utilitários de pesquisa de DNS dedicados. Essas ferramentas implementam o próprio DNS e não usam [NSS](/index.php/Name_Service_Switch_(Portugu%C3%AAs) "Name Service Switch (Português)").

*   [ldns](https://www.archlinux.org/packages/?name=ldns) fornece [drill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/drill.1), que é uma ferramenta projetada para obter informações do DNS.

Por exemplo, para consultar um servidor de nomes específico com *drill* por registros TXT de um domínio:

```
$ drill @*servidor-de-nome* TXT *domínio*

```

Se você não especificar um servidor DNS, *drill* use os servidores de nome definidos em `/etc/resolv.conf`.

*   [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) fornece [dig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dig.1), [host(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/host.1), [nslookup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nslookup.1) e um monte de ferramentas `dnssec-`.

## Desempenho de resolvedor

O resolvedor do Glibc não armazena em cache as consultas. Se você quiser que o cache local, use [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") ou configure um cache local [servidor DNS](#Servidores_DNS) e use `127.0.0.1` como seu servidor de nomes.

**Dica:**

*   Os [utilitários de pesquisa](#Utilitários_de_pesquisa) *drill* ou *dig* relatam o tempo de consulta.
*   Um roteador geralmente configura seu próprio resolvedor de cache como o servidor DNS da rede, fornecendo assim o cache DNS para toda a rede.
*   Se demorar muito para mudar para o próximo servidor DNS, você pode tentar [diminuir o tempo limite](#Limitar_o_tempo_de_pesquisa).

## Privacidade e segurança

O protocolo DNS não é criptografado e não leva em conta a confidencialidade, integridade ou autenticação, portanto, se você usar uma rede não confiável ou um ISP mal-intencionado, suas consultas DNS poderão ser interceptadas e as respostas [manipuladas](https://en.wikipedia.org/wiki/pt:Ataque_man-in-the-middle "wikipedia:pt:Ataque man-in-the-middle"). Além disso, os servidores DNS podem realizar [redirecionamento de DNS](https://en.wikipedia.org/wiki/pt:DNS_hijacking "wikipedia:pt:DNS hijacking") (*DNS hijacking*).

Você precisa confiar em seu servidor DNS para tratar suas consultas de maneira confidencial. Os servidores DNS são fornecidos por ISPs e [terceiros](#Serviços_DNS_de_terceiros). Como alternativa, você pode executar seu próprio servidor de nome recursivo, o que, no entanto, exige mais esforço. Se você usa um cliente [DHCP](/index.php/DHCP_(Portugu%C3%AAs) "DHCP (Português)") em redes não confiáveis, defina os servidores de nomes estáticos para evitar o uso e a sujeição a servidores DNS arbitrários. Para proteger sua comunicação com um servidor DNS remoto, você pode usar um protocolo criptografado, como [DNS por TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS"), [DNS por HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") ou [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt"), desde que o servidor upstream e seu [resolvedor](#Servidores_DNS) possuam suporte ao protocolo. Para verificar se as respostas são realmente de [servidores de nome autoritativos](https://en.wikipedia.org/wiki/Authoritative_name_server "wikipedia:Authoritative name server"), você pode validar [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)"), desde que ambos os servidores upstream e seu [resolvedor](#Servidores_DNS) tenha suporte a isso.

Esteja ciente de que o software cliente, como os principais navegadores da Web, também pode (começar a) implementar alguns dos protocolos. Embora a criptografia de consultas possa ser vista como um bônus, isso também significa que o software avisa sobre a configuração do resolvedor do sistema. [[2]](https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/#trr-and-doh)

## Serviços DNS de terceiros

**Nota:** Antes de usar um serviço DNS de terceiros, verifique sua política de privacidade para obter informações sobre como os dados do usuário são manipulados. Os dados do usuário têm valor e podem ser vendidos para outras partes.

Existem vários [serviços DNS de terceiros](https://en.wikipedia.org/wiki/Public_recursive_name_server#List_of_public_DNS_service_operators "wikipedia:Public recursive name server") disponíveis, alguns dos quais também possuem software dedicado:

*   **dingo** — Um cliente DNS para o DNS do Google por HTTPS

	[https://github.com/pforemski/dingo](https://github.com/pforemski/dingo) || [dingo](https://www.archlinux.org/packages/?name=dingo)

*   **opennic-up** — Automatiza a renovação de servidores DNS com os servidores OpenNIC mais responsivos

	[https://github.com/kewlfft/opennic-up](https://github.com/kewlfft/opennic-up) || [opennic-up](https://aur.archlinux.org/packages/opennic-up/)

## Servidores DNS

Os servidores [DNS](/index.php/DNS_(Portugu%C3%AAs) "DNS (Português)") podem ser [autoritativos](https://en.wikipedia.org/wiki/Authoritative_name_server "wikipedia:Authoritative name server") e [recursivos](https://en.wikipedia.org/wiki/Name_server#Recursive_query "wikipedia:Name server"). Se eles não forem, eles são chamados de ***stub resolvers*** e simplesmente encaminham todas as consultas para outro servidor de nomes recursivo. Os *stub resolvers* são normalmente usados para introduzir o cache de DNS no host ou na rede local. Observe que o mesmo também pode ser obtido com um servidor de nomes completo. Esta seção compara os servidores DNS disponíveis, para uma comparação mais detalhada, consulte o [Wikipédia](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software "wikipedia:Comparison of DNS server software").

| Nome | Pacote | [Autoritativo](https://en.wikipedia.org/wiki/Authoritative_name_server "wikipedia:Authoritative name server")
/ [Recursivo](https://en.wikipedia.org/wiki/Name_server#Recursive_query | [Valida](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions#The_lookup_procedure "wikipedia:Domain Name System Security Extensions")
[DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)") | [DNS
por TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS") | [DNS
por HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") |
| [dnscrypt-proxy](/index.php/Dnscrypt-proxy_(Portugu%C3%AAs) "Dnscrypt-proxy (Português)") | [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) | Não | Sim | Não | Não | Não | Sim |
| [Rescached](/index.php/Rescached "Rescached") | [rescached-git](https://aur.archlinux.org/packages/rescached-git/) | Não | Sim | [Sim](https://github.com/shuLhan/rescached-go#integration-with-openresolv) | Não | Não | Limitado |
| [Stubby](/index.php/Stubby "Stubby") | [stubby](https://www.archlinux.org/packages/?name=stubby) | Não | Não | Não | Sim | Sim | Não |
| [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") | [systemd](https://www.archlinux.org/packages/?name=systemd) | Não | Sim | [Sim](/index.php/Systemd-resolvconf "Systemd-resolvconf") | Sim | Inseguro | [Não](https://github.com/systemd/systemd/issues/8639) |
| [dnsmasq](/index.php/Dnsmasq_(Portugu%C3%AAs) "Dnsmasq (Português)") | [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) | Parcial | Sim | [Sim](/index.php/Openresolv_(Portugu%C3%AAs)#Assinantes "Openresolv (Português)") | Sim | [Não](http://lists.thekelleys.org.uk/pipermail/dnsmasq-discuss/2018q2/012131.html) | Não |
| [BIND](/index.php/BIND "BIND") | [bind](https://www.archlinux.org/packages/?name=bind) | Sim | Sim | [Sim](/index.php/Openresolv_(Portugu%C3%AAs)#Assinantes "Openresolv (Português)") | Sim | ? | ? |
| [Knot Resolver](/index.php/Knot_Resolver "Knot Resolver") | [knot-resolver](https://aur.archlinux.org/packages/knot-resolver/) | Sim | Sim | Não | Sim | Sim | [Não](https://gitlab.labs.nic.cz/knot/knot-resolver/issues/243) |
| [MaraDNS](https://en.wikipedia.org/wiki/MaraDNS "wikipedia:MaraDNS") | [maradns](https://aur.archlinux.org/packages/maradns/) | Sim | Sim | Não | Não | Não | Não |
| [pdnsd](/index.php/Pdnsd "Pdnsd") | [pdnsd](https://www.archlinux.org/packages/?name=pdnsd) | Sim | Permanente | [Sim](/index.php/Openresolv_(Portugu%C3%AAs)#Assinantes "Openresolv (Português)") | Não | Não | Não |
| [PowerDNS Recursor](https://www.powerdns.com/recursor.html) | [powerdns-recursor](https://www.archlinux.org/packages/?name=powerdns-recursor) | Sim | Sim | [Não](https://roy.marples.name/projects/openresolv/config#pdns_recursor) | Sim | ? | ? |
| [Unbound](/index.php/Unbound "Unbound") | [unbound](https://www.archlinux.org/packages/?name=unbound) | Sim | Sim | [Sim](/index.php/Openresolv_(Portugu%C3%AAs)#Assinantes "Openresolv (Português)") | Sim | Sim | [Não](https://nlnetlabs.nl/bugs-script/show_bug.cgi?id=1200) |

1.  Implementa um cliente de protocolo [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt").
2.  Só encaminha usando DNS por HTTPS quando Rescached em si é consultado usando DNS por HTTPS.[[3]](https://github.com/shuLhan/rescached-go#integration-with-dns-over-https)
3.  Do [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5): *Note que como o resolvedor não é capaz de autenticar o servidor, ele é vulnerável a ataques "man-in-the-middle".*[[4]](https://github.com/systemd/systemd/issues/9397) Além disso, o único modo suportado é "opportunistic", o que *torna o DNS-over-TLS vulnerável a ataques de "downgrade"*.[[5]](https://github.com/systemd/systemd/issues/10755)
4.  Do [Wikipédia](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software#cite_note-masqauth-26 "wikipedia:Comparison of DNS server software"): dnsmasq tem um suporte autoritativo limitado, sendo destinado a rede interna em vez de uso público na Internet.

### Servidores apenas autoritativos

| Nome | Pacote | [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)") | Balanceamento
geográfico |
| [gdnsd](https://gdnsd.org/) | [gdnsd](https://www.archlinux.org/packages/?name=gdnsd) | Não | Sim |
| [Knot DNS](https://www.knot-dns.cz/) | [knot](https://www.archlinux.org/packages/?name=knot) | Sim | Não |
| [NSD](/index.php/NSD "NSD") | [nsd](https://www.archlinux.org/packages/?name=nsd) | Não | Não |
| [PowerDNS](https://www.powerdns.com/auth.html) | [powerdns](https://www.archlinux.org/packages/?name=powerdns) | Sim | Sim |

## Veja também

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-resolv.html)
*   [Debian Handbook](https://www.debian.org/doc/manuals/debian-handbook/sect.hostname-name-service.en.html#sect.name-resolution)
*   [RFC:7706](https://tools.ietf.org/html/rfc7706 "rfc:7706") - Diminuindo o tempo de acesso a servidores raiz executando um com loopback (inglês)