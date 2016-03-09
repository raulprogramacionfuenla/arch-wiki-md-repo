There are two types of browser plugins, based on the plugin API they use:

*   Netscape plugin API (NPAPI): these plugins work in [Firefox](/index.php/Firefox "Firefox") and most other browsers (**not** in Chromium and Opera).
*   Pepper plugin API (PPAPI): these plugins work only in [Chromium](/index.php/Chromium "Chromium") (and Chrome) and [Opera](/index.php/Opera "Opera").

Most plugins on this page are NPAPI-only, unless noted otherwise.

## Contents

*   [1 Flash Player](#Flash_Player)
    *   [1.1 Adobe Flash Player](#Adobe_Flash_Player)
        *   [1.1.1 Installation](#Installation)
        *   [1.1.2 Upgrade](#Upgrade)
        *   [1.1.3 Configuration](#Configuration)
        *   [1.1.4 Disable the "Press ESC to exit full screen mode" message](#Disable_the_.22Press_ESC_to_exit_full_screen_mode.22_message)
        *   [1.1.5 Multiple monitor full-screen fix](#Multiple_monitor_full-screen_fix)
        *   [1.1.6 Playing DRM-protected content](#Playing_DRM-protected_content)
    *   [1.2 Shumway](#Shumway)
    *   [1.3 Gnash](#Gnash)
    *   [1.4 Lightspark](#Lightspark)
    *   [1.5 Video players workarounds](#Video_players_workarounds)
        *   [1.5.1 Open-with Firefox extension](#Open-with_Firefox_extension)
*   [2 PDF viewer](#PDF_viewer)
    *   [2.1 PDF.js](#PDF.js)
    *   [2.2 External PDF viewers](#External_PDF_viewers)
    *   [2.3 Adobe Reader](#Adobe_Reader)
        *   [2.3.1 64-bit](#64-bit)
*   [3 Citrix](#Citrix)
*   [4 Java (IcedTea)](#Java_.28IcedTea.29)
*   [5 Pipelight](#Pipelight)
*   [6 Multimedia playback](#Multimedia_playback)
    *   [6.1 Other plugins](#Other_plugins)
*   [7 Other](#Other)
    *   [7.1 Hangouts](#Hangouts)
    *   [7.2 MozPlugger](#MozPlugger)
    *   [7.3 kpartsplugin](#kpartsplugin)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Flash Player: no sound](#Flash_Player:_no_sound)
    *   [8.2 Flash Player: blocking sound for other applications or delayed playback](#Flash_Player:_blocking_sound_for_other_applications_or_delayed_playback)
    *   [8.3 Flash Player: performance](#Flash_Player:_performance)
    *   [8.4 Flash Player: low webcam resolution](#Flash_Player:_low_webcam_resolution)
    *   [8.5 Flash Player: black bars in full screen playback on multi-headed setups](#Flash_Player:_black_bars_in_full_screen_playback_on_multi-headed_setups)
    *   [8.6 Flash Player: videos not working on older systems](#Flash_Player:_videos_not_working_on_older_systems)
    *   [8.7 Flash Player: plugin version still shown older version after upgrade](#Flash_Player:_plugin_version_still_shown_older_version_after_upgrade)
        *   [8.7.1 Firefox](#Firefox)
    *   [8.8 Plugins are installed but not working](#Plugins_are_installed_but_not_working)
    *   [8.9 Gecko Media Player will not play Apple trailers](#Gecko_Media_Player_will_not_play_Apple_trailers)
*   [9 See also](#See_also)

## Flash Player

### Adobe Flash Player

#### Installation

The package you will need to install depends on the browser you use.

*   The NPAPI version can be [installed](/index.php/Pacman "Pacman") with the [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) package. This plugin was [discontinued by Adobe](https://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html) and is stuck at version 11.2; although, Adobe will provide security updates for 5 years after its release (i.e. until March 2017[[1]](https://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html)[[2]](http://helpx.adobe.com/flash-player/release-note/release-notes-developer-flash-player.html)).

*   The PPAPI version is shipped with Google Chrome. If you are using Chromium or any other browser using the PPAPI interface such as [Opera](/index.php/Opera "Opera"), see [Chromium#Flash Player plugin](/index.php/Chromium#Flash_Player_plugin "Chromium") for more information.

**Note:**

*   Some Flash apps may require the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package in order to properly render text.
*   The [freshplayerplugin-git](https://aur.archlinux.org/packages/freshplayerplugin-git/) package provides an *experimental* adapter to use [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/) with NPAPI based browsers like Firefox.

#### Upgrade

If you are using [Firefox](/index.php/Firefox "Firefox"), please make sure to follow [this instruction first](/index.php/Firefox#Firefox_detects_the_wrong_version_of_my_plugin "Firefox").

#### Configuration

To change the preferences (privacy settings, resource usage, etc.) of Flash Player, right click on any embedded Flash content (for instance the one on [this page](https://helpx.adobe.com/flash-player.html)) and choose *Settings* from the menu.

You can also use the Flash settings file `/etc/adobe/mms.cfg`. Gentoo has an extensively commented [example mms.cfg](http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/www-plugins/adobe-flash/files/mms.cfg).

To enable [VDPAU](/index.php/VDPAU "VDPAU") hardware video decoding, add/uncomment the following line:

```
EnableLinuxHWVideoDecode = 1

```

It might also be required to add/uncomment the following line:

```
OverrideGPUValidation = 1

```

#### Disable the "Press ESC to exit full screen mode" message

There is no solution other than patching the Flash plugin. Please note only the NPAPI plugin is supported. Install [flash-fullscreen-patcher](https://aur.archlinux.org/packages/flash-fullscreen-patcher/) which provides wine as a required dependency since the patch has been initially made for Windows.

After the package has been installed, backup `libflashplayer.so`:

```
# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup 

```

Then, patch `libflashplayer.so`:

```
# flash-fullscreen-patcher.sh -f /usr/lib/mozilla/plugins/libflashplayer.so

```

If you use Firefox and want to remove the message *Press ESC to exit full screen mode in HTML5 videos* too, go to about:config and set `full-screen-api.warning.timeout` to `0`.

Alternatively, install Firefox extension [Disable HTML5 Fullscreen Alert](https://addons.mozilla.org/en-gb/firefox/addon/disable-html5-fullscreen-alert/), which will suppress full screen warnings for HTML5 content.

#### Multiple monitor full-screen fix

When using a multiple monitor setup, or swapping between virtual desktops, it is possible to lose focus on a fullscreen flash window. In such a case, the adobe flash-plugin will automatically exit full-screen mode. This may not be to your liking.

Unfortunately, this behavior is hard coded into the binary. In order to change this behavior it is necessary to alter the binary.

Fixing this issue only works for the NPAPI plugin and this issue can be fixed via 3 ways.

*   Using [flash-fullscreen-patcher](https://aur.archlinux.org/packages/flash-fullscreen-patcher/) which providess wine as a required dependency since the patch has been initially made for Windows.

	After the package has been installed, backup `libflashplayer.so`:

	 `# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup` 

	Then, patch libflashplayer.so:

	 `# flash-fullscreen-patcher.sh -i /usr/lib/mozilla/plugins/libflashplayer.so` 

*   Using the [flashplugin-focusfix](https://aur.archlinux.org/packages/flashplugin-focusfix/).

*   [Patching manually](http://www.webupd8.org/2012/10/ubuntu-multi-monitor-tweaks-full-screen.html):

	After the package has been installed, backup `libflashplayer.so`:

	 `# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup` 

	Then, you will need to alter that file using a hex editor like [ghex](https://www.archlinux.org/packages/?name=ghex). You must open it with root privileges obviously.

	 `# ghex /usr/lib/mozilla/plugins/libflashplayer.so` 

	Using the hex editor find the string `_NET_ACTIVE_WINDOW`. In ghex the readable string is on the right hand side of the window, and the hex is on the left, you are trying to locate the readable string. It should be easy to find using a search function.

	Upon finding `_NET_ACTIVE_WINDOW` rewrite the line, but **do not** change the length of the line, for example `_NET_ACTIVE_WINDOW` becomes `_XET_ACTIVE_WINDOW`.

	Save the binary, and restart any processes using the plugin (as this will crash any instance of the plugin in use.)

#### Playing DRM-protected content

See [Flash DRM content](/index.php/Flash_DRM_content "Flash DRM content").

### Shumway

[Shumway](http://mozilla.github.io/shumway/) is an HTML5 technology experiment that explores building a faithful and efficient renderer for the SWF file format without native code assistance. As of 2013-01-01, the plugin may be installed directly from [Mozilla's github.io site](http://mozilla.github.io/shumway/). According to the [Shumway wiki](https://github.com/mozilla/shumway/wiki), "Integration with Firefox is a possibility if the experiment proves successful."

Shumway is also embedded in Firefox Nightly/Aurora builds.

### Gnash

See also [Wikipedia:Gnash](https://en.wikipedia.org/wiki/Gnash "wikipedia:Gnash").

[GNU Gnash](http://www.gnu.org/software/gnash/) is a free (libre) alternative to Adobe Flash Player. It is available both as a standalone player for desktop computers and embedded devices, as well as a browser plugin, and supports the SWF format up to version 7 (with versions 8 and 9 under development) and about 80% of ActionScript 2.0.

There are multiple packages available: [gnash](https://aur.archlinux.org/packages/gnash/), [gnash-kde4](https://aur.archlinux.org/packages/gnash-kde4/), [gnash-git](https://aur.archlinux.org/packages/gnash-git/).

**Note:** If you find that Gnash does not work properly right out of the box, then you may also need to [install](/index.php/Install "Install") the [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg) package.

### Lightspark

[Lightspark](http://lightspark.github.com/) is another attempt to provide a free alternative to Adobe Flash aimed at supporting newer Flash formats. Lightspark has the ability to fall back on Gnash for old content, which enables users to install both and enjoy wider coverage. Although it is still very much in development, it supports some [popular sites](https://github.com/lightspark/lightspark/wiki/Site-Support).

Lightspark can be [installed](/index.php/Install "Install") with the [lightspark](https://aur.archlinux.org/packages/lightspark/) or [lightspark-git](https://aur.archlinux.org/packages/lightspark-git/) package.

### Video players workarounds

#### Open-with Firefox extension

1.  Install [Open-with](https://addons.mozilla.org/en-US/firefox/addon/open-with/) add-on.
2.  Open `about:openwith`, select *Add...*
3.  In the dialog select a video streaming capable player (e.g. [/usr/bin/mpv](/index.php/Mpv "Mpv")).
4.  (Optional step) Add needed arguments to the player (e.g. you may want `--force-window --ytdl` for *mpv*)
5.  (Optional step) Choose how to display the dialogs using the left panel.
6.  Right click on links or visit pages containing videos. If the site is supported, the player will open as expected.

The same procedure can be used to associate video downloaders such as *youtube-dl*.

## PDF viewer

### PDF.js

[PDF.js](https://mozillalabs.com/en-US/pdfjs/) is a PDF renderer created by Mozilla and built using HTML5 technologies.

For [Firefox](/index.php/Firefox "Firefox") it is available as a [plugin](https://addons.mozilla.org/en-US/firefox/addon/pdfjs/), which is included in [Firefox](/index.php/Firefox "Firefox") since version 19.

For [Chromium](/index.php/Chromium "Chromium") and Google Chrome there is an experimental extension in the [Chrome web store](https://chrome.google.com/webstore/detail/pdf-viewer/oemmndcbldboiebfnladdacbdfmadadm) or alternatively it can be built from the source of [Pdf.js](https://github.com/mozilla/pdf.js).

### External PDF viewers

To use an external PDF viewer you need [#MozPlugger](#MozPlugger) or [#kpartsplugin](#kpartsplugin).

If you want to use MozPlugger with Evince, for example, you have to find the lines containing `pdf` in the `/etc/mozpluggerrc` file and modify the corresponding line after `GV()` as below:

```
repeat noisy swallow(evince) fill: evince "$file"

```

(replace `evince` with something else if it is not your viewer of choice).

If this is not enough, you may need to change 2 values in `about:config`:

*   Change `pdfjs.disabled`'s value to *true*;
*   Change `plugin.disable_full_page_plugin_for_types`'s value to an empty value.

Restart and it should work like a charm!

### Adobe Reader

**Note:** Adobe Reader for Linux is discontinued[[3]](http://www.omgubuntu.co.uk/2014/10/adobe-reader-linux-download-pulled-website) and the outdated version that is still available cannot easily run in a 64-bit browser.

Due to licensing restrictions, Adobe Reader is only available in the [AUR](/index.php/AUR "AUR").

Adobe Acrobat Reader is only available as a 32-bit binary. It can be installed with the [acroread](https://aur.archlinux.org/packages/acroread/) package. This package installs the Acrobat Reader application as well as the NPAPI plugin.

Also, there are [localizations](https://aur.archlinux.org/packages.php?O=0&K=acroread-&do_Search=Go) available in many languages.

#### 64-bit

There is no 64-bit version of Adobe Reader available. To use it in a 64-bit environment, you can:

*   Follow [this guide](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64") originally posted in the forums. It involves creating a chrooted environment that could be reused for other 32-bit only applications.

*   Install the [acroread](https://aur.archlinux.org/packages/acroread/) package (with all its 32-bit dependencies). Be advised that the [Firefox](/index.php/Firefox "Firefox") plugin cannot be used *directly* with this binary -- it will not load in the 64-bit browser. To load it install the [nspluginwrapper](https://www.archlinux.org/packages/?name=nspluginwrapper) package from the official [[multilib]](/index.php/Multilib "Multilib") repository and run:

```
$ nspluginwrapper -v -a -i

```

as a normal user. This checks the plugin directory and links the plugins as needed.

## Citrix

See [Citrix](/index.php/Citrix "Citrix").

## Java (IcedTea)

**Note:** Both Java plugins are NPAPI-only and thus do not work in Chromium and Opera.

To enable [Java](/index.php/Java "Java") support in your browser, you have two options: the open-source [OpenJDK](https://en.wikipedia.org/wiki/OpenJDK "wikipedia:OpenJDK") (recommended) or Oracle's proprietary version. For details about why OpenJDK is recommended see [this](https://mailman.archlinux.org/pipermail/arch-general/2011-August/021671.html).

To use OpenJDK, you have to install the [IcedTea](http://icedtea.classpath.org/wiki/Main_Page) browser plugin, [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web).

If you want to use Oracle's JRE, install the [jre](https://aur.archlinux.org/packages/jre/) package.

See [Java#OpenJDK](/index.php/Java#OpenJDK "Java") for additional details and references.

**Note:** If you experience any problems with the Java plugin (e.g. it is not recognized by the browser), you can try this [solution](#Plugins_are_installed_but_not_working).

## Pipelight

See [Pipelight](/index.php/Pipelight "Pipelight").

## Multimedia playback

Many browsers support the [GStreamer](/index.php/GStreamer "GStreamer") framework to play multimedia inside HTML5 `<audio>` and `<video>` elements. Check the optional dependencies of the browser package (or [webkitgtk](https://www.archlinux.org/packages/?name=webkitgtk)/[webkitgtk2](https://www.archlinux.org/packages/?name=webkitgtk2) if using a webkit-based browser) to see which version of GStreamer is supported: this can be either `gst-*` for the current version, or `gstreamer0.10-*` for the legacy version. See [GStreamer#Installation](/index.php/GStreamer#Installation "GStreamer") for the description of each plugin.

### Other plugins

*   **Gecko Media Player** — Mozilla browser plugin to handle media on websites, using MPlayer.

	[https://sites.google.com/site/kdekorte2/gecko-mediaplayer](https://sites.google.com/site/kdekorte2/gecko-mediaplayer) || [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer)

*   **GNOME Videos Plugin** — Browser plugin based on the [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos") media player which uses [GStreamer](/index.php/GStreamer "GStreamer").

	[https://wiki.gnome.org/Apps/Videos](https://wiki.gnome.org/Apps/Videos) || [totem](https://www.archlinux.org/packages/?name=totem)

*   **Rosa Media Player Plugin** — Qt-based browser plugin also based on MPlayer.

	[https://abf.rosalinux.ru/uxteam/ROSA_Media_Player](https://abf.rosalinux.ru/uxteam/ROSA_Media_Player) || [rosa-media-player-plugin](https://aur.archlinux.org/packages/rosa-media-player-plugin/)

*   **VLC Plugin** — NPAPI-based plugin that uses VLC technologies.

	[http://git.videolan.org/?p=npapi-vlc.git;a=summary](http://git.videolan.org/?p=npapi-vlc.git;a=summary) || [npapi-vlc-git](https://aur.archlinux.org/packages/npapi-vlc-git/)

## Other

### Hangouts

Hangouts plugin can be installed with the [google-talkplugin](https://aur.archlinux.org/packages/google-talkplugin/) package . It is a messenger by Google, that allows you to do many things. For example, it is possible to do the following: watching YouTube, making diagrams, editing documents, playing games. It is possible to make video call between 15 people simultaneously.

### MozPlugger

MozPlugger can be installed with the [mozplugger](https://aur.archlinux.org/packages/mozplugger/) package.

[MozPlugger](http://mozplugger.mozdev.org/) is a Mozilla plugin which can show many types of multimedia inside your browser. To accomplish this, it uses external programs such as MPlayer, xine, Evince, OpenOffice, TiMidity, etc. To modify or add applications to be used by MozPlugger just modify the `/etc/mozpluggerrc` file.

For example, MozPlugger uses OpenOffice by default to open `doc` files. To change it to use LibreOffice instead, look for the OpenOffice section:

 `/etc/mozpluggerrc` 
```
...
### OpenOffice
define([OO],[swallow(VCLSalFrame) fill: ooffice2.0 -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: soffice -nologo $1 "$file"])
...

```

and add LibreOffice at the beginning of the list:

 `/etc/mozpluggerrc` 
```
...
### LibreOffice/OpenOffice
define([OO],[swallow(VCLSalFrame) fill: libreoffice --nologo --norestore --view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice2.0 -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: soffice -nologo $1 "$file"])
...

```

**Note:** Be sure to also choose LibreOffice as your preferred application to open `doc` files.

As another simple example, if you want to open `cpp` files with your favorite text editor (we will use Kate) to get syntax highlighting, just add a new section to your `mozpluggerrc` file:

 `/etc/mozpluggerrc` 
```
text/x-c++:cpp:C++ Source File
text/x-c++:hpp:C++ Header File
    repeat noisy swallow(kate) fill: kate -b "$file"

```

To change the default of MPlayer so that [mpv](/index.php/Mpv "Mpv") is used instead, change the appropriate lines such that:

 `/etc/mozpluggerrc` 
```
...
### MPlayer

#define(MP_CMD,[mplayer -really-quiet -nojoystick -nofs -zoom -vo xv,x11 -ao esd,alsa,oss,arts,null -osdlevel 0 $1 </dev/null])
define(MP_CMD,[mpv -really-quiet $1 </dev/null])

#define(MP_EMBED,[embed noisy ignore_errors: MP_CMD(-xy $width -wid $window $1)])
define(MP_EMBED,[embed noisy ignore_errors: MP_CMD(--autofit=$width -wid $window $1)])

#define(MP_NOEMBED,[noembed noisy ignore_errors maxaspect swallow(MPlayer): MP_CMD($1)])
define(MP_NOEMBED,[noembed noisy ignore_errors maxaspect swallow(mpv): MP_CMD($1)])

...

#define(MP_AUDIO,[mplayer -quiet -nojoystick $1 </dev/null])
define(MP_AUDIO,[mpv -really-quiet $1 </dev/null])

#define(MP_AUDIO_STREAM,[controls stream noisy ignore_errors: mplayer -quiet -nojoystick $1 "$file" </dev/null])
define(MP_AUDIO_STREAM,[controls stream noisy ignore_errors: mpv -really-quiet $1 "$file" </dev/null])
...
```

For a more complete list of MozPlugger options see [this page](http://www.linuxmanpages.com/man7/mozplugger.7.php).

### kpartsplugin

[The KParts plugin](http://www.unix-ag.uni-kl.de/~fischer/kpartsplugin/) is a plugin that uses KDE's KPart technology to embed different file viewers in the browser, such as Okular (for PDF), Ark (for different archives), Calligra Words (for ODF), etc. It cannot use applications that are not based on the KPart technology.

The KParts plugin can be installed with the package [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin).

## Troubleshooting

### Flash Player: no sound

Flash Player outputs its sound only through the default [ALSA](/index.php/ALSA "ALSA") device, which is number **0**. If you have multiple sound devices (a very common example is having a sound card and HDMI output in the video card), then your preferred device may have a different number.

For a list of available devices with their respective numbers, run:

 `$ aplay -l` 
```
 **** List of PLAYBACK Hardware Devices ****
 card 0: Generic [HD-Audio Generic], device 3: HDMI 0 [HDMI 0]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 1: DX [Xonar DX], device 0: Multichannel [Multichannel]
   Subdevices: 0/1
   Subdevice #0: subdevice #0
 card 1: DX [Xonar DX], device 1: Digital [Digital]
   Subdevices: 1/1
   Subdevice #0: subdevice #0

```

In this case, the HDMI output is `card 0` and the sound card is `card 1`. To make your sound card the default for ALSA, create the file `.asoundrc` in your home directory, with the following content:

 `~/.asoundrc` 
```
pcm.!default {
    type hw
    card 1
}

ctl.!default {
    type hw
    card 1
}

```

### Flash Player: blocking sound for other applications or delayed playback

If sound is delayed within Flash videos or Flash stops sound from any other application, then make sure you do not have `snd_pcm_oss` module loaded:

```
$ lsmod | grep snd_pcm_oss

```

You can unload it:

```
# rmmod snd_pcm_oss

```

and restart the browser to see if it helps.

### Flash Player: performance

Adobe's Flash plugin has some serious performance issues, especially when CPU frequency scaling is used. There seems to be a policy not to use the whole CPU workload, so the frequency scaling governor does not clock the CPU any higher. To work around this issue, see [CPU frequency scaling#Switching threshold](/index.php/CPU_frequency_scaling#Switching_threshold "CPU frequency scaling")

### Flash Player: low webcam resolution

If your webcam has low resolution in Flash (the image looks very pixelated) you can try starting your browser with this:

```
$ LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so [broswer]

```

### Flash Player: black bars in full screen playback on multi-headed setups

The Flash plugin has a known bug where the full screen mode does not really work when you have a multi-monitor setup. Apparently, it incorrectly determines the full screen resolution, so the full screen Flash Player fills the correct monitor but gets scaled as if the monitor had the resolution of the total display area.

To fix this, you can use the "hack" described [here](http://al.robotfuzz.com/content/workaround-fullscreen-flash-linux-multiheaded-desktops). Simply download the source from the link given on the page, and follow the instructions in the README.

**Tip:** The hack is available and can be installed with the [fullscreenhack](https://aur.archlinux.org/packages/fullscreenhack/) package.

**Note:** While the author mentions using NVDIA's TwinView, the hack should work for any multi-monitor setup.

### Flash Player: videos not working on older systems

If you have Adobe Flash installed on an older system and you start playing a video which simply turns black with nothing happening, it is most likely that your CPU does not support SSE2\. You can simply check this by looking at your CPU flags with this command:

```
$ grep sse2 /proc/cpuinfo

```

If no results are returned, then you need to install an older version of Flash (for example 10.3, or 11.1). Older versions possibly will have vulnerabilities. You should then consider sandboxing Firefox using the [sandfox](https://aur.archlinux.org/packages/sandfox/) package See the [sandfox homepage](https://igurublog.wordpress.com/downloads/script-sandfox/) for usage information.

Older versions of Flash are available here: [https://www.adobe.com/products/flashplayer/distribution3.html](https://www.adobe.com/products/flashplayer/distribution3.html) You need to copy `libflashplayer.so` to the folder `/usr/lib/mozilla/plugins/`

The most recent package without SSE2 is `flashplugin-11.1.102.63-1-i686.pkg.tar.xz`. If you use the packaged version, you have to add `IgnorePkg = flashplugin` to `/etc/pacman.conf`.

### Flash Player: plugin version still shown older version after upgrade

#### Firefox

Solution for Firefox: delete file "pluginreg.dat" in user's profile directory.

*   Close firefox
*   Go to /home/<username>/.mozilla/firefox/<profile_folder>/
*   Delete file "pluginreg.dat"

Firefox will automatically rebuild this file once it is started again. Make sure to substitute <username> and <profile_folder> with the appropriate information.

### Plugins are installed but not working

A common problem is that the plugin path is unset. This typically occurs on a new install, when the user has not re-logged in before running Firefox after the installation. Test if the path is unset:

```
echo $MOZ_PLUGIN_PATH

```

If unset, then either re-login, or source `/etc/profile.d/mozilla-common.sh` and start Firefox from the same shell:

```
source /etc/profile.d/mozilla-common.sh && firefox

```

### Gecko Media Player will not play Apple trailers

If Apple Trailers appear to start to play and then fail, try setting the user agent for your browser to:

```
QuickTime/7.6.2 (qtver=7.6.2;os=Windows NT 5.1Service Pack 3)

```

## See also

*   [Play videos without using Flash](https://trisquel.info/en/wiki/play-videos-without-using-flash) at the Trisquel Wiki