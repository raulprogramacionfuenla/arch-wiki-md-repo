Related articles

*   [GIMP/CMYK support](/index.php/GIMP/CMYK_support "GIMP/CMYK support")
*   [List of applications/Multimedia#Raster graphics editors](/index.php/List_of_applications/Multimedia#Raster_graphics_editors "List of applications/Multimedia")

[GIMP](https://en.wikipedia.org/wiki/GIMP "wikipedia:GIMP") is a powerful raster image editing program, and commonly used for photo retouching, image composition, and general graphic design work. It can be used as a simple paint program, an expert quality photo retouching program, an online batch processing system, a mass production image renderer, an image format converter, etc.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Captions](#Captions)
    *   [2.2 Create a circle](#Create_a_circle)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Green text](#Green_text)
    *   [3.2 Hide Noto](#Hide_Noto)
    *   [3.3 PDF files](#PDF_files)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gimp](https://www.archlinux.org/packages/?name=gimp) package.

**Tip:** The GIMP implements a plug-in system and the repositories ([official](https://www.archlinux.org/packages/?sort=&q=gimp&maintainer=&flagged=), [AUR](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=gimp&outdated=off&SB=n&SO=a&PP=50&do_Search=Go)) contain more plug-ins than listed in the package's optional depends.

## Tips and tricks

### Captions

To caption an image follow these steps after inputting the desired text:

1.  Click *Layer* and *Text to Path*
2.  Click *Select* and *From Path*
3.  Click *Select* and *Invert*
4.  Click *Edit* and *Stroke Path*

### Create a circle

To draw a circle in GIMP follow these steps:

1.  Select the *Ellipse tool* and hold `Shift`
2.  Click *Edit* and *Fill with Color*
3.  Click *Select* and *Shrink*
4.  Press `Delete`

**Tip:** *Grow* and *Border* give the same result.

## Troubleshooting

### Green text

Add the following to `~/.config/GIMP/2.10/fonts.conf` if you see a green tint around letters with antialiasing enabled:

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>none</const>
    </edit>
  </match>
</fontconfig>

```

### Hide Noto

Add the following to `~/.config/GIMP/2.10/fonts.conf` if you have [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts) installed and would like to remove them from GIMP's fonts list:

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
  <rejectfont>
    <glob>/usr/share/fonts/noto</glob>
  </rejectfont>
</fontconfig>

```

See [fonts-conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fonts-conf.5) and [Font configuration#Whitelisting and blacklisting fonts](/index.php/Font_configuration#Whitelisting_and_blacklisting_fonts "Font configuration") for more information.

### PDF files

GIMP requires the [poppler-glib](https://www.archlinux.org/packages/?name=poppler-glib) library to open PDF files or it will report that they are unrecognised.

Since GIMP rasterizes PDF files right from the start, it will not exploit intrinsic PDF capabilities while editing them. Other programs (like [LibreOffice Draw](/index.php/LibreOffice "LibreOffice")) can be used to better edit PDF files.

## See also

*   [Official website](https://www.gimp.org/)
*   [debian:GIMP](https://wiki.debian.org/GIMP "debian:GIMP")
*   [GIMP Magazine](https://gimpmagazine.org/resources/) - Index of GIMP resources, tutorials, communities
*   [GIMP Forum](http://gimp-forum.net/)