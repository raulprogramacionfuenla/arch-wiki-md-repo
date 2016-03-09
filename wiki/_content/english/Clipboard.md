From [Wikipedia:Clipboard (computing)](https://en.wikipedia.org/wiki/Clipboard_(computing) "wikipedia:Clipboard (computing)"):

	The clipboard is a facility used for short-term data storage and/or data transfer between documents or applications, via [copy and paste](https://en.wikipedia.org/wiki/copy_and_paste "wikipedia:copy and paste") operations.

## Contents

*   [1 History](#History)
*   [2 Background](#Background)
*   [3 List of clipboard managers](#List_of_clipboard_managers)
*   [4 See also](#See_also)

## History

In X10, "cut buffers" were introduced. These were limited buffers that stored arbitrary text and were used by most applications. However, they were inefficient and implementation of them varied, so selections were introduced. Cut buffers are long deprecated, and although some applications (such as xterm) may have legacy support for them, it is both not likely and not recommended that they be used.

## Background

The [ICCCM](http://tronche.com/gui/x/icccm/) (Inter-Client Communication Conventions Manual) standard defines three "selections": PRIMARY, SECONDARY, and CLIPBOARD. Despite the naming, all three are basically "clipboards". Rather than the old "cut buffers" system where arbitrary applications could modify data stored in the cut buffers, only one application may control or "own" a selection at one time. This prevents inconsistencies in the operation of the selections. However, in some cases, this can produce strange outcomes, such as a bidirectional shared clipboard with Windows (which uses a single-clipboard system) in a virtual machine.

Of the three selections, users should only be concerned with PRIMARY and CLIPBOARD. SECONDARY is only used inconsistently and was intended as an alternate to PRIMARY. Different applications may treat PRIMARY and CLIPBOARD differently; however, there is a degree of consensus that CLIPBOARD should be used for Windows-style clipboard operations, while PRIMARY should exist as a "quick" option, where text can be selected using the mouse or keyboard, then pasted using the middle mouse button (or some emulation of it). This can cause confusion and, in some cases, inconsistent or undesirable results from rogue applications.

## List of clipboard managers

Clipboard managers are applications that enable users to manipulate the clipboard. Note that many of these programs can also synchronize the previously mentioned clipboards.

*   **Anamnesis** — Clipboard manager that stores all the clipboard history and offers an interface to do a full-text search. It has both a command line and GUI mode available.

	[http://anamnesis.sourceforge.net/](http://anamnesis.sourceforge.net/) || [anamnesis](https://aur.archlinux.org/packages/anamnesis/)

*   **Autocutsel** — Command line and daemon interfaces to synchronize PRIMARY, `CLIPBOARD` and cut buffer selections.

	[http://www.nongnu.org/autocutsel/](http://www.nongnu.org/autocutsel/) || [autocutsel](https://www.archlinux.org/packages/?name=autocutsel)

*   **Clipboard Indicator** — Clipboard manager extension for GNOME Shell. Adds a clipboard indicator to the top panel, and caches clipboard history.

	[https://extensions.gnome.org/extension/779/clipboard-indicator/](https://extensions.gnome.org/extension/779/clipboard-indicator/) || [https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator](https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator)

*   **ClipIt** — Fork of Parcellite.

	[http://sourceforge.net/projects/gtkclipit/](http://sourceforge.net/projects/gtkclipit/) || [clipit](https://www.archlinux.org/packages/?name=clipit)

*   **Clipman** — A clipboard manager for Xfce. It keeps the clipboard contents around while it is usually lost when you close an application. It is able to handle text and images, and has a feature to execute actions on specific text selections by matching them against regular expressions.

	[http://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin](http://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin) || [xfce4-clipman-plugin](https://www.archlinux.org/packages/?name=xfce4-clipman-plugin)

*   **Clipmenu** — Dmenu based clipboard manager

	[https://github.com/cdown/clipmenu/](https://github.com/cdown/clipmenu/) || [clipmenu](https://aur.archlinux.org/packages/clipmenu/)

*   **Clipster** — A lightweight, command-line-driven clipboard manager, written in Python.

	[https://github.com/mrichar1/clipster](https://github.com/mrichar1/clipster) ||

*   **CopyQ** — Clever clipboard manager with searchable and editable history, custom actions on items and command line support.

	[https://github.com/hluk/CopyQ](https://github.com/hluk/CopyQ) || [copyq](https://aur.archlinux.org/packages/copyq/)

*   **[Glipper](https://en.wikipedia.org/wiki/Glipper "wikipedia:Glipper")** — Clipboard manager for the GNOME desktop with many features and plugin support.

	[https://launchpad.net/glipper](https://launchpad.net/glipper) || [glipper](https://aur.archlinux.org/packages/glipper/)

*   **GPaste** — Clipboard management system that aims at being a new generation Parcellite, with a modular structure split in a couple of libraries and a daemon for adaptability. Offers a GNOME Shell extension and a CLI interface.

	[https://github.com/Keruspe/GPaste](https://github.com/Keruspe/GPaste) || [gpaste](https://www.archlinux.org/packages/?name=gpaste)

*   **Keepboard** — Cross-platform clipboard manager. Saves text, image and file clipboard items.

	[http://sourceforge.net/projects/keepboard/](http://sourceforge.net/projects/keepboard/) ||

*   **[Klipper](https://en.wikipedia.org/wiki/Klipper "wikipedia:Klipper")** — Full featured clipboard manager for the KDE desktop.

	[http://userbase.kde.org/Klipper](http://userbase.kde.org/Klipper) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **Parcellite** — Lightweight yet feature-rich clipboard manager.

	[http://parcellite.sourceforge.net/](http://parcellite.sourceforge.net/) || [parcellite](https://www.archlinux.org/packages/?name=parcellite)

*   **Pasteall** — Clipboard monitor simple and functional.

	[https://github.com/LaraCraft93/Pasteall](https://github.com/LaraCraft93/Pasteall) || [pasteall](https://aur.archlinux.org/packages/pasteall/)

*   **Qlipper** — Lightweight and cross-platform clipboard history applet based on Qt.

	[https://code.google.com/p/qlipper/](https://code.google.com/p/qlipper/) || [qlipper](https://aur.archlinux.org/packages/qlipper/)

*   **Xclip** — A lightweight, command-line based interface to the clipboard.

	[http://sourceforge.net/projects/xclip/](http://sourceforge.net/projects/xclip/) || [xclip](https://www.archlinux.org/packages/?name=xclip)

*   **xcmenu** — Clipboard synchronizer developed for window manager users.

	[https://github.com/Cloudef/xcmenu](https://github.com/Cloudef/xcmenu) || [xcmenu-git](https://aur.archlinux.org/packages/xcmenu-git/)

*   **xsel** — Command-line program for getting and setting the contents of the X selection.

	[http://www.vergenet.net/~conrad/software/xsel/](http://www.vergenet.net/~conrad/software/xsel/) || [xsel](https://www.archlinux.org/packages/?name=xsel)

## See also

*   [Cut-and-paste in X](http://standards.freedesktop.org/clipboards-spec/clipboards-latest.txt)
*   [X Selections, Cut Buffers, and Kill Rings.](http://www.jwz.org/doc/x-cut-and-paste.html)