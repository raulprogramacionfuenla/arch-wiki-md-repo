[Crostini](https://chromium.googlesource.com/chromiumos/docs/+/master/containers_and_vms.md) is Google's umbrella term for making Linux application support easy to use and integrating well with Chrome OS.

This article describes how to install Arch Linux on a Chromebook in a container (via Crostini), without needing to enable developer mode, allowing apps to run alongside other Chrome/Android apps.

	Advantages

*   Don't need to enable developer mode - Officially supported, leaves ChromeOS secure, no need to flash a BIOS etc.
*   Better battery life - Battery life of Chrome with the functionality of Linux.
*   Access to Android apps, play store etc.

	Disadvantages

*   Audio support is still [in progress](https://crbug.com/781398) (Feb 4 2019)
*   OpenGL support is still [in progress](https://crbug.com/837073) (Feb 4 2019)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
    *   [1.1 Enabling Linux support](#Enabling_Linux_support)
    *   [1.2 Replacing the default Debian Linux container with Arch Linux](#Replacing_the_default_Debian_Linux_container_with_Arch_Linux)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Network not working on Pixelbook](#Network_not_working_on_Pixelbook)
    *   [2.2 DNS resolution not working](#DNS_resolution_not_working)
    *   [2.3 App not opening in chrome OS (infinite spinner)](#App_not_opening_in_chrome_OS_(infinite_spinner))
    *   [2.4 Steam / OpenGL / GLX not working](#Steam_/_OpenGL_/_GLX_not_working)
    *   [2.5 App that requires sound card not working](#App_that_requires_sound_card_not_working)

## Introduction

### Enabling Linux support

Look for Linux under Settings and enable it. This installs a Debian Linux container that we will then replace with an Arch Linux container.

	*Settings > Linux > Enable*

Crostini is still rolling out to Chromebooks. If you don't see an option to enable Linux, you may need to switch to the beta or developer channel, if it has not rolled out to the stable channel for your laptop yet. This can be done via *Settings > About Chrome OS > Channel > Dev/Beta*.

### Replacing the default Debian Linux container with Arch Linux

The below instructions were taken from [https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux](https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux)

1\. Install an Arch linux container

Open a new terminal in Chrome (Ctrl + Alt + T). Then connect to terminal and create an arch linux container:

```
vsh termina
run_container.sh --container_name arch --user <gmail username> --lxd_image archlinux/current --lxd_remote [https://us.images.linuxcontainers.org/](https://us.images.linuxcontainers.org/)

```

The <gmail username> here is the same user you are logged in to your Chromebooks as, without the @gmail.com and dots. eg. foo.bar@gmail.com will set --user foobar. Apps launched from the ChromeOS launcher run under this user.

2\. Replace the default Debian container with Arch Linux.

The default Debian container is named penguin. Renaming the "arch" container created above to it will cause chrome to launch Linux apps from the arch container.

```
lxc stop arch
lxc stop penguin
lxc rename penguin debian
lxc rename arch penguin

```

3\. Set password for gmail username

By default the gmail user has no password set. Use lxc exec to set a password:

```
lxc exec penguin -- bash

```

You also might want to add [sudo](/index.php/Sudo "Sudo") and add the user to sudoers.

4\. Install Crostini container tools, Wayland for GUI apps, XWayland for X11 apps.

First open a console session the the Arch Linux container.

```
lxc console penguin

```

[Install](/index.php/Install "Install") the [cros-container-guest-tools-git](https://aur.archlinux.org/packages/cros-container-guest-tools-git/) package. Additionally install [wayland](https://www.archlinux.org/packages/?name=wayland) and [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) to be able to use GUI tools.

At present (11-24-2018) xkeyboard-config 2.24 break the sommelier-x service. Workaround is to comment out two lines starting with "<i372>" and "<i374>" in /usr/share/X11/xkb/keycodes/evdev. Then enable and start the services.

```
$ systemctl --user enable sommelier@0      # For Wayland GUI apps
$ systemctl --user enable sommelier-x@0    # For X11 GUI apps
$ systemctl --user start sommelier@0      # For Wayland GUI apps
$ systemctl --user start sommelier-x@0    # For X11 GUI apps

```

Make sure these services are running successfully by running:

```
$ systemctl --user status sommelier@0
$ systemctl --user status sommelier-x@0

```

Now, when apps are installed in Arch Linux, they will automatically show up and can be launched from ChromeOS. Note that while GUI apps work, rendering is still software, with no OpenGL support yet.

## Troubleshooting

### Network not working on Pixelbook

[https://tedyin.com/posts/archlinux-on-pixelbook/](https://tedyin.com/posts/archlinux-on-pixelbook/) reports that the below setting needs to be set to get the network working on the pixelbook. Make sure to restart your container after you set it.

```
lxc profile set default security.syscalls.blacklist "keyctl errno 38"

```

### DNS resolution not working

DNS resolution stopped working in the container after my install. To get it working again I had to create [/etc/resolv.conf](/index.php//etc/resolv.conf "/etc/resolv.conf").

As of Jan 2019, my container wasn't able to resolve ".org" DNS, I had to modify [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5) (only the hosts line).

```
 hosts: files dns

```

### App not opening in chrome OS (infinite spinner)

I found that launching a console (lxc console penguin) session prevents apps from launching in Chrome OS. Launching results in an infinite spinner. In that case I have to stop and start the container to get the Chrome OS launcher working

```
lxc stop penguin
lxc start penguin

```

Instead of using an lxc console session, I use a regular Linux terminal GUI launched from ChomeOS that prevents this issue.

### Steam / OpenGL / GLX not working

I found that Steam / OpenGL / GLX don't work out of the box because the Arch install is different. The issue has to do with sommelier-x. The original crostini [cros-container-guest-tools installer](https://chromium.googlesource.com/chromiumos/containers/cros-container-guest-tools/+/master/cros-sommelier-config/postinst) copies the crostini supplied swrast_dri.so to /usr/lib64/dri/ because "mesa always looks at that path" instead of the version of swrast_dri.so supplied with crostini. This line installing swrast_dri.so is not part of the Arch linux installer, and thus OpenGL apps via X11 do not function. Further, on Arch copying this library over in needed for sommelier-x to work with GLX, allowing steam to work, but glxgears/glxinfo need the default mesa-distributed swrast_dri.so. I've been able to get steam & glxgears with the right combination of libraries by running the below commands each time Arch starts up.

```
 $ glxgears
 Error: couldn't get an RGB, Double-buffered visual

 $ sudo cp /usr/lib64/dri/swrast_dri.so /usr/lib64/dri/swrast_dri.so.backup
 $ sudo cp /opt/google/cros-containers/lib/swrast_dri.so /usr/lib64/dri/swrast_dri.so
 $ systemctl --user restart sommelier-x@0.service

 $ glxinfo
 Segmentation fault (core dumped)
 $ # But Steam works at this point

 $ sudo cp /usr/lib64/dri/swrast_dri.so.backup /usr/lib64/dri/swrast_dri.so

 $ glxgears
 SUCCESS

 $ # But after a few minutes sommelier-x reloads the mesa version and fails.

```

To get steam working I had to replace /usr/lib64/dri/swrast_dri.so with the cros-containers version. This works permanently. I haven't been able to find a way to keep glxgears/glxinfo working permanently.

### App that requires sound card not working

Crostini does not yet support sound. However, a dummy sound card can be created by installing and running pulseaudio that allows apps that require a sound card to run.