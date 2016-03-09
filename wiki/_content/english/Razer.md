There are currently no official drivers for any Razer peripherals in Linux. However, Michael Buesch has created a tool called [razercfg](http://bues.ch/cms/hacking/razercfg.html) to configure Razer mice under Linux. There also exist scripts to enable macro keys of Razer keyboards.

## Contents

*   [1 Razer Peripherals](#Razer_Peripherals)
    *   [1.1 Compatibility](#Compatibility)
    *   [1.2 Installation](#Installation)
    *   [1.3 Using the Razer Configuration Tool](#Using_the_Razer_Configuration_Tool)
*   [2 Razer Blade](#Razer_Blade)
    *   [2.1 2015 version (Razer Blade Stealth)](#2015_version_.28Razer_Blade_Stealth.29)
        *   [2.1.1 Killer Wireless Network Adapter](#Killer_Wireless_Network_Adapter)
        *   [2.1.2 Touchpad](#Touchpad)
        *   [2.1.3 Graphics Drivers](#Graphics_Drivers)
        *   [2.1.4 Tweaking](#Tweaking)
        *   [2.1.5 Unresolved Issues](#Unresolved_Issues)
    *   [2.2 2014 version](#2014_version)
        *   [2.2.1 Problems](#Problems)
        *   [2.2.2 Possible trackpad solution](#Possible_trackpad_solution)
    *   [2.3 2013 version](#2013_version)
        *   [2.3.1 What works](#What_works)
        *   [2.3.2 Problems](#Problems_2)
        *   [2.3.3 Possible trackpad solution](#Possible_trackpad_solution_2)
*   [3 Razer Keyboards](#Razer_Keyboards)

## Razer Peripherals

### Compatibility

*razercfg* lists the following mice models as stable:

*   Razer DeathAdder Classic
*   Razer DeathAdder 3500 DPI
*   Razer DeathAdder Black Edition
*   Razer DeathAdder 2013
*   Razer DeathAdder Chroma
*   Razer Krait
*   Razer Naga Classic
*   Razer Naga 2012
*   Razer Naga 2014
*   Razer Naga Hex
*   Razer Taipan

And the following as stable but missing minor features:

*   Razer Lachesis
*   Razer Copperhead
*   Razer Boomslang CE

### Installation

Download and install [razercfg](https://aur.archlinux.org/packages/razercfg/) or [razercfg-git](https://aur.archlinux.org/packages/razercfg-git/) for bleeding edge git releases from the [AUR](/index.php/AUR "AUR").

You also need to edit your `/etc/X11/xorg.conf` file to disable the current mouse settings by commenting them out as in the following example, where also some defaults are set as suggested by the author:

 `/etc/X11/xorg.conf` 
```
 Section "InputDevice"
    Identifier  "Mouse"
    Driver  "mouse"
    Option  "Device" "/dev/input/mice"
 EndSection
```

It is important to only have `Mouse` and not `Mouse#` listed in `xorg.conf`.

Restart the computer, then enter:

```
# udevadm control --reload-rules

```

Then [start](/index.php/Start "Start") the `razerd` daemon and possibly enable it.

### Using the Razer Configuration Tool

There are two commands you can use, one for the command line tool *razercfg* or the Qt-based GUI tool *qrazercfg*.

From the tool you can use the 5 profiles, change the DPI, change mouse frequency, enable and disable the scroll and logo lights and configure the buttons.

## Razer Blade

Razer Blade is Razer's line of gaming laptops. There is currently a 14" model, and a 17" model. Due to the proprietary SBUI trackpad on the 17" model, it will be extremely difficult to get it to work without extensive USB protocol reversing.

### 2015 version (Razer Blade Stealth)

The normal installation process works in general with the exceptions enumerated below.

#### Killer Wireless Network Adapter

The wireless adapter won't work without proprietary firmware. You will require a USB ethernet adapter to do the installation or an ISO with the proprietary driver installed. The wireless adapter presents itself as

```
01:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

It is a [Killer Wireless-AC 1535](http://www.killernetworking.com/support/knowledge-base/17-linux/20-killer-wireless-ac-in-linux-ubuntu-debian) which requires proprietary firmware for the board. The latest 4.4.1 kernel only requires the *board.bin* to be overwritten.

```
# wget -O /lib/firmware/ath10k/QCA6174/hw3.0/board.bin http://www.killernetworking.com/support/board.bin

```

#### Touchpad

The touchpad requires the synaptic drivers to work properly.

```
# pacman -S xf86-input-synaptics

```

See [Touchpad_Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for more information on installation and configuration.

#### Graphics Drivers

The graphics card works OK with the standard intel drivers.

```
# pacman -S xf86-video-intel

```

See [Intel_graphics](/index.php/Intel_graphics "Intel graphics") for more information on installation and configuration.

Issues with screen flickering seem to be resolved by changing *AccelMethod* to *sna* As described in the wiki for the driver.

```
# cat >/etc/X11/xorg.conf.d/20-intel.conf 
Section "Device"
  Identifier  "Intel Graphics"
  Driver      "intel"
  Option      "AccelMethod"  "uxa"
  #Option      "AccelMethod"  "sna"
EndSection

```

#### Tweaking

If you are using [GNOME](/index.php/GNOME "GNOME"), the *gnome-tweak-tool* can be used to adjust the window and font scaling. A font scale of *1.25* puts the font sizes closer to how they are displayed by default in Windows 10.

If you are using an external monitor that is not [HiDPI](/index.php/HiDPI "HiDPI"), you can use *xrandr* to alter the scaling of the external monitor using the instructions for [Multiple Displays](https://wiki.archlinux.org/index.php/HiDPI#Multiple_displays). You may have better results though running [GNOME](/index.php/GNOME "GNOME") on [Wayland](/index.php/Wayland "Wayland"). When installed, clicking the gear icon in [GDM](/index.php/GDM "GDM") will allow you to select *Gnome On Wayland* and will default to that in the future.

#### Unresolved Issues

*   the webcam does not seem to work with a basic installation. External webcams work fine. It seems to fail when the resolution is anything but 640x480\. [guvcview](https://www.archlinux.org/packages/community/x86_64/guvcview/) works because it defaults to the resolution. [cheese](https://www.archlinux.org/packages/community/x86_64/cheese/) and [Google Hangouts](https://hangouts.google.com) do not because they default to the max resolution.
*   Suspending does not seem to work with a basic installation. You can suspend but once the system resumes it suffers from random suspends or the screen going blank for no apparent reason.

### 2014 version

#### Problems

[Source](http://forum.notebookreview.com/razer/751074-2014-razer-blade-14-linux.html)

*   touchpad (multitouch, although this may be a kernel bug that has since been fixed)
*   keys to increase/decrease screen illumination not working
*   keys to increase/decrease keyboard illumination not working

#### Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone https://github.com/aduggan/hid-rmi.git -b rb14 # and then install it
depmod -a
sudo pacman -S synaptics

Feature still not working: pinch to zoom, 3rd mouse button

```

### 2013 version

#### What works

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356)

*   Wireless
*   Switchable graphics
*   Bluetooth
*   Keyboard light (HW controlled)
*   UEFI boot
*   Trackpad (only on Linux 4.0+ **without** libinput-based X.Org input driver (xf86-input-libinput) thanks to [Andrew Duggan's work](http://git.kernel.org/cgit/linux/kernel/git/jikos/hid.git/log/drivers/hid/hid-rmi.c?h=for-3.20/rmi)).

#### Problems

[Source](http://forum.notebookreview.com/razer/729380-razer-blade-pro-under-linux.html)

*   SwitchBlade UI doesn't work due to lack of drivers.
*   ~~Trackpad scrolling does not work.~~

#### Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone https://github.com/aduggan/hid-rmi.git -b rb14 # and then install it
depmod -a
sudo pacman -S synaptics

Feature still not working: pinch to zoom, 3rd mouse button

```

## Razer Keyboards

There are currently two Python scripts available to enable macro keys under Linux:

*   [blackwidowcontrol](https://aur.archlinux.org/packages/blackwidowcontrol/)
    *   Should work with regular BlackWidow and might work with BlackWidow Ultimate / 2013
    *   uses Python 3
    *   does not bundle any scripts to create macros (use hot key configuration tool from your desktop environment)
    *   allows to controls the status of the LED
*   [razer-blackwidow-macro-scripts](https://aur.archlinux.org/packages/razer-blackwidow-macro-scripts/)
    *   Should work with BlackWidow Ultimate 2013
    *   uses Python 2
    *   also bundles scripts to create and execute macros