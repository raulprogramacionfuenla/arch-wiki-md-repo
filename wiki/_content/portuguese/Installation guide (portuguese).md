**Status de tradução:** Esse artigo é uma tradução de [Installation guide](/index.php/Installation_guide "Installation guide"). Data da última tradução: 2019-01-19\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=563317) na versão em inglês.

Este documento irá guiá-lo no processo de instalação [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") usando o [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Antes de instalar, é recomendável ler rapidamente o [FAQ](/index.php/FAQ_(Portugu%C3%AAs) "FAQ (Português)"). Para convenções usadas neste documento, veja [Help:Reading (Português)](/index.php/Help:Reading_(Portugu%C3%AAs) "Help:Reading (Português)"). Em especial, exemplos de código podem conter objetos reservados (formatados em `*italics*`) que devem ser substituídos manualmente.

Para instruções mais detalhadas, veja os respectivos artigos [ArchWiki](/index.php/ArchWiki_(Portugu%C3%AAs) "ArchWiki (Português)") ou as [páginas man](/index.php/P%C3%A1ginas_man "Páginas man") dos vários programas, ambos relacionados neste guia. Para uma ajuda interativa, o [canal IRC](/index.php/Canal_IRC "Canal IRC") e os [fóruns](https://bbs.archlinux.org/) também estão disponíveis.

Arch Linux deve funcionar em qualquer máquina compatível com [x86_64](https://en.wikipedia.org/wiki/pt:AMD64 "wikipedia:pt:AMD64") com um mínimo de 512 MB de RAM. Uma instalação básica com todos os pacotes do grupo [base](https://www.archlinux.org/groups/x86_64/base/) deve levar menos de 800 MB de espaço em disco. Como o processo de instalação precisa obter pacotes de repositório remoto, esse guia presume que uma conexão com a Internet esteja disponível.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pré-instalação](#Pré-instalação)
    *   [1.1 Verificar a assinatura](#Verificar_a_assinatura)
    *   [1.2 Inicializar o ambiente live](#Inicializar_o_ambiente_live)
    *   [1.3 Definir o layout do teclado](#Definir_o_layout_do_teclado)
    *   [1.4 Verificar o modo de inicialização](#Verificar_o_modo_de_inicialização)
    *   [1.5 Conectar à Internet](#Conectar_à_Internet)
    *   [1.6 Atualizar o relógio do sistema](#Atualizar_o_relógio_do_sistema)
    *   [1.7 Partição dos discos](#Partição_dos_discos)
        *   [1.7.1 Exemplos de layouts](#Exemplos_de_layouts)
    *   [1.8 Formatar as partições](#Formatar_as_partições)
    *   [1.9 Montar os sistemas de arquivos](#Montar_os_sistemas_de_arquivos)
*   [2 Instalação](#Instalação)
    *   [2.1 Selecionar os espelhos](#Selecionar_os_espelhos)
    *   [2.2 Instalar os pacotes base](#Instalar_os_pacotes_base)
*   [3 Configurar o sistema](#Configurar_o_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Fuso horário](#Fuso_horário)
    *   [3.4 Localização](#Localização)
    *   [3.5 Configuração de rede](#Configuração_de_rede)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Senha do root](#Senha_do_root)
    *   [3.8 Gerenciador de boot](#Gerenciador_de_boot)
*   [4 Reiniciar](#Reiniciar)
*   [5 Pós-instalação](#Pós-instalação)

## Pré-instalação

A mídia de instalação e suas assinaturas [GnuPG](/index.php/GnuPG "GnuPG") podem ser obtidas a partir da página de [Download](https://archlinux.org/download/).

### Verificar a assinatura

É recomendável verificar a assinatura da imagem antes de usá-la, especialmente ao fazer o download de um *espelho HTTP*, no qual os downloads geralmente são propensos a serem interceptados para [servir imagens maliciosas](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

Em um sistema com [GnuPG](/index.php/GnuPG "GnuPG") instalado, faça isso baixando a *assinatura PGP* (sob *Checksums*) para o diretório da ISO e [verificando-a](/index.php/GnuPG#Verify_a_signature "GnuPG") com:

```
$ gpg --keyserver pgp.mit.edu --keyserver-options auto-key-retrieve --verify archlinux-*versão*-x86_64.iso.sig

```

Alternativamente, de uma instalação existente de Arch Linux, execute:

```
$ pacman-key -v archlinux-*versão*-x86_64.iso.sig

```

**Nota:**

*   A assinatura em si pode ser manipulada se for baixada de um site espelho, em vez de [archlinux.org](https://archlinux.org/download/) como acima. Nesse caso, certifique-se de que a chave pública, que é usada para decodificar a assinatura, seja assinada por outra chave confiável. O comando `gpg` produzirá a impressão digital da chave pública.
*   Outro método para verificar a autenticidade da assinatura é garantir que a impressão digital da chave pública seja idêntica à impressão digital da chave do [desenvolvedor do Arch Linux](https://www.archlinux.org/people/developers/) que assinou o arquivo ISO. Veja [Wikipedia:pt:Criptografia de chave pública](https://en.wikipedia.org/wiki/pt:Criptografia_de_chave_p%C3%BAblica "wikipedia:pt:Criptografia de chave pública") para mais informações sobre o processo de chave pública para autenticar chaves.

### Inicializar o ambiente live

O ambiente *live* pode ser inicializado a partir de uma [unidade flash USB](/index.php/M%C3%ADdia_de_instala%C3%A7%C3%A3o_em_flash_USB "Mídia de instalação em flash USB"), um [disco óptico](/index.php/Optical_disc_drive#Burning "Optical disc drive") ou uma rede com [PXE](/index.php/PXE "PXE"). Para meios alternativos de instalação, consulte [Category:Installation process (Português)](/index.php/Category:Installation_process_(Portugu%C3%AAs) "Category:Installation process (Português)").

*   O apontamento do dispositivo de inicialização atual para uma unidade que contém a mídia de instalação do Arch normalmente pode ser alcançado pressionando-se uma tecla durante a fase [POST](https://en.wikipedia.org/wiki/pt:Power-on_self-test "wikipedia:pt:Power-on self-test"), conforme indicado na tela inicial. Consulte o manual da sua placa-mãe para obter detalhes.
*   Quando o menu do Arch aparecer, selecione *Boot Arch Linux* e pressione `Enter` para entrar no ambiente de instalação.
*   Consulte [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) para uma lista de [parâmetros de inicialização](/index.php/Kernel_parameters#Configuration "Kernel parameters") e [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para uma lista de pacotes incluídos.
*   Você será autenticado no primeiro [console virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") como o usuário *root* sob um prompt de shell [Zsh](/index.php/Zsh "Zsh").

Para trocar para um console diferente — por exemplo, para ver esse guia com [ELinks](/index.php/ELinks "ELinks") junto com a instalação — use o [atalho](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*seta*`. Para [editar](/index.php/Edi%C3%A7%C3%A3o_de_texto "Edição de texto") arquivos de configuração, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") e [vim](/index.php/Vim#Usage "Vim") estão disponíveis.

### Definir o layout do teclado

O [mapa de teclas de console](/index.php/Mapa_de_teclas_de_console "Mapa de teclas de console") padrão é [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Layouts disponíveis podem ser listados com:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Para modificar o layout, acrescente um nome de arquivo ao [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omitindo caminho e extensão de arquivo. Por exemplo, para definir um layout de teclado [ABNT (brasileiro)](https://en.wikipedia.org/wiki/File:KB_Portuguese_Brazil.svg "wikipedia:File:KB Portuguese Brazil.svg"):

```
# loadkeys br-abnt2   

```

[Fontes de console](/index.php/Fontes_de_console "Fontes de console") estão localizadas em `/usr/share/kbd/consolefonts/` e, de forma semelhante, podem ser definidas com [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Verificar o modo de inicialização

Se o modo UEFI estiver disponível em uma placa-mãe [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)") vai [inicializar](/index.php/Inicializar "Inicializar") o Arch Linux adequadamente via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Para verificar isso, liste o diretório [efivars](/index.php/UEFI#UEFI_variables "UEFI"):

```
# ls /sys/firmware/efi/efivars

```

Se o diretório não existir, o sistema pode ser inicializado no modo [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") ou CSM. Veja o manual da sua placa-mãe para detalhes.

### Conectar à Internet

A imagem de instalação habilita o *daemon* [dhcpcd](/index.php/Dhcpcd "Dhcpcd") para [dispositivos de rede cabeada](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) na inicialização. A conexão pode ser verificada com [ping](https://en.wikipedia.org/wiki/pt:Ping "wikipedia:pt:Ping"):

```
# ping archlinux.org

```

Se nenhuma conexão estiver disponível, [pare](/index.php/Pare "Pare") o serviço *dhcpcd* com `systemctl stop dhcpcd@*interface*`, sendo que o nome `*interface*` pode ser [completado com tab](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Continue com a configuração de rede conforme descrito em [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede").

### Atualizar o relógio do sistema

Use [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) para garantir que o relógio do sistema está certo:

```
# timedatectl set-ntp true

```

Para verificar o status do serviço, use `timedatectl status`.

### Partição dos discos

Quando reconhecido pelo sistema *live*, discos são atribuídos a um [dispositivo de bloco](https://en.wikipedia.org/wiki/Device_file#Naming_conventions ou *fdisk*.

```
# fdisk -l

```

Resultados terminando em `rom`, `loop` ou `airoot` podem ser ignorados.

As seguintes [partições](/index.php/Partition "Partition") são **exigidas** para um dispositivo escolhido:

*   Uma partição para o diretório raiz `/`.
*   Se [UEFI](/index.php/UEFI "UEFI") estiver habilitado, uma [partição de sistema EFI](/index.php/EFI_system_partition "EFI system partition").

Se você quiser criar algum dispositivo de bloco empilhado para [LVM](/index.php/LVM "LVM"), [criptografia de sistema](/index.php/Dm-crypt "Dm-crypt") ou [RAID](/index.php/RAID "RAID"), faça isso agora.

#### Exemplos de layouts

| BIOS com [MBR](/index.php/MBR "MBR") ou GPT |
| Ponto de montagem | Partição | [Tipo de partição](https://en.wikipedia.org/wiki/pt:Tipo_de_parti%C3%A7%C3%A3o "wikipedia:pt:Tipo de partição") | Tamanho sugerido |
 /dev/sd*X*1 | [Partição de inicialização BIOS](/index.php/BIOS_boot_partition "BIOS boot partition") | 1 MiB |
| `/mnt` | /dev/sd*X*2 | Linux | Restante do dispositivo |
| [SWAP] | /dev/sd*X*3 | [Swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") Linux | Mais que 512 MiB |
| UEFI com [GPT](/index.php/GPT "GPT") |
| Ponto de montagem | Partição | [Tipo de partição (GUID)](https://en.wikipedia.org/wiki/pt:Tabela_de_Parti%C3%A7%C3%A3o_GUID#Tipos_de_parti.C3.A7.C3.A3o_GUID "wikipedia:pt:Tabela de Partição GUID") | Tamanho sugerido |
| `/mnt/boot` ou `/mnt/efi` | /dev/sd*X*1 | [Partição de sistema EFI](/index.php/EFI_system_partition "EFI system partition") | 260–512 MiB |
| `/mnt` | /dev/sd*X*2 | Linux | Restante do dispositivo |
| [SWAP] | /dev/sd*X*3 | Linux [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") | Mais que 512 MiB |

**Nota:**

*   Use [fdisk](/index.php/Fdisk "Fdisk") ou [parted](/index.php/Parted "Parted") para modificar as tabelas de partição, por exemplo `fdisk /dev/sd*X*`.
*   Um espaço [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") pode ser definido em um [Arquivo swap](/index.php/Arquivo_swap "Arquivo swap") para sistemas de arquivos que possuem suporte a file systems supporting it.

### Formatar as partições

Assim que as partições tenham sido criadas, cada uma deve ser formatada com um [sistema de arquivos](/index.php/File_system "File system") adequado. Por exemplo, para formatar a partição raiz em `/dev/sd*X*2` com `*ext4*`, execute:

```
# mkfs.*ext4* /dev/sd*X*2

```

Se você criou uma partição para swap (por exemplo, `/dev/*sda3*`), inicialize-a com *mkswap*:

```
# mkswap /dev/sd*X*3
# swapon /dev/sd*X*3

```

Veja [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") para detalhes.

### Montar os sistemas de arquivos

[Monte](/index.php/Mount "Mount") o sistema de arquivos da partição raiz em `/mnt`, por exemplo:

```
# mount /dev/sd*X*2 /mnt

```

Onde necessário, crie pontos de montagem e monte as partições correspondentes. Por exemplo:

```
# mkdir /mnt/efi
# mount /dev/sd*X*2 /mnt/efi

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) vai detectar os sistemas de arquivos montados e espaços swap.

## Instalação

### Selecionar os espelhos

Pacotes a serem instalados devem ser baixados de [espelhos](/index.php/Espelhos "Espelhos") *(mirrors)*, que são definidos na `/etc/pacman.d/mirrorlist`. No sistema *live*, todos os espelhos estão habilitados e ordenados por seu status e velocidade de sincronização à época em que a imagem de instalação foi criada.

Quanto mais alto um espelho está posicionado na lista, mais prioritário ele será ao baixar um pacote. Você pode querer editar o arquivo e mover espelhos geograficamente mais pertos para o topo da lista, apesar de que outros critérios devem ser levados em consideração.

Esse arquivo será posteriormente copiado para o novo sistema por *pacstrap*, então é melhor fazer direito.

### Instalar os pacotes base

Use o script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar o grupo de pacotes [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base

```

Esse grupo não inclui todas as ferramentas da instalação *live*, tal como [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) ou firmware de rede sem fio específico; veja [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para comparação.

Para [instalar](/index.php/Instalar "Instalar") pacotes e outros grupos, tal como [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), anexe os nomes ao *pacstrap* (separados por espaço) ou a comandos [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") após a etapa do [#Chroot](#Chroot).

## Configurar o sistema

### Fstab

Gerar um arquivo [fstab](/index.php/Fstab "Fstab") (use `-U` ou `-L` para definir por [UUID](/index.php/UUID "UUID") ou rótulos, respectivamente):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Verifique o arquivo resultante em `/mnt/etc/fstab` em seguida e edite-o caso haja erros.

### Chroot

[Mude a raiz](/index.php/Change_root_(Portugu%C3%AAs) "Change root (Português)") para novo sistema:

```
# arch-chroot /mnt

```

### Fuso horário

Defina o [fuso horário](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Região*/*Cidade* /etc/localtime

```

Por exemplo, para definir para o fuso horário de Brasília (*BRT* ou *BRST*), execute:

```
# ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

```

Execute [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) para gerar `/etc/adjtime`:

```
# hwclock --systohc

```

Esse comando presume que o relógio de hardware está definido para [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). Veja [System time#Time standard](/index.php/System_time#Time_standard "System time") para mais detalhes.

### Localização

Descomente `pt_BR.UTF-8 UTF-8` e qualquer outro [locale](/index.php/Locale_(Portugu%C3%AAs) "Locale (Português)") em `/etc/locale.gen`, e gere-as com:

```
# locale-gen

```

Defina a [variável](/index.php/Vari%C3%A1vel "Variável") `LANG` em [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) adequadamente, por exemplo:

 `/etc/locale.conf`  `LANG=*pt_BR.UTF-8*` 

Se você [definir o layout do teclado](#Definir_o_layout_do_teclado), torne as alterações persistentes em [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*br-abnt2*` 

### Configuração de rede

Crie o arquivo [hostname](/index.php/Hostname_(Portugu%C3%AAs) "Hostname (Português)"):

 `/etc/hostname` 
```
*meuhostname*

```

Adicione entradas correspondentes ao [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*meuhostname*.localdomain	*meuhostname***

```

Se o sistema tem um endereço IP permanente, ele deve ser usado em vez de `127.0.1.1`.

Complete a [configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede") para o ambiente recém-instalado.

### Initramfs

Criar um novo *initramfs* geralmente não é necessário, porque [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") foi executado na instalação do pacote [linux](https://www.archlinux.org/packages/?name=linux) com *pacstrap*.

Para [LVM](/index.php/LVM#Configure_mkinitcpio "LVM"), [criptografia de sistema](/index.php/Dm-crypt "Dm-crypt") or [RAID](/index.php/RAID#Configure_mkinitcpio "RAID"), modifique o [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) e recrie a imagem initramfs:

```
# mkinitcpio -p linux

```

### Senha do root

Defina a [senha](/index.php/Senha "Senha") do *root* (também conhecido como "superusuário"):

```
# passwd

```

### Gerenciador de boot

Veja [Processo de inicialização do Arch#Gerenciador de boot](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch#Gerenciador_de_boot "Processo de inicialização do Arch") para uma lista de gerenciadores de boot com suporte a Linux.

**Nota:** Se você tiver um CPU Intel ou AMD, habilite atualizações de [microcódigo](/index.php/Microcode "Microcode").

## Reiniciar

Saia de ambiente *chroot* digitando `exit` ou pressionando `Ctrl+D`.

Opcionalmente, desmonte todas as partições com `umount -R /mnt`: isso permite noticiar quaisquer partições "ocupadas" e localizar a causa com o [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Finalmente, reinicie a máquina digitando `reboot`: quaisquer partições que ainda estejam montadas serão desmontadas automaticamente por *systemd*. Lembre-se de remover a mídia de instalação e, então, se autenticando no novo sistema com a conta de root.

## Pós-instalação

Veja [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais") por instruções de gerenciamento de sistema e tutoriais pós-instalação (como instalar uma interface gráfica de usuário, som ou um touchpad).

Para uma lista de aplicativos que podem ser de seu interesse, veja [Lista de aplicativos](/index.php/List_of_applications "List of applications").