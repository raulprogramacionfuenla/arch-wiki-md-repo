Esse artigo fornece uma visão geral do Arch Build System (ABS) junto com um tutorial para iniciantes. Ele não tem a intenção de ser um guia de referência completo.

## Contents

*   [1 O que é o Arch Build System?](#O_que_.C3.A9_o_Arch_Build_System.3F)
    *   [1.1 O que é um sistema tipo portação?](#O_que_.C3.A9_um_sistema_tipo_porta.C3.A7.C3.A3o.3F)
    *   [1.2 ABS é um conceito similar](#ABS_.C3.A9_um_conceito_similar)
    *   [1.3 Visão geral de ABS](#Vis.C3.A3o_geral_de_ABS)
        *   [1.3.1 Árvore SVN](#.C3.81rvore_SVN)
*   [2 Por que eu iria querer usar o ABS?](#Por_que_eu_iria_querer_usar_o_ABS.3F)
*   [3 Como usar o ABS](#Como_usar_o_ABS)
    *   [3.1 Pré-requisitos](#Pr.C3.A9-requisitos)
    *   [3.2 Checkout não-recursivo](#Checkout_n.C3.A3o-recursivo)
    *   [3.3 Fazer checkout de um pacote](#Fazer_checkout_de_um_pacote)
    *   [3.4 Configurar makepkg](#Configurar_makepkg)
    *   [3.5 Compilar pacote](#Compilar_pacote)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Preserve pacotes modificados](#Preserve_pacotes_modificados)
    *   [4.2 Faça checkout de uma versão anterior de um pacote](#Fa.C3.A7a_checkout_de_uma_vers.C3.A3o_anterior_de_um_pacote)
*   [5 Outras ferramentas](#Outras_ferramentas)

## O que é o Arch Build System?

O Arch Build System (em português, "Sistema de Compilação do Arch") é sistema *tipo portação* para compilar e empacotar software a partir do código-fonte. Enquanto o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") é a ferramenta especializada do Arch para gerenciamento de pacote binário (incluindo pacotes compilados com o ABS), ABS é uma coleção de ferramentas para compilar o fonte em pacotes `.pkg.tar.xz` instaláveis.

### O que é um sistema tipo portação?

*Ports* é um sistema usado por *BSD para automatizar o processo de compilação de software a partir do código-fonte. O sistema usa um *port* para baixar, descompactar, patch, compilar e instalar o software dado. Um *port* é meramente um pequeno diretório no computador do usuário, nomeado pelo software correspondente para ser instalado, que contém uns poucos arquivos com as instruções para compilar e instalar o software a partir dos fontes. Isso tornar a instalação softwares tão simples quanto digitar `make` ou `make install clean` dentro de diretório de portação.

### ABS é um conceito similar

ABS é feito de uma árvore de diretórios que pode ser obtida (*checkout*) usando o SVN. Essa árvore representa, mas não contém, todos os softwares oficiais do Arch. Subdiretórios não contêm o pacote de software nem o fonte, e sim um arquivo [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e, algumas vezes, outros arquivos. Ao executar [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") dentro de um diretório contendo um PKGBUILD, o software é primeiro compilado e então empacotado dentro do diretório de compilação. Então, você pode usar [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") para instalar ou atualizar seu novo pacote.

### Visão geral de ABS

"ABS" pode ser usado como um termo guarda-chuva já que ele inclui e depende de vários outros componentes; portanto, apesar de tecnicamente impreciso, "ABS" pode ser referir às seguintes ferramentas como um kit de ferramentas completos:

	Árvore SVN

	A estrutura de diretório contendo arquivos necessários para compilar todos os pacotes oficiais, mas não os pacotes em si nem os arquivos fontes do software. Ela está disponível nos repositórios [svn](https://www.archlinux.org/svn/) e [git](https://projects.archlinux.org/svntogit/packages.git/).

	[PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")

	Um script [Bash](/index.php/Bash "Bash") que contém a URL do código-fonte junto com as instruções de compilação e empacotamento.

	[makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")

	Ferramenta de comando shell que lê os PKGBUILDs, baixa automaticamente e compila os fontes e cria um `.pkg.tar*` de acordo com o vetor `PKGEXT` no `makepkg.conf`. Você também pode usar makepkg para fazer seus próprios pacotes personalizados do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") ou fontes de terceiros. Veja [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes") para mais informações.

	[pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")

	pacman é completamente separado, mas é necessariamente invocado pelo makepkg ou manualmente, para instalar e remover os pacotes compilados e para obter dependências.

	[AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)")

	O Arch User Repository é separado do ABS, mas PKGBUILDs do AUR (sem suporte) são compilados usando makepkg para compilar e empacotar software. Em contraste com a árvore do ABS em sua máquina local, o AUR existe como uma interface do website. Ele contém muitos milhares de PKGBUILDs contribuídos por usuários para software que está indisponível como um pacote oficial do Arch. Se você precisar compilar um pacote fora da árvore oficial do Arch, as chances são de que esteja no AUR.

**Warning:** PKGBUILDs oficiais presumem que pacotes são [compilados em um *chroot* limpo](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot"). Compilação de software em um sistema de compilação *sujo* pode falhar ou causar comportamentos inesperados em tempo de execução, porque se o sistema de compilação detecta dependências dinamicamente, o resultado depende de quais pacotes estão disponíveis no sistema de compilação.

#### Árvore SVN

Os [repositórios](/index.php/Reposit%C3%B3rios "Repositórios") *core*, *extra* e *testing* estão no repositório SVN *packages* para *[checkout](#Checkout_n.C3.A3o-recursivo)*. Os repositórios *community* e *multilib* estão no repositório SVN *community*.

Cada pacote possui seu próprio subdiretório. Dentro dele há diretórios `repos` e `trunk`. `repos` é expandido por nome de repositório (ex.: *core*) e arquitetura. PKGBUILDs e arquivos localizados em `repos` são usados em compilações oficiais. Arquivos localizados no `trunk` são usados pelos desenvolvedores na preparação antes de serem copiados para `repos`.

Por exemplo, a árvore para [acl](https://www.archlinux.org/packages/?name=acl) se parece com isso:

```
acl
acl/repos
acl/repos/core-i686
acl/repos/core-i686/PKGBUILD
acl/repos/core-x86_64
acl/repos/core-x86_64/PKGBUILD
acl/trunk
acl/trunk/PKGBUILD

```

O código-fonte do pacote não está presente no diretório ABS. Em vez disso, o `PKGBUILD` contém uma URL que vai baixar o código-fonte quando o pacote é compilado.

## Por que eu iria querer usar o ABS?

O Arch Build System é usado para:

*   Compilar ou recompilar um pacote, para qualquer motivo
*   *Make* e instalar novos pacotes de fontes de software para os quais nenhum pacote está instalado ainda (veja [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes"))
*   Personalizar pacotes existentes para atender suas necessidades (habilitar ou desabilitar opções, *patching*)
*   Recompilar todo o seu sistema usando suas *flags* de compilador, "à la FreeBSD" (ex.: com [pacbuilder-svn](https://aur.archlinux.org/packages/pacbuilder-svn/))
*   Compilar e instalar, sem interferências, seu próprio kernel personalizado (veja [Compilação de kernel](/index.php/Kernels#Compilation "Kernels"))
*   Fazer com que módulos de kernel funcionem com seu kernel personalizado
*   Compilar e instalar facilmente uma versão mais nova, antiga, beta ou de desenvolvimento de um pacote do Arch editando o número de versão no PKGBUILD

ABS não é necessário para usar o Arch Linux, mas é útil para automatizar certas tarefas de compilação de fonte.

## Como usar o ABS

### Pré-requisitos

[Instale](/index.php/Install "Install") o pacote [subversion](https://www.archlinux.org/packages/?name=subversion).

### Checkout não-recursivo

**Warning:** Não baixe todo o repositório; siga apenas as instruções abaixo. O repositório SVN todo é gigantesco. Não apenas vai gastar uma quantidade absurda de espaço em disco, mas também vai ocupar o servidor do archlinux.org para você baixá-lo. Se você abusar desse serviço, seu endereço pode ser bloqueado. Nunca use o SVN público para qualquer tipo de *scripting*.

Para fazer *checkout* dos [repositórios](/index.php/Reposit%C3%B3rios "Repositórios") *core*, *extra* e *testing*:

```
$ svn checkout --depth=empty svn://svn.archlinux.org/packages

```

Para fazer *checkout* dos repositórios *community* e *multilib*

```
$ svn checkout --depth=empty svn://svn.archlinux.org/community

```

Em ambos casos, ele cria um diretório vazio, mas ele sabe que é um *checkout* de svn.

### Fazer checkout de um pacote

No diretório contendo o repositório svn que você fez checkout (isto é, *packages* ou *community*), faça:

```
$ svn update *nome-pacote*

```

Isso vai obter o pacote que você requisitou em seu checkout. Daqui para frente, toda vez que você executar *svn update* no nível superior, esse também será atualizado.

Se você especifica um pacote que não existe, svn não vai avisar você. Ele só vai mostrar algo como "At revision 115847", sem criar quaisquer arquivos. Se isso acontecer, verifique se o nome do pacote está escrito corretamente e que o pacote não foi movido para outro repositório (ex. do da *community* para o repositório principal).

**Tip:** Para fazer *checkout* uma versão mais antiga de um pacote, veja [#Faça checkout de uma versão anterior de um pacote](#Fa.C3.A7a_checkout_de_uma_vers.C3.A3o_anterior_de_um_pacote).

Você deve atualizar periodicamente todos os pacotes baixados se você deseja realizar recompilações em revisões mais recentes dos repositórios. Para fazer isso, execute:

```
$ svn update

```

### Configurar makepkg

Veja [makepkg (Português)#Configuração](/index.php/Makepkg_(Portugu%C3%AAs)#Configura.C3.A7.C3.A3o "Makepkg (Português)") sobre como configurar o *makepkg* para compilar pacotes dos [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") que você fez *checkout*.

### Compilar pacote

Copie o diretório contendo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") que você deseja modificar para uma nova localização. Então, faça as modificações desejadas. Então, use *makepkg* como descrito em [makepkg (Português)#Uso](/index.php/Makepkg_(Portugu%C3%AAs)#Uso "Makepkg (Português)") para criar e instalar o novo pacote.

## Dicas e truques

### Preserve pacotes modificados

Atualizar o sistema com o pacman vai substituir um pacote modificado pelo ABS com o pacote de menos nome dos repositórios oficiais. Veja as instruções a seguir para como evitar isso.

Insira um vetor de grupo no PKGBUILD, e adicione o pacote para um grupo chamado `modified`.

 `PKGBUILD`  `groups=('modified')` 

Adicione esse grupo à seção `IgnoreGroup` no `/etc/pacman.conf`.

 `/etc/pacman.conf`  `IgnoreGroup = modified` 

Se novas versões estiverem disponíveis nos repositórios oficiais durante uma atualização de sistema, pacman emite uma nota de que ele está ignorando essa atualização porque ele está na seção IgnoreGroup. Neste ponto, o pacote modificado deve ser recompilado a partir do ABS para evitar atualizações parciais.

### Faça checkout de uma versão anterior de um pacote

Dentro do repositório svn que você faz checkout como descrito em [#Checkout não-recursivo](#Checkout_n.C3.A3o-recursivo) (isto é, "packages" ou "community"), primeiro examine o log:

```
$ svn log *nome-pacote*

```

Descrita a revisão que você deseja examinando o histórico e especifique a revisão que você deseja fazer *checkout*. Por exemplo, para fazer *checkout* da revisão `r1729`, você faria:

```
$ svn update -r1729 *nome-pacote*

```

Isso vai atualizar uma cópia de trabalho existente de *nome-pacote* para a revisão escolhida.

Você também pode especificar uma data. Se nenhuma revisão naquele dia existir, svn vai pegar o pacote mais recente antes daquele tempo. O seguinte exemplo faz checkout da revisão de 2009-03-03:

```
$ svn update -r{20090303} *nome-pacote*

```

Também é possível fazer *checkout* de pacotes nas versões antes de eles terem sido movidos para um outro repositório; veja os logs pela data que eles foram movidos ou o número da última revisão.

## Outras ferramentas

*   [pbget](http://xyne.archlinux.ca/projects/pbget/) - obtém PKGBUILDs de pacotes individuais diretamente da interface web. Inclui suporte ao AUR.
*   [asp](https://github.com/falconindy/asp) - uma ferramenta para gerenciar a compilação de arquivos fontes usados para criar pacotes do Arch Linux. Usa a interface git que oferece fontes mais atualizados.