**Metric-compatible fonts** are fonts that match the metrics of another font (often generics such as Helvetica, Times or Courier). Due to their matching metrics, replacing a font with a [metric-compatible](https://en.wikipedia.org/wiki/metric-compatible "wikipedia:metric-compatible") alternative does not change the formatting of the document or a web page. Such fonts are often developed for FOSS systems to display pages correctly.

## Contents

*   [1 List of metric-compatible fonts](#List_of_metric-compatible_fonts)
*   [2 Generic Families](#Generic_Families)
    *   [2.1 PostScript](#PostScript)
    *   [2.2 Microsoft](#Microsoft)
*   [3 Metric-compatible font projects](#Metric-compatible_font_projects)
    *   [3.1 TeX Gyre](#TeX_Gyre)
    *   [3.2 GNU FreeFont](#GNU_FreeFont)
    *   [3.3 Liberation](#Liberation)
    *   [3.4 Google](#Google)
        *   [3.4.1 Chrome OS](#Chrome_OS)
        *   [3.4.2 Noto](#Noto)
*   [4 Example configuration](#Example_configuration)
    *   [4.1 Example for binding method](#Example_for_binding_method)
    *   [4.2 Example for prefer method](#Example_for_prefer_method)
*   [5 See also](#See_also)

## List of metric-compatible fonts

In the following table, commonly-specified families are shown in **bold**. This table is mainly based on [<tt>30-metric-aliases.conf</tt>](https://cgit.freedesktop.org/fontconfig/tree/conf.d/30-metric-aliases.conf) from [fontconfig](/index.php/Fontconfig "Fontconfig").

<caption>"Core fonts for the web" compatibilities</caption>
| [PostScript](#PostScript) | [URW](#PostScript) | [GUST](#TeX_Gyre) | [GNU](#GNU_FreeFont) | [Windows](#Microsoft) | [Microsoft](#Microsoft) | [Liberation](#Liberation) | [CrOS](#Chrome_OS) | [StarOffice](#StarOffice) | Other |
| **Helvetica** | Nimbus Sans | TeX Gyre Heros | FreeSans | MS Sans Serif (Helv) | **Arial** | Liberation Sans | Arimo | Albany |
| **Times** | Nimbus Roman | TeX Gyre Termes | FreeSerif | MS Serif (Tms Rmn) | **Times New Roman** | Liberation Serif | Tinos | Thorndale |
| **Courier** | Nimbus Mono | TeX Gyre Cursor | FreeMono | **Courier New** | Liberation Mono | Cousine | Cumberland |
| **Helvetica Condensed** | Nimbus Sans Narrow | TeX Gyre Heros Cn | **Arial Narrow** | Liberation Sans Narrow |
| **Georgia** | Gelasio |

<caption>Microsoft Office fonts</caption>
| [Microsoft](#Microsoft) | [CrOS](#Chrome_OS) |
| **Cambria** | Caladea |
| **Calibri** | Carlito |
| **Symbol** | SymbolNeu |

<caption>Other PostScript core families</caption>
| [PostScript](#PostScript) | [URW](#PostScript) | [GUST](#TeX_Gyre) | [Windows](#Microsoft) |
| ITC Avant Garde Gothic | URW Gothic | TeX Gyre Adventor |
| ITC Bookman | Bookman URW | TeX Gyre Bonum | Bookman Old Style |
| ITC Zapf Chancery | Chancery URW | TeX Gyre Chorus |
| Palatino | Palladio URW | TeX Gyre Pagella | Palatino Linotype |
| New Century Schoolbook | Century SchoolBook URW | TeX Gyre Schola | Century Schoolbook |

## Generic Families

### PostScript

The PostScript language defines [35 core fonts](https://en.wikipedia.org/wiki/PostScript_fonts#Core_Font_Set "wikipedia:PostScript fonts") in PostScript 2\. URW released open-source versions of these 35 fonts for [w:ghostscript](https://en.wikipedia.org/wiki/ghostscript "w:ghostscript"). Projects including GUST's [TeX Gyre](#TeX_Gyre) and [GNU FreeFont](#GNU_FreeFont) release enhanced versions of these fonts.

### Microsoft

Microsoft bundles a number of fonts with Microsoft Windows and Microsoft Office. While some of these fonts are just a cheaper version (or look-alike) of corresponding PostScript families, Cambria and Calibri (default font since MS Office 2007) are independent from other families. Microsoft used to provide many core fonts in its [Core fonts for the Web](https://en.wikipedia.org/wiki/Core_fonts_for_the_Web "wikipedia:Core fonts for the Web") project. Although this project is later unavailable on Microsoft's site, the license terms that allow these fonts to be distributed from third-party sites make packages like [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) possible. See also [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts").

## Metric-compatible font projects

### TeX Gyre

[TeX Gyre](http://www.gust.org.pl/projects/e-foundry/tex-gyre/) is a remake and extension of 35 base PostScript fonts distributed with Ghostscript ver. 4.00\. The project provides TeX support and also the cross-platform OpenType format of the fonts.

### GNU FreeFont

[GNU FreeFont](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") is an outline family intended to cover as much of the UCS charset as possible. Most of the Latin characters [are from](https://www.gnu.org/software/freefont/sources/) [URW](#PostScript) fonts. This set of fonts is released under GPL v3+ + FE.

### Liberation

[Wikipedia:Liberation fonts](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") provides four families Liberation Sans, Liberation Serif, and Liberation Mono, intended to be metric-compatible with common Microsoft Windows fonts. Since version 2.0.0, this set of fonts is released under SIL OFL, and is based on [#Chrome OS](#Chrome_OS) core fonts. They are available as [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

Older, GPL-licensed versions of this font is based on Ascender Corporation's fonts, which is licensed by Red Hat, Inc. These versions of Liberation also includes Liberation Sans Narrow, which corresponds to Arial Narrow.

### Google

Google provides a high number of [fonts](https://www.google.com/fonts), including different metric-compatible font families.

#### Chrome OS

Google ships open-source metric-compatible fonts with its operating system, Chrome OS, under the Apache License 2.0\. CrOS core (croscore, [ttf-croscore](https://www.archlinux.org/packages/?name=ttf-croscore)) is a collection of Arimo (sans), Tinos (serif) and Cousine (mono), also licensed from Ascender Corporation. A set of extra fonts, CrOS extra (crosextra) provides Carlito ([ttf-carlito](https://aur.archlinux.org/packages/ttf-carlito/)) and Caladea ([ttf-caladea](https://aur.archlinux.org/packages/ttf-caladea/)) to match default fonts for Microsoft Word.

#### Noto

[Google's Noto Fonts](https://www.google.com/get/noto/) are available via [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts). They are licensed under SIL OFL.

## Example configuration

For font consistency, all applications should be set to use the serif, sans-serif, and monospace aliases, which are mapped to particular fonts by fontconfig. [Font configuration#Replace or set default fonts](/index.php/Font_configuration#Replace_or_set_default_fonts "Font configuration") explains two ways to achieve the configuration, both are covered with an example for metric-compatible fonts below.

### Example for binding method

The following example configuration uses the [#Liberation](#Liberation) fonts.

 `/etc/fonts/local.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <match target="pattern">
        <test qual="any" name="family"><string>serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Serif</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>sans-serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Sans</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>monospace</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Mono</string></edit>
    </match>
</fontconfig>
```

### Example for prefer method

The following example configuration uses the [#Chrome OS](#Chrome_OS) fonts, adding additional aliases for other fonts frequently required to refer.

 `/etc/fonts/local.conf` 
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <alias>
    <family>serif</family>
    <prefer><family>Tinos</family></prefer>
  </alias>
  <alias>
    <family>sans-serif</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>sans</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer><family>Cousine</family></prefer>
  </alias>

  <match>
    <test name="family"><string>Arial</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Helvetica</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Verdana</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Tahoma</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Times New Roman</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Tinos</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Times</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Tinos</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Consolas</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Cousine</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Courier New</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Cousine</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Calibri</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Carlito</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Cambria</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Caladea</string>
    </edit>
  </match> 
</fontconfig>
```

## See also

*   [Substituting Calibri and Cambria fonts](https://wiki.debian.org/SubstitutingCalibriAndCambriaFonts) (Debian Wiki)