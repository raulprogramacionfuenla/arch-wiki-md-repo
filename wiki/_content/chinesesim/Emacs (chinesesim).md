**翻译状态：** 本文是英文页面 [Emacs](/index.php/Emacs "Emacs") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-03-07，点击[这里](https://wiki.archlinux.org/index.php?title=Emacs&diff=0&oldid=229169)可以查看翻译后英文页面的改动。

[Emacs](https://en.wikipedia.org/wiki/Emacs "wikipedia:Emacs")是一个可扩展、可定制、自文档化的实时显示编辑器。Emacs的核心构建在[Emacs Lisp](https://en.wikipedia.org/wiki/Emacs_Lisp "wikipedia:Emacs Lisp")解释器之上，Emacs Lisp是大部分Emacs内建函数和拓展模块的实现语言。在图形界面系统下，Emacs使用GTK作为默认的X工具，在命令行界面下(CLI)，Emacs也可以工作良好。在文本编辑能力上，Emacs常被拿来和[vim](/index.php/Vim "Vim")比较。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行Emacs](#.E8.BF.90.E8.A1.8CEmacs)
    *   [2.1 没有颜色](#.E6.B2.A1.E6.9C.89.E9.A2.9C.E8.89.B2)
    *   [2.2 作为守护进程](#.E4.BD.9C.E4.B8.BA.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [2.3 作为systemd单元](#.E4.BD.9C.E4.B8.BAsystemd.E5.8D.95.E5.85.83)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
    *   [3.1 手册](#.E6.89.8B.E5.86.8C)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 TRAMP](#TRAMP)
    *   [4.2 使用Emacs作为git mergetool](#.E4.BD.BF.E7.94.A8Emacs.E4.BD.9C.E4.B8.BAgit_mergetool)
    *   [4.3 使用大写锁定作为控制键](#.E4.BD.BF.E7.94.A8.E5.A4.A7.E5.86.99.E9.94.81.E5.AE.9A.E4.BD.9C.E4.B8.BA.E6.8E.A7.E5.88.B6.E9.94.AE)
    *   [4.4 键盘宏和寄存器](#.E9.94.AE.E7.9B.98.E5.AE.8F.E5.92.8C.E5.AF.84.E5.AD.98.E5.99.A8)
    *   [4.5 正则表达式](#.E6.AD.A3.E5.88.99.E8.A1.A8.E8.BE.BE.E5.BC.8F)
*   [5 定制](#.E5.AE.9A.E5.88.B6)
    *   [5.1 多种配置](#.E5.A4.9A.E7.A7.8D.E9.85.8D.E7.BD.AE)
    *   [5.2 加载扩展程序](#.E5.8A.A0.E8.BD.BD.E6.89.A9.E5.B1.95.E7.A8.8B.E5.BA.8F)
    *   [5.3 Local and custom variables](#Local_and_custom_variables)
    *   [5.4 Custom colors and theme](#Custom_colors_and_theme)
    *   [5.5 SyncTeX support](#SyncTeX_support)
*   [6 Documentation](#Documentation)
    *   [6.1 Contextual help](#Contextual_help)
*   [7 拓展模块](#.E6.8B.93.E5.B1.95.E6.A8.A1.E5.9D.97)
*   [8 疑难杂症](#.E7.96.91.E9.9A.BE.E6.9D.82.E7.97.87)
    *   [8.1 彩色输出的问题](#.E5.BD.A9.E8.89.B2.E8.BE.93.E5.87.BA.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [8.2 菜单显示为空](#.E8.8F.9C.E5.8D.95.E6.98.BE.E7.A4.BA.E4.B8.BA.E7.A9.BA)
    *   [8.3 X 窗口下的字符显示问题](#X_.E7.AA.97.E5.8F.A3.E4.B8.8B.E7.9A.84.E5.AD.97.E7.AC.A6.E6.98.BE.E7.A4.BA.E9.97.AE.E9.A2.98)
    *   [8.4 启动速度慢](#.E5.90.AF.E5.8A.A8.E9.80.9F.E5.BA.A6.E6.85.A2)
        *   [8.4.1 错误的网络配置](#.E9.94.99.E8.AF.AF.E7.9A.84.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
        *   [8.4.2 初始化文件加载慢](#.E5.88.9D.E5.A7.8B.E5.8C.96.E6.96.87.E4.BB.B6.E5.8A.A0.E8.BD.BD.E6.85.A2)
    *   [8.5 不能打开配置文件: ...](#.E4.B8.8D.E8.83.BD.E6.89.93.E5.BC.80.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6:_...)
    *   [8.6 Dead-accent keys problem: '<dead-acute> is undefined'](#Dead-accent_keys_problem:_.27.3Cdead-acute.3E_is_undefined.27)
    *   [8.7 C-M-% and some other bindings do not work in emacs nox](#C-M-.25_and_some_other_bindings_do_not_work_in_emacs_nox)
    *   [8.8 Emacs client gets stuck when switching back to it](#Emacs_client_gets_stuck_when_switching_back_to_it)
    *   [8.9 Emacs-nox output gets messy](#Emacs-nox_output_gets_messy)
    *   [8.10 Shift + Arrow keys not working in emacs within tmux](#Shift_.2B_Arrow_keys_not_working_in_emacs_within_tmux)
*   [9 替代方案](#.E6.9B.BF.E4.BB.A3.E6.96.B9.E6.A1.88)
    *   [9.1 mg](#mg)
    *   [9.2 zile](#zile)
    *   [9.3 uemacs](#uemacs)
    *   [9.4 remacs](#remacs)
*   [10 资源](#.E8.B5.84.E6.BA.90)

## 安装

Emacs有众多发行版本（有时候称作*emacsen*）。 最常见的莫过于 [GNU Emacs](http://www.gnu.org/software/emacs/)。

在 [official repositories](/index.php/Official_repositories "Official repositories") 中可以[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [emacs](https://www.archlinux.org/packages/?name=emacs) 。如果你经常使用命令行，你可能更喜欢没有GTK+支持的 [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox)（也没有声音或其它花哨的东西）。值得注意的是，文字模式的Emacs有一些缺点：它支持的颜色和字体设置功能都要更少（实时改变字体大小，单文档多字体，等等）。而且emacs-nox存在一些高级功能上的缺陷，比如Speedbar和GUD（调试环境），处理复杂的外观（face，文本在Emacs中呈现的样子）的时候速度也会变慢。

如果你想体验Emacs的所有扩展功能而不用安装大量依赖项的话，可以使用PKGBUILD来按你的需求定制Emacs。不使用 `gtk3`， 可以让Emacs避免使用gconf。图像和声音的支持也可以禁用。在Emacs源目录下运行 `./configure --help` 可以列出所有可用选项。

 `PKGBUILD` 
```
# ...
  ./configure --prefix=/usr --sysconfdir=/etc --libexecdir=/usr/lib \
    --localstatedir=/var --with-x-toolkit=gtk2 --with-xft \
    --without-gconf --without-sound
# ...

```

## 运行Emacs

启动Emacs之前，你应该知道怎样关掉它（特别是你在终端里运行时）：使用 `Ctrl+x``Ctrl+c` 按键顺序。

启动Emacs：

```
$ emacs

```

或者以文字模式启动：

```
$ emacs -nw

```

又或者，快速启动（不解析.emacs文件）并以文字模式启动：

```
$ emacs -Q -nw

```

如果你安装的是nox版本，'emacs' 和 'emacs -nw' 效果是一样的。

可以提供文件名直接打开文件：

```
$ emacs filename.txt

```

### 没有颜色

默认情况下，Emacs以颜色主题开始，显示超链接为深蓝色。

以文本模式，不使用任何颜色主题启动Emacs：

```
$ emacs -nw --color=no

```

这将导致所有的文本采用终端的字体颜色 –– 通常是黑色背景之上的白色文本，或白色背景上的黑色文本。

### 作为守护进程

如过不想让Emacs每次启动都读取配置文件的话，可以以守护进程运行Emacs：

```
$ emacs --daemon

```

连接到守护进程：

```
$ emacsclient -nc

```

这个命令会创建一个新的frame `-c`（如果你更喜欢文字模式，使用 `-t` ）并且不会独占终端 `-n` （`--no-wait`）。 有的程序，如Mutt和Git，（为了提交信息）会等待编辑器完成编辑，所以不能使用 `-n` 参数。 如果你的默认编辑器是默认使用`-n`，你需要为那些程序指定一个替代编辑器（比如 `emacsclient -a "" -t`）。

### 作为systemd单元

旧的systemd单元方法有一些需要注意的地方。 它给了一个限制shell调用的有限的shell环境，所以我们需要使用一个user单元，它往往比调用*emacs --daemon*好得多。 为Emacs创建一个systemd单元：

**注意:** 这样一个单元文件将会包含在Emacs 26.1中， 参见 [emacs bug 16507](https://debbugs.gnu.org/cgi/bugreport.cgi?bug=16507).
 `~/.config/systemd/user/emacs.service` 
```
[Unit]
Description=Emacs: the extensible, self-documenting text editor

[Service]
Type=forking
ExecStart=/usr/bin/emacs --daemon
ExecStop=/usr/bin/emacsclient --eval "(kill-emacs)"
Restart=always

[Install]
WantedBy=default.target

```

需要启动并启用该单元，以便其在每次电脑启动时启动（请注意 - 请勿“以root运行” - 我们希望它以user，而不是根root user运行）：

```
$ systemctl --user enable --now emacs

```

请注意，systemd user单元不会从登录shell（例如`〜/.bash_profile`）继承环境变量，因此你可能需要在`〜/.pam_environment`中设置变量。有关更多信息，请参见[Systemd/User](/index.php/Systemd/User "Systemd/User")。

如启动emacs作为守护程序，你可能会想把`VISUAL`和`EDITOR`环境变量设置为`emacsclient`，以便启动编辑器的程序使用emacsclient而不是一个完整的编辑器。使用外部编辑器的程序，包括电子邮件程序（用于编辑消息），Git（用于编辑提交消息）和less（用于编辑显示文件的`v`命令）。 不要对emacsclient使用`-n`（`--nowait`）选项，因为程序通常要求在编辑器退出时编辑完成。

建议将Emacs的任何GUI开始菜单条目（或等效条目）更改为指向emacsclient而不是emacs，以便使用emacs守护程序而不是启动新的emacs进程。

## 使用

尽管Emacs很复杂，但了解定制和可扩展性带来的好处并不需要很长时间。此外，已有的各种扩展允许将其转变为针对几乎任何形式的强大文本编辑环境。

Emacs有一个很好的内置教程，可以通过点击启动画面上的第一个链接进行访问; 通过从菜单中选择*帮助-> Emacs 教程*或按'F1'然后按't'。

Emacs设计为自文档化。 因此，大量的信息可用于确定特定命令的名称或其按键绑定。 使用**C-h C-h**查看所有当前环境绑定。

Emacs还包含一组参考卡，对初学者和专家都很有用，请参阅`/usr/share/emacs/<version>/etc/refcards/`（用您的emacs版本替换<version>）。

Emacs为用户提供了大量的功能，其中包括：键盘宏，矩形区域，空白清理，书签，桌面会话，各种shell，拼写检查，表格，语义分析...

### 手册

如果你真的想要掌握Emacs，最推荐的文档来源仍然是官方手册：

*   Emacs：完整的Emacs用户手册。
*   Emacs 常见问题。
*   Emacs Lisp简介：如果你以前从未使用任何编程语言。
*   Elisp：如果你已经熟悉一门编程语言。

通过内置'info'阅读器，你可以从GNU.org将其作为PDF查看或直接从Emacs本身访问：C-h i。按m选择相应章节。

有些用户更喜欢使用'info'来阅读章节，因为它具有方便的快捷方式，其段落会适应窗口宽度，字体会适应当前屏幕分辨率。有些人觉得这样不那么刺激眼睛。最后，你可以轻松地将章节中的内容复制到任何Emacs缓冲区，甚至可以直接从示例中执行Lisp代码片段。

你可能想要阅读信息手册以了解更多信息：C-h i m info <RET>。 按 ？ 在info模式下可以快速查看快捷键列表。

## 提示和技巧

### TRAMP

TRAMP (Transparent Remote Access, Multiple Protocols) ，顾名思义，是一个可以通过很多协议透明访问远程文件的一个扩展。当提示输入文件名时，输入特定的格式就可以使用TRAMPP。比如：

在打开`/etc/hosts`文件之前提示输入root的密码以获取root权限：

```
C-x C-f /su::/etc/hosts

```

要通过SSH使用'you'用户名登录'remotehost'主机打开文件`~/example.txt`：

```
C-x C-f /ssh:you@remotehost:~/example.txt

```

TRAMP的路径一般是这种格式'/[protocol]:[[user@]host]:<file>'。

作为用户'you'连接至'myhost'并以sudo编辑`／etc/hosts`：

```
/ssh:you@remotehost|sudo:remotehost:/etc/hosts

```

TRAMP支持的不只上面的两个简单例子。请查看Emacs里面的TRAMPP info手册了解更多的信息。

### 使用Emacs作为git mergetool

默认情况下，Git支持使用Emacs的Emerge模式作为合并工具。但是你可能更喜欢Ediff模式。不幸的是，由于技术原因，这种模式不被git支持。通过在emacs调用时对一些elisp代码赋值，仍然有一种方法可以使用Ediff。

 `.gitconfig` 
```
[mergetool.ediff]
    cmd = emacs --eval \" (progn (defun ediff-write-merge-buffer () (let ((file ediff-merge-store-file)) (set-buffer ediff-buffer-C) (write-region (point-min) (point-max) file) (message \\\"Merge buffer saved in: %s\\\" file) (set-buffer-modified-p nil) (sit-for 1))) (setq ediff-quit-hook 'kill-emacs ediff-quit-merge-hook 'ediff-write-merge-buffer) (ediff-merge-files-with-ancestor \\\"$LOCAL\\\" \\\"$REMOTE\\\" \\\"$BASE\\\" nil \\\"$MERGED\\\"))\" 

[merge]
	tool = ediff

```

请注意，该命令必须在同一行上。在上面的例子中，我们启动了一个Emacs的新实例。你可能想要使用emacsclient更快地启动; 不建议这样做，因为Ediff调用不是很干净：它可能会打断当前的Emacs会话。

如果你想要一个即时启动，可以使用-q参数。如果想在保留至少一部分配置的情况下快速启动Emacs，则可以这样使用Emacs：

```
emacs -q -l ~/.emacs-light

```

light配置文件仅加载Ediff所需的内容。

关于这个技巧的细节和Ediff问题，参见[kerneltrap.org](http://kerneltrap.org/mailarchive/git/2007/7/1/250424)和 [stackoverflow](http://stackoverflow.com/questions/1817370/using-ediff-as-git-mergetool)。

### 使用大写锁定作为控制键

一些用户喜欢这种个修改，以避免所谓的'emacs pinky'。如果你想在X上试用它，运行

```
$ setxkbmap -option 'ctrl:nocaps'

```

或者，**交换**键值，运行

```
$ setxkbmap -option 'ctrl:swapcaps'

```

要永久更改它，请考虑将其添加到.xinitrc文件中。

如果要将一个区域变为大写，只需使用默认的C-x C-u键绑定，调用upcase-region函数。

参见[[1]](http://ergoemacs.org/emacs/swap_CapsLock_Ctrl.html)了解另一种方法。

如果缺少Caps Lock功能，请同时将其映射为“Shift”。

```
$ setxkbmap -option "shift:both_capslock"

```

某些桌面环境包含图形工具以简化键盘重新映射。 例如，在[Plasma 5](/index.php/Plasma "Plasma")中打开系统设置并点击输入设备。选择键盘，然后在高级选项卡中会看到Caps Lock设置，可以在其中选择Caps Lock也是一个Ctrl。

### 键盘宏和寄存器

这一部分会提供一个实用的指南来使用一些更强大的编辑特性。也就是“键盘宏”和“寄存器”。

我们的目标是产生一个字符列表和它们在这个列表中对应的位置。虽然这可以通过手工格式化来完成，但是这样会很慢而且容易出错。如果我们采用一些Emacs更高级的编辑功能却可以起到四两拨千斤的功效。在介绍这个方法之前，需要先了解一些技术背后的细节。

要介绍的第一个特性就是*寄存器*。寄存器的功能是用来保存和获取各种各样的数据。每个寄存器用一个字母来命名，这个字母就是用来调用这个寄存器的。

另一个要介绍的就是*键盘宏*。一个键盘宏存储了一个命令序列以便以后可以重复使用。下面就一步一步地讲解这个方法。

首先我们从一个包含如下字符的缓冲区开始：

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

通过`number-to-register' 命令 (**C-x r n**)我们来准备一个寄存器，把数字'0'存储在寄存器'k'中：

```
C-x r n k

```

当光标在缓冲区开头的时候，开始录制键盘宏 (**C-x (**) 然后开始对字符串进行格式化：

```
C-x ( C-f M-4 .

```

插入 (**C-x r i**) 然后将寄存器'k'加1 (**C-x r +**) 。开头的 (**C-u**) 命令是用来在插入文字之后让光标移到插入的文字后面：

```
C-u C-x r i k C-x r + k

```

最后我们来插入一个回车来结束格式化。Emacs可以重复以上过程，从我们定义键盘宏的位置开始，直到最后一个字符。**C-x e**命令停止宏的录制并开始执行这段宏。开头的 **M-0** 命令是用来让宏在出错的时候停下来，这样在它走到这行的结尾就会停下来。

```
<RET> M-0 C-x e

```

下面是结果：

```
 A....0
 B....1
 C....2
 [...]
 x....49
 y....50
 z....51

```

### 正则表达式

From the Emacs Manual: "A regular expression, or *regexp* for short, is a pattern that denotes a (possibly infinite) set of strings." This section will not go into any detail regarding regular expressions themselves (as there is simply too much to cover). It will however provide a quick demonstration of their power. See [Regular Expressions](http://www.gnu.org/software/emacs/manual/html_node/elisp/Regular-Expressions.html#Regular-Expressions) section in the Emacs Manual for further reading.

Given the same scenario presented above: A list of characters which are to be formatted to represent their respective position in the list. (see [Keyboard macros and registers](/index.php/Emacs#Keyboard_macros_and_registers "Emacs")). Again, starting with a buffer containing.

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

At the beginning of the buffer, use **C-M-%** (if the key-sequence is difficult to perform, it may be more comfortable to use **M-x query-replace-regexp**). At the prompt:

```
\(.\)

```

which simply matches one character. Then, when prompted for the replacement:

```
\1....\#^J

```

**Note:** '^J' represents where a newline should be placed, it should not be entered into the prompt. The newline must instead be inserted literally using **C-q C-j**.

The replacement expression reads: "Insert the matched text between the first set of parentheses (in this case, a single character), followed by 4 periods then insert an automatically incremented number followed by a newline.

Finally, press **!** to apply this across the entire buffer. All of the formatting that was performed in the previous section was performed with a single regexp replacement.

## 定制

Emacs能通过~/.emacs或者**M-x customize**来定制。本段落将着眼于手动定制 ~/.emacs，并且提供了一些常用配置的样例。配置命令提供了一个适应的途径，通过它你能够渐渐熟悉Emacs。

这里的所有例子都能在Emacs中奏效。比如，在Emacs中计算表达式： **C-M-x** 同时指到任何需要求值的地方。

或者

**C-x C-e** 指到最后的“）”。

用'y'和'n'来代替频繁地输入'yes’和'no‘是一个好的方法：

```
(defalias 'yes-or-no-p 'y-or-n-p)

```

取消光标闪烁：

```
(blink-cursor-mode -1)

```

类似地，开启上一节提到的列号模式：

```
(column-number-mode 1)

```

它们两者之间的相似不是偶然：光标闪烁模式和列号模式都是'副参模式'，按照规则，'副参模式’能通过正负值来设置。如果参数省略，'副参模式'将被开/关。

这里有其他一些'副参模式'的例子，下面的参数将会关闭滚动栏、菜单栏、工具栏。

```
(scroll-bar-mode -1)
(menu-bar-mode -1)
(tool-bar-mode -1)

```

变量'auto-mode-alist'修改之后能够改变默认的“主参模式”。下面的例子把'.tut'和'.req'修改成了'.text-mode'。

```
(setq auto-mode-alist
  (append
    '(("\\.tut$" . text-mode)
      ("\\.req$" . text-mode))
    auto-mode-alist))

```

Settings can also be applied on a per-mode basis. A common method for this is to add a function to a *hook*. For example, to force indentation to use spaces instead of tabs, but only in text-mode:

```
(add-hook 'text-mode-hook (lambda () (setq indent-tabs-mode nil)))

```

Similarly, to only use spaces for indentation everywhere:

```
(setq-default indent-tabs-mode nil)

```

Keybindings can be adjusted in two ways. The first of which is 'define-key'. 'define-key' creates a keybinding for a command but only in one mode. The example below will make **F8** delete any whitespace from the end of each line of a 'text-mode' buffer:

```
(define-key text-mode-map (kbd "<f8>") 'delete-trailing-whitespace)

```

The other method is 'global-set-key'. This is used to bind a key to a command everywhere. To bind 'query-replace-regexp' (**C-M-%**) to '<f7>'.

```
(global-set-key (kbd "<f7>") 'query-replace-regexp)

```

Binding a command to an alternate key does not replace any existing bindings. Which is to say, 'query-replace-regexp' would be bound to both **F7** and **C-M-%** after the above example.

Almost anything within Emacs can be configured. Browsing through the [Emacs Wiki](http://emacswiki.org/) should give a solid place to start.

### 多种配置

你可以使用少量配置然后告诉Emacs来加载其他配置。

例如，我们来定义两个配置文件。

 `.emacs` 
```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/plugins" nil t)
(load "~/.emacs.d/theme" nil t)

```

这是我们在后台载入的完整配置。但是plugins文件太大导致载入太慢，如果我们要打开一个新的Emacs窗口，可能就不会使用plugins配置，每次加载它实在是太笨重了。

 `.emacs-light` 
```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/theme" nil t)

```

现在我们这样来加载Emacs：

```
emacs -q -l ~/.emacs-light

```

你可以为这个命令创建一个别名。

### 加载扩展程序

你能用require来加载扩展程序，例如这样：

```
(require 'mediawiki)

```

如果你试着在一个买有安装mediawiki的机器上使用相同的配置，Emacs会提示错误。并且，所有制定的扩展代码都会失效。

一个小的技巧是测试require的返回值。

```
(if (require 'mediawiki nil t)
    (progn
      (setq mediawiki-site-alist '(
             ("ArchLinux" "[https://wiki.archlinux.org/](https://wiki.archlinux.org/)" "UserName" "" "Main Page")
             )
           )
      (setq mediawiki-mode-hook
            (lambda ()
              (visual-line-mode 1)
              (turn-off-auto-fill)
              ))
 ))

```

### Local and custom variables

You can define variables in your configuration file that can be later one modified locally for a file.

```
(defcustom my-compiler "gcc" "Some documentation")

```

Now in any file you can define local variables in two ways:

*   On the very first line, write

```
// -*- my-compiler:g++; mode:c++ -*-

```

*   If you cannot (or do not want to) write this on the first line, you can put it at the end:

```
// Local Variables:
// my-compiler: g++
// mode: c++
// End:

```

Note that the beginning characters need to be comments for the current language, that's why here we used two backslashes for C++. For Elisp you would use

```
;; -*- mode:emacs-lisp -*-

```

There is two functions that may help you in defining the variables: *add-file-local-variable* and *add-file-local-variable-prop-line*.

Finally, custom variable are considered insecure by default. If you try to open a file that contains local variable redefining insecure custom variables, Emacs will ask you for confirmation.

If you know what you are doing, you can declare the variable as secure, thus removing the Emacs prompt for confirmation. You need to specify a predicate that any new value has to verify so that it can be considered safe.

```
(defcustom my-compiler "gcc" "Some documentation" :safe 'stringp)

```

In the previous example, if you attempt to set anything else than a string, Emacs will consider it insecure.

### Custom colors and theme

Colors can be easily customized using the *face* facility.

```
(set-face-background  'region                 "color-17")
(set-face-foreground  'region                 "white")
(set-face-bold-p      'font-lock-builtin-face t ) 

```

You can have let Emacs tell you the name of the face where the point is. Use the *customize-face* function for that. The facility will show you how to set colors, bold, underline, etc.

Emacs in console can handle 256 colors, but you will have to use an appropriate terminal for that. For instance URxvt has support for 256 colors. You can use the *list-colors-display* for a comprehensive list of supported colors. This is highly terminal-dependent.

### SyncTeX support

Emacs is definitely one of the most powerful LaTeX editor. This is mostly due to the fact you can adapt or create a LaTeX mode to fit your needs best.

Still, there might be some challenges, like SyncTeX support. First you need to make sure your TeX distribution has it. If you installed TeX Live manually, you may need to install the *synctex* package.

```
# umask 022 && tlmgr install synctex

```

SyncTeX support is viewer-dependent. Here we will use Zathura as an example, so the code needs to be adapted if you want to use another PDF viewer.

```
(defcustom tex-my-viewer "zathura --fork -s -x \"emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"'\"'\"%{input}\"'\"'\")) (goto-line %{line}))'\"" 
  "PDF Viewer for TeX documents. You may want to fork the viewer
so that it detects when the same document is launched twice, and
persists when Emacs gets closed.

Simple command:

  zathura --fork

We can use

  emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"%{input}\")) (goto-line %{line}))'

to reverse-search a pdf using SyncTeX. Note that the quotes and double-quotes matter and must be escaped appropriately."
:safe 'stringp)

```

Here we define our custom variable. If you are using AucTeX or Emacs default LaTeX-mode, you will have to set the viewer accordingly.

Now open a LaTeX source file with Emacs, compile the document, and launch the viewer. Zathura will spawn. If you press `Ctrl+Left click` Emacs should place the point at the corresponding position.

## Documentation

You may find yourself overwhelmed by the amount of Emacs features. You may find it difficult to know how to use Emacs Lisp to customize your favorite modes, or even to create your own modes / packages. Thankfully Emacs takes a strong point to auto-documenting everything: its internals, current configuration, bindings, etc. Almost everything is documented.

### Contextual help

Emacs is self-documenting by design. As such, a great deal of information is available to determine the name of a specific command or its keybinding, for example. The following is a listing of some of the most helpful of these:

```
**C-h a**        Find a command matching a description.

```

```
**C-h b**        List all active keybindings.

```

```
**C-h f**        Describe the given function.

```

```
**C-h k**        Find which command a key is bound to.

```

```
**C-h m**        Display information regarding the currently active modes.

```

```
**C-h t**        Start the Emacs tutorial.

```

```
**C-h v**        Describe the given variable.

```

```
**C-h w**        Find which key(s) a command is bound to.

```

## 拓展模块

虽然Emacs包含了成百上千种模式(mode)，库和其它扩展，还有更多的扩展来增强Emacs。大多数扩展会详细说明安装它的时候要对~/.emacs作什么改动。这些说明一般会在一个elisp源文件开头的注释中，或者在一个README中（如果这个扩展包含了多个源文件）。

在'community'仓库中有很多流行的扩展，更多的扩展还放在了[AUR](/index.php/AUR "AUR")。这些软件包的名字有一个'emacs-'前缀（比如emacs-lua-mode）。在很多情况下，在安装的过程会显示怎样修改~/.emacs以安装该扩展到Emacs中。

想知道怎样激活一个不在上面提到的地方的扩展，查看[Emacs Wiki](http://emacswiki.org/)中的相应页面，一般会提供一个配置的例子。Emacs Wiki也是一个寻找扩展的优秀资源。

你也可以使用[Emacs Lisp Package Archive (ELPA)](http://tromey.com/elpa/) 来自动安装软件包。打开那个网站看说明。ELPA已经包括在了Emacs24中;它已经作为Emacs生态系统中的一部分了。

## 疑难杂症

### 彩色输出的问题

Emacs默认使用原生的转义串来输出颜色。也就是说，它会在要显示颜色的地方显示奇怪的字符。

在`~/.emacs`中加入下面的代码解决这个问题：

```
(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on)

```

### 菜单显示为空

一些菜单显示为空，这是GNU Emacs 23.1的一个bug（使用GTK toolkit的时候）。好像在Emacs的CVS trunk中已经修复了。对应的[Debian bug report](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=550541) 有一个应对措施。

### X 窗口下的字符显示问题

当你使用X窗口启动emacs时，如果发现主窗口中的所有字符都是黑框白块（就像你没有安装正确的字体看到的字符一样），那么你需要安装 [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) 或者 [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) 并且重启X窗口。

### 启动速度慢

启动速度慢经常是由下面两种情况引起的。

要确定是哪种情况，这样打开Emacs：

```
$ emacs -q

```

如果Emacs还是启动很慢，则是[错误的网络配置](/index.php/Emacs#Incorrect_network_configuration "Emacs")。如果不是，则可以确定是[.emacs的问题](/index.php/Emacs#Init_file_loads_slowly "Emacs")。

#### 错误的网络配置

当启动Emacs的时候，一些错误，特别是在/etc/hosts中的，经常会导致5秒以上的延迟。在网络配置指南中查看'[set the hostname](/index.php/Configuring_network#Set_the_hostname "Configuring network")' 了解更多内容。

#### 初始化文件加载慢

一个很简单的方法查找原因是注释掉（比如在行开头使用';'）你的~/.emacs（或者~/.emacs.d/init.el）里面可疑的地方，然后再启动Emacs，看速度是否有改善。记住，使用"require"和"load"会减慢启动速度，特别是用在很大的插件上。一般来说，他们应该用在当目标是Emacs启动的时候就需要或者提供仅仅是一个扩展的"autoloads"。否则，直接使用'autoload'函数。比如，不是这样：

```
(require 'anything)

```

你应该这样:

```
(autoload 'anything "anything" "Select anything" t)

```

### 不能打开配置文件: ...

这个错误最常见的原因是'load-path'变量没有包含某些插件的目录。要解决这个问题，在加载插件前，把需要加载的插件目录加入到要搜索的list中：

```
 (add-to-list 'load-path "/path/to/directory/")

```

当尝试使用一个插件的包，而这个包又被Emacs加上了非'/usr'的前缀时，load-path需要更新。把下面的代码放到使用这个插件的包的代码的前面：

```
 (add-to-list 'load-path "/usr/share/emacs/site-lisp")

```

如果手动编译Emacs，记住默认的前缀是'/usr/local'。

### Dead-accent keys problem: '<dead-acute> is undefined'

Searching about this bug on Google, we find this link: [http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html)

Explaining the problem: in recent versions of b72

```
Emacs, the normal way to use accent keys doesn't work as expected. Trying to accent a word like 'fiancé' will produce the message above.

```

A way to solve it is just put the line above on your startup file, `~/.emacs`:

```
  (require 'iso-transl)

```

And no, it isn't a bug, but a feature of new Emacs versions. Reading the subsequent messages about it on the mail list, we found it ([http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html)):

	*It seems that nothing is loaded automatically because there is a choice betwee iso-transl and iso-acc. Both seem to provide an input method with C-x 8 or Alt-<accent> prefix, but what you and I are doing is just pressing a dead key (^, ´, `, ~, ¨) for the accent and then another key to "compose" the accented character. And there is no Alt key used in this! And according to documentation it seems be appropriate for 8-bit encodings, so it should be pretty useless in UTF-8\. I reported this bug when it was introduced, but the bug seems to be*

a3b

```
classified as a feature ... Maybe it's just because the file is auto-loaded though pretty useless. 

```

### C-M-% and some other bindings do not work in emacs nox

This is because terminals are more limited than Xorg. Some terminals may handle more bindings than other, though. Two solutions:

*   either use the graphical version,
*   or change the binding to a supported one.

Example:

 `.emacs` 
```
(global-set-key (kbd "C-M-y") 'query-replace-regexp)

```

### Emacs client gets stuck when switching back to it

If you are using Emacs daemon, then you should know that input is blocking. If one Emacs instance is in the minibuffer (after an **M-x** for instance), then all other instance will wait for it to finish. Press **C-g** to cancel any input to make sure this Emacs session is not blocking.

### Emacs-nox output gets messy

When working in a terminal, the color, indentation, or anything related to the output might become crazy. This is (probably?) because Emacs was sent a special character at some point which may conflict with the current terminal. There is not much to be done but restarting emacs. If someone has a workaround or a more detailed explanation on the issue, feel free to contribute.

Graphical Emacs does not suffer from this issue.

### Shift + Arrow keys not working in emacs within tmux

First you must enable xterm-keys in your [tmux](/index.php/Tmux "Tmux") config.

 `.tmux.conf` 
```
setw -g xterm-keys on

```

But, this will break other key combinations. To fix them, put the following in your emacs config.

 `.emacs` 
```
;; handle tmux's xterm-keys
;; put the following line in your ~/.tmux.conf:
;;   setw -g xterm-keys on
(if (getenv "TMUX")
    (progn
      (let ((x 2) (tkey ""))
	(while (<= x 8)
	  ;; shift
	  (if (= x 2)
	      (setq tkey "S-"))
	  ;; alt
	  (if (= x 3)
	      (setq tkey "M-"))
	  ;; alt + shift
	  (if (= x 4)
	      (setq tkey "M-S-"))
	  ;; ctrl
	  (if (= x 5)
	      (setq tkey "C-"))
	  ;; ctrl + shift
	  (if (= x 6)
	      (setq tkey "C-S-"))
	  ;; ctrl + alt
	  (if (= x 7)
	      (setq tkey "C-M-"))
	  ;; ctrl + alt + shift
	  (if (= x 8)
	      (setq tkey "C-M-S-"))

	  ;; arrows
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d A" x)) (kbd (format "%s<up>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d B" x)) (kbd (format "%s<down>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d C" x)) (kbd (format "%s<right>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d D" x)) (kbd (format "%s<left>" tkey)))
	  ;; home
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d H" x)) (kbd (format "%s<home>" tkey)))
	  ;; end
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d F" x)) (kbd (format "%s<end>" tkey)))
	  ;; page up
	  (define-key key-translation-map (kbd (format "M-[ 5 ; %d ~" x)) (kbd (format "%s<prior>" tkey)))
	  ;; page down
	  (define-key key-translation-map (kbd (format "M-[ 6 ; %d ~" x)) (kbd (format "%s<next>" tkey)))
	  ;; insert
	  (define-key key-translation-map (kbd (format "M-[ 2 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; delete
	  (define-key key-translation-map (kbd (format "M-[ 3 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; f1
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d P" x)) (kbd (format "%s<f1>" tkey)))
	  ;; f2
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d Q" x)) (kbd (format "%s<f2>" tkey)))
	  ;; f3
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d R" x)) (kbd (format "%s<f3>" tkey)))
	  ;; f4
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d S" x)) (kbd (format "%s<f4>" tkey)))
	  ;; f5
	  (define-key key-translation-map (kbd (format "M-[ 15 ; %d ~" x)) (kbd (format "%s<f5>" tkey)))
	  ;; f6
	  (define-key key-translation-map (kbd (format "M-[ 17 ; %d ~" x)) (kbd (format "%s<f6>" tkey)))
	  ;; f7
	  (define-key key-translation-map (kbd (format "M-[ 18 ; %d ~" x)) (kbd (format "%s<f7>" tkey)))
	  ;; f8
	  (define-key key-translation-map (kbd (format "M-[ 19 ; %d ~" x)) (kbd (format "%s<f8>" tkey)))
	  ;; f9
	  (define-key key-translation-map (kbd (format "M-[ 20 ; %d ~" x)) (kbd (format "%s<f9>" tkey)))
	  ;; f10
	  (define-key key-translation-map (kbd (format "M-[ 21 ; %d ~" x)) (kbd (format "%s<f10>" tkey)))
	  ;; f11
	  (define-key key-translation-map (kbd (format "M-[ 23 ; %d ~" x)) (kbd (format "%s<f11>" tkey)))
	  ;; f12
	  (define-key key-translation-map (kbd (format "M-[ 24 ; %d ~" x)) (kbd (format "%s<f12>" tkey)))
	  ;; f13
	  (define-key key-translation-map (kbd (format "M-[ 25 ; %d ~" x)) (kbd (format "%s<f13>" tkey)))
	  ;; f14
	  (define-key key-translation-map (kbd (format "M-[ 26 ; %d ~" x)) (kbd (format "%s<f14>" tkey)))
	  ;; f15
	  (define-key key-translation-map (kbd (format "M-[ 28 ; %d ~" x)) (kbd (format "%s<f15>" tkey)))
	  ;; f16
	  (define-key key-translation-map (kbd (format "M-[ 29 ; %d ~" x)) (kbd (format "%s<f16>" tkey)))
	  ;; f17
	  (define-key key-translation-map (kbd (format "M-[ 31 ; %d ~" x)) (kbd (format "%s<f17>" tkey)))
	  ;; f18
	  (define-key key-translation-map (kbd (format "M-[ 32 ; %d ~" x)) (kbd (format "%s<f18>" tkey)))
	  ;; f19
	  (define-key key-translation-map (kbd (format "M-[ 33 ; %d ~" x)) (kbd (format "%s<f19>" tkey)))
	  ;; f20
	  (define-key key-translation-map (kbd (format "M-[ 34 ; %d ~" x)) (kbd (format "%s<f20>" tkey)))

	  (setq x (+ x 1))
	  ))
      )
  )

```

## 替代方案

有很多Emacs的实现。GNU/Emacs 可能是最受欢迎的了。
更轻量的兼容性较好的Emacs可以在Arch仓库或在[AUR](https://aur.archlinux.org/)中找到。

### mg

**mg**（原来叫MicroGnuEmacs)，是用C语言实现的轻量级Emacs。

[mg](https://www.archlinux.org/packages/?name=mg) 在 [official repositories](/index.php/Official_repositories "Official repositories") 中，也可以从上游下载源码[page](http://homepage.boetes.org/software/mg/)。注意，**mg** 没有UTF-8支持。

### zile

引用官方网站[page](https://www.gnu.org/software/zile/)的描述，"GNU Zile is a lightweight Emacs clone. Zile is short for Zile Is Lossy Emacs. Zile has been written to be as similar as possible to Emacs; every Emacs user should feel at home."，意思是'GNU Zile'是一个轻量级的Emacs的克隆。Zile是'Zile Is Lossy Emacs'的缩写。 Zile的实现与Emacs如此相似以至于每个Emacs用户使用Zile一定会有一种宾至如归的感觉。

[zile](https://www.archlinux.org/packages/?name=zile) 可以在官方仓库中找到。

最新的tarball可以在GNU的官方源[mirrors](http://ftp.sh.cvut.cz/MIRRORS/gnu/pub/gnu/zile/)中找到。

### uemacs

**uemacs** 是由Linus Torvalds定制的微型Emacs版本。在 [AUR](/index.php/AUR "AUR") 中名为[uemacs-git](https://aur.archlinux.org/packages/uemacs-git/)。

### remacs

**remacs** 是一个用Rust写成的社区驱动的Emacs移植版。在 [AUR](/index.php/AUR "AUR") 中名为 [remacs-git](https://aur.archlinux.org/packages/remacs-git/)。

## 资源

*   [GNU Emacs home page](http://www.gnu.org/software/emacs/)
*   [GNU Emacs manual](http://www.gnu.org/software/emacs/manual/emacs.html)
*   [Emacs Wiki](http://www.emacswiki.org/cgi-bin/wiki/)
*   [WikEmacs - a more readable, but less complete Emacs wiki](http://wikemacs.org)
*   [Useful introduction to Emacs and its shortcuts](http://www2.lib.uchicago.edu/keith/tcl-course/emacs-tutorial.html)
*   [The Church of Emacs (via Google drive)](https://d0edfcdc0ccc1cd13cdab5eb986fb92e8660dbef.googledrive.com/host/0B6LMD0u8OhYYZEotN2QyR1hwR1k/)
*   [Official reference card](http://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf)
*   [EXWM](/index.php/EXWM "EXWM"), the Emacs X Window Manager