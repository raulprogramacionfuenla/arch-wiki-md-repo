| **Device** | **Status** | **Modules** |
| Intel | **Working** | xf86-video-intel |
| Nvidia | **Working** | nvidia |
| Ethernet | **Working** | r8169 |
| Wireless | **Working** | ath9k |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** | xf86-input-synaptics |
| Camera | **Working** | evdev? |
| Card Reader | **Unknown** |
| Bluetooth | **Unknown** |

Related articles

*   [ASUS N56vj](/index.php/ASUS_N56vj "ASUS N56vj")

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 Audio](#Audio)
    *   [2.4 Multitouch](#Multitouch)

# Hardware

| **CPU** | Intel(R) Core(TM) i7-4700HQ CPU @ 2.40GHz |
| **RAM** | 12 GB (1x4GB,1x8GB) |
| **Display** | 15.6" LCD |
| **Integrated Graphics** | Intel HD 4000 |
| **Discrete Graphics** | NVIDIA GeForce GTX 760M |
| **Sound** | Intel HD Audio |
| **Ethernet** | RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller |
| **Wireless** | AR9485 Wireless Network Adapter |
| **Hard Disk** | 1 TB 5400rpm SATA |
| **Touchpad** | ETPS/2 Elantech Touchpad |

# Configuration

## Video

nouveau runs into some problems ([https://bbs.archlinux.org/viewtopic.php?id=178207](https://bbs.archlinux.org/viewtopic.php?id=178207)). There may be a way to patch it, but not without building a custom kernel and applying the patches mentioned in the bug report. After a full day of trying (module won't build against current kernel, patch won't apply to linux-mainline, ...), I've given up and switched to:

nvidia works fine using [bumblebee](/index.php/Bumblebee "Bumblebee").

## Wireless

**Edit:** I switched to the linux-ck kernel and no longer see this bug. I didn't see any obvious patches for it, but maybe there's something there. Either way, everything works flawlessly now...

Ugh. Why can't everyone just use Intel wireless cards?

The card (using `ath9k`) successfully scans for networks, successfully connects, successfully negotiates an IP address, and successfully disconnects immediately afterwards. Maybe the fifth or sixth time I power down the card and power it up again, it will hold the connection. After connecting once successfully, I haven't seen any problems reconnecting to a given network. This seems like a dhcp problem.

## Audio

Using `hdajackretask` to set the unconnected 0x16 pin to anything sets the external speaker as the rear right channel (`Internal (LFE)` is the closest approximation to what it should be).

## Multitouch

See [Multitouch displays](/index.php/Multitouch_displays "Multitouch displays").