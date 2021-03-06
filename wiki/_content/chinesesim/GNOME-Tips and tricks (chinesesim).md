See [GNOME](/index.php/GNOME "GNOME") for the main article.

其他GNOME系统设置和提示。

## Contents

*   [1 键盘](#.E9.94.AE.E7.9B.98)
    *   [1.1 登陆打开NumLock键](#.E7.99.BB.E9.99.86.E6.89.93.E5.BC.80NumLock.E9.94.AE)
    *   [1.2 热键选择](#.E7.83.AD.E9.94.AE.E9.80.89.E6.8B.A9)
    *   [1.3 打开键盘开关命令](#.E6.89.93.E5.BC.80.E9.94.AE.E7.9B.98.E5.BC.80.E5.85.B3.E5.91.BD.E4.BB.A4)
    *   [1.4 XkbOptions键盘选项](#XkbOptions.E9.94.AE.E7.9B.98.E9.80.89.E9.A1.B9)
    *   [1.5 De-bind Windows key](#De-bind_Windows_key)
*   [2 磁盘](#.E7.A3.81.E7.9B.98)
*   [3 从菜单隐藏的应用程序](#.E4.BB.8E.E8.8F.9C.E5.8D.95.E9.9A.90.E8.97.8F.E7.9A.84.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [4 截屏记录](#.E6.88.AA.E5.B1.8F.E8.AE.B0.E5.BD.95)
*   [5 截图](#.E6.88.AA.E5.9B.BE)
*   [6 注销延迟](#.E6.B3.A8.E9.94.80.E5.BB.B6.E8.BF.9F)
*   [7 禁用动画](#.E7.A6.81.E7.94.A8.E5.8A.A8.E7.94.BB)
*   [8 Retina (HiDPI) display support](#Retina_.28HiDPI.29_display_support)
*   [9 密码和密钥 (PGP Keys)](#.E5.AF.86.E7.A0.81.E5.92.8C.E5.AF.86.E9.92.A5_.28PGP_Keys.29)
*   [10 终端](#.E7.BB.88.E7.AB.AF)
    *   [10.1 更改默认的终端大小](#.E6.9B.B4.E6.94.B9.E9.BB.98.E8.AE.A4.E7.9A.84.E7.BB.88.E7.AB.AF.E5.A4.A7.E5.B0.8F)
    *   [10.2 新终端采用当前目录](#.E6.96.B0.E7.BB.88.E7.AB.AF.E9.87.87.E7.94.A8.E5.BD.93.E5.89.8D.E7.9B.AE.E5.BD.95)
    *   [10.3 Pad the terminal](#Pad_the_terminal)
    *   [10.4 禁用光标闪烁](#.E7.A6.81.E7.94.A8.E5.85.89.E6.A0.87.E9.97.AA.E7.83.81)
    *   [10.5 关闭终端时，禁用确认窗口](#.E5.85.B3.E9.97.AD.E7.BB.88.E7.AB.AF.E6.97.B6.EF.BC.8C.E7.A6.81.E7.94.A8.E7.A1.AE.E8.AE.A4.E7.AA.97.E5.8F.A3)
*   [11 鼠标中键](#.E9.BC.A0.E6.A0.87.E4.B8.AD.E9.94.AE)
*   [12 启用按钮和菜单图标](#.E5.90.AF.E7.94.A8.E6.8C.89.E9.92.AE.E5.92.8C.E8.8F.9C.E5.8D.95.E5.9B.BE.E6.A0.87)
*   [13 使用自定义的色彩和渐变色的桌面背景](#.E4.BD.BF.E7.94.A8.E8.87.AA.E5.AE.9A.E4.B9.89.E7.9A.84.E8.89.B2.E5.BD.A9.E5.92.8C.E6.B8.90.E5.8F.98.E8.89.B2.E7.9A.84.E6.A1.8C.E9.9D.A2.E8.83.8C.E6.99.AF)
*   [14 渐变背景](#.E6.B8.90.E5.8F.98.E8.83.8C.E6.99.AF)
*   [15 自定义 GNOME 会话](#.E8.87.AA.E5.AE.9A.E4.B9.89_GNOME_.E4.BC.9A.E8.AF.9D)

### 键盘

#### 登陆打开NumLock键

运行以下命令：

```
$ gsettings set org.gnome.settings-daemon.peripherals.keyboard numlock-state on

```

#### 热键选择

很多的快捷键可以通过系统设置菜单中更改. 例如，重新启用“显示桌面快捷键：

*System settings* > *Keyboard* > *Shortcuts* > *Navigation* > *Hide all normal windows*

However, certain hotkeys cannot be changed directly via system settings. In order to change these keys, use *dconf-editor*. An example of particular note is the hotkey `Alt-` + ``` (the key above `Tab` on US keyboard layouts). In GNOME Shell it is pre-configured to cycle through windows of an application, however it is also a hotkey often used in the [Emacs](/index.php/Emacs "Emacs") editor. It can be changed by opening *dconf-editor* and modifying the *switch-group* key found in `org.gnome.desktop.wm.keybindings`.

It is possible to manually change the keys via an application's so-called **accel** map file. Where it is to be found is up to the application: For instance, Thunar's is at `~/.config/Thunar/accels.scm`, whereas Files's is located at `~/.config/nautilus/accels` and `~/.gnome2/accels/nautilus` on old release.

The file should contain a list of possible hotkeys, each unchanged line commented out with a leading ";" that has to be removed for a change to become active. For example to replace the hotkey used by Files to move files to the trash folder, change the line:

```
; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")

```

to this:

```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

The file is regenerated regularly so do not comment the file. The uncommented line will stay but every comment you add will be lost.

#### 打开键盘开关命令

To have keyboard shortcut **Alt** + **Shift** switch keyboards:

Open Gnome-Tweak-Tool (or Keyboard Settings, in GNOME 3.16) and set *Typing* > *Modifiers-only input sources* > *select Alt-shift*. For more information see also the forum [thread](https://bbs.archlinux.org/viewtopic.php?id=152127).

#### XkbOptions键盘选项

Using the **dconf-editor**, navigate to the key named `org.gnome.desktop.input-sources.xkb-options` and add desired XkbOptions (e.g. *caps:swapescape*) to the list.

See `/usr/share/X11/xkb/rules/xorg` for all XkbOptions and `/usr/share/X11/xkb/symbols/*` for the respective descriptions.

**Note:** To enable the `Ctrl+Alt+Backspace` combination to terminate Xorg, use the [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool). Within the **Tweak Tool**, navigate to *Typing > Key sequence to kill the X server* and select the option `Ctrl+Alt+Backspace` from the dropdown menu.

#### De-bind Windows key

默认情况下，“Windows键”将打开GNOMEshelly预览模式。 You can unbind this key by running the command below

```
$ gsettings set org.gnome.mutter overlay-key 'Foo'

```

### 磁盘

GNOME提供磁盘实用程序来操作的存储驱动器设置。这是它的一些特点：

*   **Enable write cache** is a feature that most hard drives provide. Data is cached and allocated at chosen times to improve system performance. Not recommended unless the computer has a backup battery pack or is a laptop as data would be lost on power failure.

	*Settings* > *Drive Settings* > *Write Cache* > **On**

*   **Automatic Mount Options** can mount drives and partitions that are GPT based - will use default, recommended options.

**Warning:** This setting erases related [fstab](/index.php/Fstab "Fstab") entries

	*Partition Settings* > *Edit Mount Options* > *Automatic Mount Options* > **On**

### 从菜单隐藏的应用程序

**Tip:** Desktop entries can be hidden by editing the `.desktop` files themselves. See [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries").

Use the *Main Menu* application (provided by the [alacarte](https://www.archlinux.org/packages/?name=alacarte) package) to hide any applications you do not wish to show in the menu.

### 截屏记录

GNOME features built-in screencast recording with the **Ctrl** + **Shift** + **Alt** + **R** key combination. A red circle is displayed in the bottom right corner of the screen when the recording is in progress. After the recording is finished, a file named `Screencast from %d%u-%c.webm` is saved in the Videos directory. In order to use the screencast feature the gst plugins need to be installed.

### 截图

默认保存目录:

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/*USER*/Desktop

```

Check the *gnome-screenshot* manual page for more options.

### 注销延迟

去掉注销的确认和 60 秒的延迟： 这个对话框一般出现在你用状态菜单注销的时候。这个修改对于 关机 也生效。这个不是全局修改，只对使用该命令的用户生效。使用该命令立即生效。

```
$ gsettings set org.gnome.SessionManager logout-prompt false

```

### 禁用动画

To disable Shell animations (such as "Show Applications" and the wave animation in the top left activities hot corner), run:

```
$ gsettings set org.gnome.desktop.interface enable-animations false

```

### Retina (HiDPI) display support

GNOME introduced HiDPI support in version 3.10\. If your display does not provide the correct screen size through EDID, this can lead to incorrectly scaled UI elements. As a workaround you can open *dconf-editor* and find the key `scaling-factor` in `org.gnome.desktop.interface`. Set it to `1` to get the standard scale.

Also see [HiDPI](/index.php/HiDPI "HiDPI").

### 密码和密钥 (PGP Keys)

You can use the Passwords and Keys program (*seahorse*) to create a PGP key as it is a front end for [GnuPG](/index.php/GnuPG "GnuPG") and installs it as dependency. This may be useful in the future (for instance if to encrypt a file). Create a key as shown below (the process may take about 10 minutes):

*File* > *New* > *PGP Key* > *Name* > *Email* > *Defaults* > *Passphrase*.

### 终端

#### 更改默认的终端大小

新终端的默认大小可以在*编辑 > 配置文件首选项* 中调整

#### 新终端采用当前目录

By default new terminals open in the `$HOME` directory. To have new terminals adopt the current working directory: `source /etc/profile.d/vte.sh`. Add the command to the shell configuration to retain the behaviour.

#### Pad the terminal

To pad the terminal (create a small, invisible border between the window edges and the terminal contents) create the file below:

 `~/.config/gtk-3.0/gtk.css` 
```
VteTerminal,
TerminalScreen {
    padding: 10px 10px 10px 10px;
    -VteTerminal-inner-border: 10px 10px 10px 10px;
}
```

#### 禁用光标闪烁

Since GNOME 3.8 and the migration to GSettings and DConf the key required to modify in order to disable the blinking cursor in the Terminal differs slightly in contrast to the old GConf key. To disable the blinking cursor in GNOME 3.8 and above use:

```
$ gsettings set org.gnome.desktop.interface cursor-blink false

```

To disable the blinking cursor in Terminal only use (make sure profile uid is correct one):

```
$ dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/cursor-blink-mode "'off'"

```

Note that `gnome-settings-daemon`, from the package of the same name, must be running for this and other settings changes to take effect in GNOME applications - see [GNOME#Configuration](/index.php/GNOME#Configuration "GNOME").

#### 关闭终端时，禁用确认窗口

试图关闭该窗口，而一个以root身份登录时，终端将始终显示一个确认窗口。为了避免这种情况，执行以下命令：

```
$ gsettings set org.gnome.Terminal.Legacy.Settings confirm-close false

```

### 鼠标中键

By default, GNOME 3 disables middle mouse button emulation regardless of [Xorg](/index.php/Xorg "Xorg") settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### 启用按钮和菜单图标

Since GTK+ 3.10, the GSettings key 'menus-have-icons' has been deprecated. Icons in buttons and menus can still be enabled by setting the following overrides:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

### 使用自定义的色彩和渐变色的桌面背景

使用自定义颜色和渐变为您的桌面背景，您首先需要设置一个透明的图片或其他不存在的图片作为您的桌面背景。例如，下面的命令将设置一个不存在的图片为背景。

```
$ gsettings set org.gnome.desktop.background picture-uri none

```

在这一点上，桌面背景应该是一个平坦的颜色-默认的颜色设置为深蓝色。

对于不同的平面彩色你只需要改变的主要颜色设置：

```
$ gsettings set org.gnome.desktop.background primary-color <my color>

```

where <my color> is a hex value (such as *ffffff* for white).

对于颜色渐变，你也需要改变次要颜色设置 `org.gnome.desktop.background secondary-color` 并选择一个阴影类型。举例来说，如果你想有一个horizontal gradient，执行以下命令：

```
$ gsettings set org.gnome.desktop.background color-shading-type horizontal

```

如果你是使用一个透明的图片作为你的背景，你可以通过执行以下设置的透明度：

```
$ gsettings set org.gnome.desktop.background picture-opacity <value>

```

数值在100和1之间（最大不透明度为100）。

### 渐变背景

GNOME 可以在特定的时间间隔之间的使用不同的壁纸。 这是通过创建一个XML文件，指定要使用的图片和时间间隔完成的。有关创建这些文件的详细信息，请参阅下面的 [article](http://www.linuxjournal.com/content/create-custom-transitioning-background-your-gnome-228-desktop).

可替代地，一些工具可用自动化过程：

*   **mkwlppr** — This script creates XML files that can act as dynamic wallpapers for GNOME by referring to multiple wallpapers.

	[http://pastebin.com/019G2rCy](http://pastebin.com/019G2rCy) || see [mkwlppr](http://pastebin.com/019G2rCy)

*   **[Wallpapoz](/index.php/Wallpapoz "Wallpapoz")** — Wallpapoz is a tool that provides dynamic wallpapers for GNOME and Xfce desktops.

	[https://vajrasky.wordpress.com/](https://vajrasky.wordpress.com/) || [wallpapoz](https://aur.archlinux.org/packages/wallpapoz/)

*   **CreBS** — A Python/GTK application used to create and set desktop wallpaper slideshows for GNOME.

	[http://www.obfuscatepenguin.net/](http://www.obfuscatepenguin.net/) || [crebs](https://aur.archlinux.org/packages/crebs/)

对于设置XML文件作为默认的背景，参阅 [#Lock screen and background](#Lock_screen_and_background).

### 自定义 GNOME 会话

It is possible to create custom GNOME sessions which use the GNOME session manager but start different sets of components ([Openbox](/index.php/Openbox "Openbox") with [tint2](/index.php/Tint2 "Tint2") instead of GNOME Shell for example).

Two files are required for a custom GNOME session: a session file in `/usr/share/gnome-session/sessions/` which defines the components to be started and a [desktop entry](/index.php/Desktop_entry "Desktop entry") in `/usr/share/xsessions` which is read by the [display manager](/index.php/Display_manager "Display manager"). An example session file is provided below:

 `/usr/share/gnome-session/sessions/gnome-openbox.session` 
```
[GNOME Session]
Name=GNOME Openbox
RequiredComponents=openbox;tint2;gnome-settings-daemon;

```

And an example desktop file:

 `/usr/share/xsessions/gnome-openbox.desktop` 
```
[Desktop Entry]
Name=GNOME Openbox
Exec=gnome-session --session=gnome-openbox

```

**Note:** GNOME Session calls upon the `.desktop` files of each of the components to be started. If a component you wish to start does not provide a `.desktop` file, you must create a suitable desktop entry in a directory such as `/usr/local/share/applications`.