Related articles

*   [LXDE](/index.php/LXDE "LXDE")
*   [Display manager](/index.php/Display_manager "Display manager")

LXDM is a lightweight [display manager](/index.php/Display_manager "Display manager") for the [LXDE](/index.php/LXDE "LXDE") [desktop environment](/index.php/Desktop_environment "Desktop environment"). The UI is implemented with [GTK+](/index.php/GTK%2B "GTK+") 2.

LXDM does not support the [XDMCP](/index.php/XDMCP "XDMCP") protocol. An alternative that does is [LightDM](/index.php/LightDM "LightDM").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Default session](#Default_session)
        *   [2.1.1 Globally](#Globally)
        *   [2.1.2 Per user](#Per_user)
    *   [2.2 Autologin](#Autologin)
    *   [2.3 Last used options](#Last_used_options)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Adding face icons](#Adding_face_icons)
    *   [3.2 Simultaneous users and switching users](#Simultaneous_users_and_switching_users)
    *   [3.3 Themes](#Themes)
    *   [3.4 Advanced Session Configuration](#Advanced_Session_Configuration)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 White flash](#White_flash)

## Installation

[Install](/index.php/Install "Install") the [lxdm](https://www.archlinux.org/packages/?name=lxdm) package, or [lxdm-gtk3](https://www.archlinux.org/packages/?name=lxdm-gtk3) for the GTK3 version. The development package is [lxdm-git](https://aur.archlinux.org/packages/lxdm-git/).

[Enable](/index.php/Enable "Enable") the provided `lxdm.service` [systemd](/index.php/Systemd "Systemd") unit to start LXDM at boot.

## Configuration

The configuration files for LXDM are all located in `/etc/lxdm/`. The main configuration file is `lxdm.conf`, and is well documented in its comments. Another file, `Xsession`, is the systemwide x session configuration file and should generally not be edited. The other files in this folder are all shell scripts, which are run when certain events happen in LXDM.

These are:

1.  `LoginReady` is executed with root privileges when LXDM is ready to show the login window.
2.  `PreLogin` is run as root before logging a user in.
3.  `PostLogin` is run as the logged-in user right after he has logged in.
4.  `PostLogout` is run as the logged-in user right after he has logged out.
5.  `PreReboot` is run as root before rebooting with LXDM.
6.  `PreShutdown` is run as root before poweroff with LXDM.

### Default session

It can be specified which session will be loaded when the users select the 'Default' session from the session list. Note that the user setting takes preference over global setting.

#### Globally

Edit `/etc/lxdm/lxdm.conf` and change the session line to whatever session or DE is desired:

 `session=/usr/bin/startlxde` 

Example using [Xfce](/index.php/Xfce "Xfce"):

 `session=/usr/bin/startxfce4` 

Example using [Openbox](/index.php/Openbox "Openbox"):

 `session=/usr/bin/openbox-session` 

Example using [GNOME](/index.php/GNOME "GNOME"):

 `session=/usr/bin/gnome-session` 

This is useful for themes that have no visible session selection box, and if experiencing trouble using autologin.

#### Per user

To define an individual user's preferred session, simply edit his/her respective `~/.dmrc` to define the selection.

Example: user1 wants Xfce4, user2 wants [Cinnamon](/index.php/Cinnamon "Cinnamon"), and user3 wants GNOME:

For user1:

```
[Desktop]
Session=xfce

```

For user2:

```
[Desktop]
Session=cinnamon

```

For user3:

```
[Desktop]
Session=gnome

```

### Autologin

To log in to one account automatically on startup, without providing a password, find the line in `/etc/lxdm/lxdm.conf` that looks like this:

```
#autologin=dgod

```

Uncomment it, substituting the target user instead of *dgod*.

### Last used options

It stores information about last used options in the:

 `/var/lib/lxdm/lxdm.conf` 
```
[base]
last_session=/usr/share/xsessions/LXDE.desktop
last_lang=sv_SE.UTF-8
last_langs=sv_SE.UTF-8 fa_IR.UTF-8 en_US.UTF-8
```

**Note:** This file is not removed after uninstallation. And must be removed manually if you want to remove all traces of LXDM used options.

## Tips and tricks

### Adding face icons

A 96x96 px image (jpg or png) can optionally be displayed on a per-user basis replacing the stock icon. Simply copy or symlink the target image to `$HOME/.face`. The [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) package supplies some default icons suitable for the lxdm screen. Look under `/usr/share/pixmaps/faces` after installing that package.

**Note:**

*   Users need not keep [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) installed to use this images. Simply install it, copy them elsewhere, and remove it.
*   The user's directory needs have r-x permissions for others and the .face file needs have r-- permissions for others. Obviously though this has security and access implications as now anyone can browse your home directory.
*   A graphical tool `lxdm-config` shipped with lxdm can be used to place a `.face` file in the home directory, along with other configuration.

### Simultaneous users and switching users

LXDM allows multiple users to be logged into different ttys at the same time. The following command is used to allow another user to login without logging out the current user:

```
$ lxdm -c USER_SWITCH

```

**Note:** When the new user logs in, his/her session is now on the NEXT tty from tty7\. For example, user1 logs in and issues the USER_SWITCH command. Now user2 logs in. User2 will be on tty7 while user1 will be on tty1.

### Themes

The LXDM themes are located in `/usr/share/lxdm/themes`.

There is only one theme provided with LXDM, namely Industrial. To display the background file `wave.svg` which is part of this theme, make sure you have [librsvg](https://www.archlinux.org/packages/?name=librsvg) installed.

[lxdm-themes](https://aur.archlinux.org/packages/lxdm-themes/) provides 6 extra themes. Archlinux, ArchlinuxFull, ArchlinuxTop, Arch-Dark, Arch-Stripes and IndustrialArch. The ArchStripes and ArchDark themes are also provided with [lxdm-git](https://aur.archlinux.org/packages/lxdm-git/) (with different names to avoid file conflicts).

You can configure them on `/etc/lxdm/lxdm.conf`:

```
## the theme of greeter
theme=theme_name

```

You can also configure LXDM to use a GTK theme (stored in `/usr/share/themes`) on the mentioned configuration file:

```
## GTK theme
gtk_theme=gtk_theme_name

```

### Advanced Session Configuration

After a user logs on, LXDM sources *all* of the following files, in order:

1.  `/etc/profile`
2.  `~/.profile`
3.  `/etc/xprofile`
4.  `~/.xprofile`

These files can be used to set session environment variables and to start services which must set certain environment variables in order for clients in the session to be able to use the service, like ssh-agent. See [Xprofile](/index.php/Xprofile "Xprofile") for details.

Note that LXDM does *not* source `~/.xinitrc`, so those migrating from a DM that *does* use this file, like [SLiM](/index.php/SLiM "SLiM"), will have to move their settings elsewhere — probably `~/.xprofile`. Also note LXDM does not source `~/.bash_profile`.

If you still want to use your `~/.xinitrc` file, you can add a line to the `/etc/lxdm/PostLogin` event file:

```
source ~/.xinitrc

```

LXDM also makes use of .[Xresources](/index.php/Xresources "Xresources"), .[Xkbmap](/index.php/Xkbmap "Xkbmap"), and .[Xmodmap](/index.php/Xmodmap "Xmodmap"). See `/etc/lxdm/Xsession` for details on how LXDM uses system-wide and per-user configuration files to configure the session.[[1]](https://projects.archlinux.org/svntogit/community.git/tree/trunk/Xsession?h=packages/lxdm)

## Troubleshooting

### White flash

When using the default LXDM `theme=Industrial` and a dark background image (e.g. `bg=/usr/share/backgrounds/img.png`) there may be a short bright flash before LXDM starts. This is caused by the `bg_color:` property of the selected [GTK+](/index.php/GTK%2B "GTK+") theme. To avoid this change `gtk_theme=Adwaita` to `gtk_theme=Adwaita-dark` or to another dark theme.