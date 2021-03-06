Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")
*   [Wayland](/index.php/Wayland "Wayland")

From the [libinput](https://freedesktop.org/wiki/Software/libinput/) wiki page:

	libinput is a library to handle input devices in Wayland compositors and to provide a generic X.Org input driver. It provides device detection, device handling, input device event processing and abstraction so minimize the amount of custom input code compositors need to provide the common set of functionality that users expect.

The X.Org input driver supports most regular [Xorg#Input devices](/index.php/Xorg#Input_devices "Xorg"). Particularly notable is the project's goal to provide advanced support for touch (multitouch and gesture) features of touchpads and touchscreens. See the [libinput documentation](http://wayland.freedesktop.org/libinput/doc/latest/pages.html) for more information.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Via xinput](#Via_xinput)
    *   [2.2 Via Xorg configuration file](#Via_Xorg_configuration_file)
    *   [2.3 Graphical tools](#Graphical_tools)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Button re-mapping](#Button_re-mapping)
    *   [3.2 Manual button re-mapping](#Manual_button_re-mapping)
    *   [3.3 Change touchpad sensitivity](#Change_touchpad_sensitivity)
    *   [3.4 Disable touchpad](#Disable_touchpad)
    *   [3.5 Gestures](#Gestures)
        *   [3.5.1 libinput-gestures](#libinput-gestures)
        *   [3.5.2 fusuma](#fusuma)
        *   [3.5.3 GnomeExtendedGestures](#GnomeExtendedGestures)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Touchpad not working in GNOME](#Touchpad_not_working_in_GNOME)
    *   [4.2 Touchpad settings not taking effect in KDE's Touchpad KCM](#Touchpad_settings_not_taking_effect_in_KDE's_Touchpad_KCM)
    *   [4.3 Touchpad not detected at all](#Touchpad_not_detected_at_all)
*   [5 See also](#See_also)

## Installation

If you wish to use libinput under [Wayland](/index.php/Wayland "Wayland"), there is nothing to do for installation. The [libinput](https://www.archlinux.org/packages/?name=libinput) package should already be installed as a dependency of any graphical environment you use that has Wayland, and no additional driver is needed.

If you wish to use libinput with [Xorg](/index.php/Xorg "Xorg"), [install](/index.php/Install "Install") the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package, which is "a thin wrapper around libinput and allows for libinput to be used for input devices in X. This driver can be used as as drop-in replacement for evdev and synaptics." [[1]](https://freedesktop.org/wiki/Software/libinput/) In other words, other packages used for input with X (i.e., those prefixed with `xf86-input-`) can be replaced with this driver.

You may also want to install [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) to be able to change settings at runtime.

## Configuration

For [Wayland](/index.php/Wayland "Wayland"), there is no libinput configuration file. The configurable options depend on the progress of your desktop environment's support for them; see [#Graphical tools](#Graphical_tools).

For [Xorg](/index.php/Xorg "Xorg"), a default configuration file for the wrapper is installed to `/usr/share/X11/xorg.conf.d/40-libinput.conf`. No extra configuration is necessary for it to autodetect keyboards, touchpads, trackpointers and supported touchscreens.

### Via xinput

First, execute:

```
# libinput list-devices

```

It will output the devices on the system and their respective features supported by libinput.

After a [restart](/index.php/Restart "Restart") of the graphical environment, the devices should be managed by libinput with default configuration, if no other drivers are configured to take precedence.

See [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4) for general options to set and information about allowable values. The *xinput* tool is used to view or change options available for a particular device at runtime. For example:

```
$ xinput list

```

to view all devices and determine their names and numbers. In the following, `*device*` is either the name or number identifying the device to operate with.

```
$ xinput list-props *device*

```

to view and

```
$ xinput set-prop *device* *option-number* *setting*

```

to change a setting. For example, to set both options of libinput Click Method Enabled (303), the following is issued:

```
$ xinput set-prop 14 303 {1 1}

```

### Via Xorg configuration file

See [Xorg#Using .conf files](/index.php/Xorg#Using_.conf_files "Xorg") for permanent option settings. [Logitech Marble Mouse#Using libinput](/index.php/Logitech_Marble_Mouse#Using_libinput "Logitech Marble Mouse") and [#Button re-mapping](#Button_re-mapping) illustrate examples.

Alternative drivers for [Xorg#Input devices](/index.php/Xorg#Input_devices "Xorg") can generally be installed in parallel. If you intend to switch driver for a device to use libinput, ensure no legacy configuration files `/etc/X11/xorg.conf.d/` for other drivers take precedence.

**Tip:** If you have libinput and synaptics installed in parallel with default configuration (i.e. no files in `/etc/X11/xorg.conf.d` for either), synaptics will take precedence due to its higher numeric order `70-` in the default installation directory. To avoid this, you can symlink the default libinput configuration (`40-libinput.conf`) to `/etc/X11/xorg.conf.d/` where directory search order precedence over `70-synaptics.conf` will take place instead:
```
# ln -s /usr/share/X11/xorg.conf.d/40-libinput.conf /etc/X11/xorg.conf.d/40-libinput.conf

```
If you *do* have `/etc/X11/xorg.conf.d/` configuration files for both, the libinput file must be ordered second; see [Xorg#Using .conf files](/index.php/Xorg#Using_.conf_files "Xorg"). If you want to disable libinput (and fallback to older drivers) - just remove the previously created symbolic link from `/etc/X11/xorg.conf.d/`.

One way to check which devices are managed by libinput is the [xorg logfile](/index.php/Xorg#General "Xorg"). For example, the following:

 `$ grep -e "Using input driver 'libinput'" */path/to/Xorg.0.log*` 
```
[    28.799] (II) Using input driver 'libinput' for 'Power Button'
[    28.847] (II) Using input driver 'libinput' for 'Video Bus'
[    28.853] (II) Using input driver 'libinput' for 'Power Button'
[    28.860] (II) Using input driver 'libinput' for 'Sleep Button'
[    28.872] (II) Using input driver 'libinput' for 'AT Translated Set 2 keyboard'
[    28.878] (II) Using input driver 'libinput' for 'SynPS/2 Synaptics TouchPad'
[    28.886] (II) Using input driver 'libinput' for 'TPPS/2 IBM TrackPoint'
[    28.895] (II) Using input driver 'libinput' for 'ThinkPad Extra Buttons'
```

is a notebook without any configuration files in `/etc/X11/xorg.conf.d/`, i.e. devices are autodetected.

Of course you can elect to use an alternative driver for one device and libinput for others. A number of factors may influence which driver to use. For example, in comparison to [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") the libinput driver has fewer options to customize touchpad behaviour to one's own taste, but far more programmatic logic to process multitouch events (e.g. palm detection as well). Hence, it makes sense to try the alternative, if you are experiencing problems on your hardware with one driver or the other.

Custom configuration files should be placed in `/etc/X11/xorg.conf.d/` and following a widely used naming schema `30-touchpad.conf` is often chosen as filename.

**Tip:** Have a look at CONFIGURATION DETAILS in `/usr/share/X11/xorg.conf.d/40-libinput.conf` for guidance and refer to the [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4) manual page for a detailed description of available configuration options.

A basic configuration should have the following structure:

 `/etc/X11/xorg.conf.d/30-touchpad.conf` 
```
Section "InputClass"
    Identifier "devname"
    Driver "libinput"
    ...
EndSection

```

You may define as many sections as you like in a single configuration file (usually one per input device). To configure the device of your choice specify a filter by using one of the filters in the INPUTCLASS SECTION [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5), e.g.

*   `MatchIsPointer "on"` (trackpoint)
*   `MatchIsKeyboard "on"`
*   `MatchIsTouchpad "on"`
*   `MatchIsTouchscreen "on"`

The input device can then be configured with any of the lines in the CONFIGURATION DETAILS section of [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4). Common options include:

*   `Option "Tapping" "on"`: tapping a.k.a. tap-to-click
*   `Option "ClickMethod" "clickfinger"`: trackpad no longer has middle and right button areas and instead two-finger click is a context click and three-finger click is a middle click, see the [docs](https://wayland.freedesktop.org/libinput/doc/latest/clickpad-softbuttons.html#clickfinger-behavior).
*   `Option "NaturalScrolling" "true"`: natural (reverse) scrolling
*   `Option "ScrollMethod" "edge"`: edge (vertical) scrolling

Bear in mind that some of them may only apply to certain devices and you'll need to restart X for changes to take effect.

### Graphical tools

There are different GUI tools:

*   [GNOME](/index.php/GNOME "GNOME"):
    *   Control center has a basic UI. See [GNOME#Mouse and touchpad](/index.php/GNOME#Mouse_and_touchpad "GNOME").
    *   [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) offers some additional settings.
*   [Cinnamon](/index.php/Cinnamon "Cinnamon"):
    *   Similar to the GNOME UI, with more options.
*   [KDE Plasma](/index.php/KDE_Plasma "KDE Plasma") 5:
    *   Set of keyboard, mouse, controller, and touch pad options. Some features are still placeholders.
    *   [kcm-pointing-devices-git](https://aur.archlinux.org/packages/kcm-pointing-devices-git/) is a rewritten KCM for all input devices supported by libinput.

## Tips and tricks

### Button re-mapping

Swapping two- and three-finger tap for a touchpad is a straight forward example. Instead of the default three-finger tap for pasting you can configure two-finger tap pasting by setting the `TappingButtonMap` option in your [Xorg](/index.php/Xorg "Xorg") configuration file. To set 1/2/3-finger taps to left/right/middle set `TappingButtonMap` to `lrm`, for left/middle/right set it to `lmr`.

 `/etc/X11/xorg.conf.d/30-touchpad.conf` 
```
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "TappingButtonMap" "lmr"
EndSection
```

Remember to remove `MatchIsTouchpad "on"` if your device is not a touchpad and adjust the `Identifier` accordingly.

### Manual button re-mapping

For some devices it is desirable to change the button mapping. A common example is the use of a thumb button instead of the middle button (used in X11 for pasting) on mice where the middle button is part of the mouse wheel. You can query the current button mapping via:

```
$ xinput get-button-map *device*

```

where *device* is either the device name or the device ID, as returned by `xinput list`. You can freely permutate the button numbers and write them back. Example:

```
$ xinput set-button-map *device* 1 6 3 4 5 0 7

```

In this example, we mapped button 6 to be the middle button and disabled the original middle button by assigning it to button 0\. This may also be used for [Wayland](/index.php/Wayland "Wayland"), but be aware both the *device* number and its button-map will be different. Hence, settings are not directly interchangeable.

**Tip:** You can use *xev* (from the [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) package) to find out which physical button is currently mapped to which ID.

Some devices occur several times under the same device name, with a different amount of buttons exposed. The following is an example for reliably changing the button mapping for a Logitech Revolution MX mouse via [xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
...
for i in $(xinput list | grep "Logitech USB Receiver" | perl -n -e'/id=(\d+)/ && print "$1
"')
	do if xinput get-button-map "$i" 2>/dev/null| grep -q 20; then
		xinput set-button-map "$i" 1 17 3 4 5 8 7 6 9 10 11 12 13 14 15 16 2 18 19 20
	fi
done
...
```

### Change touchpad sensitivity

The method of finding the correct thresholds for when libinput registers a touch as DOWN and back UP again can be found [[2]](https://wayland.freedesktop.org/libinput/doc/latest/touchpad-pressure-debugging.html#touchpad-pressure-hwdb) in the upstream documentation.

Custom touchpad pressure values can be set via temporary local device quirks. See [[3]](https://wayland.freedesktop.org/libinput/doc/latest/device-quirks.html).

**Note:**

Quirks are an internal API and are not guaranteed to work in future libinput versions. Between versions 1.11 and 1.12, udev rules [[4]](https://wayland.freedesktop.org/libinput/doc/1.11.3/udev_config.html#hwdb) were replaced by `.quirk` files [[5]](https://wayland.freedesktop.org/libinput/doc/latest/device-quirks.html).

### Disable touchpad

To disable the touchpad, first get its name with `xinput list` and then disable it with `xinput disable *name*`.

**Note:**

*   It is more robust to disable it by name than by ID number. The devices may be renumbered.
*   It will be necessary to quote the name if it contains spaces.

To make it permanent, see [Autostarting](/index.php/Autostarting "Autostarting").

### Gestures

While the libinput driver already contains logic to process advanced multitouch events like swipe and pinch [gestures](https://wayland.freedesktop.org/libinput/doc/latest/gestures.html), the [Desktop environment](/index.php/Desktop_environment "Desktop environment") or [Window manager](/index.php/Window_manager "Window manager") might not have implemented actions for all of them yet.

#### libinput-gestures

For [EWMH](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints "w:Extended Window Manager Hints") (see also [wm-spec](https://www.freedesktop.org/wiki/Specifications/wm-spec/)) compliant window managers, the [libinput-gestures](https://github.com/bulletmark/libinput-gestures) utility can be used meanwhile. The program reads libinput gestures (through `libinput debug-events`) from the touchpad and maps them to gestures according to a configuration file. Hence, it offers some flexibility within the boundaries of libinput's built-in recognition.

To use [libinput-gestures](https://github.com/bulletmark/libinput-gestures), install the [libinput-gestures](https://aur.archlinux.org/packages/libinput-gestures/) package. You can use the default system-wide configured swipe and pinch gestures or define your own in a personal configuration file, see the [README](https://github.com/bulletmark/libinput-gestures/blob/master/README.md) for details.

#### fusuma

[Fusuma](https://github.com/iberianpig/fusuma) is a multitouch gesture recognizer, written in [Ruby](/index.php/Ruby "Ruby"), which can be used as an alternative to libinput-gestures.

Install the `fusuma` [Ruby gem](/index.php/Ruby#RubyGems "Ruby"):

```
$ gem install fusuma

```

Alternatively an outdated version is available in the AUR: [ruby-fusuma](https://aur.archlinux.org/packages/ruby-fusuma/).

then in `~/.config/fusuma/config.yml` you can set something like:

 `~/.config/fusuma/config.yml` 
```
swipe:
  3: 
    left: 
      shortcut: 'alt+Right'
    right: 
      shortcut: 'alt+Left'
    up: 
      shortcut: 'ctrl+shift+plus'
    down: 
      shortcut: 'ctrl+minus'
pinch:
  in:
    shortcut: 'ctrl+shift+plus'
  out:
    shortcut: 'ctrl+minus'

threshold:
  swipe: 0.5
  pinch: 0.2

interval:
  swipe: 0.2
  pinch: 0.2

```

The swipe threshold is important for not swiping back too many pages.

Notice that the config is for three fingers swipe.

#### GnomeExtendedGestures

For deeper integration with GNOME, there is [GnomeExtendedGestures](https://github.com/mpiannucci/GnomeExtendedGestures) ([gnome-shell-extension-extended-gestures-git](https://aur.archlinux.org/packages/gnome-shell-extension-extended-gestures-git/)). Three finger horizontal and vertical gestures can be configured to perform gnome-shell actions (such as toggling the application overview or cycling between them).

## Troubleshooting

First, see whether executing `libinput debug-events` can support you in debugging the problem, see [libinput-debug-events(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput-debug-events.1) for options.

Some inputs require kernel support. The tool *evemu-describe* from the [evemu](https://www.archlinux.org/packages/?name=evemu) package can be used to check:

Compare the output of [software supported input trackpad driver](http://ix.io/m6b) with [a supported trackpad](https://github.com/whot/evemu-devices/blob/master/touchpads/SynPS2%20Synaptics%20TouchPad-with-scrollbuttons.events). i.e. a couple of ABS_ axes, a couple of ABS_MT axes and no REL_X/Y axis. For a clickpad the `INPUT_PROP_BUTTONPAD` property should also be set, if it is supported.

### Touchpad not working in GNOME

Ensure the touchpad events are being sent to the GNOME desktop by running the following command:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad send-events enabled

```

Additionally, GNOME may override certain behaviors, like turning off Tapping and forcing Natural Scrolling. In this case the settings must be adapted using GNOMEs `gsettings` command line tool or a graphical frontend of your choice. For example if you wish to enable *Tapping* and disable *Natural Scrolling* for your user, adjust the touchpad key-values like the following:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
$ gsettings set org.gnome.desktop.peripherals.touchpad natural-scroll false

```

### Touchpad settings not taking effect in KDE's Touchpad KCM

KDE's Touchpad KCM has libinput support for [Xorg](/index.php/Xorg "Xorg"), but not all GUI settings are available yet. You may find that a setting such as *Disable touchpad when typing* has no effect and other options are greyed out. Until the support is extended, a workaround is to install [kcm-pointing-devices-git](https://aur.archlinux.org/packages/kcm-pointing-devices-git/) or set the options manually with `xinput set-prop`.

### Touchpad not detected at all

If a touchpad device is not detected and shown as a device at all, a possible solution might be using one or more of these kernel parameters.

```
i8042.noloop i8042.nomux i8042.nopnp i8042.reset

```

## See also

*   [libinput Wayland documentation](https://wayland.freedesktop.org/libinput/doc/latest/index.html)
*   [FOSDEM 2015 - libinput](https://archive.fosdem.org/2015/schedule/event/libinput/attachments/slides/591/export/events/attachments/libinput/slides/591/libinput_xorg.pdf) - Hans de Goede on goals and plans of the project
*   [Peter Hutterer's Blog](http://who-t.blogspot.com.au/) - numerous posts on libinput from one of the project's hackers