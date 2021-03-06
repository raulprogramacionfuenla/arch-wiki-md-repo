**Estado de la traducción**
Este artículo es una traducción de [RetroArch](/index.php/RetroArch "RetroArch"), revisada por última vez el **2017-09-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=RetroArch&diff=0&oldid=542813) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Nota:** RetroArch no está afiliado con [Arch Linux](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)").

[RetroArch](http://www.retroarch.com/) es un emulador multisistema, modular, impulsado por línea de comandos, diseñado para ser rápido, ligero y portátil. Algunas de sus características se pueden encontrar en algunos otros emuladores, como el rebobinado en tiempo real y el ocultamiento de juego basado en la API libretro.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Uso](#Uso)
*   [3 Configuración](#Configuración)
*   [4 Actualizador en línea](#Actualizador_en_línea)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 No se encontraron núcleos](#No_se_encontraron_núcleos)
    *   [5.2 Los dispositivos de entrada no funcionan](#Los_dispositivos_de_entrada_no_funcionan)
    *   [5.3 Rendimiento de vídeo deficiente](#Rendimiento_de_vídeo_deficiente)
*   [6 Véase también](#Véase_también)

## Instalación

1\. Instale el paquete [retroarch](https://www.archlinux.org/packages/?name=retroarch) o, alternativamente , [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) para la versión de desarrollo. 2\. Instale el paquete [retroarch-assets-xmb](https://www.archlinux.org/packages/?name=retroarch-assets-xmb) para mostrar correctamente los elementos del **menú XMB**.

## Uso

RetroArch utiliza bibliotecas separadas, llamadas "emulator cores" o "emulator implementations", disponibles tanto en la [Community](https://www.archlinux.org/packages/?q=libretro) como en el [libretro GitHub repository](https://github.com/libretro). Cada paquete básico de libretro instalará una biblioteca en `/usr/lib/libretro`. La sintaxis para elegir uno al ejecutar “retroarch” es:

```
 $ retroarch --libretro /usr/lib/libretro/libretro-*core*.so *path/to/rom*

```

Se puede definir un núcleo de emulación predeterminado en la configuración, evitando la necesidad de especificarlo en cada ejecución.

 `/etc/retroarch.cfg or ~/.config/retroarch/retroarch.cfg`  `libretro_path = "/usr/lib/libretro/libretro-*core*.so"` 

## Configuración

RetroArch proporciona un archivo de configuración guía muy bien comentado ubicado en `/etc/retroarch.cfg`. Copie el archivo de configuración guía en su directorio personal

```
 $ cp /etc/retroarch.cfg ~ / .config / retroarch / retroarch.cfg

```

También soporta archivos de configuración divididos usando la directiva `#include "foo.cfg"` dentro del archivo de configuración principal, `retroarch.cfg`. Esto puede anularse utilizando el parámetro `--appendconfig /path/to/config` y es beneficioso si se requieren diferentes combinaciones de claves, configuraciones de vídeo o ajustes de audio para las diversas implementaciones.

**Sugerencia:** RetroArch es capaz de cargar '[bsnes xml filters](https://gitorious.org/bsnes/xml-shaders) *y* [cg shaders](https://github.com/libretro/common-shaders) *que se pueden definir en `retroarch.cfg` como `video_bsnes_shader` y `video_cg_shader` respectivamente.*

**Nota:** [retroarch-git](https://aur.archlinux.org/packages/retroarch-git/) requiere [nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=nvidia-cg-toolkit) para poder usar los *cg shaders*.

**Advertencia:** Al utilizar '[ALSA](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)") *es necesario que el `audio_out_rate` sea ​​igual a la velocidad de salida predeterminada del sistema, normalmente 48000.*

## Actualizador en línea

Las versiones recientes de RetroArch han introducido un menú incorporado para actualizar los archivos de núcleo y varios activos de [RetroArch Buildbot](https://buildbot.libretro.com/) . Se puede acceder desde el menú principal en "Online Updater".

 `Actualizador en línea` 
```
Actualizar núcleo 
Actualizar archivos de información principal
Actualizar activos
Actualizar perfiles de Autoconfig
Actualizar trucos
Actualizar bases de datos
Actualizar superposiciones
Actualizar GLSL Shaders
```

Estos núcleos y activos se mantienen actualizados y se pueden extraer del actualizador en cualquier momento.

## Solución de problemas

### No se encontraron núcleos

Por defecto, RetroArch intentará encontrar núcleos en `/usr/lib/libretro`. Los núcleos descargados con el actualizador en línea incorporado fallarán al guardar a menos que retroarch se ejecute como root (no recomendado, ya que puede sobrescribir los núcleos instalados por pacman), ya que el usuario estándar no tiene permiso para modificar este directorio. Para usar núcleos desde el Online Updater, edite estas líneas:

 `~/.config/retroarch/retroarch.cfg` 
```
libretro_directory = "~/.config/retroarch/cores"
libretro_info_path = "~/.config/retroarch/cores/info"
```

### Los dispositivos de entrada no funcionan

Puede encontrar problemas si se ejecuta en una CLI o en un servidor de presentación que no sea [Xorg](/index.php/Xorg "Xorg") o si utiliza el controlador de entrada [udev](/index.php/Udev "Udev"), ya que los nodos / dev / input están limitados sólo al acceso de root. Intente agregar su usuario al grupo "input" y luego volver a iniciar sesión, por ejemplo

```
 # usermod -a -G nombre de usuario de entrada

```

Alternativamente, agregue manualmente una regla en `/etc/udev/rules.d/99-evdev.rules`, con `KERNEL=="event*", NAME="input/%k", MODE="666"` como su contenido. Vuelva a cargar las reglas de udev ejecutando:

```
 # udevadm control --reload-rules

```

Si el reinicio del sistema o la sustitución de los dispositivos no son opciones, los permisos pueden forzarse mediante:

```
 # chmod 666 / dev / input / event *

```

### Rendimiento de vídeo deficiente

Si se presenta un rendimiento de vídeo deficiente, RetroArch se puede ejecutar en un subproceso independiente estableciendo `video_threaded = true` en `~/.config/retroarch/retroarch.cfg` . Sin embargo, esta solución no debe utilizarse si ajustando la resolución de vídeo o tasa de actualización de RetroArch corrige el problema, ya que hace el perfecionamiento de V-Sync imposible, y aumenta ligeramente la latencia.

## Véase también

*   [Official Website](http://www.retroarch.com/)
*   [RetroArch wiki on GitHub](https://github.com/libretro/RetroArch/wiki)
*   [Documentation for developers](https://github.com/libretro/libretro.github.com/wiki/Documentation-devs)