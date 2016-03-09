## Contents

*   [1 Installation](#Installation)
    *   [1.1 Video](#Video)
    *   [1.2 Wireless Network](#Wireless_Network)
    *   [1.3 Suspend](#Suspend)
    *   [1.4 Power management](#Power_management)
*   [2 Keyboard](#Keyboard)
*   [3 External Links](#External_Links)

# Installation

A hub error message is printed repeatedly:

```
hub 1-0:1.0: connect-debounce failed, port 6 disabled

```

A workaround is to disable the laptop's wi-fi device in BIOS.

## Video

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

## Wireless Network

See [Wireless#iwl3945, iwl4965 and iwl5000-series](/index.php/Wireless#iwl3945.2C_iwl4965_and_iwl5000-series "Wireless") wiki article.

## Suspend

See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Power management

See [Power management](/index.php/Power_management "Power management").

# Keyboard

To setup windows keys (useful for fluxbox keybindings) as well as multimedia keys (accessed with Fn + the function keys) recognition in X, edit ~/.Xmodmap

```
keycode 115 = XF86ApplicationLeft 
add mod4 = XF86ApplicationLeft 
keycode 116 = XF86ApplicationRight
add mod4 = XF86ApplicationRight
keycode 117 = XF86MenuKB
keycode 162 = XF86AudioPlay
keycode 164 = XF86AudioStop
keycode 144 = XF86AudioPrev
keycode 153 = XF86AudioNext
keycode 223 = XF86Sleep
keycode 160 = XF86AudioMute
keycode 176 = XF86AudioRaiseVolume
keycode 174 = XF86AudioLowerVolume

```

If you have amarok, configure the global shortcuts, setting the multimedia keys as "alternate".

# External Links

*   This report is listed at the [Gentoo wiki](http://gentoo-wiki.com/HARDWARE_Gentoo_on_Fujitsu-Siemens_Amilo_Pro_V3205) and Lubos Vrbka's [homepage](http://www.lubos.vrbka.net/misc_ntb.html).