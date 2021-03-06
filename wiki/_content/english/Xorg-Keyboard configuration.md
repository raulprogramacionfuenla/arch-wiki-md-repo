Related articles

*   [X keyboard extension](/index.php/X_keyboard_extension "X keyboard extension")
*   [Linux console/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration")
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Keyboard shortcuts](/index.php/Keyboard_shortcuts "Keyboard shortcuts")

This article describes the basics of [Xorg](/index.php/Xorg "Xorg") keyboard configuration. For advanced topics such as keyboard layout modification or additional key mappings, see [X keyboard extension](/index.php/X_keyboard_extension "X keyboard extension") or [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") respectively.

The Xorg server uses the [X keyboard extension](/index.php/X_keyboard_extension "X keyboard extension") (XKB) to define keyboard layouts. Optionally, [xmodmap](/index.php/Xmodmap "Xmodmap") can be used to access the internal keymap table directly, although this is not recommended for complex tasks. Also [systemd](/index.php/Systemd "Systemd")'s *localectl* can be used to define the keyboard layout for both the Xorg server and the virtual console.

**Note:** XKB options can be overridden by the tools provided by some desktop environments such as [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Viewing keyboard settings](#Viewing_keyboard_settings)
    *   [1.1 Third party utilities](#Third_party_utilities)
*   [2 Setting keyboard layout](#Setting_keyboard_layout)
    *   [2.1 Using setxkbmap](#Using_setxkbmap)
    *   [2.2 Using X configuration files](#Using_X_configuration_files)
        *   [2.2.1 Using localectl](#Using_localectl)
*   [3 Frequently used XKB options](#Frequently_used_XKB_options)
    *   [3.1 Switching between keyboard layouts](#Switching_between_keyboard_layouts)
    *   [3.2 Terminating Xorg with Ctrl+Alt+Backspace](#Terminating_Xorg_with_Ctrl+Alt+Backspace)
    *   [3.3 Swapping Caps Lock with Left Control](#Swapping_Caps_Lock_with_Left_Control)
    *   [3.4 Enabling mouse keys](#Enabling_mouse_keys)
    *   [3.5 Configuring compose key](#Configuring_compose_key)
        *   [3.5.1 Key combinations](#Key_combinations)
    *   [3.6 Currency sign on other key](#Currency_sign_on_other_key)
    *   [3.7 Switching state immediately when Caps Lock is pressed](#Switching_state_immediately_when_Caps_Lock_is_pressed)
        *   [3.7.1 Workaround](#Workaround)
*   [4 Adjusting typematic delay and rate](#Adjusting_typematic_delay_and_rate)
    *   [4.1 Using xset](#Using_xset)
    *   [4.2 Using XServer startup options](#Using_XServer_startup_options)
*   [5 See also](#See_also)

## Viewing keyboard settings

You can use the following command to see the actual XKB settings:

 `$ setxkbmap -print -verbose 10` 
```
Setting verbose level to 10
locale is C
Applied rules from evdev:
model:      evdev
layout:     us
options:    terminate:ctrl_alt_bksp
Trying to build keymap using the following components:
keycodes:   evdev+aliases(qwerty)
types:      complete
compat:     complete
symbols:    pc+us+inet(evdev)+terminate(ctrl_alt_bksp)
geometry:   pc(pc104)
xkb_keymap {
        xkb_keycodes  { include "evdev+aliases(qwerty)" };
        xkb_types     { include "complete"      };
        xkb_compat    { include "complete"      };
        xkb_symbols   { include "pc+us+inet(evdev)+terminate(ctrl_alt_bksp)"    };
        xkb_geometry  { include "pc(pc104)"     };
};

```

### Third party utilities

There are some "unofficial" utilities which allow to print specific information about the currently used keyboard layout.

*   [xkb-switch-git](https://aur.archlinux.org/packages/xkb-switch-git/):

 `$ xkb-switch`  `us` 

*   [xkblayout-state-git](https://aur.archlinux.org/packages/xkblayout-state-git/):

 `$ xkblayout-state print "%s"`  `de` 

## Setting keyboard layout

Keyboard layout in Xorg can be set in multiple ways. Here is an explanation of used options:

*   `XkbModel` selects the keyboard model. This has an influence only for some extra keys your keyboard might have. The safe fallback are `pc104` or `pc105`. But for instance laptops usually have some extra keys, and sometimes you can make them work by simply setting a proper model.
*   `XkbLayout` selects the keyboard layout. Multiple layouts may be specified in a comma-separated list, e.g. if you want to quickly switch between layouts.
*   `XkbVariant` selects a specific layout variant. For instance, the default `sk` variant is `qwertz`, but you can manually specify `qwerty`, etc.
*   `XkbOptions` contains some extra options. Used for specifying layout switching, notification LED, compose mode etc. See the [#Frequently used XKB options](#Frequently_used_XKB_options) section for examples.

**Note:** You must specify as many variants as the number of specified layouts. If you want the default variant, specify an empty string as the variant (the comma must stay). For example, to have the default `us` layout as primary and the `dvorak` variant of `us` layout as secondary, specify `us,us` as `XkbLayout` and `,dvorak` as `XkbVariant`.

The layout name is usually a [2-letter country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2"). To see a full list of keyboard models, layouts, variants and options, along with a short description, open `/usr/share/X11/xkb/rules/base.lst`. Alternatively, you may use one of the following commands to see a list without a description:

*   `localectl list-x11-keymap-models`
*   `localectl list-x11-keymap-layouts`
*   `localectl list-x11-keymap-variants [*layout*]`
*   `localectl list-x11-keymap-options`

Examples in the following subsections will have the same effect, they will set `pc104` model, `cz` as primary layout, `us` as secondary layout, `dvorak` variant for `us` layout and the `Alt+Shift` combination for switching between layouts. See [xkeyboard-config(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xkeyboard-config.7) for more detailed information.

### Using setxkbmap

*setxkbmap* sets the keyboard layout for the current X session only, but can be made persistent in [xinitrc](/index.php/Xinitrc "Xinitrc") or [xprofile](/index.php/Xprofile "Xprofile"). This overrides system-wide configuration specified following [#Using X configuration files](#Using_X_configuration_files).

The usage is as follows (see [setxkbmap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setxkbmap.1)):

```
$ setxkbmap [-model *xkb_model*] [-layout *xkb_layout*] [-variant *xkb_variant*] [-option *xkb_options*]

```

To change just the layout (`-layout` is the default flag):

```
$ setxkbmap *xkb_layout*

```

For multiple customizations:

```
$ setxkbmap -model pc104 -layout cz,us -variant ,dvorak -option grp:alt_shift_toggle

```

### Using X configuration files

**Note:** `xorg.conf` is parsed by the X server at start-up. To apply changes, restart X.

The syntax of X configuration files is explained in [Xorg#Configuration](/index.php/Xorg#Configuration "Xorg"). This method creates system-wide configuration which is persistent across reboots.

Here is an example:

 `/etc/X11/xorg.conf.d/00-keyboard.conf` 
```
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout" "cz,us"
        Option "XkbModel" "pc104"
        Option "XkbVariant" ",dvorak"
        Option "XkbOptions" "grp:alt_shift_toggle"
EndSection

```

#### Using localectl

For convenience, the tool *localectl* may be used instead of manually editing X configuration files. It will save the configuration in `/etc/X11/xorg.conf.d/00-keyboard.conf`, this file should not be manually edited, because *localectl* will overwrite the changes on next start.

The usage is as follows:

```
$ localectl [--no-convert] set-x11-keymap *layout* [*model* [*variant* [*options*]]]

```

To set a *model*, *variant* or *options*, all preceding fields need to be specified, but the preceding fields can be skipped by passing an empty string with `""`. Unless the `--no-convert` option is passed, the specified keymap is also converted to the closest matching console keymap and applied to the [console configuration](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") in `vconsole.conf`. See [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) for more information.

To create a `/etc/X11/xorg.conf.d/00-keyboard.conf` like the above:

```
$ localectl --no-convert set-x11-keymap cz,us pc104 ,dvorak grp:alt_shift_toggle

```

## Frequently used XKB options

### Switching between keyboard layouts

To be able to easily switch keyboard layouts, first specify multiple layouts between which you want to switch (the first one is the default). Then specify a key (or key combination), which will be used for switching. For example, to switch between a US and a Swedish layout using the `CapsLock` key, use `us,se` as an argument of `XkbLayout` and `grp:caps_toggle` as an argument of `XkbOptions`.

You can use other key combinations than `CapsLock`, they are listed in `/usr/share/X11/xkb/rules/base.lst`, start with `grp:` and end with `toggle`. To get the full list of available options, run the following command:

```
$ grep "grp:.*toggle" /usr/share/X11/xkb/rules/base.lst

```

### Terminating Xorg with Ctrl+Alt+Backspace

By default, the key combination `Ctrl+Alt+Backspace` is disabled. You can enable it by passing `terminate:ctrl_alt_bksp` to `XkbOptions`. This can also be done by binding a key to `Terminate_Server` in `xmodmap` (which undoes any existing `XkbOptions` setting). In order for either method to work, one also needs to have `DontZap` set to "off" in `ServerFlags`; however, from at least version R6.8.0 (year 2004) [[1]](https://www.x.org/archive/X11R6.8.0/doc/xorg.conf.5.html) this is the default.

### Swapping Caps Lock with Left Control

To swap Caps Lock with Left Control key, add `ctrl:swapcaps` to `XkbOptions`. Run the following command to see similar options along with their descriptions:

```
$ grep -E "(ctrl|caps):" /usr/share/X11/xkb/rules/base.lst

```

### Enabling mouse keys

[Mouse keys](https://en.wikipedia.org/wiki/Mouse_keys "w:Mouse keys") is disabled by default and has to be manually enabled by passing `keypad:pointerkeys` to `XkbOptions`. This will make the `Shift+NumLock` shortcut toggle mouse keys.

See also [X keyboard extension#Mouse control](/index.php/X_keyboard_extension#Mouse_control "X keyboard extension") for advanced configuration.

### Configuring compose key

Though typically not on traditional keyboards, a [Compose key](https://en.wikipedia.org/wiki/Compose_key "wikipedia:Compose key") can be configured to an existent key.

The `Compose` key begins a keypress sequence that involves (usually two) additional keypresses. Usage is typically either for entering characters in a language that the keyboard was not designed for, or for other less-used characters that are not covered with the `AltGr` modifier. For example, pressing `Compose` `'` `e` produces `é`, or `Compose` `-` `-` `-` will produce an "em dash": `—`.

Though a few more eccentric keyboards feature a `Compose` key, its availability is usually through substituting an already existing key to it. For example, to make the `Menu` key a `Compose` key use the [Desktop environment](/index.php/Desktop_environment "Desktop environment") configuration, or pass `compose:menu` to `XkbOptions` (or [setxkbmap](#Using_setxkbmap): `setxkbmap -option compose:menu`). Allowed key substitutions are defined in `/usr/share/X11/xkb/rules/base.lst`:

```
$ grep "compose:" /usr/share/X11/xkb/rules/base.lst

```

If the desired mapping is not found in that file, an alternative is to use [xmodmap](/index.php/Xmodmap "Xmodmap") to map the desired key to the `Multi_key` keysym, which acts as a compose key by default (note that *xmodmap* settings are reset by *setxkbmap*).

#### Key combinations

The default combinations for the compose keys depend on the [locale](/index.php/Locale "Locale") configured for the session and are stored in `/usr/share/X11/locale/*used_locale*/Compose`, where `*used_locale*` is for example `en_US.UTF-8`.

You can define your own compose key combinations by copying the default file to `~/.XCompose` and editing it. Alternatively, create an empty `~/.XCompose` and include the default one using `include "%L"`, for example:

 `~/.XCompose` 
```
include "%L"

<Multi_key> <g> <a> : "α"
<Multi_key> <g> <b> : "β"
<Multi_key> <g> <g> : "γ"

```

The compose key works with any of the thousands of valid Unicode characters, including those outside the Basic Multilingual Plane. Take a look at the [Compose(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Compose.5) man page, it explains the format of the XCompose files.

However, GTK does not use [XIM](https://en.wikipedia.org/wiki/X_Input_Method "wikipedia:X Input Method") by default and therefore does not follow `~/.XCompose` keys. This can be fixed by forcing GTK to use XIM by adding `export GTK_IM_MODULE=xim` and/or `export XMODIFIERS="@im=none"` to `~/.xprofile`.

**Tip:** XIM is very old, you might have better luck with other input methods: [SCIM](/index.php/SCIM "SCIM"), [UIM](/index.php/UIM "UIM"), [IBus](/index.php/IBus "IBus"), etc. See [Localization#Input methods](/index.php/Localization#Input_methods "Localization") for details.

**Note:** XIM will prevent insertion of Unicode characters with the `Ctrl+Shift+u` combination.

### Currency sign on other key

Most European keyboards have a Euro sign (€) printed on on the `5` key. For example, to access it with `Alt+5`, use the `lv3:lalt_switch` and `eurosign:5` options.

The Rupee sign (₹) can be used the same way with `rupeesign:4`.

### Switching state immediately when Caps Lock is pressed

Those who prefer typing capital letters with the Caps Lock key may experience a short delay when Caps Lock state is switched, resulting in two or more capital letters (e.g. *THe*, *ARch LInux*). This behaviour [stems from typewriters](https://en.wikipedia.org/wiki/Caps_lock#History "wikipedia:Caps lock").

Some more popular operating systems have removed this behaviour, either voluntarily (as it can be confusing to some) or by mistake, however this is a question of preference. Bug reports have been filed on the Xserver bug tracker, as there is currently no easy way to switch to the behaviour reflected by those other operating systems. For anyone who would like to follow up the issue, bug reports and latest working progress can be found at [[2]](https://bugs.freedesktop.org/show_bug.cgi?id=27903) and [[3]](https://gitlab.freedesktop.org/xorg/xserver/issues/312).

#### Workaround

First, export your keyboard configurations to a file:

```
$ xkbcomp -xkb $DISPLAY xkbmap

```

In the file *xkbmap*, locate the Caps Lock section which begins with *key <CAPS>*:

```
 key <CAPS> {         [       Caps_Lock ] };

```

and replace whole section with the following code:

```
key <CAPS> {
    repeat=no,
    type[group1]="ALPHABETIC",
    symbols[group1]=[ Caps_Lock, Caps_Lock],
    actions[group1]=[ LockMods(modifiers=Lock), Private(type=3,data[0]=1,data[1]=3,data[2]=3)]
};

```

Save and reload keyboard configurations:

```
$ xkbcomp -w 0 xkbmap $DISPLAY

```

Consider making it a service launching after X starts, since reloaded configurations do not survive a system reboot.

## Adjusting typematic delay and rate

The *typematic delay* indicates the amount of time (typically in miliseconds) a key needs to be pressed and held in order for the repeating process to begin. After the repeating process has been triggered, the character will be repeated with a certain frequency (usually given in Hz) specified by the *typematic rate*. Note that these settings are configured seperately for Xorg and [for the virtual console](/index.php/Keyboard_configuration_in_console#Adjusting_typematic_delay_and_rate "Keyboard configuration in console").

### Using xset

The tool *xset* can be used to set the typematic delay and rate for an active X server, certain actions during runtime though may cause the XServer to reset these changes and revert instead to its *seat defaults*.

Usage:

```
$ xset r rate *delay* [*rate*]

```

For example to set a typematic delay to 200ms and a typematic rate to 30Hz, use the following command (use [xinitrc](/index.php/Xinitrc "Xinitrc") to make it permanent):

```
$ xset r rate 200 30

```

Issuing the command without specifying the delay and rate will reset the typematic values to their respective defaults; a delay of 660ms and a rate of 25Hz:

```
$ xset r rate

```

### Using XServer startup options

A more resistant way to set the typematic delay and rate is to make them the *seat defaults* by passing the desired settings to the X server on its startup using the following options:

*   `-ardelay *miliseconds*` - sets the autorepeat delay (length of time in milliseconds that a key must be depressed before autorepeat starts).
*   `-arinterval *miliseconds*` - sets the autorepeat interval (length of time in milliseconds that should elapse between autorepeat-generated keystrokes).

See [Xserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xserver.1) for a full list of X server options and refer to your [display manager](/index.php/Display_manager "Display manager") for information about how to pass these options.

## See also

*   [Madduck guide on extending XKB](https://web.archive.org/web/20170825051821/http://madduck.net:80/docs/extending-xkb/) (archived at Wayback Machine)