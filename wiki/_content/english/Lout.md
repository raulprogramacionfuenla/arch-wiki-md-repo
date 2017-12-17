[Lout](http://savannah.nongnu.org/projects/lout) is a lightware document formatting system invented by Jeffrey H. Kingston. It reads a high-level description of a document similar in style to LaTeX and produces a PostScript.

## Installation

The [lout package](https://www.archlinux.org/packages/community/x86_64/lout) could be [Installed](/index.php/Install "Install") from the [official repositories](https://wiki.archlinux.org/index.php/Official_repositories).

In order to enable cyrillic printout, fonts need to be installed separately (e.g [lout-dejavu](https://aur.archlinux.org/packages/lout-dejavu-git) from [AUR](/index.php/AUR "AUR"))

## Using

Lout supports only one byte encoding, thus you need to use specific character map in case of non-english input.

 `example.lout` 
```
@SysInclude {doc}
@SysInclude {dejavu}
@Document
  @InitialFont { DejaVuSerif Base 12p}
  @InitialLanguage { Russian }
@Text @Begin

@Display @Heading {Russian language example}

@LP
Параграф на русском языке.

@End @Text

```

[Core_utilities#iconv](/index.php/Core_utilities#iconv "Core utilities") could be used to obtain required encoding, before feed source to lout:

```
$ iconv -f utf-8 -t koi8-r example.lout example.koi8-r.lout
$ lout  example.koi8-r.lout example.ps

```

[Ps2pdf](/index.php/Ps2pdf "Ps2pdf") could be used to covert post script file to pdf:

```
$ ps2pdf example.ps example.pdf

```