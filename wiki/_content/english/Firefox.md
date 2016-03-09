[Firefox](http://www.firefox.com) is a popular open-source graphical web browser from [Mozilla](http://www.mozilla.com).

## Contents

*   [1 Installing](#Installing)
*   [2 Add-ons](#Add-ons)
*   [3 Configuration](#Configuration)
*   [4 Plugins](#Plugins)
    *   [4.1 GNOME Keyring integration](#GNOME_Keyring_integration)
    *   [4.2 KDE integration](#KDE_integration)
    *   [4.3 Dictionaries for spell checking](#Dictionaries_for_spell_checking)
    *   [4.4 Adding search engines](#Adding_search_engines)
        *   [4.4.1 arch-firefox-search](#arch-firefox-search)
    *   [4.5 Multimedia playback](#Multimedia_playback)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Firefox startup takes very long](#Firefox_startup_takes_very_long)
    *   [5.2 Font troubleshooting](#Font_troubleshooting)
    *   [5.3 Setting an email client](#Setting_an_email_client)
    *   [5.4 File association](#File_association)
        *   [5.4.1 File association problems](#File_association_problems)
    *   [5.5 Firefox keeps creating ~/Desktop even when this is not desired](#Firefox_keeps_creating_.7E.2FDesktop_even_when_this_is_not_desired)
    *   [5.6 Make plugins respect blocked pop-ups](#Make_plugins_respect_blocked_pop-ups)
    *   [5.7 Middle-click errors](#Middle-click_errors)
    *   [5.8 Backspace does not work as the 'Back' button](#Backspace_does_not_work_as_the_.27Back.27_button)
    *   [5.9 Firefox does not remember login information](#Firefox_does_not_remember_login_information)
    *   [5.10 Unreadable input fields with dark GTK+ themes](#Unreadable_input_fields_with_dark_GTK.2B_themes)
    *   [5.11 "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear](#.22Do_you_want_Firefox_to_save_your_tabs_for_the_next_time_it_starts.3F.22_dialog_does_not_appear)
    *   [5.12 Silently fails when installing desktop apps from marketplace](#Silently_fails_when_installing_desktop_apps_from_marketplace)
    *   [5.13 Firefox detects the wrong version of my plugin](#Firefox_detects_the_wrong_version_of_my_plugin)
    *   [5.14 Javascript context menu doesn't appear on some sites](#Javascript_context_menu_doesn.27t_appear_on_some_sites)
    *   [5.15 Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language)
    *   [5.16 Some MathML symbols are missing](#Some_MathML_symbols_are_missing)
    *   [5.17 Picture flickers while scrolling](#Picture_flickers_while_scrolling)
*   [6 See also](#See_also)

## Installing

Firefox can be [installed](/index.php/Installed "Installed") with the [firefox](https://www.archlinux.org/packages/?name=firefox) package.

Other alternatives include:

*   **Firefox Extended Support Release** — long-term supported version

	[https://www.mozilla.org/en-US/firefox/organizations/](https://www.mozilla.org/en-US/firefox/organizations/) || [firefox-esr-bin](https://aur.archlinux.org/packages/firefox-esr-bin/)

*   **Firefox Beta** — cutting-edge version

	[https://www.mozilla.org/en-US/firefox/channel](https://www.mozilla.org/en-US/firefox/channel) || [firefox-beta-bin](https://aur.archlinux.org/packages/firefox-beta-bin/)

*   **Firefox Aurora/Developer edition** — for developers

	[https://www.mozilla.org/en-US/firefox/aurora/](https://www.mozilla.org/en-US/firefox/aurora/) || [firefox-aurora](https://aur.archlinux.org/packages/firefox-aurora/)

*   **Firefox Nightly** — nightly builds for testing

	[https://nightly.mozilla.org/](https://nightly.mozilla.org/) || [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/)

*   **Firefox KDE** — Version of Firefox that incorporates an OpenSUSE patch for better KDE integration than is possible through simple Firefox plugins.

	[https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox](https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

*   On top of the different Mozilla build channels, a number of forks exist with more or less special features; see [List of applications#Gecko-based](/index.php/List_of_applications#Gecko-based "List of applications").

Here you can find an overview of Mozilla's [releases](https://wiki.mozilla.org/Releases).

There are a number of language packs available for Firefox, other than the standard English. Language packs are usually named as `firefox-i18n-languagecode` (where `languagecode` can be any language code, such as **de**, **ja**, **fr**, etc.). For a list of available language packs see [this](https://www.archlinux.org/packages/?sort=&q=firefox-i18n&maintainer=&last_update=&flagged=&limit=100).

## Add-ons

Firefox is well known for its large library of add-ons which can be used to add new features or modify the behavior of existing features of Firefox. You can find new add-ons or manage installed add-ons with Firefox's "Add-ons Manager."

For a list of popular add-ons, see [Mozilla's add-on list sorted by popularity](https://addons.mozilla.org/en-US/firefox/extensions/?sort=popular). See also [List of Firefox extensions](https://en.wikipedia.org/wiki/List_of_Firefox_extensions "wikipedia:List of Firefox extensions") on Wikipedia.

## Configuration

Firefox exposes a number of configuration options. To examine them, enter:

```
about:config

```

in the Firefox address bar.

Once set, these affect the user's current profile, and may be synchronized across all devices via [Firefox Sync](https://www.mozilla.org/en-US/firefox/sync/). Please note that only a subset of the `about:config` entries are synchronized by this method, and the exact subset may be found by searching for `services.sync.prefs` in `about:config`.

Firefox also allows configuration for a profile via a `user.js` file: [user.js](http://kb.mozillazine.org/User.js_file) kept in the profile folder, usually `~/.mozilla/firefox/*some name*.default/`. For a useful starting point, see e.g [custom user.js](https://github.com/pyllyukko/user.js) which is targeted at privacy/security conscious users.

One drawback of the above approach is that it is not applied system-wide. Furthermore, this is not useful as a "pre-configuration", since the profile directory is created after first launch of the browser. You can, however, let *firefox* create a new profile and, after closing it again, [copy the contents](https://support.mozilla.org/en-US/kb/back-and-restore-information-firefox-profiles#w_restoring-a-profile-backup) of an already created profile folder into it.

Sometimes it may be desired to lock certain settings, a feature useful in widespread deployments of customized Firefox. In order to create a system-wide configuration, follow the steps outlined in [Locking preferences](http://kb.mozillazine.org/Locking_preferences):

1\. Create `/usr/lib/firefox/defaults/pref/local-settings.js`:

```
pref("general.config.obscure_value", 0);
pref("general.config.filename", "mozilla.cfg");

```

2\. Create `/usr/lib/firefox/mozilla.cfg` (this stores the actual configuration):

```
//
//...your settings...
// e.g to disable Pocket, uncomment the following line
// lockPref("browser.pocket.enabled", false);

```

Please note that the first line must contain exactly `//`. The syntax of the file is similar to that of `user.js`.

## Plugins

See the main article: [Browser plugins](/index.php/Browser_plugins "Browser plugins")

To find out what plugins are installed/enabled, enter:

```
about:plugins

```

in the Firefox address bar or go to the *Add-ons* entry in the Firefox Menu and select the *Plugins* tab.

### GNOME Keyring integration

Install [firefox-gnome-keyring](https://aur.archlinux.org/packages/firefox-gnome-keyring/) or [mozilla-extension-gnome-keyring-git](https://aur.archlinux.org/packages/mozilla-extension-gnome-keyring-git/) (all-JavaScript implementation) to integrate Firefox with [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"). To make firefox-gnome-keyring use your login keychain, set extensions.gnome-keyring.keyringName to "login" (without the double quotes) in about:config. Note the lowercase 'l' despite the the keychain name having an uppercase 'L' in Seahorse.

### KDE integration

*   To bring the KDE look to GTK apps (including Firefox), install [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) and [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config). Afterwards, go to `System Settings` -> `Application Style` -> `GTK`. Be sure to choose 'Breeze' in 'Select a GTK2/GTK3 Theme' and check 'Show icons in GTK buttons' and 'Show icons in GTK'.

*   To use KDE's KPart technology with Firefox, by embedding different KDE file viewers into the browser, you can install [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin).

*   For integration with KDE’s mime type system and file dialogs, one can use [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/) variant from AUR with OpenSUSE’s patches applied.

*   Add-ons may provide some integration, such as [KWallet integration](https://addons.mozilla.org/en-US/firefox/addon/kde-wallet-password-integratio/) and [Plasma notifications](https://addons.mozilla.org/en-US/firefox/addon/plasmanotify/).

### Dictionaries for spell checking

To enable spell checking for a specific language right click on any text field and check the *Check Spelling* box. To select a language for spell checking to you have right click again and select your language from the *Languages* sub-menu.

To get more languages just click *Add Dictionaries...* and select the dictionary you want to install from the list.

Alternatively, you can install the [hunspell](https://www.archlinux.org/packages/?name=hunspell) package. You also need to install dictionaries for your language, such as [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr) (for the French language) or [hunspell-he](https://www.archlinux.org/packages/?name=hunspell-he) (for Hebrew).

By default, Firefox will try to symlink all your hunspell dictionaries in `/usr/lib/firefox/dictionaries`. If you want to have less dictionaries offered to you in Firefox, you can remove some of those links. Be aware that it may not stand an upgrade of Firefox.

When your default language choice does not stick, see [#Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language).

### Adding search engines

Search engines can be added to Firefox through normal add-ons, see [this page](https://addons.mozilla.org/en-US/firefox/search-tools/) for a list of available search engines.

A very extensive list of search engines can be found [here](http://mycroft.mozdev.org/).

Also, you can use the [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) extension to add a search to your search bar from any web site, by simply right clicking on the site's search field and selecting *Add to Search Bar...*

If you want a manual solution, take a look at `~/.mozilla/firefox/*xxxxxxxx*.default/searchplugins/` (where *xxxxxxxx* is your profile ID).

#### arch-firefox-search

Install the [arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search) package to add Arch-specific searches (AUR, wiki, forum, etc, as specified by user) to the Firefox search toolbar.

### Multimedia playback

Firefox will try to use [FFmpeg](/index.php/FFmpeg "FFmpeg") for playing multimedia inside HTML5 `<audio>` and `<video>` elements. For this to work, the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package needs to be installed.

Restart Firefox, and go to [YouTube's HTML5 page](https://www.youtube.com/html5), [video-test page](http://www.quirksmode.org/html5/tests/video.html) or [audio-test page](http://hpr.dogphilosophy.net/test/) to check which formats are actually supported.

See also [Firefox tweaks#Enable additional media codecs](/index.php/Firefox_tweaks#Enable_additional_media_codecs "Firefox tweaks") for advanced configuration.

## Troubleshooting

### Firefox startup takes very long

If Firefox takes much longer to start up than other browsers, it may be due to lacking configuration of the localhost in `/etc/hosts`. See [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration") on how to set it up.

### Font troubleshooting

See [Font configuration](/index.php/Font_configuration "Font configuration").

### Setting an email client

Inside the browser, `mailto` links by default are opened by a web application such as Gmail or Yahoo Mail. To set an external email program, go to *Preferences > Applications* and modify the *action* corresponding to the `mailto` content type; the file path will need to be designated (e.g. `/usr/bin/kmail` for Kmail).

Outside the browser, `mailto` links are handled by the `x-scheme-handler/mailto` mime type, which can be easily configured with [xdg-mime](/index.php/Xdg-mime "Xdg-mime"). See [Default applications](/index.php/Default_applications "Default applications") for details and alternatives.

### File association

See [Default applications](/index.php/Default_applications "Default applications").

#### File association problems

For non-[GNOME](/index.php/GNOME "GNOME") users, Firefox may not associate file types properly or at all (in the "Open With" part of the download dialog). Installing [libgnome](https://www.archlinux.org/packages/?name=libgnome) amends the problem.

See also [[2]](http://alien.slackbook.org/blog/make-firefox-understand-downloaded-files/).

### Firefox keeps creating ~/Desktop even when this is not desired

Firefox uses `~/Desktop` as the default place for download and upload files. To change it to another folder, set the `XDG_DESKTOP_DIR` option as explained in [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories").

### Make plugins respect blocked pop-ups

Some plugins can misbehave and bypass the default settings, such as the Flash plugin. You can prevent this by doing the following:

1.  Type `about:config` into the address bar.
2.  Right-click on the page and select `New` and then `Integer`.
3.  Name it `privacy.popups.disable_from_plugins`.
4.  Set the value to 2.

The possible values are:

*   **0**: Allow all popups from plugins.
*   **1**: Allow popups, but limit them to dom.popup_maximum.
*   **2**: Block popups from plugins.
*   **3**: Block popups from plugins, even on whitelisted sites.

### Middle-click errors

A common error message you can get while using the middle mouse button in Firefox is:

```
The URL is not valid and cannot be loaded.

```

Another symptom is that middle-clicking results in unexpected behavior, like accessing a random web page.

The reason stems from the use of the middle mouse buttons in UNIX-like operating systems. The middle mouse button is used to paste whatever text has been highlighted/added to the clipboard. Then there is the possibly conflicting feature in Firefox, which defaults to loading the URL of the corresponding text when the button is depressed. This can be easily disabled by going to `about:config` and setting the `middlemouse.contentLoadURL` option to **false**.

Alternatively, having the traditional scroll cursor on middle-click (default behavior on Windows browsers) can be achieved by searching for `general.autoScroll` and setting it to **true**.

### Backspace does not work as the 'Back' button

As per [this article](http://ubuntu.wordpress.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/), the feature has been removed in order to fix a bug. To re-introduce the original behavior go to `about:config` and set the `browser.backspace_action` option to **0** (zero).

### Firefox does not remember login information

It may be due to a corrupted `cookies.sqlite` file in [Firefox's profile](http://support.mozilla.com/en-US/kb/Profiles#How_to_find_your_profile) folder. In order to fix this, just rename or remove `cookie.sqlite` while Firefox is not running.

Open a terminal of choice and type the following:

```
$ cd ~/.mozilla/firefox/xxxxxxxx.default/
$ rm -f cookies.sqlite

```

**Note:** xxxxxxxx represents a random string of 8 characters.

Restart Firefox and see if it solved the problem.

### Unreadable input fields with dark GTK+ themes

When using a dark [GTK+](/index.php/GTK%2B "GTK+") theme, one might encounter Internet pages with unreadable input and text fields (e.g. Amazon can have white text on white background). This can happen because the site only sets either background or text color, and Firefox takes the other one from the theme.

A work around is to explicitly setting standard colors for all web pages in `~/.mozilla/firefox/xxxxxxxx.default/chrome/userContent.css` or using [stylish add-on](https://addons.mozilla.org/en-US/firefox/addon/stylish/).

The following sets input fields to standard black text / white background; both can be overridden by the displayed site, so that colors are seen as intended:

**Note:** If you want `urlbar` and `searchbar` to be `white` remove the two first `:not` css selectors.

```
input:not(.urlbar-input):not(.textbox-input):not(.form-control):not([type='checkbox']) {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

#downloads-indicator-counter {
    color: white;
}

textarea {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

select {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}
```

Another workaround is to force Firefox to use a light theme (e.g. "Adwaita:light"):

1.  Copy `/usr/share/applications/firefox.desktop` to `~/.local/share/applications/firefox.desktop` and replace all occurrences of `Exec=firefox` with `Exec=env GTK_THEME=Adwaita:light firefox`.
2.  Close all running instances of Firefox and restart your window manager/desktop environment.

### "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear

From the [Mozilla support](http://support.mozilla.com/en-US/questions/767751) site:

1.  Type `about:config` in the address bar.
2.  Set `browser.warnOnQuit` to **true**.
3.  Set `browser.showQuitWarning` to **true**.

### Silently fails when installing desktop apps from marketplace

Installation of apps from firefox os marketplace will silently fail if there's no `~/.local/share/applications` folder.

### Firefox detects the wrong version of my plugin

When you close Firefox, the latter saves the current timestamp and version of your plugins inside `pluginreg.dat` located in your profile folder, typically in `~/.mozilla/firefox/*some name*.default/`.

If you upgraded your plugin when Firefox was still running, you will thus have the wrong information inside that file. The next time you will restart Firefox you will get that message `Firefox has prevented the outdated plugin "XXXX" from running on ...` when you will be trying to open content dedicated to that plugin on the web. This problem often appears with the official [Adobe Flash Player plugin](/index.php/Browser_plugins#Flash_Player "Browser plugins") which has been upgraded while Firefox was still running.

The solution is to remove the file `pluginreg.dat` from your profile and that is it. Firefox will not complain about the missing file as it will be recreated the next time Firefox will be closed. [[3]](https://bugzilla.mozilla.org/show_bug.cgi?id=1109795#c16)

### Javascript context menu doesn't appear on some sites

In `about:config`, unset the `dom.w3c_touch_events.enabled` setting.

### Firefox does not remember default spell check language

The default spell checking language can be set as follows:

1.  Type `about:config` in the address bar.
2.  Set `spellchecker.dictionary` to your language of choice, for instance `en_GB`.
3.  Notice that the for dictionaries installed as a Firefox plugin the notation is `en-GB`, and for [hunspell](https://www.archlinux.org/packages/?name=hunspell) dictionaries the notation is `en_GB`.

When you only have system wide dictionaries installed with [hunspell](https://www.archlinux.org/packages/?name=hunspell), Firefox might not remember your default dictionary language settings. This can be fixed by having at least one [dictionary](https://addons.mozilla.org/en-US/firefox/language-tools/) installed as a Firefox plugin. Notice that now you will also have a tab **Dictionaries** in **add-ons**.

Related questions on the **StackExchange** platform: [[4]](http://stackoverflow.com/questions/26936792/change-firefox-spell-check-default-language/29446115), [[5]](http://stackoverflow.com/questions/21542515/change-default-language-on-firefox/29446353), [[6]](http://askubuntu.com/questions/184300/how-can-i-change-firefoxs-default-dictionary/576877)

Related bug reports: [Bugzilla 776028](https://bugzilla.mozilla.org/show_bug.cgi?id=776028), [Ubuntu bug 1026869](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1026869)

### Some MathML symbols are missing

You need some Math fonts, namely Latin Modern Math and STIX (see this MDN page: [[7]](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts#Linux)), to display MathML correctly.

In Arch Linux, these fonts are provided by [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) **and** [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra), but they are not available to fontconfig by default. See [TeX Live#Fonts](/index.php/TeX_Live#Fonts "TeX Live") for details.

### Picture flickers while scrolling

**Note:** Problem available in some MATE desktops

Uncheck the "smooth scrolling" settings:

```
Edit > Settings > Advanced > General > Use smooth scrolling

```

## See also

*   [Official website](http://www.mozilla.org/firefox/)
*   [Mozilla Foundation](http://www.mozilla.org/)
*   [Firefox wiki](https://wiki.mozilla.org/Firefox)
*   [Firefox Add-ons](https://addons.mozilla.org/)
*   [Firefox themes](https://addons.mozilla.org/en-US/firefox/themes/)