Related articles

*   [DPMS](/index.php/DPMS "DPMS")
*   [Xresources](/index.php/Xresources "Xresources")
*   [List of applications#Screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications")

[XScreenSaver](https://www.jwz.org/xscreensaver/) is a screen saver and locker for the X Window System.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 DPMS and blanking settings](#DPMS_and_blanking_settings)
*   [3 Usage](#Usage)
    *   [3.1 Lock on suspend](#Lock_on_suspend)
    *   [3.2 User switching from the lock screen](#User_switching_from_the_lock_screen)
        *   [3.2.1 LXDM](#LXDM)
        *   [3.2.2 LightDM](#LightDM)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Disable during media playback](#Disable_during_media_playback)
        *   [4.1.1 mpv](#mpv)
        *   [4.1.2 mplayer](#mplayer)
        *   [4.1.3 Kodi](#Kodi)
        *   [4.1.4 Browser HTML5 video/Flash](#Browser_HTML5_video/Flash)
    *   [4.2 Animated wallpaper](#Animated_wallpaper)
*   [5 Troubleshooting](#Troubleshooting)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) package.

For an Arch Linux branded experience, install the [xscreensaver-arch-logo](https://aur.archlinux.org/packages/xscreensaver-arch-logo/) package.

## Configuration

Most options are configured on a user-by-user basis by running *xscreensaver-demo*. *xscreensaver-demo* writes the chosen configuration to `~/.xscreensaver`, discarding any manual modifications to the file. Global options are defined in `/usr/share/X11/app-defaults/XScreenSaver`.

Since at least XScreenSaver 5.22, there is another way to edit XScreenSaver's user configuration, using [Xresources](/index.php/Xresources "Xresources"). This includes theming support. See [[1]](https://gist.github.com/anonymous/682d8daf5631b588e12e) for the version 5.22 defaults.

### DPMS and blanking settings

XScreenSaver manages screen blanking and display energy saving ([DPMS](/index.php/DPMS "DPMS")) independently of X itself and overrides it. To configure the timings for blanking, standby, display poweroff and such, use *xscreensaver-demo* or edit the configuration file manually, e.g. `~/.xscreensaver`:

```
timeout:	1:00:00
cycle:		0:05:00
lock:		False
lockTimeout:	0:00:00
passwdTimeout:	0:00:30
fade:		True
unfade:		False
fadeSeconds:	0:00:03
fadeTicks:	20
dpmsEnabled:	True
dpmsStandby:	2:00:00
dpmsSuspend:	2:00:00
dpmsOff:	4:00:00

```

DPMS and screen blanking can be disabled by starting *xscreensaver-demo* and, for the *Mode* setting, choosing *Disable Screen Saver*.

**Note:** If *Lock Screen After* in *xscreensaver-demo* is ticked and set to 0 minutes, the screen will be locked immediately upon blanking. If *Power Manager Enabled* is unticked, DPMS is disabled; it does not mean that XScreenSaver will relinquish control of DPMS settings.

## Usage

**Tip:** To start XScreenSaver without the splash screen, use the `-no-splash` switch. See [xscreensaver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xscreensaver.1) for a full list of options.

In the [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE") and [LXQt](/index.php/LXQt "LXQt") environments, XScreenSaver is autostarted automatically if it is available - no further action is required. For other environments, see [Autostarting](/index.php/Autostarting "Autostarting").

To immediately trigger `xscreensaver`, if it is running, and lock the screen, execute the following command:

```
$ xscreensaver-command -lock

```

### Lock on suspend

See [Power management#xss-lock](/index.php/Power_management#xss-lock "Power management"). You may want to set XScreenSaver's fade out time to 0.

### User switching from the lock screen

**Warning:** When switching users using a display manager such as GDM or LightDM, XScreenSaver will not lock the original session - it can be accessed without a password simply by switching TTY's to the session in question. If you are using LightDM, as a workaround, install [light-locker](https://www.archlinux.org/packages/?name=light-locker) and run it alongside XscreenSaver. Alternatively, use a different screen locking program altogether - see [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

By default, XScreenSaver's *New Login* button in the lock screen will call `/usr/bin/gdmflexiserver` to switch users. Other [display managers](/index.php/Display_manager "Display manager") than [GDM](/index.php/GDM "GDM") or KDM that support user switching (such as [LightDM](/index.php/LightDM "LightDM")) require a different command.

**Tip:** Adding *xscreensaver.newLoginCommand:* to `~/.Xresources` whilst leaving the argument blank will make the *New Login* button disappear.

As modifications in `~/.xscreensaver` are [discarded](#Configuration) by *xscreensaver-demo*, `~/.Xresources` is used in this section.

#### LXDM

To use LXDM's switching mode:

```
xscreensaver.newLoginCommand: lxdm -c USER_SWITCH

```

#### LightDM

To use [LightDM](/index.php/LightDM "LightDM")'s switching mode:

```
xscreensaver.newLoginCommand: dm-tool switch-to-greeter

```

**Note:** If you use this to switch to an already-logged-in user, you might have to enter the password twice (once for LightDM, and once for the XScreenSaver dialog of the user you logged in to).

## Tips and tricks

### Disable during media playback

#### mpv

By default [mpv](/index.php/Mpv "Mpv") turns off the screensaver at startup and turns it on again on exit. The screensaver is always re-enabled when the player is paused. The option can be controlled in mpv's config file located in `~/.config/mpv/mpv.conf`:

```
stop-screensaver = "yes"

```

This is not supported on all video outputs or platforms. If you face some issues you might use a Lua script to manually disable the screensaver. Create a file at `~/.config/mpv/scripts/xscreensaver.lua` with the follwing contents:

```
local utils = require 'mp.utils'
mp.add_periodic_timer(30, function()
    utils.subprocess({args={"xscreensaver-command", "-deactivate"}})
end)

```

The above script will call `xscreensaver-command -deactivate` every 30 seconds. (Formerly you could use the `heartbeat-cmd` config option, but that is no longer present in newer versions of mpv).

#### mplayer

Add the following to `~/.mplayer/config`:

```
heartbeat-cmd="xscreensaver-command -deactivate >&- 2>&- &"

```

#### Kodi

[Kodi](/index.php/Kodi "Kodi") has no native support to disable XScreenSaver (it uses its own screensaver). [Install](/index.php/Install "Install") the [kodi-prevent-xscreensaver](https://aur.archlinux.org/packages/kodi-prevent-xscreensaver/) package as a workaround or try Kodi extension from [https://sourceforge.net/projects/osscreensavermanager/](https://sourceforge.net/projects/osscreensavermanager/) .

#### Browser HTML5 video/Flash

There is no native way to disable XScreenSaver for [Flash](/index.php/Flash "Flash") or HTML5 fullscreen video, but there is a script named [lightsonplus](https://github.com/devkral/lightsonplus) with support for Firefox's Flash plugin, Chromium's Flash plugin, HTML5 fullscreen video in Firefox and Chromium, MPlayer, and VLC.

Another script based solution would be [firefox-dpms-git](https://aur.archlinux.org/packages/firefox-dpms-git/) which makes use of PulseAudio output detection of Firefox and thus also works in windowed mode (but not without audio playback).

### Animated wallpaper

One can run `xscreensaver` in the background, just like a wallpaper. First, kill any process that is controlling the background (the root window).

Then, locate the desired XScreenSaver executable (typically in `/usr/lib/xscreensaver/`) and run it with the `-root` flag, for example:

```
$ /usr/lib/xscreensaver/glslideshow -root &

```

**Note:** If [xcompmgr](/index.php/Xcompmgr "Xcompmgr") causes problems, [install](/index.php/Install "Install") the [shantz-xwinwrap-bzr](https://aur.archlinux.org/packages/shantz-xwinwrap-bzr/) package, and run:
```
$ xwinwrap -b -fs -sp -fs -nf -ov  -- /usr/lib/xscreensaver/glslideshow -root -window-id WID &

```

## Troubleshooting

You can configure xscreensaver to write to a log file by creating the logfile `# touch /var/log/xscreensaver.log` and then specifying its X resource *logFile*.

 `~/.Xresources`  `xscreensaver.logFile:/var/log/xscreensaver.log` 

To log verbose debugging information to the logFile as well start xscreensaver with the `-verbose` command line option, or add this to `~/.Xresources`

 `~/.Xresources` 
```
xscreensaver.logFile:/var/log/xscreensaver.log
xscreensaver.verbose:true
```

## See also

*   [Homepage for XScreenSaver](http://www.jwz.org/xscreensaver/)