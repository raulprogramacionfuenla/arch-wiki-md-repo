相关文章

*   [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")
*   [Nouveau (简体中文)](/index.php/Nouveau_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Nouveau (简体中文)")
*   [NVIDIA (简体中文)](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)")
*   [Intel图形卡](/index.php/Intel_Graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel Graphics (简体中文)")

**翻译状态：** 本文是英文页面 [Bumblebee](/index.php/Bumblebee "Bumblebee") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-12-01，点击[这里](https://wiki.archlinux.org/index.php?title=Bumblebee&diff=0&oldid=359259)可以查看翻译后英文页面的改动。

引自 Bumblebee [FAQ](https://github.com/Bumblebee-Project/Bumblebee/wiki/FAQ):

"*Bumblebee 致力于使 NVIDIA Optimus 在 GNU/Linux 系统上可用，实现两块不同的供电配置的显卡同时插入使用，共享同一个 framebuffer。*"

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Bumblebee: Linux上的 Optimus](#Bumblebee:_Linux上的_Optimus)
*   [2 安装](#安装)
*   [3 用法](#用法)
    *   [3.1 测试](#测试)
    *   [3.2 一般用法](#一般用法)
*   [4 配置](#配置)
    *   [4.1 速度优化](#速度优化)
        *   [4.1.1 使用VirtualGL作为桥接](#使用VirtualGL作为桥接)
        *   [4.1.2 Primusrun](#Primusrun)
    *   [4.2 电源管理](#电源管理)
        *   [4.2.1 使用bbswitch时默认的 NVIDIA 电源状态](#使用bbswitch时默认的_NVIDIA_电源状态)
        *   [4.2.2 关机时启用NVIDIA显卡](#关机时启用NVIDIA显卡)
    *   [4.3 多显示器](#多显示器)
        *   [4.3.1 显示器连接在 Intel 显卡上](#显示器连接在_Intel_显卡上)
        *   [4.3.2 显示器连接在 NVIDIA 显卡上](#显示器连接在_NVIDIA_显卡上)
            *   [4.3.2.1 xf86-video-intel-virtual-crtc 和 hybrid-screenclone](#xf86-video-intel-virtual-crtc_和_hybrid-screenclone)
*   [5 如 Windows 一般在集显和独显间切换](#如_Windows_一般在集显和独显间切换)
*   [6 不依赖Bumblebee来使用CUDA](#不依赖Bumblebee来使用CUDA)
*   [7 疑难问题](#疑难问题)
    *   [7.1 [VGL] ERROR: Could not open display :8](#[VGL]_ERROR:_Could_not_open_display_:8)
    *   [7.2 Xlib: extension "GLX" missing on display ":0.0"](#Xlib:_extension_"GLX"_missing_on_display_":0.0")
    *   [7.3 [ERROR]Cannot access secondary GPU: No devices detected](#[ERROR]Cannot_access_secondary_GPU:_No_devices_detected)
        *   [7.3.1 NVIDIA(0): Failed to assign any connected display devices to X screen 0](#NVIDIA(0):_Failed_to_assign_any_connected_display_devices_to_X_screen_0)
        *   [7.3.2 systemd-logind: failed to get session: PID XXX does not belong to any known session](#systemd-logind:_failed_to_get_session:_PID_XXX_does_not_belong_to_any_known_session)
        *   [7.3.3 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_(GPU_fallen_off_the_bus_/_RmInitAdapter_failed!))
        *   [7.3.4 Could not load GPU driver](#Could_not_load_GPU_driver)
        *   [7.3.5 NOUVEAU(0): [drm] failed to set drm interface version](#NOUVEAU(0):_[drm]_failed_to_set_drm_interface_version)
    *   [7.4 [ERROR]Cannot access secondary GPU - error: X did not start properly](#[ERROR]Cannot_access_secondary_GPU_-_error:_X_did_not_start_properly)
    *   [7.5 /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied](#/dev/dri/card0:_failed_to_set_DRM_interface_version_1.4:_Permission_denied)
    *   [7.6 ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored](#ERROR:_ld.so:_object_'libdlfaker.so'_from_LD_PRELOAD_cannot_be_preloaded:_ignored)
    *   [7.7 Fatal IO error 11 (Resource temporarily unavailable) on X server](#Fatal_IO_error_11_(Resource_temporarily_unavailable)_on_X_server)
    *   [7.8 视频撕裂](#视频撕裂)
    *   [7.9 Bumblebee cannot connect to socket](#Bumblebee_cannot_connect_to_socket)
    *   [7.10 Running X.org from console after login (rootless X.org)](#Running_X.org_from_console_after_login_(rootless_X.org))
    *   [7.11 Primusrun 鼠标延迟/禁用 VSYNC](#Primusrun_鼠标延迟/禁用_VSYNC)
*   [8 另见](#另见)

## Bumblebee: Linux上的 Optimus

[Optimus 技术](http://www.nvidia.cn/object/optimus_technology_cn.html) 是不依赖于硬件复杂结构的 *[交火显卡](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics) *实现。独立显卡按需渲染，并传输给集成显卡，集成显卡则负责显示功能。当笔记本通过电池供电时，独立显卡将关闭，以延长电池寿命。在使用 Intel 集成显卡和 NVIDIA 独立显卡的台式机上也能使用这项技术。

Bumblebee 通过软件来实现它的功能，包括两个部分：

*   利用独立显卡渲染程序，并通过集成显卡将图像显示在屏幕上。这是利用 VirtualGL 或 primus （见后面小节）实现的，相当于连接到了一个供独立显卡使用的 X 服务器。
*   独立显卡空闲的时候会被禁用。（参见 [#电源管理](#电源管理) ）

Bumblebee 试图模拟 Optimus 技术的行为；当需要的时候，使用独立显卡进行渲染，不使用的时候则关闭。当前的版本仅支持按需渲染，高负荷程序自动调用独立显卡的功能仍然在开发之中。

## 安装

安装 Bumblebee 之前，检查你的 BIOS 并尽可能激活 Optimus (老式电脑称之为"可切换显卡"，BIOS有可能没有提供此项设置)。如果 "Optimus" 和 "switchable" 都没有在BIOS里，就保证两种GPU都已启用并且集成显卡是主要显示设备。显示应该连接在主板上的集成显卡，而不是独立显卡。如果集成显卡之前被禁用而安装了独立显卡的驱动，那就删除 `/etc/X11/xorg.conf` 或者有关独立显卡的 `/etc/X11/xorg.conf.d` 中的文件。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装"):

*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) - 提供守护进程以及程序的主要安装包。
*   [mesa](https://www.archlinux.org/packages/?name=mesa) - 开源的 **OpenGL** 标准实现。
*   对于合适的NVIDIA驱动，参看[NVIDIA#安装](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85 "NVIDIA (简体中文)") 。
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) - Intel 驱动（可选）。

对于32位程序 (必须启用[Multilib](/index.php/Multilib "Multilib")）在64位机器上的支持，安装:

*   [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) - 为32位应用提供的渲染/显示桥。
*   [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) 或者 [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils)（和64位对应）。

要使用 Bumblebee，请确保添加你的用户到 `bumblebee` 组：

```
# gpasswd -a *user* bumblebee

```

并 [启用](/index.php/Enable "Enable") `bumblebeed.service`。重启系统并参考[#用法](#用法)。

## 用法

### 测试

安装 [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) 并使用 `glxgears` 测试 Bumblebee 是否工作：

```
$ optirun glxgears -info

```

如果失败，尝试下列命令:

*   64位系统:

```
$ optirun glxspheres64

```

*   32位系统:

```
$ optirun glxspheres32

```

如果一个内有动画的窗口出现，那么 Optimus 和 Bumblebee 正在工作。

**注意:** 如果 `glxgears` 失败但 `glxspheres*XX*` 有效，替换所有 "`glxgears`" 为 "`glxspheres*XX*`"。

### 一般用法

```
$ optirun [options] *application* [application-parameters]

```

例如，用 Optimus 启动 Windows 程序:

```
$ optirun wine application.exe

```

另外，用 Optimus 打开 NVIDIA 设置面板:

```
$ optirun -b none nvidia-settings -c :8

```

**注意:** 一个打了补丁的 [nvdock](https://aur.archlinux.org/packages/nvdock/) 版本可用： [nvdock-bumblebee](https://aur.archlinux.org/packages/nvdock-bumblebee/)

更多 `optirun` 的选项参见手册页:

```
$ man optirun

```

## 配置

你可以按需配置 Bumblebee 的行为，可以通过 `/etc/bumblebee/bumblebee.conf` 来调节诸如优化，电源管理，以及其他任务。

### 速度优化

#### 使用VirtualGL作为桥接

Bumblebee 使用你的 Optimus NVIDIA 显卡来渲染一个配置了 VirtualGL 的不可见的 X 服务器，并且将结果传输到你当前的 X 服务器上。传输之前将压缩侦，这可以节省带宽并且能够用于加速 bumblebee 的优化。

要为单个应用程序指定不同的压缩方法：

```
$ optirun -c *compress-method* application

```

压缩方法会影响 GPU性能和GPU使用，压缩方法会最大限度的使用 CPU,并且尽可能少的使用 GPU；非压缩的方法最大限度的使用 GPU，而尽可能少的使用 CPU。

压缩方法

*   `jpeg`
*   `rgb`
*   `yuv`

非压缩方法

*   `proxy`
*   `xv`

以下是用 [Asus N550JV](/index.php/ASUS_N550JV "ASUS N550JV") 笔记本和测试程序 [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/)的性能测试结果:

| Command | FPS | Score | Min FPS | Max FPS |
| optirun unigine-heaven | 25.0 | 630 | 16.4 | 36.1 |
| optirun -c jpeg unigine-heaven | 24.2 | 610 | 9.5 | 36.8 |
| optirun -c rgb unigine-heaven | 25.1 | 632 | 16.6 | 35.5 |
| optirun -c yuv unigine-heaven | 24.9 | 626 | 16.5 | 35.8 |
| optirun -c proxy unigine-heaven | 25.0 | 629 | 16.0 | 36.1 |
| optirun -c xv unigine-heaven | 22.9 | 577 | 15.4 | 32.2 |

**注意:** 使用 `jpeg` 压缩方法时会有延迟。

要为所有应用程序使用一个标准的压缩方法， 在 `/etc/bumblebee/bumblebee.conf` 里把 `VGLTransport` 设为 `*compress-method*`:

 `/etc/bumblebee/bumblebee.conf` 
```
[...]
[optirun]
VGLTransport=proxy
[...]
```

你也可考虑 VirtualGL 从你的显卡读回像素的方式。设置 `VGL_READBACK` 环境变量为 `pbo` 应该能提升性能。比较以下两者:

```
# PBO should be faster.
VGL_READBACK=pbo optirun glxgears
# The default value is sync.
VGL_READBACK=sync optirun glxgears

```

**注意:** 调整CPU频率将直接影响渲染性能

#### Primusrun

**注意:** 因为合成会损害性能，所以不建议在合成窗口管理器（compositing WM）工作时使用primus。参照 [#Primus issues under compositing window managers](#Primus_issues_under_compositing_window_managers)。

`primusrun` (来自 [primus](https://www.archlinux.org/packages/?name=primus)) 正成为默认选项，因为其耗电量更低并且有时可以提供比 `optirun`/`virtualgl`更好的性能。它可以独立运行，但不能接受 `optirun` 的选项。将 `primus` 设置为 `optirun` 的桥接可提供更过的灵活性。

对于64位系统上32位程序的支持，安装 [lib32-primus](https://www.archlinux.org/packages/?name=lib32-primus)（须启用[multilib](/index.php/Multilib "Multilib")）。

用法（独立运行）：

```
$ primusrun glxgears

```

`optirun` 的桥接：

默认的配置将 `virtualgl` 作为桥接。在命令行上将其覆盖：

```
$ optirun -b primus glxgears

```

或者，在 `/etc/bumblebee/bumblebee.conf` 中设置 `Bridge=primus` 使其永久生效。

**提示：** 如果要禁用 `VSYNC` 请参考 [#Primusrun mouse delay (disable VSYNC)](#Primusrun_mouse_delay_(disable_VSYNC))。这也可以取消鼠标延迟并轻微提高性能。

### 电源管理

电源管理的目的是为了自动关闭 bumblebee 不再使用的 NVIDIA 显卡。 如果已安装 [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) ，Bumblebee 守护进程启动时会自动检测到，不需要特别设置。

#### 使用bbswitch时默认的 NVIDIA 电源状态

bbswitch的默认行为是保持显卡的电源状态。 `bumblebeed` 启动时并不禁用显卡，所以你没有bumblebeed时使用bbswitch需要以下内容。

根据需要设置 `load_state` 和 `unload_state` 模块选项 (见 [bbswitch documentation](https://github.com/Bumblebee-Project/bbswitch)).

 `/etc/modprobe.d/bbswitch.conf`  `options bbswitch load_state=0 unload_state=1` 

#### 关机时启用NVIDIA显卡

如果上次关机时关闭了NVIDIA显卡的电源，NVIDIA显卡可能会在下一次启动时初始化异常。一个解决的办法是在 `/etc/bumblebee/bumblebee.conf` 里设置 `TurnCardOffAtExit=false`， 然而这么做会导致每次停止bumblebee守护进程时启用NVIDIA显卡，就算是手动停止也是一样。为确保NVIDIA显卡总是在关机时启用，添加如下 [systemd](/index.php/Systemd "Systemd") 服务(如果使用 [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) 的话):

 `/etc/systemd/system/nvidia-enable.service` 
```
[Unit]
Description=Enable NVIDIA card
DefaultDependencies=no

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'echo ON > /proc/acpi/bbswitch'

[Install]
WantedBy=shutdown.target
```

然后以root权限运行 `systemctl enable nvidia-enable.service` 以启用服务。

### 多显示器

#### 显示器连接在 Intel 显卡上

如果 (DisplayPort/HDMI/VGA) 接口连接到 Intel 显卡上，你可以通过 xorg.conf 设置多个显示器。设置他们使用 Intel 显卡，同时 Bumblebee 仍然可以使用 NVIDIA 显卡。下面的配置文件示例配置了两个不同的 1080p 的显示器，并且使用了 HDMI 输出。

 `/etc/X11/xorg.conf` 
```
Section "Screen"
    Identifier     "Screen0"
    Device         "intelgpu0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "intelgpu1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "intelgpu0"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier     "intelgpu1"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection
```

你可能需要为Intel和NVIDIA显卡调整 BusID 字段的值:

 `$ lspci | grep VGA` 
```
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)

```

BusID 值为 0:2:0

#### 显示器连接在 NVIDIA 显卡上

在一些笔记本上，数字视频输出(HDMI 或 DisplayPort) 是硬线连接到NVIDIA芯片上的。如果你想同时使用所有的显示器，你需要开两个 X Server.第一个使用Intel驱动用于笔记本面板和连接到VGA上的显示，第二个由optirun启用NVIDIA显卡用于数字显示。

目前网上有一些有关这个的设置教程。其中一个可在Bumblebee的 [wiki 页面](https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup)找到，另一个详见下文。

##### xf86-video-intel-virtual-crtc 和 hybrid-screenclone

本方法使用了一个打了补丁来扩展为含有一个虚拟显示器的Intel驱动，而hybrid-screenclone程序用于把虚拟显示器的内容复制到通过optirun运行于NVIDIA显卡的第二个X Server上的显示器上。有幸发现 [Triple-head monitors on a Thinkpad T520](http://judsonsnotes.com/notes/index.php?option=com_content&view=article&id=673:triple-head-monitors-on-thinkpad-t520&catid=37:tech-notes&Itemid=59)  它是这一切在Ubuntu系统上如何完成的详细解说。

精简起见，下文DP指代 Digital Output (DisplayPort).如果笔记本是HDMI接口的话教程也是一样。

*   设置系统为只使用 NVIDIA 显卡，测试 DP/显示器组合，并生成 xorg.nvidia.conf.这步并非必须但推荐在支持设置为nvidia-only的BIOS上执行。为此，首先卸载 bumblebee 包，并只安装 NVIDIA 驱动。然后重启，进入BIOS设置为NVIDIA-only.重启进入Arch时，把显示器连接到DP并使用 startx 来检测这一切是否正常工作。使用 Xorg -configure 来为你的NVIDIA显卡生成 xorg.conf 文件。这在向下进一步深入时会派上用场。

*   重新安装 bumlbebee 和 bbswitch,重启并在BIOS里设置系统 Gfx 值回到 Hybrid.
*   安装 [xf86-video-intel-virtual-crtc](https://aur.archlinux.org/packages/xf86-video-intel-virtual-crtc/),并以它替换掉 xf86-video-intel.
*   安装 [screenclone-git](https://aur.archlinux.org/packages/screenclone-git/)
*   改变以下 bumblebee.conf 设置:

 `/etc/bumblebee/bumblebee.conf` 
```
KeepUnusedXServer=true
Driver=nvidia
```

**注意:** 把 PMMethod 保留不变为 "bumblebee".这与上面链接里教程的做法相反，但在Arch里需这么做以使 bbswitch 模块自动加载。

*   复制在第一步里生成的 xorg.conf 到 `/etc/X11` (例如 `/etc/X11/xorg.nvidia.conf`).在 `bumblebee.conf` 的[driver-nvidia]部分，修改 `XorgConfFile` 为它的路径。
*   测试你的 `/etc/X11/xorg.nvidia.conf` 是否有效 `startx -- -config /etc/X11/xorg.nvidia.conf`
*   为了你的DP显示器在虚拟显示器上以正常分辨率出现，你需要编辑 `/etc/X11/xorg.nvidia.conf` 里的Monitor section.由于这是附加步骤，你仍需要测试你自动生成的 xorg.conf.当发现 xrandr 显示的虚拟显示器分辨率不对后，再回来参考教程里的这条步骤。
    *   首先要生成 Modeline.你需要工具 [amlc](http://zi.fi/amlc/),它用于输入一些基本参数后自动生成 Modeline.

	例子: 24" 1920x1080 Monitor

	以 `amlc -c` 参数启动工具

```
Monitor Identifier: Samsung 2494
Aspect Ratio: 2
physical size[cm]: 60
Ideal refresh rate, in Hz: 60
min HSync, kHz: 40
max HSync, kHz: 90
min VSync, Hz: 50
max VSync, Hz: 70
max pixel Clock, MHz: 400
```

这就是 `amlc` 生成的 Monitor Section:

```
Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494
```

在 `xorg.nvidia.conf` 里加入这个 Monitor Section.你还可以编辑你的文件使其包含 ServerLayout, Monitor, Device 和 Screen 部分。以下是我的，仅供参考:

 `/etc/X11/xorg.nvidia.conf` 
```
Section "ServerLayout"
        Identifier     "X.org Nvidia DP"
        Screen      0  "Screen0" 0 0
        InputDevice    "Mouse0" "CorePointer"
        InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

Section "Device"
        Identifier  "DiscreteNvidia"
        Driver      "nvidia"
        BusID       "PCI:1:0:0"
EndSection

Section "Screen"
        Identifier "Screen0"
        Device     "DiscreteNvidia"
        Monitor    "Samsung 2494"
        SubSection "Display"
                Viewport   0 0
                Depth     24
        EndSubSection
EndSection

```

*   也要把额外显示器插上之后再 startx.查看 `/var/log/Xorg.0.log`.确保你的VGA显示器以正确的模式被检测出来。你也要看看虚拟输出出现的模式。
*   运行 `xrandr` 然后三个显示器以及它们支持的模式都会被列出来。
*   如果对于你的VIRTUAL显示器没有符合你原生分辨率的Modelines输出, 记下输出的名称。对我来说是 `VIRTUAL1`.然后再看看 Xorg.0.log 文件。你应该会看到一条消息: "Output VIRTUAL1 has no monitor section".我们需要在 `/etc/X11/xorg.conf.d` 里放入含有合适 Monitor Section 的文件，稍后退出并重启X.

 `/etc/X11/xorg.conf.d/20-monitor_samsung.conf` 
```
Section "Monitor"
    Identifier     "VIRTUAL1"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

```

*   为开启NVIDIA显卡，运行: `sudo tee /proc/acpi/bbswitch <<< ON`
*   为 DisplayPort 显示器开启另一个X Server: `sudo optirun true`
*   检查位于 `/var/log/Xorg.8.log` 的第二个 X Server 的日志。
*   运行 xrandr 以把 VIRTUAL 显示器设置成正确的大小和位置，例如: `xrandr --output VGA1 --auto --rotate normal --pos 0x0 --output VIRTUAL1 --mode 1920x1080 --right-of VGA1 --output LVDS1 --auto --rotate normal --right-of VIRTUAL1`
*   请注意在 xrandr 输出列表中的 VIRTUAL 显示器的位置。计数从零开始，也就是说，如果它给出了第三个显示器，你会指定 `-x 2` 作为参数传递给 `screenclone`（注：这可能并不总是正确的。如果你看到内部的笔记本电脑显示屏克隆在监视器上，只管尝试 `-x 2`）。
*   克隆VIRTUAL显示器的内容到由Bumblebee创建的，经由NVIDIA的芯片连接到所述的DisplayPort显示器的X服务器:

	`screenclone -d :8 -x 2`

这就行了，三个显示器都应该配置好并正常工作。

## 如 Windows 一般在集显和独显间切换

在 Windows 里，Optimus 的工作方式是NVIDIA有一个请求 Optimus 的程序的白名单，并且你可以按需添加。当你启动程序时，会自动选择使用哪一张显卡。

为了在Linux里模仿这一行为，你可以使用 [libgl-switcheroo-git](https://aur.archlinux.org/packages/libgl-switcheroo-git/).安装后，往 .xprofile 里添加:

 `~/.xprofile` 
```
mkdir -p /tmp/libgl-switcheroo-$USER/fs
gtkglswitch &
libgl-switcheroo /tmp/libgl-switcheroo-$USER/fs &
```

为此，你需要往你希望启动程序的shell里添加 (我一般就加到 .xprofile 里)

```
export LD_LIBRARY_PATH=/tmp/libgl-switcheroo-$USER/fs/\$LIB${LD_LIBRARY_PATH+:}$LD_LIBRARY_PATH

```

全部完成后，你从该shell运行的每一个程序都会弹出一个GTK+窗口询问该使用哪一张卡(你也可以往配置文件的白名单里添加程序)。配置文件位于 `$XDG_CONFIG_HOME/libgl-switcheroo.conf`, 通常是 `~/.config/libgl-switcheroo.conf`

**注意:** 此工具通过创建FUSE文件系统，然后将其添加到动态库搜索路径来生效，启动软件时，可能导致速度慢甚至段错误。

## 不依赖Bumblebee来使用CUDA

你可以不依赖Bumblebee来使用CUDA,只需确保你的NVIDIA显卡是开启的:

```
 # tee /proc/acpi/bbswitch <<< ON

```

现在你可以运行一个 CUDA 程序，它会自动加载所有需要的模块。

使用完 CUDA 后为了停止NVIDIA显卡，运行:

```
 # rmmod nvidia_uvm
 # rmmod nvidia
 # tee /proc/acpi/bbswitch <<< OFF

```

## 疑难问题

**注意:** 报告 Bug 的位置在 [Bumblebee-Project](https://github.com/Bumblebee-Project/Bumblebee)，Bumblebee 的 [Wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Reporting-Issues) 中描述。

### [VGL] ERROR: Could not open display :8

一个关于部分wine程序的已知问题是它会fork并杀死父进程而不是跟踪它的动态(例如免费网络游戏 "Runes of Magic")

这是一个关于 VirtualGL 的已知问题。自从bumblebee 3.1,只要你安装了它就可以用 Primus 作为渲染桥接:

```
$ optirun -b primus wine *windows program*.exe

```

如果没用的话，一个替代方案如下:

```
$ optirun bash
$ optirun wine *windows program*.exe

```

如果使用NVIDIA驱动的话，一个该问题的解决方案是修改 `/etc/bumblebee/xorg.conf.nvidia` 把 Option `ConnectedMonitor` 改为 `CRT-0`.

### Xlib: extension "GLX" missing on display ":0.0"

从官网下载安装的NVIDIA驱动不会工作。

1\. 卸载驱动：

```
# ./NVIDIA-Linux-*.run --uninstall

```

2\. 删除生成的配置文件：

```
# rm /etc/X11/xorg.conf

```

3\. 重新从源里安装： [#安装](#安装)

### [ERROR]Cannot access secondary GPU: No devices detected

某些情况下，运行 `optirun` 会返回:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) No devices detected.
[ERROR]Aborting because fallback start is disabled.

```

这种情况下，你需要把 `/etc/X11/xorg.conf.d/20-intel.conf` 移动到别的地方， [restart](/index.php/Restart "Restart") bumblebeed 守护进程，这样应该有效。如果你要改变一些 Intel 模块的特性，把 `/etc/X11/xorg.conf.d/20-intel.conf` 合并到 `/etc/X11/xorg.conf` 中。

也需要把 `/etc/X11/xorg.conf.d/10-monitor.conf` 里的driver行注释掉。

如果你正在用 `nouveau` 驱动你应该试着换成 `nvidia` 驱动。

你需要把 NVIDIA 显卡定位到别的地方 (例如文件 `/etc/X11/xorg.conf.d`),使用根据 `lspci` 的输出确定的 `BusID`:

```
Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection

```

#### NVIDIA(0): Failed to assign any connected display devices to X screen 0

如果终端输出如下:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) NVIDIA(0): Failed to assign any connected display devices to X screen 0
[ERROR]Aborting because fallback start is disabled.

```

你要修改 `/etc/bumblebee/xorg.conf.nvidia` 里的这行:

```
Option "ConnectedMonitor" "DFP"

```

为:

```
Option "ConnectedMonitor" "CRT"

```

#### systemd-logind: failed to get session: PID XXX does not belong to any known session

如果终端输出如下 (*PID*会有所不同):

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) systemd-logind: failed to get session: PID 753 does not belong to any known session
[ERROR]Aborting because fallback start is disabled.

```

在 /etc/mkinitcpio.conf 里改变 MODULES 为:

```
MODULES="i915 bbswitch"

```

或:

```
MODULES="i915 nouveau bbswitch"

```

然后运行:

```
# mkinitcpio -p linux

```

每次内核更新之后你都要执行一次这个命令。

另外，[如下](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29) 内核参数需要加到 [boot loader](/index.php/Boot_loader "Boot loader")配置中。

#### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

把 `rcutree.rcu_idle_gp_delay=1` 加到[boot loader](/index.php/Boot_loader "Boot loader") 配置的内核参数中。 (参考设置另见[BBS post](https://bbs.archlinux.org/viewtopic.php?id=169742) )

#### Could not load GPU driver

如果终端输出如下:

```
[ERROR]Cannot access secondary GPU - error: Could not load GPU driver

```

并且尝试加载 nvidia 模块时得到:

```
modprobe nvidia
modprobe: ERROR: could not insert 'nvidia': Exec format error

```

你需要针对你的内核手动编译 nvidia 包，例如 [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) 或从 [ABS](/index.php/ABS "ABS") [nvidia](https://www.archlinux.org/packages/?name=nvidia) 编译。

#### NOUVEAU(0): [drm] failed to set drm interface version

考虑切换到 nvidia 官方驱动。在[此](https://github.com/Bumblebee-Project/Bumblebee/issues/438#issuecomment-22005923)的评论说 nouveau 驱动在某些显卡和bumblebee上有问题。

### [ERROR]Cannot access secondary GPU - error: X did not start properly

在 `/etc/bumblebee/xorg.conf.nvidia` 把 `"AutoAddDevices"` 设置为 `"true"`（看 [这里](https://github.com/Bumblebee-Project/Bumblebee/issues/88)）：

```
Section "ServerLayout"
    Identifier  "Layout0"
    Option      "AutoAddDevices" "true"
    Option      "AutoAddGPU" "false"
EndSection

```

### /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied

这可以通过在 `/etc/bumblebee/xorg.conf.nvidia` 里添加几行解决(见 [这里](https://github.com/Bumblebee-Project/Bumblebee/issues/580)):

```
Section "Screen"
    Identifier "Default Screen"
    Device "DiscreteNvidia"
EndSection

```

### ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored

你也许是想在64位系统上用bumblebee运行32位程序。见 "Note" box [Installation](#Installation).

### Fatal IO error 11 (Resource temporarily unavailable) on X server

把 `/etc/bumblebee/bumblebee.conf` 里的 `KeepUnusedXServer` 从 `false` 改为 `true`.这是因为你的程序fork到了后台并且 bumblebee 对此一无所知。

### 视频撕裂

视频撕裂是 Bumblebee 上一个常见的问题，要修复这个问题，你需要启用 vsync。默认情况下，Intel 显卡已启用此设置，但是还是检查一下 Xorg 的日志，要检查 nvidia 是否启用了此设置，运行:

```
$ optirun nvidia-settings -c :8

```

`X Server XVideo Settings -> Sync to VBlank` 以及 `OpenGL Settings -> Sync to VBlank` 应该都是已经启用状态。 Intel 显卡通常有比较少的撕裂，所以应该作为视频回放设备。特别是使用 VA-API 编码视频的时候（比如：`mplayer-vaapi` 以及 `-vsync` 参数）。

参考[Intel](/index.php/Intel_graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#避免播放视频时屏幕撕裂 "Intel graphics (简体中文)")了解如何修复 Intel 显卡的视频撕裂。

如果仍然无效，尝试从桌面环境禁用 compositing。同时可尝试禁用 triple buffering.

### Bumblebee cannot connect to socket

你可能会得到这样的输出:

```
$ optirun glxspheres64

```

或 (32位):

 `$ optirun glxspheres32` 
```
[ 1648.179533] [ERROR]You've no permission to communicate with the Bumblebee daemon. Try adding yourself to the 'bumblebee' group
[ 1648.179628] [ERROR]Could not connect to bumblebee daemon - is it running?

```

如果你已在 `bumblebee` 群组中 (`$ groups | grep bumblebee`),尝试 [removing the socket](https://bbs.archlinux.org/viewtopic.php?pid=1178729#p1178729) `/var/run/bumblebeed.socket`.

### Running X.org from console after login (rootless X.org)

见 [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_(v1.16) "Xorg").

### Primusrun 鼠标延迟/禁用 VSYNC

对于 `primusrun`, `VSYNC` 默认启用，因此会导致鼠标输入延迟甚至轻微降低性能。不用 `VSYNC` 来测试 `primusrun`:

```
$ vblank_mode=0 primusrun glxgears

```

如果你想使用它替代 `primusrun`,新建文件:

 `/usr/bin/optiprime` 
```
#!/bin/sh
vblank_mode=0 primusrun "$@"

```

让它可执行:

```
# chmod +x /usr/bin/optiprime

```

用法:

```
$ optiprime glxgears

```

总之它不会有重大性能提升，但会解决上述的鼠标延迟。

| Command | FPS | Score | Min FPS | Max FPS |
| optiprime unigine-heaven | 31.5 | 793 | 22.3 | 54.8 |
| primusrun unigine-heaven | 31.4 | 792 | 18.7 | 54.2 |

*Tested with [Asus N550JV](/index.php/ASUS_N550JV "ASUS N550JV") laptop and benchmark app [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/).*

## 另见

*   [Bumblebee project repository](http://www.bumblebee-project.org)
*   [Bumblebee project wiki](http://wiki.bumblebee-project.org/)
*   [Bumblebee project bbswitch repository](https://github.com/Bumblebee-Project/bbswitch)

Join us at #bumblebee at freenode.net.