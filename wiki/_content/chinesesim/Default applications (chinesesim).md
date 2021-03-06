**翻译状态：** 本文是英文页面 [Default applications](/index.php/Default_applications "Default applications") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-03，点击[这里](https://wiki.archlinux.org/index.php?title=Default+applications&diff=0&oldid=525282)可以查看翻译后英文页面的改动。

相关文章

*   [桌面配置项](/index.php/%E6%A1%8C%E9%9D%A2%E9%85%8D%E7%BD%AE%E9%A1%B9 "桌面配置项")
*   [桌面环境](/index.php/%E6%A1%8C%E9%9D%A2%E7%8E%AF%E5%A2%83 "桌面环境")
*   [窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")

Programs sometimes need to open a file or a [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier "wikipedia:Uniform Resource Identifier") in the user's preferred application. To open a file in the user's preferred application the filetype needs to be detected (usually using filename extensions or [magic numbers](https://en.wikipedia.org/wiki/List_of_file_signatures "wikipedia:List of file signatures") mapped to [MIME types](https://en.wikipedia.org/wiki/Media_type "wikipedia:Media type")) and there needs to be an application associated with the filetype.

*   Some programs (particularly command-line programs) detect default programs using [environment variables](/index.php/Environment_variables "Environment variables"), see [Environment variables#Default programs](/index.php/Environment_variables#Default_programs "Environment variables").
*   Some programs (particularly heirloom UNIX programs) use [mime.types](https://en.wikipedia.org/wiki/Media_type#mime.types "wikipedia:Media type") for MIME type detection and [mailcap](https://en.wikipedia.org/wiki/Media_type#Mailcap "wikipedia:Media type") for application association.
*   Many programs outsource the task completely to a [#Resource opener](#Resource_openers).

Freedesktop.org has standardized filetype detection with the [Shared MIME database](/index.php/Shared_MIME_database "Shared MIME database") specification and application association with the [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") specification.

Some desktop environments also provide a GUI or a file-manager which can interactively configure default applications. If you do not use a desktop environment, you may need to install additional software in order to conveniently manage default applications.

## Contents

*   [1 Resource openers](#Resource_openers)
    *   [1.1 xdg-open](#xdg-open)
    *   [1.2 perl-file-mimeinfo](#perl-file-mimeinfo)
    *   [1.3 mimeo](#mimeo)
    *   [1.4 whippet](#whippet)
    *   [1.5 Minimalist replacements](#Minimalist_replacements)
        *   [1.5.1 run-mailcap](#run-mailcap)

## Resource openers

*   **XDG MIME Apps**: implements the [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") specification
*   **RegEx rules**: allows MIME types to be associated with applications using regular expressions
*   **URI support**: allows arbitrary URI schemes to be associated with applications

| Name | Package | XDG MIME Apps | RegEx rules | URI support |
| [xdg-open](/index.php/Xdg-open "Xdg-open") | [xdg-utils](/index.php/Xdg-utils "Xdg-utils") | Yes | No | Yes |
| [mimeopen(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mimeopen.1p) | [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) | Yes | No | No |
| mimeo | [mimeo](https://aur.archlinux.org/packages/mimeo/) | Yes | Yes | Yes |
| whippet | [whippet](https://aur.archlinux.org/packages/whippet/) | Yes | No | Yes |
| linopen | [linopen](https://aur.archlinux.org/packages/linopen/) | No | Yes | Yes |
| mimi | [mimi-git](https://aur.archlinux.org/packages/mimi-git/) | No | No | partly |
| busking | [busking-git](https://aur.archlinux.org/packages/busking-git/) | No | Yes | Yes |
| sx-open | [sx-open](https://aur.archlinux.org/packages/sx-open/) | No | Yes | Yes |
| [rifle(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rifle.1) | [ranger](/index.php/Ranger "Ranger") | No | Yes | No |

### xdg-open

[xdg-open](/index.php/Xdg-open "Xdg-open") (part of [xdg-utils](/index.php/Xdg-utils "Xdg-utils")) implements [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") and is used by many programs.

Because of the complexity of the [xdg-utils](/index.php/Xdg-utils "Xdg-utils") version of [xdg-open](/index.php/Xdg-open "Xdg-open"), it can be difficult to debug when the wrong default application is being opened. Because of this, there are many alternatives that attempt to improve upon it. Several of these alternatives replace the `/usr/bin/xdg-open` executable, thus changing the default application behavior of most applications. Others simply provide an alternative method of choosing default applications.

### perl-file-mimeinfo

[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) provides the tools [mimeopen(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mimeopen.1p) and [mimetype(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mimetype.1p). These have a slightly nicer interface than their [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) equivalents:

```
# determine a file's MIME type
$ mimetype photo.jpeg
photo.jpeg: image/jpeg

# choose the default application for this file
$ mimeopen -d photo.jpeg
Please choose an application

    1) Feh (feh)
    2) GNU Image Manipulation Program (gimp)
    3) Pinta (pinta)

use application #

# open a file with its default application
$ mimeopen -n photo.jpeg

```

Most importantly, [xdg-utils](/index.php/Xdg-utils "Xdg-utils") programs will actually call `mimetype` instead of `file` for MIME type detection, if it does not detect your [desktop environment](/index.php/Desktop_environment "Desktop environment"). This is important because `file` does not follow the XDG standard.

**Note:** [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) before 0.28-1 does not *entirely* follow the XDG standard. For example it does not read [distribution-wide defaults](https://github.com/mbeijen/File-MimeInfo/issues/20) and it saves its config in [deprecated locations](https://github.com/mbeijen/File-MimeInfo/issues/8).

### mimeo

[mimeo](https://aur.archlinux.org/packages/mimeo/) provides the tool `mimeo`, which unifies the functionality of `xdg-open` and `xdg-mime`.

```
# determine a file's MIME type
$ mimeo -m photo.jpeg
photo.jpeg
  image/jpeg

# choose the default application for this MIME type
$ mimeo --add image/jpeg feh.desktop

# open a file with its default application
$ mimeo photo.jpeg

```

However a big difference with *xdg-utils* is that mimeo also supports custom "association files" that allow for more complex associations. For example, passing specific command line arguments based on a regular expression match:

```
# open youtube links in VLC without opening a new instance
vlc --one-instance --playlist-enqueue %U
  ^https?://(www.)?youtube.com/watch\?.*v=

```

[xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/) patches *xdg-utils* so that `xdg-open` falls back to mimeo if no desktop environment is detected.

### whippet

[whippet](https://aur.archlinux.org/packages/whippet/) provides the tool `whippet`, which is similar to `xdg-open`. It has X11 integration by using [libnotify](https://www.archlinux.org/packages/?name=libnotify) to display errors and [dmenu](https://www.archlinux.org/packages/?name=dmenu) to display choices between applications to open.

```
# open a file with its default application
$ whippet -M photo.jpeg

# choose from all possible applications for opening a file (without setting a default)
$ whippet -m photo.jpeg

```

In addition to implementing [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications"), *whippet* can also use a SQlite database of weighted application/MIME type/regex associations to determine which app to use.

### Minimalist replacements

The following packages conflict with and provide [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) because they provide their own `/usr/bin/xdg-open` script.

If you want to use one of these resource openers while still being able to use [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), install them manually in a PATH directory before `/usr/bin`.

*   [linopen](https://aur.archlinux.org/packages/linopen/) - 170-line Bash script, supports regex rules
*   [mimi-git](https://aur.archlinux.org/packages/mimi-git/) - 130-line Bash script, can change command arguments for each MIME type
*   [busking-git](https://aur.archlinux.org/packages/busking-git/) - 80-line Perl script similar to *mimi* but also supports regex rules
*   [sx-open](https://aur.archlinux.org/packages/sx-open/) - 60-line Bash script, uses a simple shell-based config file

#### run-mailcap

**Warning:** If you use [run-mailcap](https://aur.archlinux.org/packages/run-mailcap/), it is possible for `xdg-open` to delegate to it. This will cause an infinite loop if you are using the `/etc/mailcap` from [mailcap](https://www.archlinux.org/packages/?name=mailcap), because it also delegates to `xdg-open`.