DisplayLink devices on Linux still only have experimental support. While some people have had success in using them, it is generally not an easy process and not guaranteed to work. The steps on this page describe the generally most successful methods of using external monitors with DisplayLink.

Also be warned that even over USB 3.0, a DisplayLink monitor may exhibit noticeably more lag than e.g. a DisplayPort monitor, especially when large portions of the screen are being redrawn.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 USB 2.0 DL-1xx Devices](#USB_2.0_DL-1xx_Devices)
    *   [1.2 USB 3.0 DL-5xxx, DL-41xx, DL-3x00 Devices](#USB_3.0_DL-5xxx.2C_DL-41xx.2C_DL-3x00_Devices)
    *   [1.3 Setting up X Displays](#Setting_up_X_Displays)
*   [2 Configuration](#Configuration)
    *   [2.1 Load the framebuffer device](#Load_the_framebuffer_device)
    *   [2.2 Configuring X Server](#Configuring_X_Server)
        *   [2.2.1 xrandr](#xrandr)
        *   [2.2.2 Enabling DVI output on startup](#Enabling_DVI_output_on_startup)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Screen redraw is broken](#Screen_redraw_is_broken)
    *   [3.2 DisplayLink refresh rate is extremely slow with gnome 3](#DisplayLink_refresh_rate_is_extremely_slow_with_gnome_3)
*   [4 See Also](#See_Also)

## Installation

### USB 2.0 DL-1xx Devices

The kernel [DRM](https://en.wikipedia.org/wiki/Direct_Rendering_Manager "wikipedia:Direct Rendering Manager") driver for DisplayLink is `udl`, a rewrite of the original [udlfb](https://www.kernel.org/doc/Documentation/fb/udlfb.txt) driver. It allows configuring DisplayLink monitors using [Xrandr](/index.php/Xrandr "Xrandr").

First, the setup and installation:

*   [Blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") the old kernel module, `udlfb`, which may attempt to load itself first.

### USB 3.0 DL-5xxx, DL-41xx, DL-3x00 Devices

Install the [displaylink](https://aur.archlinux.org/packages/displaylink/) driver from the AUR. It allows configuring DisplayLink monitors using [Xrandr](/index.php/Xrandr "Xrandr") in the same manner as the `udl` driver. Use systemctl to enable and start `displaylink.service`.

### Setting up X Displays

After that, run:

 `# xrandr --listproviders` 
```
Providers: number : 2
Provider 0: id: 0x49 cap: 0xb, Source Output, Sink Output, Sink Offload crtcs: 2 outputs: 8 associated providers: 0 name:Intel
Provider 1: id: 0x13c cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 0 name:modesetting

```

In the above output, we can see that provider 0 is the system's regular graphics provider (Intel), and provider 1 (modesetting) is the DisplayLink provider. To use the DisplayLink device, connect provider 1 to provider 0:

```
# xrandr --setprovideroutputsource 1 0

```

and xrandr will add a DVI output you can [use as normal with xrandr](/index.php/Xrandr#Configuration "Xrandr"). This is still experimental but supports hotplugging and when works, it is by far the simplest setup. If it works then everything below is unnecessary.

## Configuration

These instructions assume that you already have an up and running X server and are simply adding a monitor to your existing setup.

### Load the framebuffer device

Before your system will recognize your DisplayLink device, the `udl` kernel module must be loaded. To do this, run

```
# modprobe udl

```

If your DisplayLink device is connected, it should show some visual indication of this. Although a green screen is the standard indicator of this, other variations have been spotted and are perfectly normal. Most importantly, the output of `dmesg` should show something like the following, indicating a new DisplayLink device was found:

```
usb 2-1.1: new high-speed USB device number 7 using ehci-pci
usb 2-1.1: New USB device found, idVendor=17e9, idProduct=03e0
usb 2-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 2-1.1: Product: Lenovo LT1421 wide
usb 2-1.1: Manufacturer: DisplayLink
usb 2-1.1: SerialNumber: 6V9BBRM1
[drm] vendor descriptor length:17 data:17 5f 01 00 15 05 00 01 03 00 04
udl 2-1.1:1.0: fb1: udldrmfb frame buffer device
[drm] Initialized udl 0.0.1 20120220 on minor 1

```

Furthermore, `/dev` should contain a new `fb` device, likely `/dev/fb1` if you already had a framebuffer for your primary display.

To automatically load `udl` at boot, create the file `udl.conf` in `/etc/modules-load.d/` with the following contents:

 `/etc/modules-load.d/udl.conf`  `udl` 

For more information on loading kernel modules, see [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

### Configuring X Server

Use `xrandr` or your Desktop Environment's display setup UI to configure your USB monitors running either the `udl` or `displaylink` driver.

#### xrandr

Once the driver is loaded, the DisplayLink monitor is listed as an output provider:

 `$ xrandr --listproviders` 
```
Providers: number : 2
Provider 0: id: 0x43 cap: 0xb, Source Output, Sink Output, Sink Offload crtcs: 2 outputs: 2 associated providers: 1 name:Intel
Provider 1: id: 0xcb cap: 0x2, Sink Output crtcs: 1 outputs: 1 associated providers: 1 name:modesetting

```

In the above example, provider 1 is the DisplayLink device, and provider 0 is the default display. Running `xrandr --current` gives a list of available screens:

 `$ xrandr --current` 
```
Screen 0: minimum 320 x 200, current 1600 x 900, maximum 8192 x 8192
LVDS1 connected 1600x900+0+0 (normal left inverted right x axis y axis) 309mm x 174mm
   1600x900       60.0*+   40.0  
   1440x900       59.9  
   1360x768       59.8     60.0  
   1152x864       60.0  
   1024x768       60.0  
   800x600        60.3     56.2  
   640x480        59.9  
VGA1 disconnected (normal left inverted right x axis y axis)
DVI-1-0 connected (normal left inverted right x axis y axis)
   1366x768       60.0 +
   1368x768_59.90   59.9  
  1368x768_59.90 (0xd0)   85.7MHz
        h: width  1368 start 1440 end 1584 total 1800 skew    0 clock   47.6KHz
        v: height  768 start  769 end  772 total  795           clock   59.9Hz

```

If the above does not list the DisplayLink screen, then you will need to offload DisplayLink to the main GPU:

 `xrandr --setprovideroutputsource 1 0` 

Once the screen is available, refer to [Xrandr](/index.php/Xrandr "Xrandr") for info on setting it up. For automating the configuration process, see [displaylink.sh](https://github.com/nathantypanski/displaylink.sh).

#### Enabling DVI output on startup

The DisplayLink provider will not be automatically connected to the main provider in most cases, therefore the DVI output device will not be available. It can be helpful to automatically do this when X starts to facilitate automatic display configuration by the window manager.

Edit your desktop manager's startup configuration and add commands similar to:

```
$(xrandr --listproviders | grep -q "modesetting") && xrandr --setprovideroutputsource 1 0

```

For example, the appropriate startup configuration file for [SDDM](/index.php/SDDM "SDDM") is `/usr/share/sddm/scripts/Xsetup`.

Avoid placing these commands in `~/.xprofile` as this breaks the display configuration of some window managers. Instead these commands should be run prior to any display output or setup.

**Note:** If you have additional providers, specify the name of the provider instead of using indexes. The name of the DisplayLink device will be `modesetting`

## Troubleshooting

### Screen redraw is broken

If you are using `udl` as your kernel driver and the monitor appears to work, but is only updating where you move the mouse or when windows change in certain places, then you probably have the wrong modeline for your screen. Getting a proper modeline for your screen with a command like

```
gtf 1366 768 59.9

```

where `1366` and `768` are the horizontal and vertical resolutions for your monitor, and `59.9` is the refresh rate from its specs. To use this, create a new mode with `xrandr` like follows:

```
xrandr --newmode "1368x768_59.90"  85.72  1368 1440 1584 1800  768 769 772 795  -HSync +Vsync

```

and add it to [Xrandr](/index.php/Xrandr "Xrandr"):

```
xrandr --addmode DVI-0 1368x768_59.90

```

Then tell the monitor to use that mode for the DisplayLink monitor, and this should fix the redraw issues. Check the [Xrandr](/index.php/Xrandr "Xrandr") page for information on using a different mode.

If this does not solve the problem (or if the correct modeline was already in place because of correct DDC data), it can help to run a compositor. E.g. when using plain i3, running [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr) or [compton](https://www.archlinux.org/packages/?name=compton) can mitigate the problem.

### DisplayLink refresh rate is extremely slow with gnome 3

If once you set up your DisplayLink your entire desktop becomes slow, try setting a "simpler" background image, such as complete black.

## See Also

*   [DisplayLink Open Source](http://displaylink.org/forum/forumdisplay.php?f=29): Official DisplayLink open source support forum
*   [Plugable](http://plugable.com/platforms/linux): Vendor blog chronicling Linux support for DisplayLink.
*   [Ubuntu Driver Download](http://www.displaylink.com/downloads/ubuntu.php): DisplayLink Ubuntu Driver Download and Information
*   [Release Notes](http://downloads.displaylink.com/releasenotes/DisplayLink_Ubuntu_1.0.68_release-note.txt): Latest release notes for DisplayLink Ubuntu Software