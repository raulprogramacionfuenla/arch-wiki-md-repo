Related articles

*   [GNOME](/index.php/GNOME "GNOME")

[Guake](http://guake-project.org/) is a top-down terminal for [GNOME](/index.php/GNOME "GNOME") (in the style of [Yakuake](/index.php/Yakuake "Yakuake") for [KDE](/index.php/KDE "KDE"), [Tilda](/index.php/Tilda "Tilda") or the terminal used in Quake).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Autostartup](#Autostartup)
*   [4 Guake scripting](#Guake_scripting)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 In Floating WM](#In_Floating_WM)
    *   [5.2 Toggling Guake visibility does not work (Wayland)](#Toggling_Guake_visibility_does_not_work_.28Wayland.29)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [guake](https://www.archlinux.org/packages/?name=guake), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Once installed, you can start Guake from the terminal with:

```
$ guake

```

After guake has started you can right click on the interface and select *Preferences* to change the hotkey to drop the terminal automatically, by default it is set to `F12`.

## Autostartup

You may want Guake to load on starting up Desktop Environment. To do this, you need to

```
# cp /usr/share/applications/guake.desktop /etc/xdg/autostart/

```

See [Autostarting](/index.php/Autostarting "Autostarting") for more info.

## Guake scripting

Like [Yakuake](/index.php/Yakuake "Yakuake"), Guake allows to control itself at runtime by sending the [D-Bus](/index.php/D-Bus "D-Bus") messages. Thus it can be used to start Guake in a user defined session. You can create tabs, assign names for them and also ask to run any specific command in any opened tab or just to show/hide Guake window, manually in a terminal or by creating a custom script for it.

Example of such a script is given below this section.

You can use *guake* executable itself to send D-Bus messages. Here is the list of available options you may be interested in:

*   `-t`, `--toggle-visibility` — toggle the visibility of the terminal window. Actually, you can just type `guake`, and it will toggle the visibility of already running instance.
*   `-f`, `--fullscreen` — put Guake to fullscreen mode.
*   `--show` — show Guake main window.
*   `--hide` — hide Guake main window.
*   `-n *CUR_DIR*`, `--new-tab=*CUR_DIR*` — create new tab and select it. Value of `CUR_DIR` used to set a current directory for the tab, if specified.
*   `-s *INDEX*`, `--select-tab=*INDEX*` — select tab with index `INDEX`. Tab indexes are started with 0.
*   `-g`, `--selected-tab` — print index of currently selected tab.
*   `-e *CMD*`, `--execute-command=*CMD*` — execute an arbitrary command `CMD` in the selected tab.
*   `-i *INDEX*`, `--tab-index=*INDEX*` — used with `--rename-tab` to specify index `INDEX` of a tab to rename. Default value is 0.
*   `--rename-tab=*TITLE*` — set the tab name to `TITLE`. You can reset tab title to default value by passing a single dash (`"-"`). Use `-i` option to specify which tab to rename.
*   `--bgcolor=*RGB*` — set the hexadecimal (`#rrggbb`) background color `RGB` of the selected tab.
*   `--fgcolor=*RGB*` — set the hexadecimal (`#rrggbb`) foreground color `RGB` of the selected tab.
*   `-r *TITLE*`, `--rename-current-tab=*TITLE*` — same as `--rename-tab`, but renames the currently selected tab.
*   `-q`, `--quit` — shutdown running Guake instance.

Multiple options may be combined in a single call. If there's no guake instance running, all of the options specified will be applied to the newly created instance.

To display list of all available options, type `guake --help`.

There are 2 ways of starting guake while applying these scripts

*   copying the below example into a file like `guake-init.sh` making it executable and running that file instead of guake
*   right clicking on `Guake Terminal > Preferences > General` and adding the path to the `guake-init.sh` script in the "Path to script executed on Guake start:" section while making certain to comment out `/usr/bin/guake &` from the script below

The second option is preferable if you want the script to run regardless of how guake is started and you can still instruct guake not to run the script with `guake --no-startup-script` if needed.

Example:

```
#!/bin/bash

/usr/bin/guake &
sleep 5 # let main guake process start and initialize D-Bus session

# adjust tab which was opened by default
guake --rename-tab="iotop" --execute="/usr/bin/iotop"

# create new tab, start bash session in it
guake --new-tab --execute="/usr/bin/bash"
# and then execute htop, renaming the tab to "htop"
guake --execute="/usr/bin/htop" --rename-current-tab="htop"

# ...
guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/atop" --rename-current-tab="atop"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="~/.iptables.sh" --rename-current-tab="iptables -nvL"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/journalctl --follow --full" --rename-current-tab="journalctl"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/irssi" --rename-current-tab="irssi"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-current-tab="rootshell0"

guake --new-tab --execute="/usr/bin/bash"
guake --execute="/usr/bin/sudo -i" --rename-current-tab="rootshell1"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-current-tab="shell0"

guake --new-tab --execute="/usr/bin/bash"
guake --rename-current-tab="shell1"

```

Notice than we should wait some time calling *sleep* to avoid race conditions between running instances.

**Warning:** `--execute` option can make harmful things on a tab running text interface program, like `fdisk` or `innotop`. Use it with caution. There is a bug on github about it: [guake#921](https://github.com/Guake/guake/issues/921).

## Troubleshooting

### In Floating WM

If you are using Tilda and a floating WM, you may find out that you can use class string "Tilda" to set the window keep floating. But that Guake's WM_CLASS(STRING)'s out put is "Main.py", so you should use "Main.py" to do this. For example, in i3wm, add this to your .i3/config:

```
for_window [class="Main.py"] floating enable

```

### Toggling Guake visibility does not work (Wayland)

If you are using Wayland, the Guake visibility toggle hotkey may not work under some applications. This is because Guake uses a global hotkey library made for X environments and there is no equivalent global hotkey interface for Wayland. Many applications (e.g. Firefox) run on Wayland through XWayland where the Guake toggle will work but others that natively run Wayland (e.g. GNOME apps) disable Guake toggle functionality.

If you do not wish to switch over to an X environment, a simple workaround requires configuring a shortcut with your window manager/desktop environment for the command `guake-toggle`.

See [github issue](https://github.com/Guake/guake/issues/994) for more details.

**Note:** Using `guake-toggle` is [recommended](https://github.com/Guake/guake/blob/master/docs/source/user/faq.rst#manual-keybinding) over `guake -t`. It is much faster since it goes directly over D-Bus without fully initializing Guake.

## See also

*   [guake(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/guake.1)