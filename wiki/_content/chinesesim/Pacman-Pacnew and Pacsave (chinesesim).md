**翻译状态：** 本文是英文页面 [Pacnew_and_Pacsave_Files](/index.php/Pacnew_and_Pacsave_Files "Pacnew and Pacsave Files") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-18，点击[这里](https://wiki.archlinux.org/index.php?title=Pacnew_and_Pacsave_Files&diff=0&oldid=487323)可以查看翻译后英文页面的改动。

在使用 pacman 移除一个带有配置文档的软件包时，pacman 通常会将配置文档复制为一个后缀名为 .pacsave 的备份文档。

同样的，当 pacman 升级一个软件包，而新软件包含有与与当前配置不同的新配置文件时，pacman 会将新配置写入 .pacnew 文件。当写入这些文件时，pacman 会输出提示信息。

## Contents

*   [1 为什么创建了这样的文件](#.E4.B8.BA.E4.BB.80.E4.B9.88.E5.88.9B.E5.BB.BA.E4.BA.86.E8.BF.99.E6.A0.B7.E7.9A.84.E6.96.87.E4.BB.B6)
*   [2 包备份文件](#.E5.8C.85.E5.A4.87.E4.BB.BD.E6.96.87.E4.BB.B6)
*   [3 类型说明](#.E7.B1.BB.E5.9E.8B.E8.AF.B4.E6.98.8E)
    *   [3.1 .pacnew](#.pacnew)
    *   [3.2 .pacsave](#.pacsave)
*   [4 定位 .pac* 文件](#.E5.AE.9A.E4.BD.8D_.pac.2A_.E6.96.87.E4.BB.B6)
*   [5 .管理 .pacnew 文件](#..E7.AE.A1.E7.90.86_.pacnew_.E6.96.87.E4.BB.B6)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 为什么创建了这样的文件

当升级某个软件包（命令为 `pacman -Syu`，`pacman -Su` 或者`pacman -U`）时，可能会创建一个 `.pacnew` 文件，以避免覆盖一个之前被用户修改过的已存在文件。此时，pacman会输出如下信息：

```
warning: /etc/pam.d/usermod installed as /etc/pam.d/usermod.pacnew

```

当卸载某个软件包（命令为 `pacman -R`）或升级某个软件包（该软件包必须首先被卸载）时，可能会创建一个 `.pacsave` 文件。当 pacman 数据库记录了应当备份该软件包的某个文件时，pacman 会创建一个 `.pacsave` 文件。此时，pacman 会输出如下信息：

```
warning: /etc/pam.d/usermod saved as /etc/pam.d/usermod.pacsave

```

这些文件需要用户手动干预，我们推荐您在每次软件包升级或卸载之后马上处理它们。如果不处理，不当的配置可能导致软件功能出问题，甚至完全无法使用。

## 包备份文件

软件包的 `PKGBUILD` 文件指定了升级或卸载软件包时哪写文件需要被保存或备份。例如，`puslseaudio` 的 `PKGBUILD` 文件包含如下行：

```
backup=('etc/pulse/client.conf' 'etc/pulse/daemon.conf' 'etc/pulse/default.pa')

```

## 类型说明

### .pacnew

对于包升级过程中的每个备份文件，pacman 会交叉校验三个版本的文件内容生成的 [md5sums](https://en.wikipedia.org/wiki/zh:Md5sum "wikipedia:zh:Md5sum") 值：一个为软件包最初创建的版本，一个为文件系统中当前的版本，还有一个为新软件包中的版本。如果软件包安装的版本被修改为文件系统中当前的版本，pacman 不知道如何将这些修改合并到新版本的文件中。因此，pacman 以扩展名 `.pacnew` 保存新版本的文件，修改过的版本保持不变，而不是被覆盖。

更细一步来说，3路MD5值校验结果为下述输出之一：

	original = *X*, current = *X*, new = *X* 

	三个版本的文件具有相同的内容，因此覆盖不会产生问题。pacman 将用新版本覆盖当前版本而不通知用户。（尽管文件内容相同，覆盖操作会更新文件系统中和文件创建，修改和访问时间有关的信息，也确保了任何文件权限的修改被实施。）

	original = *X*, current = *X*, new = *Y* 

	当前版本文件的内容和原始版本的相同，但与新版本不同。既然用户没有修改过当前版本文件，且新版本可能包含改进和 bug 修正，pacman 用新版本覆盖当前版本，而不通知用户。这是 pacman 有能力执行的唯一一个新改动的自动合并。

	original = *X*, current = *Y*, new = *X* 

	原始软件包和新软件包都包含版本完全相同的文件，但当前文件系统中的版本是被修改过的。此时 pacman 保留当前版本，忽略新版本，且不通知用户。

	original = *X*, current = *Y*, new = *Y* 

	新版本和当前版本相同。此时 pacman 将用新版本覆盖当前版本且不通知用户。（尽管文件内容相同，覆盖操作会更新文件系统中和文件创建，修改和访问时间有关的信息，也确保了任何文件权限的修改被实施。）

	original = *X*, current = *Y*, new = *Z* 

	三个版本的文件都不相同，所以保留当前版本，以扩展名 `.pacnew` 创建新版本，且警告用户创建了新版本。希望用户手动将需要的更改由新版本合并至当前版本。

### .pacsave

如果用户修改了 `backup` 中指定的某个文件，那么那个文件将被重命名，带上 `.pacsave` 扩展名，且在其他软件包移除之后仍然存在于文件系统中。

**注意:** 使用命令 `pacman -R` 中的 `-n` 选项会移除指定软件包中的所有文件，因此不会创建 `.pacsave` 文件。

## 定位 .pac* 文件

首先需要确定这些文件的位置，才能手动维护这些文件。当升级或卸载大量软件包时，可能会错过升级的 *.pac* 的信息。你需要寻找是否产生了 `*.pac*` 文件：

仅搜索绝大多数全局配置文件所存放的位置：

```
$ find /etc -regextype posix-extended -regex ".+\.pac(new|save)" 2> /dev/null

```

或全盘搜索：

```
$ find / -regextype posix-extended -regex ".+\.pac(new|save)" 2> /dev/null

```

如果你安装了 [locate](/index.php/Locate "Locate")，还可以使用它来搜索。首先需要更新索引数据库：

```
# updatedb

```

然后:

```
$ locate -e --regex "\.pac(new|save)$"

```

或者使用pacman日志来找到它们：

```
$ egrep "pac(new|save)" /var/log/pacman.log

```

注意：日志不会记录文件系统里现在有哪些文件，也不会记录哪些文件已经被移除。

## .管理 .pacnew 文件

Pacman 包含了 *pacdiff* 工具管理 pacnew/pacsave 文件。这个工具会搜索所有的 `pacnew` 和 `pacsave` 文件并询问要执行的操作。默认使用 [vimdiff](/index.php/Vim#Merging_files "Vim") 工具，可以通过 `DIFFPROG=your_editor pacdiff` 指定要使用的差异比较工具。参考 [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison.2C_diff.2C_merge "List of applications/Utilities").

下面一些 [AUR](/index.php/AUR "AUR") 三方工具可以自动处理这些文件：

*   **[Dotpac](/index.php/Dotpac "Dotpac")** — Basic interactive script with ncurses-based text interface and helpful walkthrough. No merging or auto-merging features.

	[https://github.com/AladW/dotpac](https://github.com/AladW/dotpac) || [dotpac](https://aur.archlinux.org/packages/dotpac/)

*   **etc-update** — Arch port of Gentoo's *etc-update* utility, providing a simple CLI to view, merge and interactively edit changes. Trivial changes (such as comments) can be merged automatically.

	[https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update](https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update) || [etc-update](https://aur.archlinux.org/packages/etc-update/)

*   **pacmarge** — A tool for automatically merging .pacnew files

	[https://github.com/foutrelis/pacmarge](https://github.com/foutrelis/pacmarge) || [pacmarge](https://aur.archlinux.org/packages/pacmarge/)

*   **pacnew-auto** — Automatic `pacnew` merging using [git](https://www.archlinux.org/packages/?name=git) rebase.

	[https://github.com/joanrieu/pacnew-auto](https://github.com/joanrieu/pacnew-auto) || [pacnew-auto-git](https://aur.archlinux.org/packages/pacnew-auto-git/)

*   **pacnews-git** — A simple script aimed at finding all *.pacnew* files, then editing them with [vimdiff](/index.php/Vim#Merging_files "Vim").

	[https://github.com/pbrisbin/scripts/blob/master/pacnews](https://github.com/pbrisbin/scripts/blob/master/pacnews) || [pacnews-git](https://aur.archlinux.org/packages/pacnews-git/)

## 参阅

*   Arch Linux 论坛: [处理 .pacnew 文件](https://bbs.archlinux.org/viewtopic.php?id=53532)