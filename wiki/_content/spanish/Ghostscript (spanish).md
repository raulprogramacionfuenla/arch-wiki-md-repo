**Estado de la traducción**
Este artículo es una traducción de [Ghostscript](/index.php/Ghostscript "Ghostscript"), revisada por última vez el **2018-10-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Ghostscript&diff=0&oldid=547274) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Ghostscript](https://en.wikipedia.org/wiki/es:Ghostscript "wikipedia:es:Ghostscript") es un intérprete para PostScript y PDF.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Utilización](#Utilizaci.C3.B3n)
    *   [2.1 ps2pdf](#ps2pdf)
*   [3 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [ghostscript](https://www.archlinux.org/packages/?name=ghostscript).

## Utilización

Véase [gs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gs.1).

### ps2pdf

*ps2pdf* es un wrapper alrededor de ghostscript para convertir PostScript a PDF:

```
$ ps2pdf -sPAPERSIZE=a4 -dOptimize=true -dEmbedAllFonts=true SuArchivoPS.ps

```

Explicación:

*   con `-sPAPERSIZE=something` define el tamaño del papel. Para valores válidos de PAPERSIZE, véase [[1]](http://ghostscript.com/doc/current/Use.htm#Known_paper_sizes).
*   `-dOptimize=true` optimiza el PDF creado para la carga.
*   `-dEmbedAllFonts=true` hace que las fuentes se vean bien siempre.

**Nota:** No puede elegir la orientación del papel en ps2pdf. Si su archivo PS de entrada está en buen estado, este ya contiene la información de orientación. Si está intentando utilizar un archivo PS encapsulado, tendrá problemas si no se ajusta a la `-sPAPERSIZE` que especificó, ya que los archivos EPS generalmente no contienen información sobre la orientación del papel. una solución es crear un nuevo documento en la configuración de ghostscript (llámelo, por ejemplo, "slide") y utilícelo como `-sPAPERSIZE=slide`.

## Véase también

*   [Sitio Web Oficial](https://www.ghostscript.com/)