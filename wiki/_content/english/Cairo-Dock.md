Cairo-Dock is a highly customizable dock written in C.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Plugin dependencies](#Plugin_dependencies)
*   [2 Configuration](#Configuration)
    *   [2.1 Running the dock](#Running_the_dock)
    *   [2.2 Running the dock at startup](#Running_the_dock_at_startup)
        *   [2.2.1 Cairo-Dock method](#Cairo-Dock_method)
        *   [2.2.2 Openbox/Fluxbox](#Openbox.2FFluxbox)
        *   [2.2.3 Xfce](#Xfce)
        *   [2.2.4 GNOME](#GNOME)
    *   [2.3 Configuring the dock](#Configuring_the_dock)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Two Cairo-Docks are running](#Two_Cairo-Docks_are_running)
    *   [3.2 The background is black](#The_background_is_black)
    *   [3.3 Wifi plugin does not show the network strength](#Wifi_plugin_does_not_show_the_network_strength)
*   [4 See also](#See_also)

## Installation

Install [cairo-dock](https://www.archlinux.org/packages/?name=cairo-dock) from the [official repositories](/index.php/Official_repositories "Official repositories"). The core package provides only the strict minimum to run Cairo-Dock - to use applets, animations, views, effects and dialogs you will also need [cairo-dock-plug-ins](https://www.archlinux.org/packages/?name=cairo-dock-plug-ins).

You can also try the development branch with [cairo-dock-git](https://aur.archlinux.org/packages/cairo-dock-git/) and [cairo-dock-plug-ins-git](https://aur.archlinux.org/packages/cairo-dock-plug-ins-git/).

### Plugin dependencies

The applets in [cairo-dock-plug-ins](https://www.archlinux.org/packages/?name=cairo-dock-plug-ins) require quite a lot of dependencies, therefore all of them have been made optional not to bloat your system if you do not use a particular applet. Please refer to the optdepends list and install those you need.

**Note:** If for some reason an applet is not working, make sure you have GVFS installed, it is required for several applets as well as GNOME, XFCE and KDE integration.

## Configuration

### Running the dock

Run the dock in the background:

```
$ cairo-dock &

```

This will generate a startup message that will ask you to choose a backend for the current session (OpenGL or Cairo). There is an option to remember the choice and if not choosing to remember the choice, a startup message will be generated each time Cairo-Dock is run without backend options. To supress the startup message, you can specify which backend to use when running Cairo-Dock by specifying it as an option.

Run the dock with OpenGL backend:

```
$ cairo-dock -o &

```

Run the dock with Cairo backend:

```
$ cairo-dock -c &

```

**Tip:** All using ATI graphics cards should use this option. Some cards/drivers do not support OpenGL, which may prevent Cairo-Dock from running correctly.

### Running the dock at startup

This depends on which desktop environment or window manager that is being used and which backend Cairo-Dock should be run with. The following section shows how to run Cairo-Dock at startup without forcing a backend.

#### Cairo-Dock method

Run Cairo-Dock and right-click the dock and go to **Cairo-Dock > Launch Cairo-Dock on startup**. The settings will be stored in `~/.config/autostart/` and sourced the next time you login.

#### Openbox/Fluxbox

Add the following to `~/.config/openbox/autostart` or `~/.fluxbox/startup` accordingly:

```
cairo-dock &

```

#### Xfce

If you have `xfce4-autostart-editor` installed, simply run it and add an entry for Cairo-Dock. If you are not using a session manager you can add the following to `~/.config/xfce4/xinitrc` or `~/Desktop/Autostart`:

```
cairo-dock &

```

#### GNOME

Add a Cairo-Dock entry to Startup Programs using

```
$ gnome-session-properties

```

### Configuring the dock

To configure the dock, right-click the dock and go to **Cairo-Dock > Configure**.

## Troubleshooting

### Two Cairo-Docks are running

This is most likely a result of saved sessions being runned at login. If you are using a desktop environment like [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE") or [Xfce](/index.php/Xfce "Xfce") you need to disable automatic startup of sessions in your session manager settings. You may also need to delete the sessions cache:

```
$ rm ~/.cache/sessions/x*

```

If you are not using a desktop environment with a session manager or choose to have Cairo-Dock startup by itself, you need to remove autostart files generated by Cairo-Dock:

```
$ rm ~/.config/autostart/cairo-dock*

```

### The background is black

This is most likely caused by not running a composite manager, like [Xcompmgr](/index.php/Xcompmgr "Xcompmgr"). Cairo-Dock uses the transparency feature of the composite manager to display the dock, and without it the dock will be displayed with a black background. If you are using a desktop environment, simply enable the composite manager or desktop effects in the settings.

An alternative solution that does not require a composite manager is to enable fake transparency in Cairo-Dock. To do this, right-click the dock and go to **Cairo-Dock > Configure > Advanced Mode > System > Composition**. Then enable both **Emulate composition with fake transparency** and **Make the config panel transparent**.

### Wifi plugin does not show the network strength

If you added the wifi plugin, and it isn't showing the network strength, you have to certify that you have iwconfig installed (the plugin depends on it) and that you have permission to read the full output of iwconfig.

To install iwconfig:

```
# pacman -S wireless_tools

```

And to get the permission to read the full output of the iwconfig as a normal user (read more about [Capabilities](/index.php/Capabilities "Capabilities")):

```
# setcap cap_net_raw,cap_net_admin=eip /usr/bin/iwconfig

```

## See also

*   [glx-dock.org](http://www.glx-dock.org/index.php)
*   [Launchpad](https://launchpad.net/cairo-dock/)