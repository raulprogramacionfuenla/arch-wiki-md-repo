相关文章

*   [Fonts](/index.php/Fonts "Fonts")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")

**翻译状态：** 本文是英文页面 [MS_Fonts](/index.php/MS_Fonts "MS Fonts") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-18，点击[这里](https://wiki.archlinux.org/index.php?title=MS_Fonts&diff=0&oldid=486060)可以查看翻译后英文页面的改动。

本文介绍如何安装微软 TrueType 字体并模拟 Windows 渲染设置。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 从Windows使用字体](#.E4.BB.8EWindows.E4.BD.BF.E7.94.A8.E5.AD.97.E4.BD.93)
    *   [1.2 当前软件包](#.E5.BD.93.E5.89.8D.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [1.3 旧程序包](#.E6.97.A7.E7.A8.8B.E5.BA.8F.E5.8C.85)
*   [2 微软字体适用的 Fontconfig 规则](#.E5.BE.AE.E8.BD.AF.E5.AD.97.E4.BD.93.E9.80.82.E7.94.A8.E7.9A.84_Fontconfig_.E8.A7.84.E5.88.99)
*   [3 Windows 8](#Windows_8)

## 安装

### 从Windows使用字体

如果有一个安装了Windows的分区, 可以通过链接它们来使用其字体。

*例如, Windows的C:\盘被挂载在`/windows`:*

```
# ln -s /windows/Windows/Fonts /usr/share/fonts/WindowsFonts

```

然后重新生成字体缓存：

```
# fc-cache -f

```

或者,将Windows的字体复制到`/usr/share/fonts`:

```
# mkdir /usr/share/fonts/WindowsFonts
# cp /windows/Windows/Fonts/* /usr/share/fonts/WindowsFonts
# chmod 755 /usr/share/fonts/WindowsFonts/*

```

然后重新生成字体缓存：

```
# fc-cache -f 

```

### 当前软件包

**Note:** 这些包需要访问 Windows 7 和/或 Office 2007 的安装程序或安装媒体。

*   [ttf-office-2007-fonts](https://aur.archlinux.org/packages/ttf-office-2007-fonts/) - Microsoft Office 2007字体
*   [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/) - Windows 7字体
*   [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) - Windows 8.1 字体
*   [ttf-ms-win10](https://aur.archlinux.org/packages/ttf-ms-win10/) — Windows 10 字体

### 旧程序包

**Note:** 由这些包提供的字体已过期和缺少现代提示的指令和全字符集。建议使用上面所述软件包。

[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) 包含:

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono")
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial")
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black")
*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans")
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New")
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) "wikipedia:Georgia (typeface)")
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) "wikipedia:Impact (typeface)")
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans")
*   [Lucida Console](https://en.wikipedia.org/wiki/Lucida_Console "wikipedia:Lucida Console")
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif")
*   [Symbol](https://en.wikipedia.org/wiki/Symbol_(typeface) "wikipedia:Symbol (typeface)")
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman")
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS")
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana")
*   [Webdings](https://en.wikipedia.org/wiki/Webdings "wikipedia:Webdings")
*   [Wingdings](https://en.wikipedia.org/wiki/Wingdings "wikipedia:Wingdings")

根据[微软的最终用户许可协议](http://web.archive.org/web/20020227054122/www.microsoft.com/typography/fontpack/eula.htm)，有“一些”法律限制时使用的字体。

[ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/)包含 [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) "wikipedia:Tahoma (typeface)")。

[ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)是一个[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")包，它包括：

*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri")
*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) "wikipedia:Cambria (typeface)")
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara")
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas")
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) "wikipedia:Constantia (typeface)")
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) "wikipedia:Corbel (typeface)")

## 微软字体适用的 Fontconfig 规则

网站通常使用字体的通用名称(helvetica, courier, times 或 times new roman)，fontconfig 的一个规则文件将其替换为不太美观的免费字体：

```
/etc/fonts/conf.d/30-metric-aliases-free.conf

```

要使用微软字体，需要将通用名称映射到微软的字体：

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
       <alias binding="same">
         <family>Helvetica</family>
         <accept>
         <family>Arial</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Times</family>
         <accept>
         <family>Times New Roman</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Courier</family>
         <accept>
         <family>Courier New</family>
         </accept>
       </alias>
</fontconfig>

```

建议在浏览器中，将 serif,sans-serif,monospace 字体也映射到 MS 字体。

## Windows 8

The [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) split package is intended as a more up-to-date replacement for [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/), [ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/) and [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/).

Although it provides newer versions of the fonts, it **cannot automatically download the fonts** due to license issues .

**Note:** usage of Microsoft fonts outside running Windows system is prohibited by EULA (although in certain countries EULA is invalid). Please consult Microsoft license before using fonts.

You can acquire fonts from an installed and fully updated Windows 8.1 system. Any edition of *Windows 8.1 build **Windows 8.1 6.3.9600.17238*** will work.

On the installed Windows 8.1 system fonts are usually located in `[%WINDIR%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\Fonts` and license file is `[%SYSTEM32%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\license.rtf`.

You need the files listed in the `source=()` array. Place them in the same directory as this [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") file, then run [makepkg](/index.php/Makepkg "Makepkg").

`makepkg --pkg ttf-ms-win8` will make just the Windows 8.1 core fonts package which should cover even more than [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).