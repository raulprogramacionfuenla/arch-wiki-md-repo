**翻译状态：** 本文是英文页面 [ATI](/index.php/ATI "ATI") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-09，点击[这里](https://wiki.archlinux.org/index.php?title=ATI&diff=0&oldid=390492)可以查看翻译后英文页面的改动。

**ATI/AMD**显卡用户有两个选择：官方的专有驱动([catalyst](https://aur.archlinux.org/packages/catalyst/))和开源驱动([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati))。本文介绍开源驱动.

目前，开源驱动在新显卡的 3D 性能上不及官方专属版本，也缺乏TV输出等功能。但另一方面，它能更好地支持双显示，优秀的2D加速，为基于 OpenGL 的[窗口管理器](/index.php/Window_manager "Window manager")如 Mutter, KWin 或 [Compiz](/index.php/Compiz "Compiz") 提供了足够的 3D 加速。

如果你不确定该用哪种，请先试一试开源版的。开源驱动能满足大多数的需要，而且，一般来说遇到的麻烦也更少些。查看现在功能开发进展情况可访问 [功能矩阵](http://www.x.org/wiki/RadeonFeature)。

## Contents

*   [1 命名规范](#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83)
*   [2 概览](#.E6.A6.82.E8.A7.88)
*   [3 安装](#.E5.AE.89.E8.A3.85)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
*   [5 载入](#.E8.BD.BD.E5.85.A5)
    *   [5.1 早启动KMS](#.E6.97.A9.E5.90.AF.E5.8A.A8KMS)
*   [6 性能调整](#.E6.80.A7.E8.83.BD.E8.B0.83.E6.95.B4)
    *   [6.1 模块参数](#.E6.A8.A1.E5.9D.97.E5.8F.82.E6.95.B0)
    *   [6.2 关闭 PCI-E 2.0](#.E5.85.B3.E9.97.AD_PCI-E_2.0)
*   [7 混合交火](#.E6.B7.B7.E5.90.88.E4.BA.A4.E7.81.AB)
*   [8 节能](#.E8.8A.82.E8.83.BD)
    *   [8.1 老方法](#.E8.80.81.E6.96.B9.E6.B3.95)
        *   [8.1.1 动态频率调整](#.E5.8A.A8.E6.80.81.E9.A2.91.E7.8E.87.E8.B0.83.E6.95.B4)
        *   [8.1.2 基于计划的频率调整](#.E5.9F.BA.E4.BA.8E.E8.AE.A1.E5.88.92.E7.9A.84.E9.A2.91.E7.8E.87.E8.B0.83.E6.95.B4)
        *   [8.1.3 永久配置](#.E6.B0.B8.E4.B9.85.E9.85.8D.E7.BD.AE)
        *   [8.1.4 图形化工具](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E5.B7.A5.E5.85.B7)
    *   [8.2 动态电源管理](#.E5.8A.A8.E6.80.81.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [8.3 其它](#.E5.85.B6.E5.AE.83)
*   [9 TV输出（TV out）](#TV.E8.BE.93.E5.87.BA.EF.BC.88TV_out.EF.BC.89)
    *   [9.1 在KMS中强制TV输出](#.E5.9C.A8KMS.E4.B8.AD.E5.BC.BA.E5.88.B6TV.E8.BE.93.E5.87.BA)
*   [10 HDMI 音频输出](#HDMI_.E9.9F.B3.E9.A2.91.E8.BE.93.E5.87.BA)
*   [11 Dual Head setup](#Dual_Head_setup)
    *   [11.1 独立的 X screen](#.E7.8B.AC.E7.AB.8B.E7.9A.84_X_screen)
*   [12 启动视频加速](#.E5.90.AF.E5.8A.A8.E8.A7.86.E9.A2.91.E5.8A.A0.E9.80.9F)
*   [13 关闭垂直同步刷新](#.E5.85.B3.E9.97.AD.E5.9E.82.E7.9B.B4.E5.90.8C.E6.AD.A5.E5.88.B7.E6.96.B0)
*   [14 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [14.1 登录后出现Artifacts](#.E7.99.BB.E5.BD.95.E5.90.8E.E5.87.BA.E7.8E.B0Artifacts)
    *   [14.2 添加没有被侦测到的分辨率](#.E6.B7.BB.E5.8A.A0.E6.B2.A1.E6.9C.89.E8.A2.AB.E4.BE.A6.E6.B5.8B.E5.88.B0.E7.9A.84.E5.88.86.E8.BE.A8.E7.8E.87)
    *   [14.3 AGP被禁用(KMS启用)](#AGP.E8.A2.AB.E7.A6.81.E7.94.A8.28KMS.E5.90.AF.E7.94.A8.29)
    *   [14.4 电视屏幕显示黑边](#.E7.94.B5.E8.A7.86.E5.B1.8F.E5.B9.95.E6.98.BE.E7.A4.BA.E9.BB.91.E8.BE.B9)
    *   [14.5 从睡眠恢复后X显示一个黑屏,鼠标指针还在](#.E4.BB.8E.E7.9D.A1.E7.9C.A0.E6.81.A2.E5.A4.8D.E5.90.8EX.E6.98.BE.E7.A4.BA.E4.B8.80.E4.B8.AA.E9.BB.91.E5.B1.8F.2C.E9.BC.A0.E6.A0.87.E6.8C.87.E9.92.88.E8.BF.98.E5.9C.A8)
    *   [14.6 X1300上KDE4没有桌面特效](#X1300.E4.B8.8AKDE4.E6.B2.A1.E6.9C.89.E6.A1.8C.E9.9D.A2.E7.89.B9.E6.95.88)
    *   [14.7 KMS启用时,黑幕,没有控制台,但是 X 能够工作](#KMS.E5.90.AF.E7.94.A8.E6.97.B6.2C.E9.BB.91.E5.B9.95.2C.E6.B2.A1.E6.9C.89.E6.8E.A7.E5.88.B6.E5.8F.B0.2C.E4.BD.86.E6.98.AF_X_.E8.83.BD.E5.A4.9F.E5.B7.A5.E4.BD.9C)
    *   [14.8 2D 性能(比如滚动滑块)缓慢](#2D_.E6.80.A7.E8.83.BD.28.E6.AF.94.E5.A6.82.E6.BB.9A.E5.8A.A8.E6.BB.91.E5.9D.97.29.E7.BC.93.E6.85.A2)
    *   [14.9 显示器旋转对光标起效却对窗口/内容不起效](#.E6.98.BE.E7.A4.BA.E5.99.A8.E6.97.8B.E8.BD.AC.E5.AF.B9.E5.85.89.E6.A0.87.E8.B5.B7.E6.95.88.E5.8D.B4.E5.AF.B9.E7.AA.97.E5.8F.A3.2F.E5.86.85.E5.AE.B9.E4.B8.8D.E8.B5.B7.E6.95.88)
    *   [14.10 在ATI X1600 (RV530 series)上3D应用程序显示黑窗口](#.E5.9C.A8ATI_X1600_.28RV530_series.29.E4.B8.8A3D.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E6.98.BE.E7.A4.BA.E9.BB.91.E7.AA.97.E5.8F.A3)
    *   [14.11 从休眠中唤醒后光标崩溃](#.E4.BB.8E.E4.BC.91.E7.9C.A0.E4.B8.AD.E5.94.A4.E9.86.92.E5.90.8E.E5.85.89.E6.A0.87.E5.B4.A9.E6.BA.83)
    *   [14.12 多显示器模式下DisplayPort黑屏](#.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8.E6.A8.A1.E5.BC.8F.E4.B8.8BDisplayPort.E9.BB.91.E5.B1.8F)
    *   [14.13 Gallium HUD](#Gallium_HUD)

## 命名规范

[Radeon](https://en.wikipedia.org/wiki/Radeon "wikipedia:Radeon")品牌遵循这样的命名规则:每个产品关联与某个市场分段.这篇文章中读者将会见到*产品*名(比如 HD 4850, X1900)与*代码*或者*核心*名(比如 RV770, R580). 传统地, 一个*产品系列*将匹配一个*核心系列* (比如产品系列 "X1000" 包含 X1300, X1600, X1800, 和 X1900 ,他们的核心系列是"R500" – 包含 RV515, RV530, R520, 和 R580 核心).

具体对应关系可以查看维基百科： [Wikipedia:Comparison of AMD graphics processing units](https://en.wikipedia.org/wiki/Comparison_of_AMD_graphics_processing_units "wikipedia:Comparison of AMD graphics processing units").

## 概览

`xf86-video-ati`(**radeon**) 驱动：

*   支持至 Radeon HD 6xxx 和 7xxxM 显卡系列（“北方群岛” 系列显卡）。
    *   HD 77xx (南方群岛系列)已大部分支持.查看[功能矩阵](http://www.x.org/wiki/RadeonFeature)以了解不受支持的功能.
    *   Radeons X1xxx 以及之前的显卡系列，拥有稳定、完整的功能以及2D、3D加速功能。
    *   Radeons HD 2xxx 到 HD 6xxx系列具备完整2D加速和较好的3D加速功能，但相比ati官方驱动，功能仍然不全(比如, powersaving仍然处于测试阶段)。
*   支持 DRI1, RandR 1.2/1.3/1.4, Glamor, EXA 加速 和 [kernel mode-setting](/index.php/KMS "KMS")/DRI2.

一般来说，**xf86-video-ati** 应该是是你的首选，无论你用什么ATI/AMD卡。当然如果你使用的是最新的AMD显卡，你可能更喜欢 **catalyst** 驱动。

**注意:** xf86-video-ati 驱动在Xorg (`xorg.conf`) 被识别为 "**radeon**"

## 安装

**注意:** 如果你之前安装过私有驱动(catalyst)，请参见[这里](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.8D.B8.E8.BD.BD "AMD Catalyst (简体中文)")来卸载

[安装](/index.php/Install "Install")软件包[xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati).它为2D加速提供DDX驱动,而作为其依赖的[mesa](https://www.archlinux.org/packages/?name=mesa)提供DRI支持和3D加速.(It provides the DDX driver for 2D acceleration and it pulls in [mesa](https://www.archlinux.org/packages/?name=mesa) as a dependency, providing the DRI driver for 3D acceleration.)

为了获得OpenGL支持，还需安装 [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl)。若需要x86_64下的32位支持,可以从[multilib](/index.php/Multilib "Multilib")安装[lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl).

[加速视频解码](#.E5.90.AF.E5.8A.A8.E8.A7.86.E9.A2.91.E5.8A.A0.E9.80.9F) 由 [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) 和 [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) 包提供支持。

## 配置

Xorg 会自动装入驱动并通过 EDID 获得显示器分辨率，只有性能优化时才需要额外配置。

如果要手动配置，请添加文件 `/etc/X11/xorg.conf.d/20-radeon.conf`, 并加入：

```
Section "Device"
    Identifier "Radeon"
    Driver "radeon"
EndSection

```

通过此段可以调整显卡的设置。

## 载入

radeon模块应该在启动时被正常载入.

要是没有的话...

*   确保 [内核参数](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)") 中**没有** `nomodeset` 或 `vga=`,因为现在 radeon 需要 [KMS](/index.php/Kernel_Mode_Setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel Mode Setting (简体中文)").
*   另外,检查 `/etc/modprobe.d/` 或 `/usr/lib/modprobe.d/` 以确保radeon模块没有被禁用.

### 早启动KMS

**小贴士:** 若分辨率有问题,试试[强设模式](/index.php/Kernel_Mode_Setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.BC.BA.E8.AE.BE.E6.A8.A1.E5.BC.8F "Kernel Mode Setting (简体中文)")也许可以解决.

radeon支持(并且现在强制需要)[Kernel Mode Setting](/index.php/Kernel_Mode_Setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel Mode Setting (简体中文)")(KMS).KMS默认启用.

KMS一般在[载入initramfs](/index.php/Arch_Boot_Process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#initramfs "Arch Boot Process (简体中文)")后初始化.不过,也可以在载入initramfs时启用KMS:将 `radeon` 模块添加到 `/etc/mkinitcpio.conf` 的 `MODULES` 列:

```
MODULES="... radeon ..."

```

重生成initramfs:

```
# mkinitcpio -p linux

```

下次重启生效.

## 性能调整

下面这些选项属于`/etc/X11/xorg.conf.d/**20-radeon.conf**`.

**ColorTiling** 是绝对安全的,并且默认被启用. 大多数用户能注意到性能的提升,但是这个功能R200及更早的显卡不支持. 早的显卡虽可以启用,但是工作负担转移到了cpu上

```
Option "ColorTiling" "on"

```

**Acceleration architecture**; Glamor是一种使用OpenGL的 2D加速方式，适用于R300及以上显卡驱动。 自xf86-video-ati版本1:7.2.0-1后, 在radeonsi(南方群岛系列 和 superior GFX 显卡)上glamor默认启用; 在其他显卡上想启用的话,添加 AccelMethod **glamor** 到配置文件:

```
Option "AccelMethod" "Glamor"

```

**Page Flip** 一般来说是安全的. 老显卡可以启用这个功能,不过这样将会禁用EXA. 最近的驱动可以使这项功能和EXA都启用.

```
Option "EnablePageFlip" "on"

```

**EXAVSync** 选项试图通过stalling the engine until the display controller has passed the destination region来避免撕裂。在开启了Xv overlay视频选项的3D加速桌面非常有用，使用KMS时则没有必要。

```
Option "EXAVSync" "yes"

```

下面是一个简单的配置文件示例： `/etc/X11/xorg.conf.d/**20-radeon.conf**`:

```
Section "Device"
	Identifier  "My Graphics Card"
	Driver	"radeon"
	Option	"SWcursor"              "off" #software cursor might be necessary on some rare occasions, hence set off by default
	Option	"AccelMethod"           "Glamor" #valid options are XAA, EXA and Glamor. Default value varies per-GPU.
	#Option	"EXAVSync"              "off" #default is off, otherwise on. Only works **if EXA activated**
	#Option	"EXAPixmaps"            "on"  #when on icreases 2D performance, but may also cause artifacts on some old cards. Only works **if EXA activated**
	Option	"AccelDFS"              "on"  #default is off, because it can give problems with some PCI-e/AGP cards (artefacts, corruption, etc.)
EndSection

```

**小贴士:** [driconf](https://www.archlinux.org/packages/?name=driconf) 是一个可以修改诸多设置的小工具，如 vsync, anisotropic filtering, texture compression 等。它还有一些程序（比如Goole Earth）需要的"disable Low Impact fallback"功能。

### 模块参数

应用模块参数前请阅读 `man radeon` 与 [RadeonFeature](http://www.x.org/wiki/RadeonFeature/#index4h2) 。

这些[内核参数](/index.php/Kernel_parameters "Kernel parameters")可能会有用：`radeon.bapm=1` [[1]](https://www.phoronix.com/scan.php?page=news_item&px=MTczMzI), `radeon.disp_priority=2` [[2]](http://lists.freedesktop.org/pipermail/xorg/2013-February/055477.html), `radeon.hw_i2c=1` [[3]](https://superuser.com/questions/723760/does-radeon-hw-i2c-1-has-any-thing-to-do-with-temperature-readings), `radeon.mst=1` [[4]](https://www.phoronix.com/scan.php?page=news_item&px=Linux-4.1-Radeon-DP-MST), `radeon.msi=1` (强制启用 MSI 支持), `radeon.audio=0` (强制禁用 GPU 音频) 和/或 `radeon.tv=0` (禁用 TV-out).

使用 `systool` 来调试模块参数，参阅 [Kernel_modules#Obtaining_information](/index.php/Kernel_modules#Obtaining_information "Kernel modules")：

 `$ systool -v -m radeon` 
```
  Parameters:
    agpmode             = "0"
    aspm                = "-1"
    audio               = "-1"
    auxch               = "-1"
    backlight           = "-1"
    bapm                = "-1"
    benchmark           = "0"
    connector_table     = "0"
    deep_color          = "0"
    disp_priority       = "0"
    dpm                 = "-1"
    dynclks             = "-1"
    fastfb              = "0"
    hard_reset          = "0"
    hw_i2c              = "0"
    lockup_timeout      = "10000"
    msi                 = "-1"
    mst                 = "0"
    no_wb               = "0"
    pcie_gen2           = "-1"
    r4xx_atom           = "0"
    runpm               = "-1"
    test                = "0"
    tv                  = "1"
    use_pflipirq        = "2"
    vm_block_size       = "12"
    vm_size             = "8"
```

如果**gartsize**没有自动检测到，可以通过向[内核参数](/index.php/Kernel_parameters "Kernel parameters")添加`radeon.gartsize=32`来实现，单位是Mb，对于RV280显卡是32M。

**注意：** 对于新的AMD显卡不再需要设置这个参数：

```
[drm] Detected VRAM RAM=2048M, BAR=256M
[drm] radeon: 2048M of VRAM memory ready
[drm] radeon: 2048M of GTT memory ready.

```

### 关闭 PCI-E 2.0

从3.6版内核开始，radeon里PCI-E v2.0选项默认启用。

对一些主板可能不稳定，可以向[内核参数](/index.php/Kernel_parameters "Kernel parameters")添加 `radeon.pcie_gen2=0` 来关闭。

参考 [Phoronix 文章](http://www.phoronix.com/scan.php?page=article&item=amd_pcie_gen2&num=1)

## 混合交火

这是一项通常在配备了双显卡——一块比较节能（比如Intel的核芯显卡），另一块为高性能、高能耗（Radeon或NVIDIA）的笔记本上启用的特性。有两种方法可以启用它：

*   如果不需要运行很吃GPU的程序，可以禁用独立显卡（参见[Ubuntu wiki](https://help.ubuntu.com/community/HybridGraphics#Using_vga_switcheroo) ）： `echo OFF > /sys/kernel/debug/vgaswitcheroo/switch`。
*   [PRIME](/index.php/PRIME "PRIME")是在Linux系统中使用双显卡切换的正确方式，但仍然需要用户进行大量手动设置。

## 节能

**注意:** 所有vbios中包含有适当电源状态表的显卡芯片（R1xx 及更新的）都支持电源管理。"dpm"仅在 R6xx 以及更新的芯片上被支持。

开源驱动的节电功能默认关闭,需要可手动启用.

三种方法可供选择:

1.  [dynpm](#.E5.8A.A8.E6.80.81.E9.A2.91.E7.8E.87.E8.B0.83.E6.95.B4)
2.  [profile](#.E5.9F.BA.E4.BA.8E.E8.AE.A1.E5.88.92.E7.9A.84.E9.A2.91.E7.8E.87.E8.B0.83.E6.95.B4)
3.  [dpm](#.E5.8A.A8.E6.80.81.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)(3.13内核后默认启用)

**不好说哪个方法对你最合适，你该自己试试。**

详见 [http://www.x.org/wiki/RadeonFeature/#index3h2](http://www.x.org/wiki/RadeonFeature/#index3h2) .

### 老方法

#### 动态频率调整

此方法根据GPU负载自动改变时钟频率，所以GPU忙碌时显示性能提高，空闲时降低。自动变频试图在垂直消隐期间进行，但由于变频函数可能在周期内无法完成，这种方法可能导致显示闪烁。因此，动态调整只能在单显示器下正常工作。

可以通过以下命令启用：

```
# echo dynpm > /sys/class/drm/card0/device/power_method

```

#### 基于计划的频率调整

该方法允许你选择5种不同的计划。主要来说,不同的计划最终都改变GPU时钟频率和电压。这种方式不同于积极方式,但更稳定,少闪屏,而且可用于多显示器环境

要激活此方法，可运行以下命令：

```
# echo profile > /sys/class/drm/card0/device/power_method

```

可选的计划：

*   `default` 使用默认时钟频率，不改变电源状态。这是默认启用的计划。
*   `auto` 根据系统是否使用电池，在电源状态 `mid` 和 `high` 间自动切换
*   `low` 强制GPU运行于`low`电源状态.注意`low`在某些笔记本上可能导致显示问题, 如`auto` 计划在显示器关闭时只选中`low`.(Note that `low` can cause display problems on some laptops, which is why `auto` only uses `low` when monitors are off. ) 在其他计划中,当显示器进入节能状态时,将自动切换为 `low` 计划
*   `mid` 强制GPU运行于`mid`电源状态.
*   `high` 强制GPU运行于`high`电源状态.

例如，我们可以激活`low` 计划(你可以根据需要替换为上述其他计划):

```
# echo low > /sys/class/drm/card0/device/power_profile

```

#### 永久配置

上述方法不是永久性的，系统重启后将丢失。为了让它一直有效，你可以使用[systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd") (例如 [#Dynamic frequency switching](#Dynamic_frequency_switching)):

 `/etc/tmpfiles.d/radeon-pm.conf` 
```
w /sys/class/drm/card0/device/power_method - - - - dynpm

```

你也可以使用[udev](/index.php/Udev "Udev")规则替代 (例如 [#Profile-based frequency switching](#Profile-based_frequency_switching)):

 `/etc/udev/rules.d/30-radeon-pm.rules` 
```
KERNEL=="dri/card0", SUBSYSTEM=="drm", DRIVERS=="radeon", ATTR{device/power_method}="profile", ATTR{device/power_profile}="low"

```

**注意:** 如果上述规则失效，你可以试试删除 `dri/` 前辍.

KERNEL=="card0", SUBSYSTEM=="drm", DRIVERS=="radeon", ATTR{device/power_method}="profile",

#### 图形化工具

*   **Radeon-tray** — 通过状态栏图标控制配置方式的小工具。基于PyQt4编写，适合非gnome桌面的用户。

	[https://github.com/StuntsPT/Radeon-tray](https://github.com/StuntsPT/Radeon-tray) || [radeon-tray](https://aur.archlinux.org/packages/radeon-tray/)

*   **power-play-switcher** — 控制开源Radeon驱动电源的小工具

	[https://code.google.com/p/power-play-switcher/](https://code.google.com/p/power-play-switcher/) || [power-play-switcher](https://aur.archlinux.org/packages/power-play-switcher/)

*   **Gnome-shell-extension-Radeon-Power-Profile-Manager** — gnome-shell扩展，允许你改变开源Radeon驱动的电源配置方式

	[https://github.com/StuntsPT/shell-extension-radeon-power-profile-manager](https://github.com/StuntsPT/shell-extension-radeon-power-profile-manager) || [gnome-shell-extension-radeon-ppm](https://aur.archlinux.org/packages/gnome-shell-extension-radeon-ppm/) [gnome-shell-extension-radeon-power-profile-manager-git](https://aur.archlinux.org/packages/gnome-shell-extension-radeon-power-profile-manager-git/)

### 动态电源管理

从3.13内核开始,在[很多AMD Radeon设备](http://kernelnewbies.org/Linux_3.13#head-f95c198f6fdc7defe36f470dc8369cf0e16898df)上DPM默认启用。如果要禁用可加入参数 `radeon.dpm=0` 到 [kernel parameters](/index.php/Kernel_parameters "Kernel parameters")。

不像[dynpm](#.E5.8A.A8.E6.80.81.E9.A2.91.E7.8E.87.E8.B0.83.E6.95.B4)，“dpm"方式根据GPU负载情况动态调整时钟频率和电压，同时它会启用频率和电压门控.

dpm有3种模式可选:

*   `battery` 最节能
*   `balanced` 默认
*   `performance` 最佳性能

可以通过sysfs来更改dpm的模式,如下:

```
# echo battery > /sys/class/drm/card0/device/power_dpm_state

```

你也许想要强制显卡工作在某一性能等级下:

*   `auto` 默认; 使用当前dpm模式限定的所有性能等级
*   `low` 强制在最低性能
*   `high` 强制在最高性能

```
# echo low > /sys/class/drm/card0/device/power_dpm_force_performance_level

```

### 其它

要查看当前GPU频率，可以运行如下命令，你可以看到类似如下输出：

 `# cat /sys/kernel/debug/dri/0/radeon_pm_info` 
```
  state: PM_STATE_ENABLED
  default engine clock: 300000 kHz
  current engine clock: 300720 kHz
  default memory clock: 200000 kHz

```

It depends on which GPU line yours is, however. Along with the radeon driver versions, kernel versions, etc. So it may not have much/any voltage regulation at all.

Thermal sensors are implemented via external i2c chips or via the internal thermal sensor (rv6xx-evergreen only). To get the temperature on asics that use i2c chips, you need to load the appropriate hwmon driver for the sensor used on your board (lm63, lm64, etc.). The drm will attempt to load the appropriate hwmon driver. On boards that use the internal thermal sensor, the drm will set up the hwmon interface automatically. When the appropriate driver is loaded, the temperatures can be accessed via [lm_sensors](/index.php/Lm_sensors "Lm sensors") tools or via sysfs in `/sys/class/hwmon`.

## TV输出（TV out）

首先，检查你有S-video输出：`xrandr`应该会给你类似如下的结果：

```
Screen 0: minimum 320x200, current 1024x768, maximum 1280x1200
...
S-video disconnected (normal left inverted right x axis y axis)

```

现在我们应该告诉Xorg它已经接上了 (本来就是,对吧)

```
xrandr --output S-video --set "load detection" 1

```

设定TV制式标准

```
xrandr --output S-video --set "tv standard" ntsc

```

为它添加一个分辨率（目前只支持800x600）

```
xrandr --addmode S-video 800x600

```

复制模式（clone mode)

```
xrandr --output S-video --same-as VGA-0

```

好了，让我们来看看效果吧

```
xrandr --output S-video --mode 800x600

```

这时，在电视上你应该能看到你的桌面，分辨率是800x600。

要关掉这一输出：

```
xrandr --output S-video --off

```

你可能还发现视频只在显示器上播放，而电视上没有。XV_CRTC属性控制着Xv overlay的输出方向。

把输出指向电视：

```
xvattr -a XV_CRTC -v 1

```

**Note:** you need to install [xvattr](https://aur.archlinux.org/packages/xvattr/) to execute this command.

要切换回显示器，把`1`改成`0`。`-1`应用于双头显示（dual head)设置中的自动切换。

Please see [Enabling TV-Out Statically](http://www.x.org/wiki/radeonTV) for how to enable TV-out in your xorg configuration file.

### 在KMS中强制TV输出

内核可识别下列格式的 `video=` 参数 （参见[KMS](/index.php/KMS "KMS")）：

```
video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

例如：

```
video=DVI-I-1:1280x1024-24@60e

```

带有空格的参数必须用引号括起：

```
"video=9-pin DIN-1:1024x768-24@60e"

```

Current mkinitcpio implementation also requires `#` in front. For example:

```
root=/dev/disk/by-uuid/d950a14f-fc0c-451d-b0d4-f95c2adefee3 ro quiet radeon.modeset=1 security=none # video=DVI-I-1:1280x1024-24@60e "video=9-pin DIN-1:1024x768-24@60e"

```

*   Grub 可直接接受如上参数。
*   Lilo 需要在双引号前使用“\”转义 (例如 `# \"video=9-pin DIN-1:1024x768-24@60e\"`)
*   Grub2: TODO

You can get list of your video outputs with following command:

 `$ ls -1 /sys/class/drm/ | grep -E '^card[[:digit:]]+-' | cut -d- -f2-` 

## HDMI 音频输出

HDMI音频输出在 [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) 软件包中提供支持。由于可能引发一些问题，在 Linux内核版本 >=3.0 中默认禁用了HDMI音频输出。要启用它，在 [内核参数](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)") 中添加 `radeon.audio=1` 。

如果启动后没有视频输出，则请禁用这个参数。

**注意:**

*   如果在安装驱动后HDMI音频没有工作，请使用 [这里](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#HDMI_.E8.BE.93.E5.87.BA.E6.97.A0.E6.95.88 "Advanced Linux Sound Architecture (简体中文)") 中提供的方法进行检测。
*   如果在PulseAudio中声音出现问题，尝试设置 `tsched=0` （参见 [PulseAudio/Troubleshooting#Glitches, skips or crackling](/index.php/PulseAudio/Troubleshooting#Glitches.2C_skips_or_crackling "PulseAudio/Troubleshooting")） 并确保 `rtkit` 守护进程正在运行。
*   Your sound card might use the same module, since HDA compliant hardware is pretty common. [Change the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture") using one of the suggested methods, which include using the `defaults` node in alsa configuration.

## Dual Head setup

### 独立的 X screen

独立的双显示器可以按正常方式配置，radeon 驱动有一个 `"ZaphodHeads"` 选项可以把显示的区域绑定到固定的设备，例如：

```
       Section "Device"
       Identifier     "Device0"
       Driver         "radeon"
       Option         "ZaphodHeads"   "VGA-0"
       VendorName     "ATI"
       BusID          "PCI:1:0:0"
       Screen          0
       EndSection

```

有些设备有多个输出(HDMI, DVI 和 VGA)，但是双屏显示的时候只使用其中的某两个组合例如 HDMI+DVI，所以需要通过 `"ZaphodHeads" "VGA-0"` 更改输出设备。

## 启动视频加速

[mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) 包已为开源驱动带来MPEG1/2的硬件解码支持，安装 [libvdpau](https://www.archlinux.org/packages/?name=libvdpau) 后将自动启用。

要是它不会自动使用的话,你也可以通过声明环境变量 `LIBVA_DRIVER_NAME` 为 `vdpau` 和 `VDPAU_DRIVER` 为对应驱动来强制启用，例如：

 `~/.bashrc` 
```
export LIBVA_DRIVER_NAME=vdpau
export VDPAU_DRIVER=r600
```

这用于基于 r600 系列及以上的显卡（所有可用VDPAU 驱动位于 `/usr/lib/vdpau/` 目录下找到）。

如果你拥有一块[南方群岛](https://en.wikipedia.org/wiki/Radeon_HD_7000_Series "wikipedia:Radeon HD 7000 Series")(HD 7XXX) 或者更高的显卡，`VDPAU_DRIVER`变量应该设置成`radeonsi`：

 `~/.bashrc`  `export VDPAU_DRIVER=radeonsi` 

使用 `vainfo` 来验证新设置：

 `$ vainfo` 
```
libva info: VA-API version 0.38.0
libva info: va_getDriverName() returns 0
libva info: User requested driver 'vdpau'
libva info: Trying to open /usr/lib/dri/vdpau_drv_video.so
libva info: Found init function __vaDriverInit_0_35
libva info: va_openDriver() returns 0
vainfo: VA-API version: 0.38 (libva 1.6.0)
vainfo: Driver version: Splitted-Desktop Systems VDPAU backend for VA-API - 0.7.4
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            :	VAEntrypointVLD
      VAProfileMPEG2Main              :	VAEntrypointVLD
      VAProfileMPEG4Simple            :	VAEntrypointVLD
      VAProfileMPEG4AdvancedSimple    :	VAEntrypointVLD
      VAProfileH264Baseline           :	VAEntrypointVLD
      VAProfileH264Main               :	VAEntrypointVLD
      VAProfileH264High               :	VAEntrypointVLD
      VAProfileVC1Advanced            :	VAEntrypointVLD
```

## 关闭垂直同步刷新

radeon驱动默认启用垂直同步刷新，除了跑分外各种情况下工作良好。要关闭它，可以创建 `~/.drirc` （如果已存在请修改），加入以下部分 :

 `~/.drirc` 
```
<driconf>
    <device screen="0" driver="dri2">
        <application name="Default">
            <option name="vblank_mode" value="0" />
        </application>
    </device>
    <!-- Other devices ... -->
</driconf>

```

请确保是 **dri2** , 而不是你的显卡型号（如 r600 ）。

## 故障排除

### 登录后出现Artifacts

如果遇到了artifacts, 先试试不用`/etc/X11/xorg.conf`启动X. 最近版本的Xorg有可靠的自动检测/配置能力.过时或者不当的 `xorg.conf` 会导致问题.

不以配置文件启动时,推荐先安装`xorg-input-drivers`软件包组.

你也可以试着禁用 `EXAPixmaps`.在`/etc/X11/xorg.conf.d/20-radeon.conf`中:

```
Section "Device"
    Identifier "Radeon"
    Driver "radeon"
    Option "EXAPixmaps" "off"
EndSection

```

若想进一步地调整,还可以禁用 `AccelDFS`:

```
Option "AccelDFS" "off"

```

### 添加没有被侦测到的分辨率

参见[Xrandr的文章](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### AGP被禁用(KMS启用)

如果性能很差,dmesg也有如下信息

```
[drm:radeon_agp_init] *ERROR* Unable to acquire AGP: -19

```

那么检查针对你主板的agp驱动(如 `via_agp`, `intel_agp` 等)是否在 `radeon` 前被加载, 参见 [#启用 KMS](#.E5.90.AF.E7.94.A8_KMS).

### 电视屏幕显示黑边

我的Radeon HD 5770用HDMI连接到电视时, 电视显示图像模糊,周围有2-3cm黑边,用催化剂时不是这样. 这是对付过扫描(Overscan)的(参见[Wikipedia:Overscan](https://en.wikipedia.org/wiki/Overscan "wikipedia:Overscan")),使用xrandr关闭它:

```
xrandr --output HDMI-0 --set underscan off

```

### 从睡眠恢复后X显示一个黑屏,鼠标指针还在

32MB或者更低的卡可能会有这个问题. 鼠标指针移动过的区域可能会被重绘.在 `/etc/X11/xorg.conf.d/20-radeon.conf` 中强制`EXAPixmaps` 为 `"enabled"` 可能能解决此问题.参见[#性能调整](#.E6.80.A7.E8.83.BD.E8.B0.83.E6.95.B4) .

### X1300上KDE4没有桌面特效

KDE4的一个问题可能使视频硬件检测不准确,因此禁用了桌面特效,即使X1300的GPU有足够的能力. 一个可行的办法是,禁用掉KDE的检测,在`/usr/share/kde-settings/kde-profile/default/share/config/kwinrc` 和/或 `.kde/share/config/kwinrc`中

添加

```
DisableChecks=true 

```

到 [Compositing] 部分. 确保compositing是启用的:

```
Enabled=true

```

### KMS启用时,黑幕,没有控制台,但是 X 能够工作

当在同一台PC使用两张或以上的ATI显卡时可能会遇到此问题. 例如 Fujitsu Siemens Amilo PA 3553 笔记本就有这个问题. 这是因为fbcon控制台驱动程序映射自己到已存在于错误的显卡的framebuffer设备上(This is due to fbcon console driver mapping itself to wrong framebuffer device that exist on the wrong card). 在内核参数添加:

```
fbcon=map:1

```

这将告诉fbcon映射自己到 `/dev/fb1` 而不是 `/dev/fb0`.如果这并未解决你的问题，尝试如下配置启动:

```
fbcon=map:0

```

### 2D 性能(比如滚动滑块)缓慢

如果2D性能(比如在终端或浏览器的滚动滑块)有问题, 你可以将 `Option "MigrationHeuristic" "greedy"` 添加到你的 `xorg.conf` 文件的 `**Device**` 部分.

**注意:** 仅适用于EXA。

这是一个样例 `/etc/X11/xorg.conf.d/**20-radeon.conf**`:

```
Section "Device"
        Identifier  "My Graphics Card"
        Driver  "radeon"
        Option  "MigrationHeuristic"  "greedy"
EndSection

```

### 显示器旋转对光标起效却对窗口/内容不起效

启用EXA代替glamor的新显卡用户可能会发现,用xrandr旋转显示器将导致光标和显示器尺寸旋转了,但窗口与里面内容却保持原来方向. 另外移动鼠标时光标按照原来的方向移动.若有此问题,在你的 `/var/log/Xorg.0.log` 中查找下面这一行:

```
(EE) RADEON(0): Rotation requires acceleration!

```

新显卡上使用EXA时加速将被禁用(来源: [这里](https://bugs.freedesktop.org/show_bug.cgi?id=73420#c17)). 你必须从启用EXA ([参见这里](#Glamor)) 和旋转中二选一.

### 在ATI X1600 (RV530 series)上3D应用程序显示黑窗口

这三种方法可能有效:

*   将 `pci=nomsi` 添加到你的启动器的 [内核参数](/index.php/Kernel_parameters "Kernel parameters").
*   如果没用的话,试试用`noapic`代替`pci=nomsi`.
*   如果还是没用,你可以试试`vblank_mode=0 glxgears` 或者 `vblank_mode=1 glxgears`,看看哪个对你有用. 然后安装[driconf](https://www.archlinux.org/packages/?name=driconf) , 在`~/.drirc`里设置此参数.

### 从休眠中唤醒后光标崩溃

如果显示器唤醒后光标垂直方向重复刷新，可以在xorg的配置文件的"Device"部分中将"SWCursor"设置成"true".

### 多显示器模式下DisplayPort黑屏

尝试以[内核参数](/index.php/Kernel_parameter "Kernel parameter") `radeon.audio=0` 启动。

### Gallium HUD

radeon 支持激活一个HUD，来显示透明的图像及文字于正在渲染的程序（如游戏）之上。可以显示当前帧率，每个CPU核心负载或者CPU负载平均值。这个HUD受 GALLIUM_HUD 环境变量控制，可以添加一些参数如：

*   "fps" - 显示当前帧率
*   "cpu" - 显示平均CPU负载
*   "cpu0" - 显示第一个CPU核心负载
*   "cpu0+cpu1" - 显示前两个CPU核心负载
*   "draw-calls" - 显示一个物体的每个材质被显示到屏幕上多少次(displays how many times each material in an object is drawn to the screen）
*   "requested-VRAM" - 显示GPU的VRAM使用量
*   "pixels-rendered" - 显示正在显示的像素计数

关于参数的完整列表以及操作GALLIUM_HUD的一些注意事项，你可以添加"help"参数运行一个简单程序（如glxgears）来查看相应的终端输出。

 `# GALLIUM_HUD="help" glxgears` 

更多信息参见 [邮件列表页面](http://lists.freedesktop.org/archives/mesa-dev/2013-March/036586.html) 或 [这篇博客](https://kparal.wordpress.com/2014/03/03/fraps-like-fps-overlay-for-linux/).