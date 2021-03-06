[Touchegg](https://github.com/JoseExposito/touchegg) is a multitouch gesture program, that runs as a user in the background, recognizes gestures, translates them to more conventional types of events and/or performs custom actions in response to them.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Gnome Shell](#Gnome_Shell)
        *   [2.1.1 Start on login](#Start_on_login)

## Installation

Install [touchegg](https://aur.archlinux.org/packages/touchegg/) package. Alternatively, it is also available [touchegg-git](https://aur.archlinux.org/packages/touchegg-git/).

Touchegg comes with its own minimal GUI, but you can also install [touchegg-gce-git](https://aur.archlinux.org/packages/touchegg-gce-git/) - [Touchegg-GCE](https://github.com/Raffarti/Touchegg-gce) (GUI configuration editor).

## Configuration

The configuration file is found in `~/.config/touchegg/touchegg.conf`.

It is a basic XML file that defines various gestures. Please note that at this time `TAP_AND_HOLD`, `PINCH`, and `ROTATE`, do not appear to work.

The list of triggers can be found [here](https://github.com/JoseExposito/touchegg/wiki/All-gestures-supported-by-Touch%C3%A9gg).

The list of actions can be found [here](https://github.com/JoseExposito/touchegg/wiki/All-actions-supported-by-Touch%C3%A9gg).

### Gnome Shell

Very basic so far. This should give you basic functionality. Hopefully we can update this for complete application support.

Edit `~/.config/touchegg/touchegg.conf`, add this:

```
<gesture type="DRAG" fingers="1" direction="ALL">
    <action type="DRAG_AND_DROP">BUTTON=1</action>
</gesture>

```

and then edit this entry:

```
<gesture type="DRAG" fingers="2" direction="ALL">
    <action type="SCROLL">SPEED=7:INVERTED=**true**</action>
</gesture>

```

#### Start on login

1.  Hit `alt-f2`;
2.  Type `gnome-session-properties`;
3.  Hit `add`;
4.  In the box labeled "Command" type `touchegg`. Fill in "Name" and "Label" as you choose;
5.  Hit `OK`.

**Note:** `gnome-session-properties` has been removed from `gnome 3.12`. Currently, you can install [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) from the [AUR](/index.php/AUR "AUR"). See more details in the [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=180282)

Alternatively, you can modify your [.xprofile](/index.php/.xprofile ".xprofile"):

 `~/.xprofile`  `touchegg &`