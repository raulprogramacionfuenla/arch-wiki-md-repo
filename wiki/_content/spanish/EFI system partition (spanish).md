**Estado de la traducción**
Este artículo es una traducción de [EFI system partition](/index.php/EFI_system_partition "EFI system partition"), revisada por última vez el **2018-12-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=EFI_system_partition&diff=0&oldid=556360) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")
*   [Boot loaders (Español)](/index.php/Boot_loaders_(Espa%C3%B1ol) "Boot loaders (Español)")

La [partición del sistema EFI](https://en.wikipedia.org/wiki/EFI_system_partition "wikipedia:EFI system partition") (también llamada, por sus siglas en inglés, ESP) es una partición independiente del sistema operativo, que actúa como el lugar de almacenamiento para los cargadores de arranque EFI, las aplicaciones y los controladores que serán lanzados por el firmware UEFI. Es obligatoria para el arranque UEFI.

La especificación UEFI exige soporte para los sistemas de archivos FAT12, FAT16 y FAT32 (vea [UEFI specification version 2.7, section 13.3.1.1](https://www.uefi.org/sites/default/files/resources/UEFI%20Spec%202_7_A%20Sept%206.pdf#G17.1019485)), pero cualquier proveedor puede opcionalmente agregar soporte para otros sistemas de archivos adicionales; por ejemplo, algunos proveedores añaden soporte de Apple [Macs](/index.php/Mac "Mac") (y de forma predeterminada) para sus propios controladores del sistema de archivos HFS +.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Comprobar la existencia de una partición](#Comprobar_la_existencia_de_una_partición)
*   [2 Crear la partición](#Crear_la_partición)
    *   [2.1 Discos particionados con GPT](#Discos_particionados_con_GPT)
    *   [2.2 Discos particionados con MBR](#Discos_particionados_con_MBR)
*   [3 Formatear la partición](#Formatear_la_partición)
*   [4 Montar la partición](#Montar_la_partición)
    *   [4.1 Puntos de montaje alternativos](#Puntos_de_montaje_alternativos)
        *   [4.1.1 Utilizar el montaje con bind](#Utilizar_el_montaje_con_bind)
        *   [4.1.2 Utilizar systemd](#Utilizar_systemd)
        *   [4.1.3 Utilizar eventos del sistema de archivos](#Utilizar_eventos_del_sistema_de_archivos)
        *   [4.1.4 Utilizar un hook de mkinitcpio](#Utilizar_un_hook_de_mkinitcpio)
        *   [4.1.5 Utilizar un hook de mkinitcpio (2)](#Utilizar_un_hook_de_mkinitcpio_(2))
        *   [4.1.6 Utilizar un hook de pacman](#Utilizar_un_hook_de_pacman)
*   [5 Problemas conocidos](#Problemas_conocidos)
    *   [5.1 Partición ESP sobre RAID](#Partición_ESP_sobre_RAID)
*   [6 Véase también](#Véase_también)

## Comprobar la existencia de una partición

Si está instalando Arch Linux en un equipo compatible con UEFI que ya tiene un sistema operativo instalado, como [Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") 10, por ejemplo, es muy probable que ya tenga una partición del sistema EFI.

Para conocer el esquema de particionado del disco y la «*system partition*», utilice [fdisk](/index.php/Fdisk_(Espa%C3%B1ol) "Fdisk (Español)") como root sobre el disco desde el que desea iniciar:

```
# fdisk -l /dev/sd*x*

```

Esta orden devolverá:

*   La tabla de particionado del disco: si indica `Disklabel type: gpt` la tabla de particionado es [GPT](/index.php/GPT "GPT") o `Disklabel type: dos` si es [MBR](/index.php/MBR "MBR").
*   La lista de particiones en el disco: busque la partición del sistema EFI en la lista, es una partición pequeña (generalmente alrededor de 100–550 MiB) con un tipo `EFI System` o `EFI (FAT-12/16/32)`. Para confirmar que esta es la ESP, móntela y verifique si contiene un directorio llamado `EFI`, si es así, definitivamente es la ESP.

**Advertencia:** al realizar un arranque dual, evite volver a formatear la ESP, ya que puede contener los archivos necesarios para iniciar otros sistemas operativos.

Si encontró una partición del sistema EFI existente, solo tiene que [#Montar la partición](#Montar_la_partición). Si no encontró una, deberá crearla, proceda con [#Crear la partición](#Crear_la_partición).

## Crear la partición

Las siguientes dos secciones muestran cómo crear una partición del sistema EFI (ESP).

**Nota:** es recomendable utilizar [GPT](/index.php/GPT "GPT") para el arranque UEFI, porque algunos firmwares UEFI no permiten el arranque UEFI/MBR.

Para evitar posibles problemas con algunas implementaciones de UEFI, la ESP debería estar formateada con FAT32 y con un tamaño de, al menos, 512 MiB. Se recomienda 550 MiB para evitar la confusión entre MiB/MB y la creación accidental de FAT16 [[1]](https://www.rodsbooks.com/efi-bootloaders/principles.html), aunque tamaños más grandes también están de más.

De acuerdo con una nota de Microsoft [[2]](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions#diskpartitionrules), el tamaño mínimo para la partición del sistema EFI sería de 100 MiB, aunque esto no se recoge en las especificaciones UEFI. Téngase en cuenta que para [formatos avanzados](/index.php/Advanced_Format "Advanced Format") de unidades con 4K nativo (4-KiB-por-sector), el tamaño mínimo requerido será de, al menos, 256 MiB, porque es el tamaño mínimo de la partición de las unidades FAT32 (calculado del siguiente modo: tamaño de sector (4KiB) x 65527 = 256 MiB), y ello debido a una limitación presente en el formato del sistema de archivos FAT32.

### Discos particionados con GPT

La partición del sistema EFI en una tabla de particionado [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") está identificada por la [GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") `C12A7328-F81F-11D2-BA4B-00A0C93EC93B`.

**Elija uno** de los siguientes métodos para crear una ESP para un disco particionado con GPT:

*   [fdisk](/index.php/Fdisk_(Espa%C3%B1ol) "Fdisk (Español)"): cree una partición con el tipo de partición `EFI System`.
*   [gdisk](/index.php/Gdisk "Gdisk"): cree una partición con el tipo de partición `EF00`.
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): cree una partición con `fat32` como tipo de sistema de archivos y establezca/active el indicador `esp` en él.

Continúe en la sección [#Formatear la partición](#Formatear_la_partición) a continuación.

### Discos particionados con MBR

La partición del sistema EFI en una tabla de particionado [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") está identificada por el [ID](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") `EF`.

**Elija uno** de los siguientes métodos para crear un ESP para un disco particionado MBR:

*   [fdisk](/index.php/Fdisk_(Espa%C3%B1ol) "Fdisk (Español)"): crre una partición primaria con el tipo de partición `EFI (FAT-12/16/32)`.
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): cree una partición primaria con `fat32` como el tipo de sistema de archivos y establezca/active el indicador `esp` en ella.

Continúe en la sección [#Formatear la partición](#Formatear_la_partición) a continuación.

## Formatear la partición

Después de crear la ESP, debe [formatearla](/index.php/Format "Format") con el sistema de archivos [FAT32](/index.php/FAT32 "FAT32"):

```
# mkfs.fat -F32 /dev/sd*xY*

```

Si obtiene el mensaje `WARNING: Not enough clusters for a 32 bit FAT!`, reduzca el tamaño del clúster con `mkfs.fat -s2 -F32 ...` o `-s1`; de lo contrario, la partición puede no ser legible por UEFI. Consulte [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) para conocer los tamaños de clúster admitidos.

## Montar la partición

El kernel y los archivos initramfs deben ser accesibles por el [gestor de arranque](/index.php/Boot_loader "Boot loader") o el propio UEFI para poder arrancar correctamente el sistema. Por lo tanto, si desea mantener una configuración simple, la elección del cargador de arranque limitará los puntos de montaje disponibles para la partición del sistema EFI.

Los escenarios más simples para montar la partición del sistema EFI son:

*   [montar](/index.php/Mount "Mount") ESP en `/efi` y utilizar un [gestor de arranque](/index.php/Boot_loader "Boot loader") que sea capaz de dirigirle a su sistema de archivos raíz (por ejemplo, [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), [rEFInd](/index.php/REFInd "REFInd")).
*   [montar](/index.php/Mount "Mount") ESP en `/boot`. Este es el método preferido cuando se arranca directamente un kernel [EFISTUB](/index.php/EFISTUB "EFISTUB") desde UEFI.

**Nota:** la ESP generalmente contendrá un directorio llamado `EFI` en su raíz, por lo tanto, al montar ESP en `/boot` puede encontrar una ruta de directorio como `/boot/EFI`. No confunda esta ruta con el punto de montaje ESP `/boot/efi` popularmente usado (y posiblemente aún utilizado por otras distribuciones de Linux).

### Puntos de montaje alternativos

Si no utiliza uno de los métodos simples para [#Montar la partición](#Montar_la_partición), tendrá que copiar los archivos de arranque a la ESP (en adelante `*esp* `).

```
# mkdir -p *esp*/EFI/arch
# cp -a /boot/vmlinuz-linux *esp*/EFI/arch/
# cp -a /boot/initramfs-linux.img *esp*/EFI/arch/
# cp -a /boot/initramfs-linux-fallback.img *esp*/EFI/arch/

```

**Nota:** es posible que deba copiar el [Microcódigo](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") en la línea de la entrada de arranque.

Además, deberá mantener actualizados los archivos en el ESP con las últimas actualizaciones del kernel. De lo contrario, podría producirse un sistema no arrancable. Las siguientes secciones muestran varios mecanismos para automatizarlo.

**Nota:** si la ESP no está montada en `/boot`, no se fie del [mecanismo de automontaje de systemd](/index.php/Fstab#Automount_with_systemd "Fstab") (que se incluye en [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8)). Monte siempre manualmente la partición de arranque antes de cualquier actualización del sistema o del kernel, de lo contrario puede que no pueda montarla después de la actualización, ya que el nuevo kernel en ejecución, bloqueará la partición de arranque, imposibilitando la actualización de la copia del kernel presente en la ESP.

También es posible [precargar los módulos requeridos por el kernel en el arranque](/index.php/Kernel_module#Automatic_module_loading_with_systemd "Kernel module"), por ejemplo:

 `/etc/modules-load.d/vfat.conf` 
```
vfat
nls_cp437
nls_iso8859-1

```

#### Utilizar el montaje con bind

En lugar de montar la ESP en el mismo punto de montaje que `/boot`, puede montar un directorio de la ESP en `/boot`, [montándola](/index.php/Mount "Mount") con bind (vea [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8)). Esto permite a [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") actualizar el kernel directamente, mientras mantiene organizada a su gusto la ESP.

**Nota:**

*   Este método requiere un [kernel](/index.php/FAT#Kernel_configuration "FAT") y un [gestor de arranque](/index.php/Bootloader "Bootloader") compatible con FAT32\. Esto no es un problema para una instalación normal de Arch, pero podría ser problemático para otras distribuciones (esto es, aquellas que requieren enlaces simbólicos en `/boot/`). Consulte la publicación del foro [aquí](https://bbs.archlinux.org/viewtopic.php?pid=1331867#p1331867).
*   *Debe* utilizar el [parámetro del kernel](/index.php/Kernel_parameters#Parameter_list "Kernel parameters") `root=` para poder arrancar con este método.

Al igual que se hizo en [#Puntos de montaje alternativos](#Puntos_de_montaje_alternativos), debemos copiar todos los archivos de arranque en un directorio de su ESP, pero monte la ESP **fuera** de `/boot`. A continuación, monte el directorio con la opción bind:

```
# mount --bind *esp*/EFI/arch /boot

```

Después de verificar el éxito de la operación, edite [Fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") para hacer estos cambios persistentes:

 `/etc/fstab` 
```
*esp*/EFI/arch /boot none defaults,bind 0 0

```

#### Utilizar systemd

[Systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") tiene la capacidad de programar tareas que se desencadenarán cuando se produzca un evento. En este caso particular, la capacidad de detectar un cambio en una ruta determinada es usada para sincronizar los archivos del kernel de EFISTUB e initramfs cuando se actualizan en `/boot/`. El archivo observado en busca de cambios es `initramfs-linux-fallback.img`, ya que este es el último archivo creado por mkinitcpio, para asegurarse de que todos los archivos han sido correctamente compilados antes de iniciar la copia. Los archivos de ruta y servicio de *system* que se crearán son:

 `/etc/systemd/system/efistub-update.path` 
```
[Unit]
Description=Copiar el kernel EFISTUB en la partición del sistema EFI

[Path]
PathChanged=/boot/initramfs-linux-fallback.img

[Install]
WantedBy=multi-user.target
WantedBy=system-update.target
```
 `/etc/systemd/system/efistub-update.service` 
```
[Unit]
Description=Copiar el kernel EFISTUB en la partición del sistema EFI

[Service]
Type=oneshot
ExecStart=/usr/bin/cp -af /boot/vmlinuz-linux *esp*/EFI/arch/
ExecStart=/usr/bin/cp -af /boot/initramfs-linux.img *esp*/EFI/arch/
ExecStart=/usr/bin/cp -af /boot/initramfs-linux-fallback.img *esp*/EFI/arch/
```

Después, [active](/index.php/Enable "Enable") e [inicie](/index.php/Start "Start") `efistub-update.path`.

**Sugerencia:** para permitir [Secure Boot](/index.php/Secure_Boot "Secure Boot") con sus propias claves, puede configurar el servicio para que también firme la imagen utilizando [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools): `ExecStart=/usr/bin/sbsign --key */path/to/db.key* --cert */path/to/db.crt* --output *esp*/EFI/arch/vmlinuz-linux /boot/vmlinuz-linux` 

#### Utilizar eventos del sistema de archivos

Los [eventos del sistema de archivos](/index.php/Autostarting#On_filesystem_events "Autostarting") se pueden usar para ejecutar un script que sincronice el kernel EFISTUB después actualizar el kernel. He aquí un ejemplo con [incron](/index.php/Incron "Incron") a continuación.

 `/usr/local/bin/efistub-update` 
```
#!/bin/sh
cp -af /boot/vmlinuz-linux *esp*/EFI/arch/
cp -af /boot/initramfs-linux.img *esp*/EFI/arch/
cp -af /boot/initramfs-linux-fallback.img *esp*/EFI/arch/

```

**Nota:** el primer parámetro `/boot/initramfs-linux-fallback.img` es el archivo objeto de seguimiento. El segundo parámetro `IN_CLOSE_WRITE` es la acción a tener en cuenta. El tercer parámetro `/usr/local/bin/efistub-update` es el script que se ejecutará.
 `/etc/incron.d/efistub-update.conf` 
```
/boot/initramfs-linux-fallback.img IN_CLOSE_WRITE /usr/local/bin/efistub-update

```

Con el fin de utilizar este método, [active](/index.php/Enable "Enable") el servicio `incrond.service`.

#### Utilizar un hook de mkinitcpio

Mkinitcpio puede generar un hook que no necesita un demonio de nivel de sistema para funcionar. Mantiene un proceso en segundo plano a la espera de que se genere `vmlinuz`, `initramfs-linux.img` y `initramfs-linux-fallback.img` antes de copiar los archivos.

Añada `efistub-update` a la lista de hooks en `/etc/mkinitcpio.conf`.

 `/etc/initcpio/install/efistub-update` 
```
#!/usr/bin/env bash
build() {
	/usr/local/bin/efistub-copy $$ &
}

help() {
	cat <<HELPEOF
Este hook espera a que mkinitcpio termine y luego copia el ramdisk y el kernel terminados a la ESP
HELPEOF
}

```
 `/usr/local/bin/efistub-copy` 
```
#!/usr/bin/env bash

if [[ $1 -gt 0 ]]
then
	while [ -e /proc/$1 ]
	do
		sleep .5
	done
fi

rsync -a /boot/ *esp*/

echo "Sincronizado /boot con ESP"

```

#### Utilizar un hook de mkinitcpio (2)

Esta es otra **alternativa** a las soluciones anteriores, que es potencialmente más limpia porque hay menos copias y no necesita tampoco un demonio de nivel de sistema para funcionar. La lógica se invierte en este caso, initramfs se almacena directamente en la partición EFI, no se copia en `/boot/`. Luego, el kernel y cualquier otro archivo adicional se copian en la partición ESP, gracias a un hook mkinitcpio.

Edite el archivo `/etc/mkinitcpio.d/linux.preset` :

 `/etc/mkinitcpio.d/linux.preset` 
```
# archivo predeterminado de mkinitcpio para el paquete 'linux'

# Directorio donde copiar el kernel, initramfs...
ESP_DIR="*esp*/EFI/arch"

ALL_config="/etc/mkinitcpio.conf"
ALL_kver="/boot/vmlinuz-linux"

PRESETS=('default' 'fallback')

#default_config="/etc/mkinitcpio.conf"
default_image="${ESP_DIR}/initramfs-linux.img"
default_options="-A esp-update-linux"

#fallback_config="/etc/mkinitcpio.conf"
fallback_image="${ESP_DIR}/initramfs-linux-fallback.img"
fallback_options="-S autodetect"
```

A continuación, cree el archivo `/etc/initcpio/install/esp-update-linux` y hágalo ejecutable:

 `/etc/initcpio/install/esp-update-linux` 
```
# Directorio donde copiar el kernel, initramfs...

build() {
	cp -af /boot/vmlinuz-linux "${ESP_DIR}/"
	[[ -e /boot/intel-ucode.img ]] && cp -af /boot/intel-ucode.img "${ESP_DIR}/"
	[[ -e /boot/amd-ucode.img ]] && cp -af /boot/amd-ucode.img "${ESP_DIR}/"
}

help() {
	cat <<HELPEOF
Este hook copia el kernel a la partición ESP
HELPEOF
}

```

Para probarlo, basta ejecutar:

```
# rm /boot/initramfs-linux-fallback.img
# rm /boot/initramfs-linux.img
# mkinitcpio -p linux

```

#### Utilizar un hook de pacman

Una última opción depende de los [hooks de pacman](/index.php/Pacman_hooks "Pacman hooks") que se ejecutan al final de la instalación.

El primer archivo es un hook que supervisa los archivos relevantes, y se ejecuta si los mismos se modifican en la preinstalación.

 `/etc/pacman.d/hooks/999-kernel-efi-copy.hook` 
```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Target = boot/vmlinuz*
Target = usr/lib/initcpio/*
Target = boot/*-ucode.img

[Action]
Description = Copiando linux y initramfs al directorio EFI...
When = PostTransaction
Exec = /usr/local/bin/kernel-efi-copy.sh

```

El segundo archivo es el script en sí. Cree el archivo y hágalo [ejecutable](/index.php/Help:Reading_(Espa%C3%B1ol)#Hacer_ejecutable "Help:Reading (Español)"):

 `/usr/local/bin/kernel-efi-copy.sh` 
```
#!/usr/bin/env bash
#
# Copiar las imágenes kernel e initramfs al directorio EFI
#

ESP_DIR="*esp*/EFI/arch"

for file in /boot/vmlinuz*
do
        cp -af "$file" "$ESP_DIR/$(basename "$file").efi"
        [[ $? -ne 0 ]] && exit 1
done

for file in /boot/initramfs*
do
        cp -af "$file" "$ESP_DIR/"
        [[ $? -ne 0 ]] && exit 1
done

[[ -e /boot/intel-ucode.img ]] && cp -af /boot/intel-ucode.img "$ESP_DIR/"
[[ -e /boot/amd-ucode.img ]] && cp -af /boot/amd-ucode.img "$ESP_DIR/"

exit 0

```

## Problemas conocidos

### Partición ESP sobre RAID

Es posible hacer que la partición ESP sea parte de una matriz RAID1, pero al hacerlo se corre el riesgo de dañar los datos, y se deben tomar más consideraciones al crear la ESP. Consulte [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) y [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741) para conocer más detalles.

## Véase también

*   [La partición del sistema EFI y el comportamiento de arranque predeterminado](https://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)