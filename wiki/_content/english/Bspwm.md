Related articles

*   [Window manager](/index.php/Window_manager "Window manager")
*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")

[bspwm](https://github.com/baskerville/bspwm) is a tiling window manager that represents windows as the leaves of a full binary tree. bspwm supports multiple monitors and is configured and controlled through messages. [EWMH](https://standards.freedesktop.org/wm-spec/wm-spec-latest.html) is partially supported.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
    *   [3.1 Note for multi-monitor setups](#Note_for_multi-monitor_setups)
    *   [3.2 Rules](#Rules)
    *   [3.3 Panels](#Panels)
        *   [3.3.1 Using lemonbar](#Using_lemonbar)
        *   [3.3.2 Using yabar](#Using_yabar)
    *   [3.4 Scratchpad](#Scratchpad)
    *   [3.5 Different monitor configurations for different machines](#Different_monitor_configurations_for_different_machines)
    *   [3.6 Set up a desktop where all windows are floating](#Set_up_a_desktop_where_all_windows_are_floating)
    *   [3.7 Keyboard](#Keyboard)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Blank screen and keybindings don't work](#Blank_screen_and_keybindings_don't_work)
    *   [4.2 Window box larger than the actual application](#Window_box_larger_than_the_actual_application)
    *   [4.3 Problems with Java applications](#Problems_with_Java_applications)
    *   [4.4 Problems with keybindings using fish](#Problems_with_keybindings_using_fish)
    *   [4.5 Error messages "Could not grab key 43 with modfield 68" on start](#Error_messages_"Could_not_grab_key_43_with_modfield_68"_on_start)
    *   [4.6 Firefox context menu automatically selects first option on right click](#Firefox_context_menu_automatically_selects_first_option_on_right_click)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [bspwm](https://www.archlinux.org/packages/?name=bspwm) package or [bspwm-git](https://aur.archlinux.org/packages/bspwm-git/) for the development version.

## Starting

Run `bspwm` using [xinit](/index.php/Xinit "Xinit").

## Configuration

**Important:** Make sure your environment variable $XDG_CONFIG_HOME is set or your bspwmrc will not be found. This can be done by adding `XDG_CONFIG_HOME="$HOME/.config"` and `export XDG_CONFIG_HOME` to your `~/.profile`.

The example configuration is located in `/usr/share/doc/bspwm/examples/`.

Copy `bspwmrc` from there into `~/.config/bspwm/` and `sxhkdrc` into `~/.config/sxhkd/`.

These two files are where you will be setting wm settings and keybindings, respectively.

See the [bspwm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bspwm.1) and [sxhkd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sxhkd.1) manuals for detailed documentation.

#### Note for multi-monitor setups

The example bspwmrc configures ten desktops on one monitor like this:

```
bspc monitor -d I II III IV V VI VII VIII IX X

```

You will need to change this line and add one for each monitor, similar to this:

```
bspc monitor DVI-I-1 -d I II III IV
bspc monitor DVI-I-2 -d V VI VII
bspc monitor DP-1 -d VIII IX X

```

You can use `xrandr -q` or `bspc query -M` to find the monitor names.

The total number of desktops were maintained at ten in the above example. This is so that each desktop can still be addressed with `super + {1-9,0}` in the sxhkdrc.

### Rules

There are two ways to set window rules (as of [cd97a32](https://github.com/baskerville/bspwm/commit/cd97a3290aa8d36346deb706fa307f5f8faa2f34)).

The first is by using the built in rule command, as shown in the example bspwmrc:

```
bspc rule -a Gimp desktop=^8 follow=on state=floating
bspc rule -a Chromium desktop=^2
bspc rule -a mplayer2 state=floating
bspc rule -a Kupfer.py focus=on
bspc rule -a Screenkey manage=off

```

The second option is to use an external rule command. This is more complex, but can allow you to craft more complex window rules. See [these examples](https://github.com/baskerville/bspwm/tree/master/examples/external_rules) for a sample rule command.

If a particular window does not seem to be behaving according to your rules, check the class name of the program. This can be accomplished by running `xprop | grep WM_CLASS` to make sure you're using the proper string.

### Panels

#### Using lemonbar

An example panel for [lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/) is provided in the examples folder on the GitHub page. You might also get some insights from the [lemonbar](/index.php/Lemonbar "Lemonbar") wiki page. The panel will be executed by placing `panel &` in your bspwmrc. Check the opt-depends in the bspwm package for dependencies that may be required.

To display system information on your status bar you can use various system calls. This example will show you how to edit your `panel` to get the volume status on your BAR:

```
panel_volume()
{
        volStatus=$(amixer get Master | tail -n 1 | cut -d '[' -f 4 | sed 's/].*//g')
        volLevel=$(amixer get Master | tail -n 1 | cut -d '[' -f 2 | sed 's/%.*//g')
        # is alsa muted or not muted?
        if [ "$volStatus" == "on" ]
        then
                echo "%{Fyellowgreen} $volLevel %{F-}"
        else
                # If it is muted, make the font red
                echo "%{Findianred} $volLevel %{F-}"
        fi
}
```

Next, we will have to make sure it is called and piped to `$PANEL_FIFO`:

```
while true; do
echo "S" "$(panel_volume) $(panel_clock)" > "$PANEL_FIFO"
        sleep 1s
done &

```

#### Using yabar

Using the example panel using lemonbar requires you to set your environment (.profile), and make sure the panel scripts are on your path. Easier panel to set up is [yabar](https://aur.archlinux.org/packages/yabar/), which has just one config file.

### Scratchpad

You can emulate a dropdown terminal (like i3's scratchpad feature if you put a terminal in it) using bspwm's window flags. Append the following to the end of the bspwm config file (adapt to your own terminal emulator):

```
bspc rule -a scratchpad sticky=on state=floating hidden=on
st -c scratchpad -e ~/bin/scratch &

```

The sticky flag ensures that the window is always present on the current desktop. And `~/bin/scratch` is:

```
#!/usr/bin/sh
bspc query -N -n .floating > /tmp/scratchid
$SHELL

```

The hotkey for toggling the scratchpad should be bound to:

```
id=$(cat /tmp/scratchid);\
bspc node $id --flag hidden;bspc node -f $id

```

For a scratch-pad which can use any window type without pre-defined rules, see: [[1]](https://www.reddit.com/r/bspwm/comments/3xnwdf/i3_like_scratch_for_any_window_possible/cy6i585)

For a more sophisticated scratchpad script that supports many terminals out of the box and has flags for doing things like optionally starting a tmuxinator/tmux session, turning any window into a scratchpad on the fly, and automatically resizing a scratchpad to fit the current monitor see [tdrop-git](https://aur.archlinux.org/packages/tdrop-git/).

### Different monitor configurations for different machines

Since the `bspwmrc` is a shell script, it allows you to do things like these:

```
#! /bin/sh

 if [[ $(hostname) == 'myhost' ]]; then
     bspc monitor eDP1 -d I II III IV V VI VII VIII IX X
 elif [[ $(hostname) == 'otherhost' ]]; then
     bspc monitor VGA-0 -d I II III IV V
     bspc monitor VGA-1 -d VI VII VIII IX X
 elif [[ $(hostname) == 'yetanotherhost' ]]; then
     bspc monitor DVI-I-3 -d VI VII VIII IX X
     bspc monitor DVI-I-2 -d I II III IV V
 fi

```

### Set up a desktop where all windows are floating

Here is how to setup the desktop 3 to have only floating windows. It can be useful for Gimp or other apps with multiple windows.

Put this script somewhere in your $PATH and call it from .xinitrc or similar (with a & at the end):

```
#!/bin/bash

 # change the desktop number here
 FLOATING_DESKTOP_ID=$(bspc query -D -d '^3')

 bspc subscribe node_manage | while read -a msg ; do
    desk_id=${msg[2]}
    wid=${msg[3]}
    [ "$FLOATING_DESKTOP_ID" = "$desk_id" ] && bspc node "$wid" -t floating
 done

```

([source](https://github.com/baskerville/bspwm/issues/428#issuecomment-199985423))

### Keyboard

Bspwm does not handle any keyboard input and instead provides the `bspc` program as its interface.

For keyboard shortcuts you will have to setup a hotkey daemon like [sxhkd](https://www.archlinux.org/packages/?name=sxhkd) ([sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/) for the development version).

## Troubleshooting

### Blank screen and keybindings don't work

*   Make sure you are starting sxhkd (in the background as it is blocking).
*   Make sure `~/.config/bspwm/bspwmrc` is executable.

### Window box larger than the actual application

This can happen if you are using GTK3 apps and usually for dialog windows. The fix is to create or add the below to a gtk3 theme file (`~/.config/gtk-3.0/gtk.css`).

```
.window-frame, .window-frame:backdrop {
  box-shadow: 0 0 0 black;
  border-style: none;
  margin: 0;
  border-radius: 0;
}

.titlebar {
  border-radius: 0;
}

```

(source: [Bspwm forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1404973#p1404973))

### Problems with Java applications

If you have problems, like Java application Windows not resizing, or menus immediately closing after you click, see [Java#Applications not resizing with WM, menus immediately closing](/index.php/Java#Applications_not_resizing_with_WM,_menus_immediately_closing "Java").

### Problems with keybindings using fish

If you use [fish](/index.php/Fish "Fish"), you will find that you are unable to switch desktops. This is because bspc's use of the ^ character is incompatible with fish. You can fix this by explicitly telling sxhkd to use bash to execute commands:

```
$ set -U SXHKD_SHELL /usr/bin/bash

```

Alternatively, the ^ character may be escaped with a backslash in your sxhkdrc file.

### Error messages "Could not grab key 43 with modfield 68" on start

Either you try to use the same key twice, or you start sxhkd twice. Check bspwmrc and `~/.profile` or `~/.bash_profile` for excessive commands starting sxhkd.

### Firefox context menu automatically selects first option on right click

Add the following line to the ```userChrome.css``` file of your firefox profile

```
#contentAreaContextMenu{ margin: 5px 0 0 5px }

```

## See also

*   Mailing List: bspwm *at* librelist.com.
*   `#bspwm` - IRC channel at irc.freenode.net
*   [https://bbs.archlinux.org/viewtopic.php?id=149444](https://bbs.archlinux.org/viewtopic.php?id=149444) - Arch BBS thread
*   [https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) - GitHub project
*   [https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies](https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies) - earsplit's "bspwm for dummies"