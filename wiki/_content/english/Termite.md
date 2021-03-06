[Termite](https://www.github.com/thestinger/termite) is a minimal VTE-based [terminal emulator](/index.php/Category:Terminal_emulators "Category:Terminal emulators"). It is a *modal* application, similar to [Vim](/index.php/Vim "Vim"), with an insert mode and selection mode where keybindings have different functions. Termite is based on the [VTE](https://developer.gnome.org/vte/unstable/) library.

The configuration file allows to change colors and set some options. Termite supports transparency along with both the 256 color and true color (16 million colors) palettes. It has a similar look and feel to [urxvt](/index.php/Urxvt "Urxvt").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Font](#Font)
    *   [3.2 Colors](#Colors)
*   [4 Transparency](#Transparency)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Ctrl+Shift+t](#Ctrl+Shift+t)
    *   [5.2 Remote SSH error](#Remote_SSH_error)
*   [6 See also](#See_also)

## Installation

Install the [termite](https://www.archlinux.org/packages/?name=termite) package, or [termite-git](https://aur.archlinux.org/packages/termite-git/) for the development version. For Wayland tiling WM users, you may want to install [termite-nocsd](https://aur.archlinux.org/packages/termite-nocsd/) which disable client side decorations.

## Usage

Termite starts in insert mode by default. Text may be selected using the mouse, or by using selection-mode keys. In insert mode, `Ctrl+Shift+c` is used to copy selected text to the [X](/index.php/X "X") clipboard, `Ctrl+Shift+v` to paste. `Ctrl+Tab` starts scrollback completion, and `Ctrl+Shift+Up` / `Ctrl+Shift+Down` scroll the screen up or down.

`Ctrl+Shift+Space` enters selection-mode, similar to vim's normal-mode. Many commands are borrowed from [Vim](/index.php/Vim "Vim"), for example `v` for visual mode, `Shift+v` for visual line mode, `Ctrl+v` for visual block mode, `y` to copy ("yank") selected text, `/` and `?` for searching, `w`, `b`, `^`, `$` for movement, and `Escape` to go back to insert mode.

## Configuration

Termite looks for configuration files in `$XDG_CONFIG_HOME/termite/config`, `~/.config/termite/config`, `$XDG_CONFIG_DIRS/termite/config` and `/etc/xdg/termite.cfg`. The configuration file is used to change options such as font, colors, window hints, etc. The configuration file syntax is inspired by [XDG Desktop Entry Specification](https://standards.freedesktop.org/desktop-entry-spec/latest/) [.desktop](/index.php/.desktop ".desktop") files (inspired by Microsoft Windows *.ini* files), with three sections: *options*, *colors*, and *hints*.

To start customizing termite copy the base example file to your home dir first:

```
 $ cp /etc/xdg/termite/config ~/.config/termite/config

```

### Font

Fonts are specified in the format `font=<font_name> <font_size>` under the *options* section. `<font_name>` is specified according to [fontconfig](/index.php/Fontconfig "Fontconfig"), not [Xft](/index.php/X_Logical_Font_Description "X Logical Font Description"). Use `fc-list` to see which fonts are available on the system (see also [Font configuration#Font paths](/index.php/Font_configuration#Font_paths "Font configuration")).

 `~/.config/termite/config` 
```
[options]
font = Monospace 9
font = xos4 Terminus 12px
font = Droid Sans Mono 8
```

### Colors

Colors consist of either a 24-bit hex value (e.g. `#4a32b1`), or an rgba vector (e.g. `rgba(16, 32, 64, 0.5)`). Valid properties for colors are `foreground`, `foreground_bold`, `foreground_dim`, `background`, `cursor`, and `colorN` (where N is an integer from zero through 254; used to assign a 24-bit color value to terminal colorN).

An amazing collection of termite color schemes can be found here: [https://github.com/khamer/base16-termite/tree/master/themes](https://github.com/khamer/base16-termite/tree/master/themes)

 `~/.config/termite/config` 
```
[colors]
foreground = #dcdccc
background  = #3f3f3f
```

## Transparency

As of version 9, Termite supports true transparency via color definitions that specify an alpha channel value [[1]](https://github.com/thestinger/termite/issues/191). This requires a compositor to be running, such as [Compton](/index.php/Compton "Compton") or [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr). Most compositors do not require special configuration for Termite to use transparency.

 `~/.config/termite/config` 
```
[colors]
background = rgba(63, 63, 63, 0.8)
```

**Note:** In [i3](/index.php/I3 "I3"), in stacked/tabbed layout, this shows all windows "stacked" on top of each other, in the order they were most recently in the foreground, rather than showing the desktop (the root window) directly behind Termite. This is due to i3 reordering windows rather than hiding invisible windows in tiling mode. You can configure your compositor to make windows with `_NET_WM_STATE=_NET_WM_STATE_HIDDEN` fully transparent to solve this. For example, for compton use `~/.compton.conf` 
```
opacity-rule = [
  "0:_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"
];
```

## Troubleshooting

### Ctrl+Shift+t

If opening a new tab through `Ctrl+Shift+t` fails with `no directory uri set`, [source](/index.php/Source "Source") `/etc/profile.d/vte.sh`. See [GNOME/Tips and tricks#New terminals adopt current directory](/index.php/GNOME/Tips_and_tricks#New_terminals_adopt_current_directory "GNOME/Tips and tricks").

If it continues to fail, ensure your [hostname](/index.php/Hostname "Hostname") is valid. See [hostname(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.7).

### Remote SSH error

When Termite is using remote SSH connection sometimes the error occurs: *Error opening terminal: xterm-termite.* or *Open terminal failed: missing or unsuitable terminal: xterm-termite.*

This error can occur when trying to edit file with vim or nano. To fix this issue you should execute this command on the remote system:

```
$ export TERM=xterm-color

```

Alternatively, follow the instructions on Termite's [GitHub](https://github.com/thestinger/termite#terminfo). This will allow you to use all of Termite's features when using SSH, whereas the above may not. [[2]](https://github.com/thestinger/termite/issues/229#issuecomment-250659169)

## See also

*   [Termite readme](https://github.com/thestinger/termite/blob/master/README.rst)