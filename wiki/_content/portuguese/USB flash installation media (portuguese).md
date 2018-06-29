Artigos relacionados

*   [CD Burning](/index.php/CD_Burning "CD Burning")
*   [Archiso](/index.php/Archiso "Archiso")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

Esta página discute vários métodos multiplataforma sobre como criar uma unidade USB do instalador do Arch Linux (também conhecida como *"unidade flash", "pendrive", "USB stick", "flash drive", "USB key"* etc.) para inicializar na BIOS e sistemas UEFI. O resultado será um sistema LiveUSB (similar a LiveCD) que pode ser usado para instalar o Arch Linux, manutenção do sistema ou para fins de recuperação, e que, por causa da natureza do [SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS"), descartará todas as alterações quando o computador for desligado.

Se você deseja executar uma instalação completa do Arch Linux a partir de uma unidade USB (por exemplo, com configurações persistentes), consulte [Instalando Arch Linux em um pendrive](/index.php/Instalando_Arch_Linux_em_um_pendrive "Instalando Arch Linux em um pendrive"). Se você gostaria de usar seu pendrive inicializável com Arch Linux como um sistema de recuperação, veja [chroot](/index.php/Change_root_(Portugu%C3%AAs) "Change root (Português)").

## Contents

*   [1 USB inicializável com BIOS e UEFI](#USB_inicializ.C3.A1vel_com_BIOS_e_UEFI)
    *   [1.1 Usando dd](#Usando_dd)
        *   [1.1.1 No GNU/Linux](#No_GNU.2FLinux)
        *   [1.1.2 No Windows](#No_Windows)
            *   [1.1.2.1 Usando Rufus](#Usando_Rufus)
            *   [1.1.2.2 Usando USBwriter](#Usando_USBwriter)
            *   [1.1.2.3 Usando win32diskimager](#Usando_win32diskimager)
            *   [1.1.2.4 Usando Cygwin](#Usando_Cygwin)
            *   [1.1.2.5 dd para Windows](#dd_para_Windows)
        *   [1.1.3 No macOS](#No_macOS)
    *   [1.2 Usando formatação manual](#Usando_formata.C3.A7.C3.A3o_manual)
        *   [1.2.1 No GNU/Linux](#No_GNU.2FLinux_2)
        *   [1.2.2 No Windows](#No_Windows_2)
*   [2 Outros métodos para sistemas BIOS](#Outros_m.C3.A9todos_para_sistemas_BIOS)
    *   [2.1 No GNU/Linux](#No_GNU.2FLinux_3)
        *   [2.1.1 Usando uma unidade USB multiboot](#Usando_uma_unidade_USB_multiboot)
        *   [2.1.2 Usando o utilitário de disco do GNOME](#Usando_o_utilit.C3.A1rio_de_disco_do_GNOME)
        *   [2.1.3 Fazendo uma unidade USB-ZIP](#Fazendo_uma_unidade_USB-ZIP)
        *   [2.1.4 Usando UNetbootin](#Usando_UNetbootin)
    *   [2.2 No Windows](#No_Windows_3)
        *   [2.2.1 A forma Flashnul](#A_forma_Flashnul)
        *   [2.2.2 Carregar a mídia de instalação da RAM](#Carregar_a_m.C3.ADdia_de_instala.C3.A7.C3.A3o_da_RAM)
            *   [2.2.2.1 Preparar a unidade flash USB](#Preparar_a_unidade_flash_USB)
            *   [2.2.2.2 Copiar os arquivos necessários à unidade flash USB](#Copiar_os_arquivos_necess.C3.A1rios_.C3.A0_unidade_flash_USB)
            *   [2.2.2.3 Criar o arquivo de configuração](#Criar_o_arquivo_de_configura.C3.A7.C3.A3o)
            *   [2.2.2.4 Etapas finais](#Etapas_finais)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## USB inicializável com BIOS e UEFI

### Usando dd

**Nota:** Este método é recomendado devido à sua simplicidade. Se não funcionar, mude para o método alternativo [#Usando formatação manual](#Usando_formata.C3.A7.C3.A3o_manual) abaixo.

**Atenção:** Isso destruirá irrevogavelmente todos os dados em `/dev/**sdx**`. Para restaurar a unidade USB como um dispositivo de armazenamento utilizável vazio após usar a imagem ISO do Arch, a assinatura do sistema de arquivos iso9660 precisa ser removida executando `wipefs --all /dev/**sdx**` como root, antes de [reparticionar](/index.php/Repartition "Repartition") e [reformatar](/index.php/Reformat "Reformat") a unidade USB.

#### No GNU/Linux

**Dica:** Descubra o nome do sua unidade USB com `lsblk`. Certifique-se de que ela **não** esteja montada.

Execute o seguinte comando, substituindo `/dev/**sdx**` pela sua unidade, por exemplo `/dev/sdb`. (**não** anexe um número de partição, de forma a **não** usar algo como `/dev/sdb**1**`)

```
# dd bs=4M if=/path/to/archlinux.iso of=/dev/**sdx** status=progress oflag=sync

```

Veja [Utilitários principais#dd](/index.php/Utilit%C3%A1rios_principais#dd "Utilitários principais") para mais informações sobre `dd`. Veja [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1#DESCRIPTION) para mais informações sobre `oflag=sync`.

#### No Windows

##### Usando Rufus

[Rufus](https://rufus.akeo.ie/) é um escritor multiuso de ISO em USB. Basta selecionar a ISO do Arch Linux, a unidade USB na qual você deseja criar o Arch Linux inicializável e clicar em Iniciar.

Como o Rufus não se importa se a unidade está formatada corretamente ou não e fornece uma GUI, ela pode ser a ferramenta mais fácil e mais robusta a ser usada.

**Nota:** Certifique-se de selecionar o modo **Imagem DD** no menu suspenso ou a imagem será transferida incorretamente.

##### Usando USBwriter

Esse método não requer nenhuma solução alternativa e é tão simples quanto `dd` no Linux. Basta baixar o ISO do Arch Linux e, com permissões de administrador local, use o utilitário [USBwriter](http://sourceforge.net/p/usbwriter/wiki/Documentation/) para gravar na memória flash USB.

##### Usando win32diskimager

[win32diskimager](https://sourceforge.net/projects/win32diskimager/) é outra ferramenta gráfica de gravação de ISO para Windows. Basta selecionar sua imagem ISO e a letra da unidade USB de destino (talvez seja necessário formatá-la primeiro para atribuir uma letra de unidade) e clicar em Write.

##### Usando Cygwin

Certifique-se que sua instalação de [Cygwin](http://www.cygwin.com/) contém o pacote `dd`.

**Dica:** Se você não quiser instalar o Cygwin, você pode fazer o download do `dd` para Windows em [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd) aqui. Veja a próxima seção para mais informações.

Coloque seu arquivo de imagem em seu diretório *home*:

```
C:\cygwin\home\joao\

```

Execute o cygwin como administrador (necessário para o cygwin acessar o hardware). Para escrever na sua unidade USB, use o seguinte comando:

```
dd if=*imagem.iso* of=\\.\**x**: bs=4M

```

sendo *imagem.iso* o caminho para o arquivo de imagem iso dentro do diretório `cygwin` e `\\.\**x**:` é a sua unidade flash USB onde `**x**` é a letra designada pelo Windows, por exemplo `\\.\d:`.

No Cygwin 6.0, descubra a partição correta com:

```
cat /proc/partitions

```

e escreva a imagem ISO com as informações da saída. Exemplo:

**Atenção:** Isso excluirá irrevogavelmente todos os arquivos da sua unidade flash USB. Portanto, certifique-se de não ter arquivos importantes na unidade flash antes de fazer isso.

```
dd if=imagem.iso of=/dev/sdb bs=4M

```

##### dd para Windows

Uma versão do *dd* licenciada sob GPL para Windows está disponível em [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd). A vantagem dela sobre o Cygwin é um download menor. Use-a como mostrado nas instruções do Cygwin acima.

Para começar, baixe a última versão do dd para Windows. Uma vez baixado, extraia o conteúdo do arquivo em Downloads ou em outro lugar.

Agora, inicie seu `prompt de comando` como administrador. Em seguida, mude o diretório (`cd`) para o diretório Downloads.

Se a sua ISO do Arch Linux estiver em outro lugar, você pode precisar declarar o caminho completo, por conveniência, você pode querer colocar o ISO do Arch Linux na mesma pasta que o executável dd. O formato básico do comando será semelhante a este:

```
# dd if=*archlinux-2017-XX-YY-x86_64.iso* od=\\.\*x*: bs=4M

```

**Nota:** As letras da unidade do Windows estão vinculadas a uma partição. Para permitir a seleção de todo o disco, o *dd para Windows* fornece o parâmetro `od`, que é usado nos comandos acima. Note, entretanto, que este parâmetro é específico para *dd para Windows* e não pode ser encontrado em outras implementações de *dd*.

**Atenção:** Porque o `od` é usado, todas as partições no disco selecionado serão destruídas. Esteja absolutamente certo de que você está direcionando dd para a unidade correta antes de executar.

Simplesmente substitua os vários pontos nulos (indicados por um "x") com a data correta e letra de unidade correta. Aqui está um exemplo completo. Por exemplo:

```
# dd if=ISOs\archlinux-2017.04.01-x86_64.iso od=\\.\d: bs=4M

```

**Nota:** Alternativamente, substitua a letra da unidade com `\\.\PhysicalDrive*X*`, sendo `*X*` o número da unidade física (inicia do 0). Por exemplo: `# dd if=ISOs\archlinux-2017.04.01-x86_64.iso of=\\.\PhysicalDrive1 bs=4M` 

Você pode descobrir o número da unidade física digitando `wmic diskdrive list brief` no prompt de comando ou com `dd --list`

Qualquer janela do Explorer deve ser fechada ou o dd informará um erro.

#### No macOS

Primeiro, você precisa identificar o dispositivo USB. Abra `/Applications/Utilities/Terminal` e liste todos os dispositivos de armazenamento com o comando:

```
$ diskutil list

```

Seu dispositivo USB aparecerá como algo como `/dev/disk2 (external, physical)`. Verifique se esse é o dispositivo que você deseja apagar verificando seu nome e tamanho e, em seguida, use seu identificador para os comandos abaixo, em vez de /dev/disk*X*.

Um dispositivo USB é normalmente automontado no macOS e você pode ter que desmontá-lo (não ejetar) antes de escrever blocos nele com `dd`. No Terminal, execute:

```
$ diskutil unmountDisk /dev/disk*X*

```

Agora, copie o arquivo de imagem ISO para o dispositivo. O comando `dd` é similar à sua contraparte Linux, mas note o 'r' antes do modo 'disk' para modo *raw*, que torna a transferência muito mais rápida:

```
# dd if=caminho/para/arch.iso of=/dev/**r**disk*X* bs=1m

```

Note que `disk*X*` aqui não deve incluir o sufixo `s1` ou, do contrário, o dispositivo USB só será inicializável no modo UEFI e não no legado. Após a conclusão, o macOS reclamar "O disco que você inseriu não podia ser lido por este computador". Selecione 'Ignorar'. O dispositivo USB será inicializável.

### Usando formatação manual

#### No GNU/Linux

Esse método é mais complicado do que gravar a imagem diretamente com `dd`, mas mantém a unidade flash utilizável para armazenamento de dados (ou seja, o ISO é instalado em uma partição específica dentro de um [dispositivo já particionado](/index.php/Partitioning "Partitioning") sem alterar outras partições).

**Nota:** Aqui, denotaremos a partição de destino como `/dev/sd**Xn**`. Em qualquer um dos seguintes comandos, ajuste **X** e **n** de acordo com o seu sistema.

*   Certifique-se que o pacote [syslinux](https://www.archlinux.org/packages/?name=syslinux) está instalado no sistema.

*   Se ainda não tiver feito, crie a tabela de partição e/ou a partição no dispositivo antes de continuar. A partição `/dev/sd**Xn**` deve ser formatada para [FAT32](/index.php/FAT32 "FAT32").

*   Monte a imagem ISO, monte o sistema de arquivos FAT32 localizado no dispositivo flash USB e copie o conteúdo da imagem ISO para ele. Em seguida, desmonte a imagem ISO, mas mantenha a partição FAT32 montada (isso será usado em etapas subsequentes). Por exemplo:

```
# mkdir -p /mnt/{iso,usb}
# mount -o loop archlinux-2017.04.01-x86_64.iso /mnt/iso
# mount /dev/sd**Xn** /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/iso

```

Para inicializar um rótulo ou um [UUID](/index.php/UUID "UUID") para selecionar, é necessário informar a partição a ser inicializada. Por padrão, o rótulo `ARCH_2017**XX**` (com o mês de lançamento apropriado) é usado. Assim, o rótulo da partição precisa ser definido de acordo, por exemplo, usando *gparted*. Alternativamente, você pode mudar este comportamento alterando as linhas terminadas por `archisolabel=ARCH_2017**XX**` no arquivo `/mnt/usb/arch/boot/syslinux/archiso_sys.cfg` (para inicialização de BIOS), e em `/mnt/usb/loader/entries/archiso-x86_64.conf` (para inicialização com UEFI). Para usar um UUID, substitua as porções de linhas com `archiso*dispositivo*=/dev/disk/by-uuid/**SEU-UUID**`. O UUID pode ser recuperado com `blkid -o *valor* -s UUID /dev/sd**Xn**`.

**Atenção:** A incompatibilidade de rótulos ou o UUID errado impede a inicialização da mídia criada.

O Syslinux já está pré-instalado em */mnt/usb/arch/boot/syslinux*. Instale-o completamente nessa pasta seguindo [Syslinux#Manual install](/index.php/Syslinux#Manual_install "Syslinux"). As instruções são reproduzidas aqui para sua conveniência:

*   Sobrescreva os módulos existentes do Syslinux (`*.c32` arquivos presentes no USB (da ISO) com os do pacote syslinux (encontrado em */usr/lib/syslinux/bios*). Isso é necessário para evitar falhas de inicialização devido a uma possível incompatibilidade de versão.

```
# cp /usr/lib/syslinux/bios/*.c32 /mnt/usb/arch/boot/syslinux

```

*   Execute:

```
# extlinux --install /mnt/usb/arch/boot/syslinux

```

*   Desmonte a partição (`umount /mnt/usb`).

*   Marque a partição como ativa (ou “inicializável”).

#### No Windows

**Nota:**

*   Para formatação manual, não use nenhum utilitário **criador de USB inicializável** para criar o USB UEFI inicializável. Para formatação manual, não use *dd para Windows* para inserir o ISO na unidade USB.

*   Nos comandos abaixo, **X:** é considerado como sendo a unidade flash USB no Windows.

*   Windows usa barra invertida `\` como separador de caminho, então o mesmo é usado nos comandos abaixo.

*   Todos os comandos devem ser executados no prompt de comandos do Windows **como administrador**.

*   `>` denota o prompt de comando do Windows.

*   Particione e formate o drive USB usando o [particionador de USB Rufus](http://rufus.akeo.ie/). Selecione a opção de esquema de partição como **MBR para BIOS e UEFI** e sistema de arquivos como **FAT32**. Desmarque a opção "Criar um disco inicializável usando imagem ISO" e "Criar arquivos estendidos de rótulo e ícone".

*   Altere o **Rótulo do Volume** da unidade flash USB `X:` para corresponder ao LABEL mencionado na parte `archisolabel=` em `<ISO>\loader\entries\archiso-x86_64.conf`. Esta etapa é necessária para o ISO oficial ([Archiso](/index.php/Archiso "Archiso")). Esta etapa também pode ser executada usando o Rufus, durante a etapa anterior de "particionamento e formatação".

*   Extraia a ISO (similar a extrair o arquivo ZIP) para a unidade flash USB (usando [7-Zip](http://7-zip.org/).

*   Baixe os binários oficiais Syslinux 6.xx (arquivo zip) de [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) e extrai-a. A versão do Syslinux deve ser a mesma versão usada na imagem ISO.

*   Execute o comando a seguir (no prompt de comando do Windows, como admin):

```
> cd bios\
> for /r %Y in (*.c32) do copy "%Y" "X:\arch\boot\syslinux\" /y
> copy mbr\*.bin X:\arch\boot\syslinux\ /y

```

*   Instale Syslinux no USB executando (use `win64\syslinux64.exe` para Windows x64):

```
> cd bios\
> win32\syslinux.exe -d /arch/boot/syslinux -i -a -m X:

```

**Nota:**

*   A etapa acima instala o `ldlinux.sys` do Syslinux no VBR da partição USB, define a partição como "active/boot" na tabela de partições MBR e grava o código de inicialização do MBR no primeiro código de inicialização de 440 bytes região do USB.

*   O opção `-d` espera um caminho com separador de caminho de barra como nos sistemas * unix.

## Outros métodos para sistemas BIOS

### No GNU/Linux

#### Usando uma unidade USB multiboot

Isso permite inicializar vários ISOs de um único dispositivo USB, incluindo o archiso. Atualizar uma unidade USB existente para uma ISO mais recente é mais simples do que na maioria dos outros métodos. Veja [Unidade USB de inicialização múltipla](/index.php/Multiboot_USB_drive "Multiboot USB drive").

#### Usando o utilitário de disco do GNOME

As distribuições Linux que usam o GNOME podem facilmente criar um live CD através do [nautilus](https://www.archlinux.org/packages/?name=nautilus) e do [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility). Basta clicar com o botão direito no arquivo .iso e selecionar "Abrir com Gravador de imagem de disco". Quando o Utilitário de disco do GNOME abrir, especifique a unidade flash no menu suspenso "Destino" e clique em "Iniciar Restauração".

#### Fazendo uma unidade USB-ZIP

Para alguns sistemas BIOS antigos, somente a inicialização de unidades USB-ZIP é suportada. Este método permite que você ainda inicialize a partir de uma unidade USB-HDD.

**Atenção:** Isso destruirá todas as informações da sua unidade flash USB!

*   Baixe [syslinux](https://www.archlinux.org/packages/?name=syslinux) e [mtools](https://www.archlinux.org/packages/?name=mtools) de repositórios oficiais.
*   Localize sua unidade usb com `lsblk`.
*   Digite `mkdiskimage -4 /dev/sd**x** 0 64 32` (substitua x com a letra de sua unidade). Isso vai levar um tempo.

A partir daqui, continue com o método de formatação manual. A partição será `/dev/sd**x**4` por causa da forma que unidades ZIP funcionam.

**Nota:** Não formate a unidade como FAT32; mantenha-o como FAT16.

#### Usando UNetbootin

O UNetbootin pode ser usado em qualquer distribuição Linux ou no Windows para copiar seu iso para um dispositivo USB. No entanto, o Unetbootin sobrescreve o syslinux.cfg, portanto, ele cria um dispositivo USB que não inicializa corretamente. Por esse motivo, *'Unetbootin não é recomendado'* -- use `dd` ou um dos outros métodos discutidos neste tópico.

**Atenção:** O UNetbootin escreve sobre o `syslinux.cfg` padrão; isso deve ser restaurado antes que o dispositivo USB seja inicializado corretamente.

Edite `syslinux.cfg`:

 `sysconfig.cfg` 
```
default menu.c32
prompt 0
menu title Archlinux Installer
timeout 100

label unetbootindefault
menu label Archlinux_x86_64
kernel /arch/boot/x86_64/vmlinuz
append initrd=/arch/boot/x86_64/archiso.img archisodevice=/dev/sd**x1** ../../
```

Em `/dev/sd**x1**` você deve substituir **x** pela primeira letra livre após a última letra em uso no sistema onde você está instalando o Arch Linux (p.ex., Se você tiver dois discos rígidos, use `c`. Você pode fazer essa alteração durante a primeira fase de inicialização pressionando `Tab` quando o menu é exibido.

### No Windows

#### A forma Flashnul

[flashnul](https://translate.google.com/translate?hl=&sl=ru&tl=en&u=http%3A%2F%2Fshounen.ru%2Fsoft%2Fflashnul%2Freadme.rus.html&sandbox=1) is an utility to verify the functionality and maintenance of Flash-Memory (USB-Flash, IDE-Flash, SecureDigital, MMC, MemoryStick, SmartMedia, XD, CompactFlash etc).

From a command prompt, invoke flashnul with `-p`, and determine which device index is your USB drive, e.g.:

 `C:\>flashnul -p` 
```
Avaible physical drives:
Avaible logical disks:
C:\
D:\
E:\

```

When you have determined which device is the correct one, you can write the image to your drive, by invoking flashnul with the device index, `-L`, and the path to your image, e.g:

```
C:\>flashnul **E:** -L *path\to\arch.iso*

```

As long as you are really sure you want to write the data, type yes, then wait a bit for it to write. If you get an access denied error, close any Explorer windows you have open.

If under Vista or Win7, you should open the console as administrator, or else flashnul will fail to open the stick as a block device and will only be able to write via the drive handle windows provides

**Note:** Confirmed that you need to use drive letter as opposed to number. flashnul 1rc1, Windows 7 x64.

#### Carregar a mídia de instalação da RAM

This method uses [Syslinux](/index.php/Syslinux "Syslinux") and a [Ramdisk](/index.php/Ramdisk "Ramdisk") ([MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)) to load the entire Arch Linux ISO image into RAM. Since this will be running entirely from system memory, you will need to make sure the system you will be installing this on has an adequate amount. A minimum amount of RAM between 500 MB and 1 GB should suffice for a MEMDISK based, Arch Linux install.

For more information on Arch Linux system requirements as well as those for MEMDISK see the [Installation guide](/index.php/Installation_guide "Installation guide") and [here](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries). For reference, here is the [preceding forum thread](https://bbs.archlinux.org/viewtopic.php?id=135266).

**Tip:** Once the installer has completed loading you can simply remove the USB stick and even use it on a different machine to start the process all over again. Utilizing MEMDISK also allows booting and installing Arch Linux to and from the same USB flash drive.

##### Preparar a unidade flash USB

Begin by formatting the USB flash drive as **FAT32**. Then create the following folders on the newly formatted drive.

*   `Boot`
    *   `Boot/ISOs`
    *   `Boot/Settings`

##### Copiar os arquivos necessários à unidade flash USB

Next copy the ISO that you would like to boot to the `Boot/ISOs` folder. After that, extract from the following files from the latest release of [syslinux](https://www.archlinux.org/packages/?name=syslinux) from [here](http://www.kernel.org/pub/linux/utils/boot/syslinux/) and copy them into the following folders.

*   `./win32/syslinux.exe` to the Desktop or Downloads folder on your system.
*   `./memdisk/memdisk` to the `Settings` folder on your USB flash drive.

##### Criar o arquivo de configuração

After copying the needed files, navigate to the USB flash drive, /boot/Settings and create a `syslinux.cfg` file.

**Warning:** On the `INITRD` line, be sure to use the name of the ISO file that you copied to your `ISOs` folder!
 `/Boot/Settings/syslinux.cfg` 
```
DEFAULT arch_iso

LABEL arch_iso
        MENU LABEL Arch Setup
        LINUX memdisk
        INITRD /Boot/ISOs/archlinux-2017.04.01-x86_64.iso
        APPEND iso
```

For more information on Syslinux see the [Arch Wiki article](/index.php/Syslinux "Syslinux").

##### Etapas finais

Finally, create a `*.bat` file where `syslinux.exe` is located and run it ("Run as administrator" if you are on Vista or Windows 7):

 `C:\Documents and Settings\username\Desktop\install.bat` 
```
@echo off
syslinux.exe -m -a -d /Boot/Settings X:
```

## Solução de problemas

*   If you get the "device did not show up after 30 seconds" error due to the `/dev/disk/by-label/ARCH_XXXXYY` not mounting, try renaming your USB media to `ARCH_XXXXYY` (e.g. `ARCH_201501`).

*   If you get errors, try using another USB device. There are case scenarios in which it solved all issues.

## Veja também

*   [Gentoo wiki - LiveUSB/HOWTO](https://wiki.gentoo.org/wiki/LiveUSB/HOWTO)
*   [Fedora wiki - How to create and use Live USB](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)
*   [openSUSE wiki - SDB:Live USB stick](http://en.opensuse.org/SDB:Live_USB_stick)