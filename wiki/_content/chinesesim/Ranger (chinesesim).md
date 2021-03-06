Related articles

*   [Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")
*   [vifm](/index.php/Vifm "Vifm")

**翻译状态：** 本文是英文页面 [Ranger](/index.php/Ranger "Ranger") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-24，点击[这里](https://wiki.archlinux.org/index.php?title=Ranger&diff=0&oldid=494276)可以查看翻译后英文页面的改动。

[ranger](http://ranger.nongnu.org/) 是一个基于文本的文件管理器，以 Python 编写。不同层级的目录分别在一个面板的三列中进行展示. 可以通过快捷键, 书签, 鼠标以及历史命令在它们之间移动. 当选中文件或目录时, 会自动显示文件或目录的内容.

主要特性有: vi 风格的快捷键, 书签, 选择, 标签, 选项卡, 命令历史, 创建符号链接的能力, 多种终端模式, 以及任务视图. ranger 可以定制命令和快捷键，包括绑定到外部脚本。最接近的竞争者是 [Vifm](/index.php/Vifm "Vifm")， 它有 2 个面板以及 vi 风格的快捷键，但是总体特性相对较少。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 用法](#.E7.94.A8.E6.B3.95)
*   [3 定制](#.E5.AE.9A.E5.88.B6)
    *   [3.1 命令定义](#.E5.91.BD.E4.BB.A4.E5.AE.9A.E4.B9.89)
    *   [3.2 配色方案](#.E9.85.8D.E8.89.B2.E6.96.B9.E6.A1.88)
    *   [3.3 文件关联](#.E6.96.87.E4.BB.B6.E5.85.B3.E8.81.94)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 存档相关](#.E5.AD.98.E6.A1.A3.E7.9B.B8.E5.85.B3)
        *   [4.1.1 解压缩](#.E8.A7.A3.E5.8E.8B.E7.BC.A9)
        *   [4.1.2 压缩](#.E5.8E.8B.E7.BC.A9)
    *   [4.2 外部驱动](#.E5.A4.96.E9.83.A8.E9.A9.B1.E5.8A.A8)
    *   [4.3 镜像挂载](#.E9.95.9C.E5.83.8F.E6.8C.82.E8.BD.BD)
    *   [4.4 在当前目录打开新标签](#.E5.9C.A8.E5.BD.93.E5.89.8D.E7.9B.AE.E5.BD.95.E6.89.93.E5.BC.80.E6.96.B0.E6.A0.87.E7.AD.BE)
    *   [4.5 Shell tips](#Shell_tips)
        *   [4.5.1 目录同步](#.E7.9B.AE.E5.BD.95.E5.90.8C.E6.AD.A5)
        *   [4.5.2 Start a shell from ranger](#Start_a_shell_from_ranger)
        *   [4.5.3 避免在 ranger 启动的 shell 内创建新的 ranger](#.E9.81.BF.E5.85.8D.E5.9C.A8_ranger_.E5.90.AF.E5.8A.A8.E7.9A.84_shell_.E5.86.85.E5.88.9B.E5.BB.BA.E6.96.B0.E7.9A.84_ranger)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Artifacts in image preview](#Artifacts_in_image_preview)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 安装

安装 [ranger](https://www.archlinux.org/packages/?name=ranger) 包，或其开发版 [ranger-git](https://aur.archlinux.org/packages/ranger-git/)。

## 用法

在 [终端](/index.php/List_of_applications#Terminal_emulators "List of applications") 里执行 `ranger` 来启动 ranger.

<caption></caption>
| 快捷键 | 命令 |
| `?` | 打开帮助手册或列出快捷键、命令以及设置项 |
| `l`, `Enter` | 打开文件 |

## 定制

启动之后 ranger 会创建一个目录 `~/.config/ranger/`。可以使用以下命令复制默认配置文件到这个目录:

 `ranger --copy-config=all` 

了解一些基本的 python 知识可能对定制 ranger 会有帮助。

*   `rc.conf` - 选项设置和快捷键
*   `commands.py` - 能通过 `:` 执行的命令
*   `rifle.conf` - 指定不同类型的文件的默认打开程序。

`rc.conf` 只需要包含与默认配置文件不同的部分, 因为它们都会被加载。对于 `commands.py`，如果你没有包含整个文件，把下面这一行加入到文件起始处：

```
from ranger.api.commands import *

```

如果想添加一个把文件移动到目录 `~/.Trash/` 的快捷键 `DD`, 把以下这一行添加到 `~/.config/ranger/rc.conf`:

```
map DD shell mv -t /home/${USER}/.Trash %s

```

可以在 [man ranger](http://ranger.nongnu.org/ranger.1.html) 中查阅所有配置.

### 命令定义

继续上面的例子，在 `~/.config/ranger/commands.py` 增加如下代码将会定义一个清空垃圾箱 `~/.Trash` 的命令。

```
class empty(Command):
    """:empty

    Empties the trash directory ~/.Trash
    """

    def execute(self):
        self.fm.run("rm -rf /home/myname/.Trash/{*,.[^.]*}")

```

输入 `:empty` 与 `Enter` 来执行命令， 如果希望的话，也可以使用 tab 补全。

**Warning:** 注意 [^.] 是上面命令的必要部分。否则，它会删除所有 ..* 形式的文件和目录，即删除你家目录的所有数据。

### 配色方案

Ranger 配备了四个配色方案：`默认`、`丛林`、`积雪`和`烈日`。 下列命令可自定义配色：

```
 set colorscheme *scheme*

```

自定义配色方案放在 `~/.config/ranger/colorschemes`。

### 文件关联

Ranger 使用自己的文件打开程序，名为`rifle`，它的配置文件为 `~/.config/ranger/rifle.conf`。如果该文件不存在，可运行 `ranger --copy-config=rifle` 生成。例如，如下的代码指定 [kile](https://www.archlinux.org/packages/?name=kile) 为打开 tex 文件的默认程序。

```
ext tex = kile "$@"

```

使用 [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) 来打开所有文件:

```
has xdg-open, flag f = xdg-open "$1"

```

## 提示与技巧

### 存档相关

可以使用 [atool](https://www.archlinux.org/packages/?name=atool) 或 [p7zip](https://www.archlinux.org/packages/?name=p7zip) 来进行存档操作。

#### 解压缩

下面的命令实现了复制(yy)一个或多个存档文件，然后执行 ":extracthere" 解压到需要的目录。

```
import os
from ranger.core.loader import CommandLoader

class extracthere(Command):
    def execute(self):
        """ Extract copied files to current directory """
        copied_files = tuple(self.fm.copy_buffer)

        if not copied_files:
            return

        def refresh(_):
            cwd = self.fm.get_directory(original_path)
            cwd.load_content()

        one_file = copied_files[0]
        cwd = self.fm.thisdir
        original_path = cwd.path
        au_flags = ['-X', cwd.path]
        au_flags += self.line.split()[1:]
        au_flags += ['-e']

        self.fm.copy_buffer.clear()
        self.fm.cut_buffer = False
        if len(copied_files) == 1:
            descr = "extracting: " + os.path.basename(one_file.path)
        else:
            descr = "extracting files from: " + os.path.basename(one_file.dirname)
        obj = CommandLoader(args=['aunpack'] + au_flags \
                + [f.path for f in copied_files], descr=descr)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)
```

对于使用 7z 的用户, 可以在添加以下命令后, 选中压缩包然后执行 ":extract" 或通过绑定的快捷键来解压

```
class extract(Command):
    """:extract <paths>

    Extract archives using 7z
    """
    def execute(self):
        import os
        fail=[]
        for i in self.fm.thistab.get_selection():
            ExtractProg='7z x'
            if i.path.endswith('.zip'):
                # zip encoding issue
                ExtractProg='unzip -O gbk'
            elif i.path.endswith('.tar.gz'):
                ExtractProg='tar xvf'
            elif i.path.endswith('.tar.xz'):
                ExtractProg='tar xJvf'
            elif i.path.endswith('.tar.bz2'):
                ExtractProg='tar xjvf'
            if os.system('{0} "{1}"'.format(ExtractProg, i.path)):
                fail.append(i.path)
        if len(fail) > 0:
            self.fm.notify("Fail to extract: {0}".format(' '.join(fail)), duration=10, bad=True)
        self.fm.redraw_window()
```

PS: 如果需要解压 ZIP 压缩包还需要安装 [unzip-iconv](https://aur.archlinux.org/packages/unzip-iconv/)(为了解决中文乱码问题)

#### 压缩

The following command allows the user to compress several files on the current directory by marking them and then calling ":compress <package name>". It supports name suggestions by getting the basename of the current directory and appending several possibilities for the extension.

```
import os
from ranger.core.loader import CommandLoader

class compress(Command):
    def execute(self):
        """ Compress marked files to current directory """
        cwd = self.fm.thisdir
        marked_files = cwd.get_selection()

        if not marked_files:
            return

        def refresh(_):
            cwd = self.fm.get_directory(original_path)
            cwd.load_content()

        original_path = cwd.path
        parts = self.line.split()
        au_flags = parts[1:]

        descr = "compressing files in: " + os.path.basename(parts[1])
        obj = CommandLoader(args=['apack'] + au_flags + \
                [os.path.relpath(f.path, cwd.path) for f in marked_files], descr=descr)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

    def tab(self):
        """ Complete with current folder name """

        extension = ['.zip', '.tar.gz', '.rar', '.7z']
        return ['compress ' + os.path.basename(self.fm.thisdir.path) + ext for ext in extension]
```

### 外部驱动

外部驱动可以通过 [udev](/index.php/Udev "Udev") 或 [udisks] 自动挂载。挂载在 `/media` 下的驱动可以通过快捷键 `gm` (go, media) 访问。

### 镜像挂载

以下命令假设你正在使用 [CDemu](/index.php/CDemu "CDemu") 作为你的镜像挂载器和一些挂载虚拟驱动器到指定位置 (如 '/media/virtualrom') ，类似于 [autofs](/index.php/Autofs "Autofs")的系统。**不要忘记根据你的系统设置修改挂载路径**.

为了从 ranger 里把镜像挂载到 cdemud 虚拟驱动器, 需要选中镜像文件然后在终端输入 ':mount'。根据你的设置，挂载可能会需要一些时间(我的需要长达一分钟的时间). 以下命令使用自定义的 loader 会等待加载过程结束然后通过后台在第 9 标签打开挂载了的镜像.

```
import os, time
from ranger.core.loader import Loadable
from ranger.ext.signals import SignalDispatcher
from ranger.ext.shell_escape import *

class MountLoader(Loadable, SignalDispatcher):
    """
    Wait until a directory is mounted
    """
    def __init__(self, path):
        SignalDispatcher.__init__(self)
        descr = "Waiting for dir '" + path + "' to be mounted"
        Loadable.__init__(self, self.generate(), descr)
        self.path = path

    def generate(self):
        available = False
        while not available:
            try:
                if os.path.ismount(self.path):
                    available = True
            except:
                pass
            yield
            time.sleep(0.03)
        self.signal_emit('after')

class mount(Command):
    def execute(self):
        selected_files = self.fm.env.cwd.get_selection()

        if not selected_files:
            return

        space = ' '
        self.fm.execute_command("cdemu -b system unload 0")
        self.fm.execute_command("cdemu -b system load 0 " + \
                space.join([shell_escape(f.path) for f in selected_files]))

        mountpath = "/media/virtualrom/"

        def mount_finished(path):
            currenttab = self.fm.current_tab
            self.fm.tab_open(9, mountpath)
            self.fm.tab_open(currenttab)

        obj = MountLoader(mountpath)
        obj.signal_bind('after', mount_finished)
        self.fm.loader.add(obj)
```

### 在当前目录打开新标签

你可能已经注意到有两个快捷键能够以家目录为默认目录创建新的标签 (`gn` 和 `Ctrl+n`). 不妨重新绑定 `Ctrl+n`:

 `rc.conf` 
```
map <c-n>  eval fm.tab_new('%d')

```

### Shell tips

#### 目录同步

*ranger* 提供了一个 shell [function](/index.php/Bash#Functions "Bash") `/usr/share/doc/ranger/examples/bash_automatic_cd.sh`. 执行 `ranger-cd` 会自动切换到最后一次浏览的目录.

If you launch ranger from a graphical launcher (such as `$TERMCMD -e ranger`, where TERMCMD is an X terminal), you cannot use `ranger-cd`. Create an executable script:

 `ranger-launcher.sh` 
```
#!/bin/sh
export RANGERCD=true
$TERMCMD

```

and add at the *very end* of your shell configuration:

 `.*shell*rc` 
```
$RANGERCD && unset RANGERCD && ranger-cd

```

This will launch `ranger-cd` only if the `RANGERCD` variable is set. It is important to unset this variable again, otherwise launching a subshell from this terminal will automatically relaunch `ranger`.

#### Start a shell from ranger

With the previous method you can switch to a shell in last browsed path simply by leaving ranger. However you may not want to quit ranger for several reasons (numerous opened tabs, copy in progress, etc.). You can start a shell from ranger (`S` by default) without losing your ranger session. Unfortunately, the shell will not switch to the current folder automatically. Again, this can be solved with an executable script:

 `shellcd` 
```
#!/bin/sh
export AUTOCD="$(realpath "$1")"

$SHELL

```

and - as before - add this to at the very end of your shell configuration:

 `shellrc` 
```
cd "$AUTOCD"

```

Now you can change your shell binding for ranger:

 `rc.conf` 
```
map S shell shellcd %d

```

Alternatively, you can make use of your shell history file if it has any. For instance, you could do this for [zsh](/index.php/Zsh#Dirstack "Zsh"):

 `shellcd` 
```
## Prepend argument to zsh dirstack.
BUF="$(realpath "$1")
$(grep -v "$(realpath "$1")" "$ZDIRS")"
echo "$BUF" > "$ZDIRS"

zsh

```

Change ZDIRS for your dirstack.

#### 避免在 ranger 启动的 shell 内创建新的 ranger

Put this in your [shell's startup file](/index.php/Autostarting#Shells "Autostarting"):

```
rg() {
    if [ -z "$RANGER_LEVEL" ]
    then
        ranger
    else
        exit
    fi
}

```

Execute `rg` to start or restore ranger.

## Troubleshooting

### Artifacts in image preview

Borderless columns may cause stripes in image previews. [[1]](https://bbs.linuxdistrocommunity.com/showthread.php?tid=1051) In `~/.config/ranger/rc.conf` set:

```
set draw_borders true

```

## 参见

*   [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=93025)
*   [DotShare.it configurations](http://dotshare.it/category/fms/ranger/)
*   [GitHub](http://github.com/hut/ranger)
*   [Installing and using ranger](https://www.digitalocean.com/community/tutorials/installing-and-using-ranger-a-terminal-file-manager-on-a-ubuntu-vps)
*   [Mailing list](https://lists.nongnu.org/mailman/listinfo/ranger-users)
*   [Official website](http://nongnu.org/ranger)
*   [Ranger tutorial](http://bloerg.net/2012/10/17/ranger-file-manager.html)