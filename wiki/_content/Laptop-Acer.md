# Laptop/Acer

| [Laptop main page](/index.php/Laptop "Laptop") |
| **Acer** - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

## Model List

| Model Version | Arch Linux
Install CD Version
 | Hardware Support | Remark |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power Management | Modem | Other |
| TravelMate 2413NLC | Gimmick 0.7.2 | Intel GMA 915 driver: _i810_ | Intel 82801FB with internal microphone | OK | -- | -- | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
CPU frequency scaling: Yes | untested | Hot keys: untested |
| Aspire 5100-3825 | 0.8 (Voodoo) | ATI Radeon Xpress 1100 | Intel | Realtek | Atheros | n/a | untested | Hot keys: untested |
| Aspire 1501LMi | 0.9 (Don't Panic) | ATI Radeon 9600: HW acceleration only with proprietary driver | VIA: OK | Broadcom: OK | untested | none | Suspend to RAM: ??
Disk: Yes
Battery: Yes
CPU frequency scaling: Yes | untested | Hot keys: untested |
| Travelmate 6292 | Core Dump,
Overlord | Intel x3100: HW acceleration with Intel's open-source driver, ~1100 FPS in the glxgears | Intel HDA: OK (model=acer) | Broadcom BCM5787M: OK | Intel iwl4965: OK | Broadcom: OK | Suspend to RAM: ??
Disk: Ok
Battery: Yes
CPU frequency scaling: Yes | untested | Hot keys: untested
FireWire (Texas Instruments) TSB43AB23: OK(?) | FireWire detects well but I haven't tested it yet |
| Aspire 5024 | 0.7.2 | ATI Radeon X700
Runs Compiz on both fglrx ([catalyst](https://aur.archlinux.org/packages/catalyst/)<sup><small>AUR</small></sup>) >= 8.02 and radeon driver | AC97: OK | Realtek: OK | Broadcom 4318
Needs _acer_apci_ + firmware or ndiswrapper driver | N/A | Battery: Yes
Suspend: Video and Wi-Fi problems
CPU frequency scaling: powernow-k8 driver | untested | KeyTouch works for hot keys
Volume control, etc. |
| [Aspire 7720](/index.php/Acer_Aspire_7720 "Acer Aspire 7720") | 2009.02 | Intel i965 | ALC268: working OK | Broadcom BCM5787M (tg3): OK | Intel 3945: Needs microcode | Detected, works | Battery: Yes
Suspend: Seems to work ok
Hibernation: still flaky (often hangs in the middle of restoring) | With linuxant drivers, might work | Web cam driver: _uvcvideo_; card reader: only SD cards seem to work; special keys (Acer Arcade, direct access to browser/mail) seem to not work; volume knob at the side is seen as a multimedia key. | FireWire seems to be recognized, untested. For 64-bit, update BIOS to fix ACPI and wireless problems. |
| [Aspire E5-573](/index.php/Acer_Aspire_E5-573 "Acer Aspire E5-573") | 2015.12 | Intel i965 | OK | OK | OK | not detected | OK | not present | ... | ... |
| Aspire 7730 | 2009.08 i686 & x86_64 | Intel Mobile 4 Series
i810
Autoconfiguration works. Compiz OK, with indirect rendering. | ALC888
Playback & internal microphone: OK; microphone input socket: not tested
`options snd-hda-intel model=laptop` added to `/etc/modprobe.d/sound.conf` to get headphone output working | OK | OK, with iwlagn | None | Suspend to RAM: OK
Suspend to disk crashes on i686, OK on x86_64
CPU frequency scaling: OK
(using cpufreq) | Untested | Hot keys: OK
Web cam: OK
HDMI: untested
Card reader: untested | Problem booting install CD
Solved with `ln -sf /dev/sr0 /dev/archiso` at ramfs |
| TravelMate 8371G (TM8371G-944G32n) | 2010.05 x86_64 | Intel GM45, works with _i915_. Radeon HD 4330 listed but cannot switch to it. | OK | OK, works with _r8169_ | OK, works with _iwlagn_ | OK, works with _btusb_ | s2ram works (see remarks), s2disk works, CPU scaling works, no fan control | No modem | Web cam works with _uvcvideo_.
Card reader works.
Fingerprint reader does not seem to have a driver! | Suspend to RAM only works with the `i8042.reset=1` kernel parameter. Otherwise, it fails to wake up, and ends up rebooting itself uncleanly!
Generally, this Acer seems to work quite well with Arch Linux :-) |
| Aspire 4935 | 2009.08 x86_64 | Nvidia GeForce 9300M GS | OK, Intel HDA | OK | OK | Untested | Suspend to RAM: OK
Suspend to disk: OK
Frequency scaling: OK
(using cpufreq) | Untested | Hot keys: OK
Audio touch panel NOT working
Web cam: OK
HDMI: OK | By "audio touch panel" I mean the illuminated plastic hot key touch panel on the right-hand side of the keyboard. |
| AspireOne D255e | [Archboot 2010.12-1](https://wiki.archlinux.org/index.php/Archboot) | Intel GMA 3150 | OK | OK, Atheros 8132 worked only with latest Archboot not official images | OK, Broadcom worked only with latest Archboot not official images | Untested | Untested | Untested | Hot keys: OK
Synaptic Touchpad: OK |
| Aspire 2920Z | 2009.2 | Intel Mobile GM965/GL960 Integrated Graphics Controller | OK, Intel 82801H | OK, Broadcom NetLink BCM5787M Gigabit Ethernet PCI Express | OK, Broadcom BCM4311 802.11b/g WLAN | n/a | Suspend to RAM: OK.
Suspend to disk: OK.
CPU frequency scaling: untested | Untested | Hot keys: web, mail, and wireless work. Blue _e_ on the left: not working
Synaptic touchpad: OK
 | Not everything worked fine on fresh installation. Requires some work. |
| Aspire 5735z [[1]](http://panam.acer.com/acerpanam/notebook/0000/Acer/Aspire5735Z/Aspire5735Zsp3.shtml) | archlinux-2014.09.03-dual | Intel GMA 4500M | OK | OK | OK | Untested | Suspend to RAM: OK.
Suspend to disk: OK.
CPU frequency scaling: untested | Untested | Hot keys: OK (except Bluetooth: untested)
Synaptic Touchpad: OK |

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Acer&oldid=411299](https://wiki.archlinux.org/index.php?title=Laptop/Acer&oldid=411299)"