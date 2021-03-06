相关文章

*   [Desktop environment (简体中文)](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")
*   [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [Window manager (简体中文)](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")
*   [Qt (简体中文)](/index.php/Qt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Qt (简体中文)")
*   [SDDM (简体中文)](/index.php/SDDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SDDM (简体中文)")
*   [Dolphin (简体中文)](/index.php?title=Dolphin_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Dolphin (简体中文) (page does not exist)")
*   [KDE Wallet (简体中文)](/index.php/KDE_Wallet_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE Wallet (简体中文)")
*   [KDevelop](/index.php/KDevelop "KDevelop")
*   [Trinity](/index.php/Trinity "Trinity")
*   [Uniform Look for Qt and GTK Applications (简体中文)](/index.php/Uniform_Look_for_Qt_and_GTK_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform Look for Qt and GTK Applications (简体中文)")

**翻译状态：** 本文是英文页面 [KDE](/index.php/KDE "KDE") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-08，点击[这里](https://wiki.archlinux.org/index.php?title=KDE&diff=0&oldid=532333)可以查看翻译后英文页面的改动。

KDE 是由 Plasma [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")、库、框架 (KDE Frameworks)、和应用组成的软件项目。KDE 上游有一份维护良好的 [UserBase Wiki](https://userbase.kde.org/)。大多数 KDE 应用程序的详细信息都可以在那里找到。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 Plasma 桌面](#Plasma_桌面)
    *   [1.2 KDE 应用](#KDE_应用)
    *   [1.3 不稳定版](#不稳定版)
*   [2 启动 Plasma](#启动_Plasma)
    *   [2.1 使用显示管理器](#使用显示管理器)
    *   [2.2 控制台启动](#控制台启动)
*   [3 配置](#配置)
    *   [3.1 个性化](#个性化)
        *   [3.1.1 Plasma 桌面](#Plasma_桌面_2)
            *   [3.1.1.1 主题](#主题)
                *   [3.1.1.1.1 Qt 和 GTK+ 应用外观](#Qt_和_GTK+_应用外观)
            *   [3.1.1.2 小部件](#小部件)
            *   [3.1.1.3 系统托盘中的声音应用](#系统托盘中的声音应用)
            *   [3.1.1.4 禁用面板阴影](#禁用面板阴影)
        *   [3.1.2 窗口装饰](#窗口装饰)
        *   [3.1.3 图标主题](#图标主题)
        *   [3.1.4 字体](#字体)
            *   [3.1.4.1 字体感觉模糊](#字体感觉模糊)
            *   [3.1.4.2 字体太大或变形](#字体太大或变形)
        *   [3.1.5 空间效率](#空间效率)
        *   [3.1.6 缩略图生成](#缩略图生成)
    *   [3.2 打印](#打印)
    *   [3.3 Samba/Windows 的支持](#Samba/Windows_的支持)
    *   [3.4 KDE 桌面活动](#KDE_桌面活动)
    *   [3.5 节能](#节能)
    *   [3.6 程序自启动](#程序自启动)
    *   [3.7 Phonon](#Phonon)
        *   [3.7.1 我应该选择哪个后端？](#我应该选择哪个后端？)
*   [4 应用程序](#应用程序)
    *   [4.1 系统管理](#系统管理)
        *   [4.1.1 KDE 系统设置中配置终止 Xorg-server](#KDE_系统设置中配置终止_Xorg-server)
        *   [4.1.2 KCM](#KCM)
    *   [4.2 桌面搜索](#桌面搜索)
        *   [4.2.1 Baloo](#Baloo)
            *   [4.2.1.1 使用及配置 Baloo](#使用及配置_Baloo)
            *   [4.2.1.2 如何把可移动设备加入索引？](#如何把可移动设备加入索引？)
    *   [4.3 Web 浏览器](#Web_浏览器)
    *   [4.4 个人信息管理](#个人信息管理)
        *   [4.4.1 Akonadi](#Akonadi)
            *   [4.4.1.1 安装](#安装_2)
            *   [4.4.1.2 禁用 Akonadi](#禁用_Akonadi)
            *   [4.4.1.3 配置数据库](#配置数据库)
                *   [4.4.1.3.1 MariaDB/MySQL (使用 ZFS)](#MariaDB/MySQL_(使用_ZFS))
                *   [4.4.1.3.2 PostgreSQL](#PostgreSQL)
                *   [4.4.1.3.3 SQLite](#SQLite)
    *   [4.5 KDE Telepathy](#KDE_Telepathy)
        *   [4.5.1 使用 Telegram 与 KDE Telepathy](#使用_Telegram_与_KDE_Telepathy)
    *   [4.6 安卓整合](#安卓整合)
*   [5 提示和技巧](#提示和技巧)
    *   [5.1 使用其他窗口管理器](#使用其他窗口管理器)
        *   [5.1.1 KDE/Openbox 会话](#KDE/Openbox_会话)
        *   [5.1.2 重新启用特殊效果](#重新启用特殊效果)
    *   [5.2 显示器分辨率 / 多显示器配置](#显示器分辨率_/_多显示器配置)
    *   [5.3 禁用超级键（Windows 键）打开应用程序启动器](#禁用超级键（Windows_键）打开应用程序启动器)
*   [6 疑难解答](#疑难解答)
    *   [6.1 有关配置的问题](#有关配置的问题)
        *   [6.1.1 Plasma 桌面行为异常](#Plasma_桌面行为异常)
        *   [6.1.2 清理缓存以解决升级故障](#清理缓存以解决升级故障)
    *   [6.2 清理 akonadi 配置来修复 kmail](#清理_akonadi_配置来修复_kmail)
    *   [6.3 KMail 中空的 IMAP 收件箱](#KMail_中空的_IMAP_收件箱)
    *   [6.4 获取 KWin 的当前状态以进行支持和调试](#获取_KWin_的当前状态以进行支持和调试)
    *   [6.5 KF5/Qt5 应用在 i3/fvwm/awesome 中不显示图标](#KF5/Qt5_应用在_i3/fvwm/awesome_中不显示图标)
    *   [6.6 图形问题](#图形问题)
        *   [6.6.1 禁用桌面特效](#禁用桌面特效)
        *   [6.6.2 禁用混合项（compositing）](#禁用混合项（compositing）)
        *   [6.6.3 启用混合项（compositing）后全屏时闪烁](#启用混合项（compositing）后全屏时闪烁)
        *   [6.6.4 Nvidia 显卡屏幕撕裂](#Nvidia_显卡屏幕撕裂)
        *   [6.6.5 Plasma 光标有时显示不正确](#Plasma_光标有时显示不正确)
    *   [6.7 声音问题](#声音问题)
        *   [6.7.1 睡眠后没声音](#睡眠后没声音)
        *   [6.7.2 在播放任何声音时出现 "返回默认" 消息](#在播放任何声音时出现_"返回默认"_消息)
        *   [6.7.3 使用 GStreamer Phonon 后端时不能播放 MP3 文件](#使用_GStreamer_Phonon_后端时不能播放_MP3_文件)
    *   [6.8 Inotify 文件夹监控上限](#Inotify_文件夹监控上限)
    *   [6.9 自动挂载NFS卷时卡死](#自动挂载NFS卷时卡死)
    *   [6.10 没有挂起/休眠选项](#没有挂起/休眠选项)
    *   [6.11 保存凭据和持续显示 KWallet 对话框的问题](#保存凭据和持续显示_KWallet_对话框的问题)
*   [7 参见](#参见)

## 安装

### Plasma 桌面

在安装 Plasma 之前，请确保 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") 已经被安装到您的系统中。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) 元软件包或者 [plasma](https://www.archlinux.org/groups/x86_64/plasma/) 组。 关于 [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) 和 [plasma](https://www.archlinux.org/groups/x86_64/plasma/) 两者的不同请参阅[这里](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#元软件包和软件包组 "Creating packages (简体中文)")。若要最小化安装 Plasma，可以安装 [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) 包。

若要为 Plasma 启动 [Wayland](/index.php/Wayland "Wayland") 支持，请安装 [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) 软件包。

### KDE 应用

可以通过安装 [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) 组或者 [kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta) 元软件包，从而安装 KDE 的全套应用。请注意这仅仅安装应用程序，并不会安装 Plasma 桌面。

### 不稳定版

参阅 [Official repositories#kde-unstable](/index.php/Official_repositories#kde-unstable "Official repositories")（英文）。

## 启动 Plasma

**注意:** 虽然可以使用 [Wayland](/index.php/Wayland_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wayland (简体中文)") 启动 Plasma，但 Plasma 5.13 仍存在一些缺失的功能和已知问题。问题清单详见 [Plasma 5.13 Errata（英文）](https://community.kde.org/Plasma/5.13_Errata#Wayland)，当前开发状况详见 [Plasma on Wayland workboard（英文）](https://phabricator.kde.org/project/board/99/)。使用 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") 以获得最完整和稳定的体验。

Plasma 可以通过[显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")启动,也可以从控制台手动启动。

### 使用显示管理器

*   在菜单中选择 *Plasma* 用 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") 启动。
*   安装 [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session) 软件包，然后选择 *Plasma (Wayland)* 用 [Wayland](/index.php/Wayland_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wayland (简体中文)") 启动。

**注意:** [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)") 的专有驱动需要 EGLStreams 启动 Wayland。KDE 还没有将 EGLStreams 加入到其 Wayland [配置（英文）](https://blog.martin-graesslin.com/blog/2016/09/to-eglstream-or-not)中。因此存在以下解决方法：

*   使用 [Nouveau](/index.php/Nouveau_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Nouveau (简体中文)") 驱动。
*   使用 Xorg 会话（默认）。

### 控制台启动

若要使用 "[xinit/startx](/index.php/Xinit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinit (简体中文)")" 启动 Plasma 桌面，请在 `.xinitrc` 文件中添加 `exec startkde`。若要在登录的时候开启 Xorg 请参阅[在启动时自动启用 X](/index.php/Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Start X at Login (简体中文)")。若要从终端启动 Wayland 会话, 运行 `export XDG_SESSION_TYPE=wayland && export $(dbus-launch) && startplasmacompositor`。[[1]](https://community.kde.org/KWin/Wayland#Start_a_Plasma_session_on_Wayland%7C在控制台启动Wayland会话)

## 配置

大部分配置被储存在 `~/.config`。KDE 主要在**“系统设置”**内配置。它也可通过 `systemsettings5` 启动。

### 个性化

#### Plasma 桌面

##### 主题

[Plasma 主题](http://kde-look.org/index.php?xcontentmode=76)定义面板和 plasmoids。官方资料库和 [AUR](https://aur.archlinux.org/packages.php?K=plasma+theme) 提供了很多主题。

通过桌面设置控制面板来安装主题是最简单的方法：

```
 系统设置 > 工作空间主题 > 桌面主题 > 获取新主题

```

这将呈现出 [https://store.kde.org/](https://store.kde.org/) 的前端让你轻松安装，卸载，或者更新第三方 Plasma 脚本。

加载页面和锁定页面暂时无法自定义，但你可以在 `/usr/share/plasma/look-and-feel/` 修改原本的主题。请阅 Kubuntu论坛的[这个帖子](https://www.kubuntuforums.net/showthread.php?67599-Plasma-5-background-images&s=59832dc20e5bfc2948dbb591d8453f61)。

注意[SDDM](/index.php/SDDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SDDM (简体中文)")的登录界面主题并不在此处设置。

###### Qt 和 GTK+ 应用外观

**提示：** 为了 Qt 和 GTK 主题的一致性，请参见 [外观统一的 QT 和 GTK 应用](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform look for Qt and GTK applications (简体中文)")。

	Qt4

请安装[breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4)，然后从 `qtconfig-qt4` 中挑选微风作为图形用户界面风格。

	GTK+

在 GTK 中推荐外形美观的主题是 [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) 或 [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/)。安装 [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) （该软件是[plasma](https://www.archlinux.org/groups/x86_64/plasma/) 的一部分），在 *系统设置 > 应用风格 > GNOME 应用设置* 中选择想要的 GTK 主题。

在某些主题中，GTK+ 应用程序的工具栏显示为白底白字。若要更改 GTK2 应用程序中的颜色，请找到 `.gtkrc-2.0` 并修改工具栏区。若要更改 GTK3 应用程序中的颜色，`gtk.css` 和 `settings.ini` 文件需要被修改。您也可以尝试在 *系统设置 > 颜色* 中取消对 *将颜色应用于非Qt应用程序* 的勾选。

一些例如 [vuescan-bin](https://aur.archlinux.org/packages/vuescan-bin/) 的 GTK2 程序仍然因为 Plasma 的微风和 Adwaita 主题拥有透明的复选框.要解决这个问题，请安装并在 *系统设置 > 应用风格 > GNOME 应用设置* 中选择例如 [numix-frost-themes](https://aur.archlinux.org/packages/numix-frost-themes/) 这样的皮肤。Numix-Frost-Light 看起来与微风相似。

##### 小部件

Plasmoid包含短的脚本（plasmoid scripts）或者编译过的（plasmoid binaries）的KDE应用程序，用于增强桌面的功能。 Plasmoid二进制文件可以从[AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v)上获得的PKGBUILD安装，或者您可以编写自己的PKGBUILD。 最简单的安装Plasmoid脚本的方式是右击面板或桌面：

```
添加部件 > 获得新部件 > 下载新 Plasma 部件

```

这将显示 [kde-look.org](http://www.kde-look.org/) 的前端界面，并可一键可以安装/卸载/更新第三方 plasmoid 脚本。

大部分 plasmoids 的二进位编码可从 [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&PP=50&SO=d&SB=v) 上获得。

##### 系统托盘中的声音应用

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) 或 [kmix](https://www.archlinux.org/packages/?name=kmix) (从程序启动器启动 Kmix)。前者已被自动安装，无需其他设定。

**注意:** 要调整 [音量增减的步长](https://bugs.kde.org/show_bug.cgi?id=313579#c28)，将诸如 `VolumePercentageStep=1` 一行添加到 `~/.kde4/share/config/kmixrc` 的 `[Global]` 一节中。

##### 禁用面板阴影

因为 Plasma 的面板在其他窗口之上，所以它的阴影会渲染在其他窗口之上。[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1228394#p1228394)若要在不影响其他阴影的情况下禁用此行为，[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) 并运行:

```
$ xprop -remove _KDE_NET_WM_SHADOW

```

然后用增大光标选择面板。[[3]](https://forum.kde.org/viewtopic.php?f=285&t=121592) 若要自动化，[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo) 并创建以下脚本：

 `/usr/local/bin/kde-no-shadow` 
```
#!/bin/bash
for WID in $(xwininfo -root -tree | sed '/"Plasma": ("plasmashell" "plasmashell")/!d; s/^  *\([^ ]*\) .*/\1/g'); do
   xprop -id $WID -remove _KDE_NET_WM_SHADOW
done

```

添加可执行权限

```
# chmod 755 /usr/local/bin/kde-no-shadow

```

此脚本可以在登录时启动，请将其加在*自动启动*：

```
$ kcmshell5 autostart

```

#### 窗口装饰

[窗口装饰](http://kde-look.org/index.php?xcontentmode=75)可以在 *系统设置 > 应用程序风格 > 窗口装饰* 中设置。

您也可以在[AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v)上找到,直接下载并安装更多的主题。

#### 图标主题

图标主题可以在 *系统设置 > 图标* 中安装或改变.

**注意:** 虽然所有现代的Linux发行版都共享统一的图标主题格式，但像 [GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")这样的桌面使用更少的图标（特别在工具栏和菜单中）。为这些桌面开发的主题一边都缺少 Plasma 和 KDE 应用需要的图标。建议安装与 Plasma 兼容的主题。

**提示：** 部分图标主题不从默认图标主题中引入图标，这将导致部分图标缺失。要想从默认图标主题中导入缺失图标，把`breeze`添加到 `/usr/share/icon/*theme-name*/index.theme`的`Inherits=` 中，比如`Inherits=breeze,hicolor`。每次更新图标主题时你都需要重新使用这个补丁，尝试使用[Pacman hooks](/index.php/Pacman_hooks "Pacman hooks")来自动完成这项任务。

#### 字体

##### 字体感觉模糊

尝试安装 [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) 和 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 软件包。

安装后，确保注销并重新登录。不需要修改*系统设置 > 应用程序外观 > 字体*里的设置。 如果你使用 [qt5ct](https://www.archlinux.org/packages/?name=qt5ct) 包，Qt5 设置工具将有可能覆盖系用设置内的字体设置。

如果您个人已经设置了[字体](/index.php/Fonts "Fonts")渲染，小心系统设置可能会改变它们的外观。当改变了*系统设置 > 应用程序外观 > 字体*里的设置，系统将可能改写字体配置文件(`fonts.conf`)。

没有办法避免这种情况，但是如果把数值调到了匹配 `fonts.conf` 文件的话，所期望的字体渲染效果将会重新出现（这需要重启您的应用程序，在某些情况下可能需要重启桌面环境）。注意 Gnome 中的字体设置也会有这样的效果。

##### 字体太大或变形

从 *系统设置 > 应用程序外观 > 字体* 将字体 DPI 强制设置为 **96**

如果还是不行请尝试直接通过 Xorg 配置文件设置 DPI。[参见这里](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#手动设置DPI "Xorg (简体中文)").

#### 空间效率

Plasma Netbool shell （上网本交互界面）已从 Plasma 5 中移除，请阅[此KDE论坛帖子](https://forum.kde.org/viewtopic.php?f=289&t=126631&p=335947&hilit=plasma+netbook#p335899)。但是你仍然可以通过编辑 `~/.config/kwinrc`，在 `[Windows]` 区内加上 `BorderlessMaximizedWindows=true` 来实现类似的操作。

#### 缩略图生成

若要在桌面和 Dolphin 内为媒体或文档文件生成缩略图，安装 [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers)，[ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs) 和 [kde-thumbnailer-odf](https://aur.archlinux.org/packages/kde-thumbnailer-odf/)。

然后在 *桌面背景* > *配置桌面* > *图标* > *更多预览选项...* 内通过 *右键单击* 启用桌面的缩略图类别。

在 *Dolphin* 中，浏览到 *控制* > *通用* > *预览*。

### 打印

**提示：** 使用 [CUPS](/index.php/CUPS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "CUPS (简体中文)") 的 Web 接口进行快速配置。这种方式配置的打印机可以被 KDE 应用使用。

你也可以在 **系统设置 > 打印机配置** 中配置打印机。要使用这种配置方式，必须首先安装 [print-manager](https://www.archlinux.org/packages/?name=print-manager) 和 [cups](https://www.archlinux.org/packages/?name=cups) 软件包。请阅[CUPS配置](/index.php/CUPS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#配置 "CUPS (简体中文)")

### Samba/Windows 的支持

若要使用 Windows 服务，安装 [Samba](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Samba (简体中文)") ([samba](https://www.archlinux.org/packages/?name=samba) 软件包)。

Dophin 的共享服务需要 [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) 软件包以及 usershares。关于如何配置usershares（`smb.conf`未启动它），详见 [Samba (简体中文)#建立 Usershare 路径](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#建立_Usershare_路径 "Samba (简体中文)")。在重新启动Samba之后，Dolphin的共享应该无需进一步配置。

Plasma 访问 SMB 共享的能力有限。写入到 Windows 共享存在问题，打开 Windows 共享内文件（例：大的视频文件）会让 Plasma 先将整个文件先复制到本地系统。要解决这个问题，您可以安装类似 [thunar](https://www.archlinux.org/packages/?name=thunar) 加 [gvfs](https://www.archlinux.org/packages/?name=gvfs) 和 [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb)（和 [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) 用于保存登录凭据）的基于GTK的文件浏览器，以更有效的方式访问 SMB 共享。 另一种可能的解决方法则是通过 {Pkg|cifs-utils}} 来 [挂载](/index.php/File_systems#Mount_a_file_system "File systems") Samba 共享从而让 Plasma 把 SMB 共享当成一个普通的本地文件夹从而正常访问。对于公共共享的写入访问，mount命令可能如下所示：

```
# mount -t cifs -o username=*,password=*,uid=1000,gid=1000,file_mode=0660,dir_mode=0770 //networkhost/share/ /home/user/localmountpoint/

```

若要永久将其挂载：

 `/etc/fstab` 
```
//networkhost/share/ /home/user/localmountpoint/ cifs defaults,username=*,password=*,uid=1000,gid=1000,file_mode=0660,dir_mode=0770 0 2

```

可能需要将 `.local` 附加到 hostname。对于某些 NAS 设备，可能需要将 `vers=1.0` 附加到参数行以实现 SMB 1.0 的兼容性。

另一种简单的解决办法则是使用 [samba-mounter-git](https://aur.archlinux.org/packages/samba-mounter-git/)。它在 *系统设置* > *网络驱动* 中提供了基本相同的功能。

### KDE 桌面活动

KDE 桌面活动是类似于“虚拟桌面”的 Plasma 组件，你可以独立地对某个特定的活动进行特别的设定。 只有当你在用这个活动时，这些设定才会生效。

### 节能

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) 以便使用 KDE 内置的 "**PowerDevil 电源管理**"的节能服务，它可以调整系统的节能配置文件和/或（如果支持的话）屏幕的亮度。

**注意:** Powerdevil 可能无法 [覆盖](/index.php/Power_management#Power_managers "Power management") 所有的 logind 设置(例如笔记本翻盖动作). 请修改 [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### 程序自启动

Plasma 可以在启动和关闭时自动启动应用程序并运行shell脚本。若要自动启动应用程序，请浏览到 *系统设置 > 开关机 > 自启动* 并添加您想要的程序或shell脚本。对于应用程序，`.desktop` 文件将被创建。对于shell脚本，symlink 将被创建。

**注意:**

*   程序只能在登录时自启动，而shell脚本也可以在关机和 Plasma 启动前启动。
*   Shell脚本只有在被标记为可执行文件时才会运行。

将[桌面配置项](/index.php/Desktop_entries_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop entries (简体中文)")（即`.desktop`文件）放在这里：

	`~/.config/autostart`

	在登录时启动应用程序。

将shell脚本的symlink放入以下目录之一中：

	`~/.config/plasma-workspace/env`

	在 Plasma 启动前启动脚本。

	`~/.config/autostart-scripts`

	在登录时启动脚本。

	`~/.config/plasma-workspace/shutdown`

	在关机时启动脚本。

### Phonon

摘自 [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)")： *Phonon 是 KDE 的多媒体 API, 提供了多个多媒体框架的抽象，为 KDE 和一些 QT 程序提供多媒体流处理功能。*

Phonon 最初是为了让 KDE 和 Qt 软件独立于其他多媒体框架（例如GStreamer或xine）并其提供一个稳定的 API。

KDE 中广泛地使用 Phonon 用于声音（例如系统通知或者 KDE 声音应用）和视频（例如 Dolphin 中的视频缩略图）中。

#### 我应该选择哪个后端？

你可以在 [GStreamer](/index.php/GStreamer "GStreamer") 和 [VLC](/index.php/VLC "VLC") 之间做选择–每个后端都有 Qt4 和 Qt5 版本 ([phonon-qt4-gstreamer](https://aur.archlinux.org/packages/phonon-qt4-gstreamer/), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

[KDE-Multimedia 上游建议使用 VLC 后端](http://lists.kde.org/?l=kde-multimedia&m=137994906723790&w=2)，但是很多 Linux 发行版 (例如 Kubuntu 和 Fedora-KDE ) 选择 GStreamer，因为它可以更方便的去掉专利 MPEG codecs。它们的 [功能](http://community.kde.org/Phonon/FeatureMatrix)有稍许不同。

之前还有一些后端，但是因为缺乏维护，已经从 Arch 中删除。

**注意:**

*   可以同时安装多个后端，并在 *系统设置 > 多媒体 > 后端* 中进行优先级设定。
*   根据 [KDE 这个帖子](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), VLC 后端不支持 [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain")。
*   如果你选择 VLC 后端，你可能会在每次kde想要发送一个语音警告时遇到崩溃（以及在很多其他情况下，参见[[4]](https://forum.kde.org/viewtopic.php?f=289&t=135956))
*   你可以尝试运行以下代码进行修复：

 `# /usr/lib/vlc/vlc-cache-gen -f /usr/lib/vlc/plugins` 

## 应用程序

KDE项目提供了一套与Plasma桌面集成的应用程序。有关可用应用程序的完整列表，详见 [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) 软件包。另请参阅 [KDE 相关应用页面](/index.php/Category:KDE "Category:KDE")。

除了 KDE 应用程序包提供的程序之外，还有许多其他可用于补充 Plasma 的应用程序。其中一些将在下面讨论。

### 系统管理

#### KDE 系统设置中配置终止 Xorg-server

浏览到子菜单：

```
   系统设置 > 硬件 > 输入设备 > 键盘 > 高级（标签） > "Key Sequence to kill the X server" 

```

然后选中复选框。

#### KCM

KCM 意为 KDE 控制模块（**KC**onfig **M**odule）。这些模块在系统设置中提供了界面从而帮助你配置系统，或通过命令行（'kcmshell5*）。*

*   **kde-gtk-config** — GTK2 和 GTK3 的 KDE 设置器。

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

*   **KCM Qt Graphics System** — 该 KCM 让您轻松配置标准的Qt图形系统。

	[https://www.linux-apps.com/p/1127857/](https://www.linux-apps.com/p/1127857/) || [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)

*   **UFW KControl Module** — KDE4 UFW 控制组件 ([Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall"))。

	[https://www.linux-apps.com/p/1127851/](https://www.linux-apps.com/p/1127851/) || [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

*   **System policies** — 配置[PolicyKit](/index.php/PolicyKit "PolicyKit")。

	[https://cgit.kde.org/polkit-kde-kcmodules-1.git](https://cgit.kde.org/polkit-kde-kcmodules-1.git) || [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

*   **wacom tablet** — KDE Wacom 驱动图形界面。

	[https://www.linux-apps.com/p/1127862/](https://www.linux-apps.com/p/1127862/) || [kcm-wacomtablet](https://www.archlinux.org/packages/?name=kcm-wacomtablet)

*   **Kcmsystemd** — KDE 系统控制组件.

	[https://github.com/rthomsen/kcmsystemd](https://github.com/rthomsen/kcmsystemd) || [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/)

可从 [linux-apps.com](https://www.linux-apps.com/search?projectSearchText=KCM) 找到更多的 KCM 。

### 桌面搜索

KDE 使用 Baloo 实现文件索引和查找。

#### Baloo

##### 使用及配置 Baloo

为了在 Plasma 桌面上使用 Baloo 进行搜索，启动 krunner （默认快捷键 `ALT+F2`）并键入查询。若要在 Dophin（文件管理器）内搜索，按`CTRL+F`。

在默认情况下，桌面搜索的 KCM 仅显示两个选项：一个将文件夹放入黑名单的面板以及一种一次点击来禁用它的方法。

或者你可以编辑 `~/.config/baloofilerc` 文件[[5]](https://community.kde.org/Baloo/Configuration)。另外你也可以使用 `balooctl` 进程。运行 `balooctl stop` 和 `balooctl disable`。

将文件夹添加到黑名单或完全禁用了Baloo之后，`baloo_file_cleaner` 进程将会自动删除所有不需要的索引文件。它们被存储在 `~/.local/share/baloo/` 。

##### 如何把可移动设备加入索引？

默认情况下，所有可移动设备都在黑名单内。你只需要在 KCM 面板中移除你的设备即可。

### Web 浏览器

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — KDE项目的一部分, 支持两种渲染引擎 – KHTML 和基于[Chromium](/index.php/Chromium "Chromium")的 Qt Web引擎。

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **[QupZilla](https://en.wikipedia.org/wiki/QupZilla "wikipedia:QupZilla")** — 包含 Plasma 集成特性的 Qt web 浏览器。其使用 Qt Web引擎。

	[https://www.qupzilla.com/](https://www.qupzilla.com/) || [qupzilla](https://www.archlinux.org/packages/?name=qupzilla)

*   **[Chromium](/index.php/Chromium "Chromium")** — Chromium 及它的专有版本 Google Chrome 具有有限的 Plasma 集成。 [它们可以使用 KWallet](/index.php/KDE_Wallet#KDE_Wallet_for_Chrome_and_Chromium "KDE Wallet") 以及 KDE 窗口 打开/保存。

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Firefox](/index.php/Firefox "Firefox")** — Firefox 可以通过配置以和 Plasma 更好地集成。参考 [Firefox KDE整合](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#KDE_整合 "Firefox (简体中文)")。

	[https://mozilla.org/firefox](https://mozilla.org/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

### 个人信息管理

KDE 提供了其自己的个人信息管理应用储存，包括电子邮件，联系人，日历等。可以使用 [kdepim-meta](https://www.archlinux.org/packages/?name=kdepim-meta) 元软件包安装所有相关的软件包。

#### Akonadi

Akonadi 是系统中本地缓存各种来源的 PIM 数据的一种方法，接着这些数据可以被其它的应用使用。这包含了用户的邮件、联系人、日历、事件、刊物、闹钟、笔记等。

Akonadi 自身并不存储任何数据：存储格式依赖于数据的性质（例如，联系人可能以 vcard 格式存储）。

##### 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [akonadi](https://www.archlinux.org/packages/?name=akonadi). 若需其他插件，安装 [kdepim-addons](https://www.archlinux.org/packages/?name=kdepim-addons)。

**注意:** 若要使用除 MariaDB/MySQL 以外的数据库引擎，请在安装 [akonadi](https://www.archlinux.org/packages/?name=akonadi) 包时使用以下命令从而跳过 [mariadb](https://www.archlinux.org/packages/?name=mariadb) 依赖项的安装: `# pacman -S akonadi --assume-installed mariadb` 

##### 禁用 Akonadi

请参见 KDE userbase 的[这一节](http://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem)。

##### 配置数据库

###### MariaDB/MySQL (使用 ZFS)

如果您的主目录位于ZFS池中，你将需要创建 `~/.config/akonadi/mysql-local.conf` 并添加以下内容：

```
[mysqld]
innodb_use_native_aio = 0

```

否则你会收到 [OS error 22](/index.php/MySQL#OS_error_22_when_running_on_ZFS "MySQL")。

###### PostgreSQL

安装并设置 [PostgreSQL (简体中文)](/index.php/PostgreSQL_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PostgreSQL (简体中文)")。确保 `postgresql.service` 已被[激活](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)").

编辑Akonadi配置文件，使其具有以下内容：

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QPSQL

[QPSQL]
Host=/run/postgresql/
InitDbPath=/usr/bin/initdb
Name=akonadi
Options=
Password=
Port=5432
ServerPath=/usr/bin/pg_ctl
StartServer=true
User=postgres

```

**注意:** 如果你的 PostgreSQL 数据库用户名，密码和端口不同于 `postgres` 及 `5432`, 请确保你别更改了配置选项：`User=`, `Password=`, 以及 `Port=`.

运行 `akonadictl start` 启动 Akonadi 并检查其状态: `akonadictl status`。

###### SQLite

编辑Akonadi配置文件以匹配以下配置：

 `~/.config/akonadi/akonadiserverrc` 
```
[%General]
Driver=QSQLITE3

[QSQLITE3]
Name=/home/*username*/.local/share/akonadi/akonadi.db
```

### KDE Telepathy

[KDE Telepathy](http://community.kde.org/KTp) 是一个把即时信息功能紧密整合到 KDE 桌面中的项目。它使用 Telepathy 框架作为后端，意在替代 Kopete。

若要安装所有 Telepathy 协议，安装 [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) 组。 若要使用 KDE Telepathy 客户端，安装 [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta) 元软件包，它包含了所有在 [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/) 组中的软件包。

#### 使用 Telegram 与 KDE Telepathy

[Telegram](/index.php/Telegram "Telegram") 协议需要使用 [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), 安装 [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) 或 [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) 和 [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/)。用户名是 Telegram 账户电话号码 (加国家前缀 `+*xx*`，例如德国是 `+49`).

通过图形界面进行配置可能会很棘手：如果在KDE Telepathy客户端中配置新帐户时不接受电话号码（出现一个错误信息表明参数无效并阻止创建账户），请把其添加在单引号中，并在帐号创建好后从配置文件（`~/.local/share/telepathy/mission-control/accounts.cfg`）中手动移除引号（如果引号未被移除，会发生认证错误）。

**注意:** 配置文件应当在 KDE Telepathy 未运行时手动编辑，例如当 KDE 桌面未激活时，否则手动更改可能会被软件覆盖。

### 安卓整合

[KDE Connect](https://community.kde.org/KDEConnect) 提供了一些功能：

*   从任何应用向 KDE 共享文件和 URL 或从 KDE 向任何应用共享，无需连线。
*   触摸板模拟：将手机屏幕用作计算机的触摸板。
*   通知同步（4.3+）：从桌面读取您的安卓通知。
*   共享剪贴板：在手机和电脑之间复制粘贴。
*   多媒体远程控制：将手机用作 Linux 媒体播放器的遥控器。
*   WiFi 连接：不需要 usb 和蓝牙。
*   RSA加密：保证您的信息安全。

你需要同时在电脑和安卓上安装 KDE Connect。在PC端上安装 [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) 软件包。对于安卓端，请通过 [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) 或 [F-Droid](https://f-droid.org/repository/browse/?fdid=org.kde.kdeconnect_tp) 安装 `KDE Connect`。

即使不使用 Plasma 桌面，你也可以使用 KDE Connect。对于使用 AppIndicator（如Unity）的桌面环境，也需要安装indicator-kdeconnect 软件包。

## 提示和技巧

### 使用其他窗口管理器

Plasma 中的组件选择器设置已不再允许更改窗口管理器。[[6]](https://github.com/KDE/plasma-desktop/commit/2f83a4434a888cd17b03af1f9925cbb054256ade)若需要更改窗口管理器，你需要在 KDE 启动之前设置 `KDEWM` [环境变量](/index.php/Environment_variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Environment variables (简体中文)")。[[7]](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE)为此，你可以在 `~/.config/plasma-workspace/env` 中创建一个名为 `set_window_manager.sh` 的脚本，并在这导出 `KDEWM` 变量。例：使用 i3 窗口管理器：

 `~/.config/plasma-workspace/env/set_window_manager.sh`  `export KDEWM=/usr/bin/i3` 

然后标记其为可执行：

 `$ chmod +x ~/.config/plasma-workspace/env/set_window_manager.sh` 

#### KDE/Openbox 会话

软件包 [openbox](https://www.archlinux.org/packages/?name=openbox) 为在plasma下使用 [Openbox](/index.php/Openbox "Openbox") 提供了会话. 要使用这个会话，请在 [display manager](/index.php/Display_manager "Display manager") 菜单中选择 *KDE/Openbox* .

若要手动启动会话，请将下面这行添加到你的 `.xinitrc` 文件中:

```
exec openbox-kde-session

```

#### 重新启用特殊效果

当你用不包含窗口混合器（Compositor）的窗口管理器（例如 Openbox）替换 Kwin 时，任何桌面特殊效果都会失效（例如窗口透明度）。在这种情况下，请安装并运行其他独立混合器，比如 [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") 或 [Compton](/index.php/Compton "Compton")。

### 显示器分辨率 / 多显示器配置

要在 Plasma 中启用分辨率和多显示器管理, 请安装 [kscreen](https://www.archlinux.org/packages/?name=kscreen). 它在 *系统设置 > 显示* 中添加了更多选项.

### 禁用超级键（Windows 键）打开应用程序启动器

若要禁用此功能，请运行以下命令：

```
$ kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta ""

```

## 疑难解答

### 有关配置的问题

KDE 中许多问题都跟配置相关。

#### Plasma 桌面行为异常

Plasma 故障通常是由不稳定的 **plasma 小部件**（plasmoids）或者 **plasma 主题**引起的。首先寻找最近安装的 plasmoid 或者 plasma 主题并禁用或者卸载它。

因此，如果你的桌面突然被"锁定"了，很可能是由于安装了有问题的组件造成的。如果你不记得故障发生前你安装了什么小部件（有时它可能是一个不寻常的问题），通过逐个移除小部件直到问题不再出现。然后你可以卸载这个小部件并提交一份缺陷报告，**若是官方小部件时**到[KDE 缺陷跟踪页](https://bugs.kde.org/)提交一份缺陷报告。如果它不是，你可以在 [https://store.kde.org/](https://store.kde.org/) 上寻找它的条目并告知小部件的开发者你所碰到的问题（以及再现它的详细步骤等）。

如果你找不到问题，也不想丢失*所有的*设置，浏览到`~/.config`：

```
$ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

这个命令会将**所有你用户跟 Plasma 有关的设置** 重命名为 *.bak (例如 `plasmarc.bak`)，并且当您重新登录 Plasma 时，您将恢复**默认**设置。若要撤销该操作，请删除.bak文件扩展名。若已有 *.bak 文件，请先重命名，移动或删除它们。强烈建议您经常备份。 有关可能的方案列表，请参阅[同步和备份程序（英文）](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")。

#### 清理缓存以解决升级故障

故障可能由旧的缓存导致。有时，升级后旧缓存可能会产生奇怪的、难以调试的行为，例如关不掉的 shell、改变设置时失去响应、以及像 ark 不能解压 rar/zip 文件又或者 amarok 不能识别音乐等各种其它问题。这个办法也能解决 KDE 和 Qt 程序在升级后变得难看的问题。

用以下命令来重建缓存：

```
$ rm ~/.config/Trolltech.conf
$ kbuildsycoca5 --noincremental

```

### 清理 akonadi 配置来修复 kmail

首先确保 KMail 不在运行。然后备份配置文件：

```
$ cp -a ~/.local/share/akonadi ~/.local/share/akonadi-old
$ cp -a ~/.config/akonadi ~/.config/akonadi-old

```

启动 *系统设置 > 个人信息* 并删除所有资源。回到 Dolphin 中移除原始的 `~/.local/share/akonadi` 和 `~/.config/akonadi` - 之前所作的备份能让你在必要时恢复它们。

现在回到 系统设置 页面并小心地添加必要的资源。你应该看到读取你邮件目录的资源。然后启动 Kontact/KMail 查看它是否正常运作。

### KMail 中空的 IMAP 收件箱

对于某些 IMAP 账户，kmail将把收件箱当作一个包含此帐户所有其他文件夹的容器显示。Kmail 不会在收件箱容器中显示消息，而是在所有其他子文件夹中显示消息，请参阅 [KDE Bug 284172](https://bugs.kde.org/show_bug.cgi?id=284172)。若要解决此问题，只需在kmail帐户设置中禁用服务器端订阅即可。

### 获取 KWin 的当前状态以进行支持和调试

这行命令输出了一份关于 KWin 当前状况的总结，包括使用的选项、混合（compositing）后端以及相关 OpenGL 驱动的能力。更多信息参见 [Martin的博客](http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/)

```
$ qdbus org.kde.KWin /KWin supportInformation

```

### KF5/Qt5 应用在 i3/fvwm/awesome 中不显示图标

参考 [Qt#Configuration of Qt5 apps under environments other than KDE Plasma](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma "Qt").

### 图形问题

请先确保您已安装了适合您 GPU 的驱动程序。有关详细信息，请参阅 [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg")。如果你的显卡较旧，你可以尝试 [#禁用桌面特效](#禁用桌面特效) 或 [#禁用混合项（compositing）](#禁用混合项（compositing）)。

#### 禁用桌面特效

Plasma 默认启用了桌面特效，并且不是所有的游戏都会自动禁用它们。你可以通过*系统设置 > 桌面特效* 禁用桌面特效。你也可以使用 `Alt+Shift+F12` 切换桌面效果。另外，您也可以在 *系统设置 > 窗口管理 > 窗口规则* 下创建自定义KWin规则，以在某个应用程序/窗口启动时自动禁用/启用混合项。

#### 禁用混合项（compositing）

在 *系统设置 > 显示*中取消选中*启动时激活混合器（compositing）*并重启 Plasma

#### 启用混合项（compositing）后全屏时闪烁

在 *系统设置 > 显示*中取消选中*允许应用程序阻止混合项（compositing）*。这可能会影响性能。

#### Nvidia 显卡屏幕撕裂

**提示：** 翻译人员使用，请无视本提示。英文页面本章搬到 NVIDIA/Troubleshooting 页面去了，但这页面中文没有，故中文保留此章

默认情况下，KWin 混合项在与 Nvidia 闭源驱动一起使用时会遭受屏幕撕裂。要解决此问题，运行 `kwin_x11 --replace` 并在其之前陈述环境变量 `export __GL_YIELD="USLEEP"`：

```
export __GL_YIELD="USLEEP" && kwin_x11 --replace

```

与使用全局环境变量不同，这只会影响 KWin，并不会降低其他 3D 应用程序的 CPU 性能。也可以通过在 Plasma 的 `~/.config/autostart-scripts` 文件夹中创建一个简单的脚本，使其在登录时自动执行。

 `~/.config/autostart-scripts/restartkwinusleep.sh` 
```
(sleep 2s &&
export __GL_YIELD="USLEEP" && kwin_x11 --replace
)

```

`sleep` 参数有助于防止 KWin 在登录后过早重新启动时出现问题，可以根据需要调整时间。 不要忘记将脚本标记为可执行文件。

#### Plasma 光标有时显示不正确

创建 `~/.icons/default` 目录并在其内创建一个包含以下内容的 `index.theme` 的文件：

 `/home/*archie*/.icons/default/index.theme` 
```
[Icon Theme]
Inherits=breeze_cursors
```

执行以下命令：

```
$ ln -s /usr/share/icons/breeze_cursors/cursors ~/.icons/default/cursors

```

### 声音问题

**注意:** 首先保证你已经安装了 [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)。

#### 睡眠后没声音

如果睡眠后没有声音并且 Kmix 没有显示应该显示的音频设备，可以尝试重新启动 plasmeshell 和 pulseaudio：

```
$ killall plasmashell
$ systemctl --user restart pulseaudio.service
$ plasmashell

```

某些应用程序也可能需要重新启动才能再次播放声音。

#### 在播放任何声音时出现 "返回默认" 消息

当你碰到这些消息：

```
The audio playback device *声音设备的名称* does not work.
Falling back to default

```

访问：

```
 系统设置 > 多媒体

```

并在每一栏中都把名称为 "**默认（default）**" 的设备设置在所有其它设备的上面。

#### 使用 GStreamer Phonon 后端时不能播放 MP3 文件

安装 GStreamer libav 插件（软件包[gst-libav](https://www.archlinux.org/packages/?name=gst-libav)）可以解决问题。如果仍然碰到，你可以尝试换一个软件包，例如 [phonon-qt4-vlc](https://aur.archlinux.org/packages/phonon-qt4-vlc/) 或 [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)。然后，请确保它是首选的后端，通过：

```
 系统设置 > 多媒体 > 后端

```

### Inotify 文件夹监控上限

如果收到以下错误:

```
KDE Baloo Filewatch service reached the inotify folder watch limit. File changes may be ignored.

```

您就需要增加 inotify 文件夹监控上限：

```
# echo 524288 > /proc/sys/fs/inotify/max_user_watches

```

永久设置可以创建文件`/etc/sysctl.d/40-max-user-watches.conf`：

```
#increase inotify watch limit
fs.inotify.max_user_watches = 524288

```

### 自动挂载NFS卷时卡死

对 [NFS](/index.php/NFS "NFS") 卷使用 [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") 可能导致卡死，见 [bug report upstream](https://bugs.kde.org/show_bug.cgi?id=354137).

### 没有挂起/休眠选项

如果你的系统可以使用 systemd 挂起/休眠，但 KDE 中没有这些选项，请确保 [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) 已被安装。

### 保存凭据和持续显示 KWallet 对话框的问题

不建议在用户设置中关闭 KWallet 密码保存系统，因为需要它为每个用户保存加密凭证（如WiFi密码）。持续显示的 KWallet 对话框可能是关闭它的后果。如果你嫌每当应用程序想要访问 Kwallet 时需要解锁烦，你可以让登录管理器 SDDM 和 LightDM 在登录时自动解锁 KWallet，请参阅 [KDE Wallet (简体中文)](/index.php/KDE_Wallet_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE Wallet (简体中文)")。第一个钱包需要由 KWallet 生成（而不是“用户生成”），以便用于系统程序凭据。如果你不希望让钱包凭据在内存内为每个应用打开，可以通过 [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) 在KWallet设置中限制应用程序访问它。如果您根本不关心凭证加密，您可以在创建钱包，KWallet 要求输入密码时，将密码留空。这样，应用程序将可以在不解锁钱包的情况下访问密码。

## 参见

*   [KDE 主页](https://www.kde.org/)
*   [KDE 缺陷跟踪页](https://bugs.kde.org/)
*   [Martin Graesslin 的博客](https://blog.martin-graesslin.com/blog/kategorien/kde/)