Related articles

*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture")

The computer often seems to make beep noises or other sounds at various times, whether we want them or not. They come from various sources, and as such, you may be able to configure if or when they occur. For situations where no sound card or speakers are available and a simple audio notification is desired, see [#Beep](#Beep).

Sounds from the computer can be heard from the built-in case speaker, the speakers, or headphones which are plugged into the soundcard (in which case the noise may be unexpectedly loud).

**Note:** The sounds are caused by the BIOS (Basic Input/Output System), the OS (Operating System), the DE (Desktop Environment), or various software programs. The BIOS is a particularly troublesome problem because it is kept inside an EPROM chip on the motherboard, and the only direct control the user has is by turning the power on or off. Unless the BIOS setup has a setting you can adjust or you wish to attempt to reprogram that chip with the proper light source, it is not likely you will be able to change it at all. BIOS-generated beep sounds are not addressed here, except to say that unplugging your computer case speaker will stop all such sounds from being heard. (Do so at your own risk.)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Disable PC Speaker](#Disable_PC_Speaker)
    *   [1.1 Globally](#Globally)
    *   [1.2 Console](#Console)
        *   [1.2.1 Less pager](#Less_pager)
    *   [1.3 Xorg](#Xorg)
    *   [1.4 ALSA](#ALSA)
    *   [1.5 GNOME](#GNOME)
    *   [1.6 Cinnamon](#Cinnamon)
    *   [1.7 GTK+](#GTK+)
*   [2 Beep](#Beep)
    *   [2.1 Installation](#Installation)
    *   [2.2 Access for non-root users](#Access_for_non-root_users)
    *   [2.3 Tips and Tricks](#Tips_and_Tricks)
*   [3 See also](#See_also)

## Disable PC Speaker

Turning off a particular instance of a sound, while leaving the others operational, is possible if and only if one can identify which portion of the environment generates the particular sound. This allows customizing the selection of sounds. Please feel free to add any configurations and settings to this wiki page that may be useful for other users.

### Globally

The PC speaker can be disabled by [unloading](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") the `pcspkr` [kernel module](/index.php/Kernel_module "Kernel module"):

```
# rmmod pcspkr

```

[Blacklisting](/index.php/Blacklisting "Blacklisting") the `pcspkr` module will prevent [udev](/index.php/Udev "Udev") from loading it at boot:

```
# echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

[Blacklisting it on the kernel command line](/index.php/Kernel_modules#Using_kernel_command_line_2 "Kernel modules") is yet another way. Simply add `modprobe.blacklist=pcspkr` to your bootloader's kernel line.

### Console

You can add this command in `/etc/profile` or a dedicated file like `/etc/profile.d/disable-beep.sh`:

```
setterm -blength 0

```

Another way is to uncomment or add this line in `/etc/inputrc` or `~/.inputrc`:

```
set bell-style none

```

#### Less pager

To disable PC speaker in [less](https://www.archlinux.org/packages/?name=less) pager, you can launch it with `less -q` to mute PC speaker for end of line events or `less -Q` to mute it altogether. For [man pages](/index.php/Man_page "Man page"), launch `man -P "less -Q"` or set the `$MANPAGER` or `$PAGER` [environment variables](/index.php/Environment_variable "Environment variable").

Alternatively, you can add these lines to your `~/[.bashrc](/index.php/.bashrc ".bashrc")`:

```
alias less='less -Q'
alias man='man -P "less -Q"'

```

### Xorg

```
$ xset -b

```

You can add this command to a startup file such as `/etc/xprofile` to make it permanent. See [xprofile](/index.php/Xprofile "Xprofile") for more information.

### ALSA

For most sound cards the PC speaker is listed as an [ALSA](/index.php/ALSA "ALSA") channel, named either *PC Speaker*, *PC Beep*, or *Beep*. To mute the speaker, either use *alsamixer* or *amixer*:

```
$ amixer set *channel* 0% mute

```

To unmute the channel, see [Advanced Linux Sound Architecture#Unmuting the channels](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture").

**Tip:** If you are using PulseAudio and the PC speaker channel is not listed for the default ALSA device, try selecting the device corresponding to the sound card - PulseAudio proxy controls may not list the PC speaker

### GNOME

Using GSettings:

```
$ gsettings set org.gnome.desktop.wm.preferences audible-bell false

```

### Cinnamon

Cinnamon seems to play a "water drop" sound. To disable it, set in dconf:

```
$ dconf write /org/cinnamon/desktop/wm/preferences/audible-bell false

```

### GTK+

Append this line to `~/.gtkrc-2.0`:

```
gtk-error-bell = 0

```

Add the same line to the [Settings] section of `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`:

```
[Settings]
gtk-error-bell = 0

```

This is documented in the [Gnome Developer Handbook](https://developer.gnome.org/gtk3/stable/GtkSettings.html).

## Beep

Beep is an advanced PC speaker beeping program. It is useful for situations where no sound card and/or speakers are available, and simple audio notification is desired.

### Installation

[Install](/index.php/Install "Install") the [beep](https://www.archlinux.org/packages/?name=beep) package.

You may also need to [unmute](#ALSA) the PC speaker in [ALSA](/index.php/ALSA "ALSA").

### Access for non-root users

**Warning:** All the following notes are vulnerable to root privilege escalation, as described in [[1]](https://www.debian.org/security/2018/dsa-4163), which has not been fixed upstream as of 2018-04-03\. It is strongly not recommended to allow beep to run without root authentication

By default `beep` will fail if not run by the root. Other users may call it using [sudo](/index.php/Sudo "Sudo"). To let group `users` call `sudo beep` without a password (for example to use it in scripts), `/etc/sudoers` [should be edited](/index.php/Sudo#Using_visudo "Sudo"):

```
%users ALL=(ALL) NOPASSWD: /usr/bin/beep

```

or, to let only a single user do that:

```
username ALL=(ALL) NOPASSWD: /usr/bin/beep

```

Another way is setting the sticky bit on `/usr/bin/beep`:

```
# chmod 4755 /usr/bin/beep

```

Note however that this way **anyone** can execute `/usr/bin/beep` with root permissions. The change also creates a difference between local copy and the package, which will be reported by `pacman -Qkk`.

### Tips and Tricks

While many people are happy with the traditional beep sound, some may like to change its properties a bit. The following example plays slighly higher and shorter sound and repeats it two times.

```
# beep -f 5000 -l 50 -r 2

```

## See also

*   [xset(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xset.1), [setterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setterm.1), [readline(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/readline.3)