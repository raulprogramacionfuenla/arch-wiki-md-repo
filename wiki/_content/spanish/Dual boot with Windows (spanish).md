Este es una artículo simple que detalla los diferentes métodos de coexistencia entre Arch y Windows.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Información Importante](#Información_Importante)
    *   [1.1 Limitaciones UEFI vs. BIOS en Windows](#Limitaciones_UEFI_vs._BIOS_en_Windows)
    *   [1.2 Limitiaciones del medio de instalación](#Limitiaciones_del_medio_de_instalación)
    *   [1.3 Limitaciones de los cargadores de arranque UEFI v/s BIOS](#Limitaciones_de_los_cargadores_de_arranque_UEFI_v/s_BIOS)
    *   [1.4 Arranque seguro UEFI](#Arranque_seguro_UEFI)
    *   [1.5 Arranque rápido](#Arranque_rápido)
    *   [1.6 Limitaciones de nombres de archivos en Windows](#Limitaciones_de_nombres_de_archivos_en_Windows)
*   [2 Instalación](#Instalación)
    *   [2.1 Sistemas BIOS](#Sistemas_BIOS)
        *   [2.1.1 Utilizando un cargador de arranque Linux](#Utilizando_un_cargador_de_arranque_Linux)
        *   [2.1.2 Utilizando un cargador de aranque Windows](#Utilizando_un_cargador_de_aranque_Windows)
            *   [2.1.2.1 Cargador de arranque de Windows Vista/7/8/8.1](#Cargador_de_arranque_de_Windows_Vista/7/8/8.1)
            *   [2.1.2.2 Cargador de arranque de Windows 2000/XP](#Cargador_de_arranque_de_Windows_2000/XP)
    *   [2.2 Sistema UEFI](#Sistema_UEFI)
    *   [2.3 Solución de Problemas](#Solución_de_Problemas)
        *   [2.3.1 No es posible crear una nueva partición ni localizar la existente](#No_es_posible_crear_una_nueva_partición_ni_localizar_la_existente)
*   [3 Estandares de Tiempo](#Estandares_de_Tiempo)
*   [4 Ver también](#Ver_también)

## Información Importante

### Limitaciones UEFI vs. BIOS en Windows

Microsoft impone limitaciones en el modo de arranque de firmware y el estilo de partición que están soportadas, según la versión de Windows utilizada:

*   **Windows XP** versiones **x86 32 bits** como **x86_64** (también llamado x64) (RTM y todos los Service Packs) solo admiten arranque BIOS y de discos MBR/msdos. No soportan el arranque en modo UEFI (IA32 o x86_64) desde ningún tipo de partición (MBR o GPT) ni tampoco en modo BIOS desde discos GPT.
*   **Windows Vista** o **7** versiones **x86 32 bits** (RTM y todos los Service Packs) solo admiten arranque BIOS y de discos MBR/msdos. No soportan el arranque en modo UEFI (IA32 o x86_64) desde ningún tipo de partición (MBR o GPT) ni tampoco en modo BIOS desde discos GPT.
*   **Windows Vista RTM x86_64** (solo versión RTM) admiten únicamente arranque BIOS y de discos MBR/msdos. No soportan el arranque en modo UEFI (IA32 o x86_64) desde ningún tipo de partición (MBR o GPT) ni tampoco en modo BIOS desde discos GPT.
*   **Windows Vista** (SP1 o superior, no RTM) y **Windows 7** versiones **x86_64** permiten el arranque en modo UEFI x86_64 solo de disco GPT, o en modo BIOS desde discos MBR/msdos. No soportan arranque UEFI IA32 (x86 de 32 bits) desde el disco GPT/MBR, arranque UEFI x86_64 de discos MBR/msdos o arranque BIOS desde discos GPT.
*   **Windows 8/8.1 x86 de 32 bits** admite el arranque en modo UEFI IA32 desde discos GPT solamente, o en modo BIOS desde discos MBR/msdos. No soportan arranques UEFI x86_64 desde discos GPT/MBR ni arranque UEFI x86_64 desde discos MBR/msdos disco ni arranque BIOS desde discos GPT. En el mercado, los únicos sistemas que se sabe que se entregue con IA32 (U)EFI son algunos modelos antiguos (pre-2010?) de Macs Intel o tablet Windows con Sistemas Intel Atom System-on-Chip (Clover Trail y Bay Trail), en el que se arranca en modo UEFI IA32 y solo desde disco GPT.
*   **Windows 8/8.1** **x86_64** permiten el arranque en modo UEFI x86_64 de disco GPT solamente, o en modo BIOS desde disco MBR/msdos. No soportan arranque UEFI IA32, arranque UEFI x86_64 desde discos MBR/msdos o arranque BIOS desde discos GPT.

En el caso de un sistema preinstalado:

*   TODOS los sistemas preinstalados con Windows XP, Vista o 7 de 32 bits, con independencia de la versión de Service Pack, el modo de bits (bitness) del procesador (32 o 64), la edición (SKU) o la presencia de soporte UEFI del firmware, arrancan en modo BIOS-MBR por defecto.
*   LA MAYORÍA de los sistemas de preinstalado con Windows 7 x86_64, con independencia de la versión de Service Pack, el modo de bits o la edición (SKU), arrancan en modo BIOS-MBR por defecto. Muy pocos sistemas recientes preinstalados con Windows 7 arrancan en modo UEFI x86_64-GPT de forma predeterminada.
*   TODOS los sistemas preinstalados con Windows 8/8.1 en modo UEFI-GPT. El modo de bits del firmware coincide con el de Windows es decir, Windows 8/8.1 x86_64 arranca en modo UEFI x86_64 y Windows 8/8.1 de 32 bits arranca en modo UEFI IA32.

La mejor manera de detectar el modo de inicio de Windows es hacer lo siguiente (información del [.html aquí](http://www.eightforums.com/tutorials/29504-bios-mode-see-if-windows-boot-uefi-legacy-mode)):

*   Arranque Windows
*   Pulse la tecla Win y "R" para iniciar la ventana Ejecutar
*   En la ventana Ejecutar teclee "msinfo32" y pulse Enter
*   En la ventana **Información del sistema**, seleccione **Resumen del sistema** en la izquierda y verifique el valor de **modo de BIOS** en la derecha.
*   Si el valor es **UEFI**, Windows se inicia en modo UEFI-GPT. Si el valor es **Heredado**('legacy'), Windows se inicia en modo BIOS-MBR.

En general, Windows fuerza el tipo de partición dependiendo del modo de firmware utilizado, es decir, si Windows se arranca en modo UEFI, solo se puede instalar en un disco GPT. Si Windows se inicia en modo tradicional BIOS, se puede instalar solo en un disco MBR (también llamado particionado estilo**msdos**) de disco. Esta es una limitación impuesta por el instalador de Windows, y a partir de abril de 2014 no hay oficialmente (Microsoft) modo para instalar Windows en configuraciones UEFI-MBR o BIOS-GPT. Así, Windows solo soporta arranque UEFI-GPT o BIOS-MBR.

Esta limitación no se aplica para el kernel de Linux, pero puede determinar qué gestor de arranque se utilice y/o cómo el gestor de arranque está configurado. La limitación de Windows se debe considerar si el usuario desea iniciar Windows y Linux desde el mismo disco, ya que el procedimiento de instalación del gestor de arranque depende de la configuración del tipo de firmware y la partición de disco. En caso de que Windows y Linux realizaran un arranque dual desde el mismo disco, es recomendable seguir el método utilizado por Windows, es decir configurar para arranque UEFI-GPT o BIOS-MBR. Ver [http://support.microsoft.com/kb/2581408](http://support.microsoft.com/kb/2581408) para obtener más información.

### Limitiaciones del medio de instalación

Las tabletas Intel Atom System-on-Chip (Clover Trail y Bay Trail) solo proveen soporte para el firmware UEFI IA32, y NO para soporte heredado de BIOS (a diferencia de la mayoría de los sistemas UEFI x86_64), debido a las guías Connected Standby Guidelines para OEMs de Microsoft. Debido a la falta de soporte heredado de BIOS en estos sistemas y la ausencia de arranque UEFI de 32 bits en la ISO oficial de Arch o la ISO Archboot (de abril de 2014), estos medios de instalación no pueden arrancar las tabletas ATOM Soc pre-instaladas con Windows 8/8.1 de 32 bits

### Limitaciones de los cargadores de arranque UEFI v/s BIOS

La mayoría de los gestores de arranque de linux que se instalan para una versión de firmware, no permiten el inicio de gestores de arranque de otra versión del firmware. Esto es, si Arch se instala en modo UEFI-GPT o UEFI-MBR en un disco, y Windows se instala en modo BIOS-MBR en otro disco, el gestor de arranque UEFI utilizado por Arch no puede cargar el arranque BIOS del disco con Windows. De manera similar, si se instala Arch en modo BIOS-MBR o BIOS-GPT en un disco y se instala Windows en modo UEFI-GPT, el gestor de arranque BIOS utilizado por Arch no puede cargar el gestor UEFI del disco con Windows. Las únicas excepciones a esto son utilizando grub(2) en Apple Macs, en los que grub(2) instalado con EFI permite cargar el SO installado con BIOS utilizando el commando **appleloader** (No funciona en sistemas que no sean Apple) y con rEFInd que técnicamente soporta el arranque de SO BIOS desde sistemas con arranque UEFI, aunque el sistema de [BIOS no siempre funciona en sistemas UEFI que no sean Apple](http://rodsbooks.com/refind/using.html#legado) según explica el autor Rod Smith.

De todas maneras, si se instala Arch en modo BIOS-GPT en un disco y se instala Windows en modo BIOS-MBR en otro disco, el gesto de arranque utilizado por Arch SÍ PUEDE cargar Windows desde el otro disco, siempre y cuando el gestor de arranque soporte el cargar en cadena desde otro disco.

**Note:** Si Arch y Windows cargan de manera dual desde el mismo disco, ARCH DEBE utilizar el mismo modo de firmware y formato de partición utilizada por el sistema Windows ya instalado en el disco.

### Arranque seguro UEFI

Todos los sistemas preinstalados de Windows 8/8.1 arrancan de forma predeterminada en el modo UEFI/GPT y tienen activado por defecto el arranque en modo seguro UEFI *(UEFI Secure Boot)*. Esto es obligatorio por Microsoft para todos los sistemas preinstalados OEM.

Actualmente los medios de instalación de Arch Linux soportan este modo seguro. Consulte [iniciando archiso](/index.php/Secure_Boot#Booting_archiso "Secure Boot").

Se recomienda desactivar el arranque seguro UEFI manualmente en la configuración del firmware antes de intentar iniciar Arch Linux. Windows 8/8.1 DEBERÍA continuar arrancando correctamente incluso si el modo seguro está deshabilitado. El único problema para deshabilitar la compatibilidad con el arranque seguro UEFI es que requiere acceso físico al sistema para deshabilitar la opción de arranque seguro en la configuración del firmware, ya que Microsoft ha prohibido explícitamente la presencia de cualquier método de forma remota o programática (desde el SO). arranque en todos los sistemas preinstalados de Windows 8/8.1.

### Arranque rápido

El arranque rápido es una caracterítica de Windows 8, que hiberna al sistema en vez de apagarlo para acelerar el tiempo de arranque. El sistema puede llegar a perder datos is es que Windows hiberna, se arranca un segundo SO y se realizan cambios a archivos. Aun cuando no planee compartir sistemas de archvo, el particionado EFI puede dañarse (en un sistema EFI). De esta forma se recomienda la desahabilitación del arranque rápido, como se describe [here](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html), antes de la instalación de Arch en un ordenador que utilice Windows 8\.

[ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) agregó una [salva guarda](http://sourceforge.net/p/ntfs-3g/ntfs-3g/ci/559270a8f67c77a7ce51246c23d2b2837bcff0c9/) para prevenir el montaje en modo lectura/escritura de discos hibernados, pero el controlador NTFS utilizado por el kernel de Linux no posee este tipo de salvaguardia.

### Limitaciones de nombres de archivos en Windows

Windows está limitado a rutas de archivos más cortas que[260 caractéres](http://blogs.msdn.com/b/bclteam/archive/2007/02/13/long-paths-in-net-part-1-of-3-kim-hamilton.aspx).

Windows también pone a [algunos carcacteres fuera de límites](http://msdn.microsoft.com/en-us/library/aa365247(VS.85).aspx#naming_conventions) en los nombres de archivo por razones que se pueden trazar hasta el DOS:

*   < (menor que)
*   > (mayor que)
*   : (dos puntos)
*   " (cremillas)
*   / (slash)
*   \ (backslash)
*   | (barra)
*   ? (interrogación)
*   * (asterisco)

Estas son limitaciones del Sistema Windows, y no de la partición NTFS; otro SO que utilice la partición no tendrá estas limitaciones. Windows no podría detectar estos archivos y correr `chkdsk` probablemente cause su borrado, lo que puede provocar pérdida de datos. **NTFS-3G** aplica las restricciones de Windows para nombrar nuevos archivos a través de la opción [windows_filenames](http://www.tuxera.com/community/ntfs-3g-manual/#4) (vea [fstab](/index.php/Fstab "Fstab")).

## Instalación

La manera recomendada de configurar un sistema con arranque dual Linux/Windows es instalando primero Windows, utilizando solo parte del disco para sus particiones. Al finalizar la instalación de Windows, arranque el instalador de Linux, que le permita crear particiones adicionales para Linux, manteniendo la integridad de las particiones creadas por Windows.La instalación de Windows creará la partición de sistema EFI que puede ser utilizada por el cargador de arranque del sistema Linux

### Sistemas BIOS

#### Utilizando un cargador de arranque Linux

Puede utilizar [GRUB](/index.php/GRUB#Dual-booting "GRUB") o [Syslinux](/index.php/Syslinux#Chainloading "Syslinux").

#### Utilizando un cargador de aranque Windows

Con esta configuración el cargador de arranque de Windows carga GRUB que luego arranca Arch.

##### Cargador de arranque de Windows Vista/7/8/8.1

La siguiente sección contiene extractos de [http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/](http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/).

Para posibilitar que el cargador de arranque de Windows pueda detectar las particiones de Linux, al menos una de las particiones debe tener el formato FAT32 (en el caso del artículo, `/dev/sda3`). l resto de la configuración es similar a una instalación típica. Algunos documentos refieren que la partición que es cargada por el cargador de arranque de Windows debe ser primaria, pero se ha reportado que se puede utilizar una partición extendida sin mayor problema.

*   Al instalar el cargador de arranque GRUB, debe instalarlo en la partición `/boot` en vez de en el MBR.
    **Nota:** por ejemplo, la partición `/boot` es `/dev/sda5`. Por lo que se instalo GRUB en `/dev/sda5` y no en `/dev/sda`. Para obtener ayuda, consulte [Instalar en un disco con o sin particiones](/index.php/GRUB/Tips_and_tricks_(Espa%C3%B1ol)#Instalar_en_un_disco_con_o_sin_particiones "GRUB/Tips and tricks (Español)")

*   Bajo Linux, realice una copia de la información de arranque tecleando lo siguiente en la línea de órdenes:

```
my_windows_part=/dev/sda3
my_boot_part=/dev/sda5
mkdir /media/win
mount $my_windows_part /media/win
dd if=$my_boot_part of=/media/win/linux.bin bs=512 count=1

```

*   Arranque en Windows y debiera poder ver la partición FAT32\. Copie el archivo linux.bin a `C:\`. Ejecute **cmd** con privilegios de administrador (navegue a *Inicio > Todos los Programas > Accesorios*, click derecho en *Terminal de Comando* y seleccione *Ejecutar como administrador*):

```
bcdedit /create /d “Linux” /application BOOTSECTOR

```

*   BCDEdit retorna un identificador alfanumérico para esta entrada a la cual se referirá como {ID} en los siguientes pasos. Deberá reemplazar {ID} por el identificador alfanumérico obtenido. Un ejemplo de {ID} es {d7294d4e-9837-11de-99ac-f3f3a79e3e93}.

```
bcdedit /set {ID} device partition=c:
bcdedit /set {ID}  path \linux.bin
bcdedit /displayorder {ID} /addlast
bcdedit /timeout 30

```

*   Reinicie el sistema y disfrute. En el caso del ejemplo se utiliza el cargador de arranque de Windows por lo que es posible mapear el segundo botón de arranque del Dell Precision M4500 para arrancar Linux en lugar de Windows

##### Cargador de arranque de Windows 2000/XP

Para más información de este método vea [http://www.geocities.com/epark/linux/grub-w2k-HOWTO.html](http://www.geocities.com/epark/linux/grub-w2k-HOWTO.html). No parecen haber muchas ventajas de utilizar este método por sobre el de utilizar un cargador de arranque de Linux; De todas formas necesitará crear una partición `/boot`, y este método es definitivamente más difícil de configurar.

### Sistema UEFI

Tanto [systemd-boot](/index.php/Systemd-boot "Systemd-boot") (anteriormente llamado **gummiboot**) como [rEFInd](/index.php/REFInd "REFInd") detectan automáticamente el **cargador de arranque Windows** `\EFI\Microsoft\Boot\bootmgfw.efi` y lo muestran en su menu de inicio, por lo que no es necesario realizar ninguna configuración manual.

Para utilizar [GRUB](/index.php/GRUB "GRUB") siga la guía en [GRUB#Windows installed in UEFI/GPT mode](/index.php/GRUB#Windows_installed_in_UEFI/GPT_mode "GRUB").

Tanto Syslinux (version 6.02 y 6.03-pre9) como ELILO no soportan el arranque en cadena de otras aplicaciones EFI, por lo que no pueden ser utilizadas para el arranque en cadena de `\EFI\Microsoft\Boot\bootmgfw.efi`.

Algunos ordenadores con versiones mas nuevas de Windows, usualmente traen la opción de [arranque seguro](/index.php/Secure_Boot "Secure Boot") habilitada. Deberá realizar algunos pasos extra para deshabilitar el arranque seguro o hacer que su medio de instalación sea compatible con el arranque seguro.

### Solución de Problemas

#### No es posible crear una nueva partición ni localizar la existente

La llave USB utilizada para instalar Windows 8.1 necesita una tabla de partición MBR (no GPT), de otra forma la instalación no funciona y devuelve algo como "No es posible crear una nueva partición ni localizar la existente", a pesar de que las particiones fueron creadas.

## Estandares de Tiempo

*   Recomendado: Configurar tanto Arch como Windows para utilizar UTC, siguiendo [System time#UTC in Windows](/index.php/System_time#UTC_in_Windows "System time"). Además, prevenir que Windows sincronice la fecha y hora online, ya que de otra forma el reloj de hardware se configurará con *localtime*.

*   No recomendado: Configurar Arch para utilizar *localtime* y deshabilitar cualquier servicio relacionado con la hora, como [NTPd](/index.php/NTPd "NTPd"). Esto hará que solo Windows pueda configurar la hora, por lo que deberá recordar arrancar Windows al menos dos veces por año (Primavera y Otoño) en caso de que se utilice [horario de verano](https://en.wikipedia.org/wiki/Daylight_saving_time_(Espa%C3%B1ol) "wikipedia:Daylight saving time (Español)"). POr favor no utilice los foros para preguntar porque su reloj esta adelantado o atrasado en 1 hora si es que pasa dias o semanas sin arrancar Windows.

## Ver también

*   [Booting Windows from a desktop shortcut](https://bbs.archlinux.org/viewtopic.php?id=140049)