This page is a work in progress! More info coming soon.

| Device | Status |
| Network | Works |
| Wireless | Works |
| Sound | Works |
| Bluetooth | Works |
| Touchpad | Works |
| Graphics | Modify |
| USB 3.0 | Works |
| Webcam | Works |
| System info | Not tested |
| Power management | Buggy |
| WiDi | Not working |
| Touchpad gestures | Modify |

*   Works - Works out-of-the-box
*   Modify - Works with modifications
*   Not tested
*   Not working

## Contents

*   [1 System Settings](#System_Settings)
*   [2 Differences between XPS 9550 & Precision 5510](#Differences_between_XPS_9550_&_Precision_5510)
*   [3 XPS 15 9560 and "early 2017" revision](#XPS_15_9560_and_"early_2017"_revision)
*   [4 System Setup](#System_Setup)
    *   [4.1 Power Management](#Power_Management)
    *   [4.2 Sound](#Sound)
    *   [4.3 Graphics](#Graphics)
        *   [4.3.1 Intel only](#Intel_only)
            *   [4.3.1.1 acpi_call usage](#acpi_call_usage)
        *   [4.3.2 Intel with Nvidia](#Intel_with_Nvidia)
    *   [4.4 Screen](#Screen)
    *   [4.5 External Display](#External_Display)
        *   [4.5.1 Multihead](#Multihead)
    *   [4.6 WLAN](#WLAN)
    *   [4.7 Bluetooth](#Bluetooth)
    *   [4.8 BIOS](#BIOS)
    *   [4.9 Webcam](#Webcam)
    *   [4.10 Special Touch Keys](#Special_Touch_Keys)
        *   [4.10.1 Alternative method](#Alternative_method)
    *   [4.11 Hidden Keyboard Keys](#Hidden_Keyboard_Keys)
    *   [4.12 Touchpad Gestures](#Touchpad_Gestures)
        *   [4.12.1 libinput](#libinput)
            *   [4.12.1.1 XPS 9550](#XPS_9550)
        *   [4.12.2 Synaptics](#Synaptics)
    *   [4.13 Notes](#Notes)
*   [5 Howtos & Helpful Info](#Howtos_&_Helpful_Info)

## System Settings

Hardware settings om January 2011 model

```
00:00.0 Host bridge: Intel Corporation Core Processor DRAM Controller (rev 18)
00:01.0 PCI bridge: Intel Corporation Core Processor PCI Express x16 Root Port (rev 18)
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 18)
00:16.0 Communication controller: Intel Corporation 5 Series/3400 Series Chipset HECI Controller (rev 06)
00:1a.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1b.0 Audio device: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 06)
00:1c.0 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 (rev 06)
00:1c.1 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 2 (rev 06)
00:1c.3 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 4 (rev 06)
00:1c.4 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 5 (rev 06)
00:1c.5 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 6 (rev 06)
00:1d.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 06)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev a6)
00:1f.0 ISA bridge: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller (rev 06)
00:1f.2 SATA controller: Intel Corporation 5 Series/3400 Series Chipset 6 port SATA AHCI Controller (rev 06)
00:1f.3 SMBus: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller (rev 06)
00:1f.6 Signal processing controller: Intel Corporation 5 Series/3400 Series Chipset Thermal Subsystem (rev 06)
02:00.0 VGA compatible controller: nVidia Corporation Device 0df1 (rev a1)
02:00.1 Audio device: nVidia Corporation GF108 High Definition Audio Controller (rev a1)
04:00.0 Network controller: Intel Corporation Centrino Wireless-N 1000
05:00.0 USB Controller: NEC Corporation uPD720200 USB 3.0 Host Controller (rev 03)
09:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 06)
ff:00.0 Host bridge: Intel Corporation Core Processor QuickPath Architecture Generic Non-core Registers (rev 05)
ff:00.1 Host bridge: Intel Corporation Core Processor QuickPath Architecture System Address Decoder (rev 05)
ff:02.0 Host bridge: Intel Corporation Core Processor QPI Link 0 (rev 05)
ff:02.1 Host bridge: Intel Corporation Core Processor QPI Physical 0 (rev 05)
ff:02.2 Host bridge: Intel Corporation Core Processor Reserved (rev 05)
ff:02.3 Host bridge: Intel Corporation Core Processor Reserved (rev 05)

```

For Sandy Bridge model (L502X)

```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation 2nd Generation Core Processor Family PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 6 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #2 (rev 05)
00:1b.0 Audio device: Intel Corporation 6 Series Chipset Family High Definition Audio Controller (rev 05)
00:1c.0 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 1 (rev b5)
00:1c.1 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 2 (rev b5)
00:1c.3 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 4 (rev b5)
00:1c.4 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 5 (rev b5)
00:1c.5 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 6 (rev b5)
00:1d.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #1 (rev 05)
00:1f.0 ISA bridge: Intel Corporation HM67 Express Chipset Family LPC Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 6 Series Chipset Family 6 port SATA AHCI Controller (rev 05)
00:1f.3 SMBus: Intel Corporation 6 Series Chipset Family SMBus Controller (rev 05)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)
03:00.0 Network controller: Intel Corporation Centrino Wireless-N 1030 (rev 34)
04:00.0 USB Controller: NEC Corporation uPD720200 USB 3.0 Host Controller (rev 04)
06:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 06)

```

For 2012 Model (L521X)

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
00:1c.3 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 4 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 RAID bus controller: Intel Corporation 82801 Mobile SATA Controller [RAID mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
01:00.0 VGA compatible controller: NVIDIA Corporation GK107 [GeForce GT 640M] (rev ff)
07:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168 PCI Express Gigabit Ethernet controller (rev 07)
08:00.0 Network controller: Atheros Communications Inc. AR9462 Wireless Network Adapter (rev 01)
09:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5209 PCI Express Card Reader (rev 01)
09:00.1 SD Host controller: Realtek Semiconductor Co., Ltd. RTS5209 PCI Express Card Reader (rev 01)

```

For 2013 Model (9350)

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor DRAM Controller (rev 06) 
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller (rev 06)
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06)
00:04.0 Signal processing controller: Intel Corporation Device 0c03 (rev 06)
00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 05)
00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #2 (rev 05)
00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 05)
00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #1 (rev d5)
00:1c.2 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #3 (rev d5)
00:1c.3 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d5)
00:1d.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #1 (rev 05)
00:1f.0 ISA bridge: Intel Corporation HM87 Express LPC Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode] (rev 05)
00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 05)
00:1f.6 Signal processing controller: Intel Corporation 8 Series Chipset Family Thermal Management Controller (rev 05)
02:00.0 3D controller: NVIDIA Corporation GK107M [GeForce GT 750M] (rev ff)
06:00.0 Network controller: Intel Corporation Wireless 7260 (rev 6b)
07:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. Device 5249 (rev 01)

```

lspci for model 9550 (variant with touchscreen & PCIe m.2 ssd):

```
00:00.0 Host bridge: Intel Corporation Sky Lake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Sky Lake PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Device 191b (rev 06)
00:04.0 Signal processing controller: Intel Corporation Device 1903 (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-H LPSS I2C Controller #0 (rev 31)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-H LPSS I2C Controller #1 (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA Controller [AHCI mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.1 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #2 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #13 (rev f1)
00:1d.6 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #15 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 960M] (rev a2)
02:00.0 Network controller: Broadcom Corporation BCM43602 802.11ac Wireless LAN SoC (rev 01)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. Device 525a (rev 01)
04:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a802 (rev 01)

```

lsusb for model 9550 (variant with touchscreen & PCIe m.2 ssd):

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 04f3:21d5 Elan Microelectronics Corp. 
Bus 001 Device 003: ID 0a5c:6410 Broadcom Corp. 
Bus 001 Device 005: ID 1bcf:2b95 Sunplus Innovation Technology Inc. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

lspci for model Precision 5510:

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics P530 (rev 06)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO I2C Controller #0 (rev 31)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-H Serial IO I2C Controller #1 (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #13 (rev f1)
00:1d.6 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #15 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
01:00.0 3D controller: NVIDIA Corporation GM107GLM [Quadro M1000M] (rev a2)
02:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
03:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)

```

lspci for model Precision 5530 (With i9, Quadro P2000M, Hynix SSD, Intel Wireless-AC 9260):

```
00:00.0 Host bridge: Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Device 3e9b
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 07)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Lake PCH Thermal Controller (rev 10)
00:14.0 USB controller: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller (rev 10)
00:14.2 RAM memory: Intel Corporation Cannon Lake PCH Shared SRAM (rev 10)
00:15.0 Serial bus controller [0c80]: Intel Corporation Device a368 (rev 10)
00:15.1 Serial bus controller [0c80]: Intel Corporation Device a369 (rev 10)
00:16.0 Communication controller: Intel Corporation Cannon Lake PCH HECI Controller (rev 10)
00:17.0 SATA controller: Intel Corporation Device a353 (rev 10)
00:1b.0 PCI bridge: Intel Corporation Device a340 (rev f0)
00:1c.0 PCI bridge: Intel Corporation Device a338 (rev f0)
00:1c.4 PCI bridge: Intel Corporation Device a33c (rev f0)
00:1d.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port 9 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Device a30e (rev 10)
00:1f.3 Audio device: Intel Corporation Cannon Lake PCH cAVS (rev 10)
00:1f.4 SMBus: Intel Corporation Cannon Lake PCH SMBus Controller (rev 10)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller (rev 10)
01:00.0 3D controller: NVIDIA Corporation GP107GLM [Quadro P2000 Mobile] (rev ff)
02:00.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
03:00.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
03:01.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
03:02.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
04:00.0 System peripheral: Intel Corporation JHL6340 Thunderbolt 3 NHI (C step) [Alpine Ridge 2C 2016] (rev 02)
3a:00.0 USB controller: Intel Corporation Device 15db (rev 02)
3b:00.0 Network controller: Intel Corporation Wireless-AC 9260 (rev 29)
3c:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
3d:00.0 Non-Volatile memory controller: SK hynix Device 1504

```

## Differences between XPS 9550 & Precision 5510

The Precision 5510 is essentially identical to the [XPS 9550](/index.php/Dell_XPS_15_(9550) "Dell XPS 15 (9550)") variant, with the exception of an Intel Wireless NIC & Quadro 1000M Graphics Chip. Compared to the 9550's Broadcom NIC & 960M graphics chip.

## XPS 15 9560 and "early 2017" revision

There is [a dedicated page](/index.php/Dell_XPS_15_9560 "Dell XPS 15 9560") for version 9560 from 2016 and 2017 (especially troubleshouting video related problems).

## System Setup

### Power Management

For the Sandy Bridge model (L502X): Suspend works; hibernation does not (it gets hung on a flashing cursor in text mode and does not even switch video modes).

If hibernation/resume fails, or does not consistently work, try each of the following:

*   [Enable early KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for `intel_agp` and `i915`.

*   Create the following configuration file ([Source](https://bbs.archlinux.org/viewtopic.php?id=204739)):

 `/etc/systemd/sleep.conf` 
```
[Sleep]
HibernateState=disk
HibernateMode=shutdown

```

### Sound

For the XPS 9550 variant, sound works out of the box with the linux kernel. If you try to plug in headphones, you won't hear any output from them. Upon restart, you'll receive a **Dummy Output** as your sound card.

dmesg gives you this output:

```
snd_hda_intel 0000:00:1f.3: CORB reset timeout#1, CORBRP = 0
snd_hda_intel 0000:00:1f.3: no codecs found!

```

aplay -l should give you this output if Arch can detect your soundcard:

```
**** List of PLAYBACK Hardware Devices ****
card 0: PCH [HDA Intel PCH], device 0: ALC3266 Analog [ALC3266 Analog]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 0: PCH [HDA Intel PCH], device 3: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: PCH [HDA Intel PCH], device 7: HDMI 1 [HDMI 1]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: PCH [HDA Intel PCH], device 8: HDMI 2 [HDMI 2]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

aplay -l will give you this output if Arch cannot detect your soundcard:

```
aplay: device_list:268: no soundcards found...

```

You may or may not get sound back after a few restarts. This is a bug and has been documented here: [[1]](https://bugs.archlinux.org/task/49157)

Workarounds:

*   Install alsa-utils and run hdajackretask just toggle the drop down.
*   Suspend and resume your computer [(thank you spheenik)](https://www.reddit.com/r/Dell/comments/4y1svp/gnulinux_on_xps_9550_questions_arch/)
*   Restart your computer
*   Disable sound BIOS, powerboot into Arch, enable sound in BIOS, start Arch with sound back
*   Connect external sound card via USB

Regardless, for now, it is recommended that you don't/reduce hot-plugging headphones as it makes ALSA/PulseAudio break/very unstable.

### Graphics

By default, both Intel and NVidia cards are active, which can consume a lot of power. Using the Intel-only setup below, you can reduce your battery usage due to disabling the Nvidia card. The Intel and Nvidia setup describes how to utilize both cards and save power using [Bumblebee](/index.php/Bumblebee "Bumblebee"). See also [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics").

#### Intel only

If your model comes with an nVidia card which you don't use then you can try to disable it with an ACPI command. Depending on the model, this can have a small to *profound* effect on the laptop's temperature and battery life (it can more than *double* battery life!)

*   Install the Intel video driver using the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package.

*   To make sure nVidia module will not load into your system:
    *   Remove nouveau and/or nvidia drivers
    *   Use acpi_call (compile [acpi_call](http://github.com/mkottman/acpi_call) or use one of the [AUR packages](https://aur.archlinux.org/packages/?K=acpi_call)) to disable the nVidia card

##### acpi_call usage

```
modprobe acpi_call
./usr/share/acpi_call/examples/turn_off_gpu.sh

```

One of the many results will be "works!". Use the value that works in the following call:

```
echo '\_SB.<YOUR>.<POSITIVE>.<VALUE>._OFF' > /proc/acpi/call

```

If none worked, you can try one of the other files in the `/usr/share/acpi_call/examples` directory.

For example, the following works on the XPS 15 9550:

```
echo '\_SB.PCI0.PEG0.PEGP._OFF' > /proc/acpi/call

```

You can use this command *before* and *after* to see how the battery consumption change (you need to disconnect sector first and the lower the better):

```
cat /sys/class/power_supply/BAT0/current_now

```

To make this permanent, just create a [systemd unit file](/index.php/Systemd#Writing_unit_files "Systemd") with your working command.

#### Intel with Nvidia

The [Optimus](/index.php/Optimus "Optimus") setup consists of the integrated Intel chip connected to the laptop screen and the Nvidia card runs through this. As such, the Nvidia chip cannot be used without the Intel chip (some other laptops have the option in BIOS to turn Intel off and use just Nvidia, but not this laptop).

See the [Bumblebee](/index.php/Bumblebee "Bumblebee") page [set of instructions](/index.php/Bumblebee#Installation "Bumblebee"), particularly the Intel/Nvidia section which has been tested. The main thing to note is that installing both the Intel and Nvidia packages at once tends to avoid dependency issues.

### Screen

**9550 Flickering Screen:**

To fix screen flickering issues add `i915.edp_vswing=2` [to your boot parameters](https://blog.spirotot.com/2016/08/11/xps-9550-arch-linux-fix-screen-flickering/).

### External Display

Since the Display Port is controlled by the Intel driver, it tends to work quite well and will usually mirror the laptop display without configuration. Getting both the HDMI and DP adapters to display separate requires additional setup.

The Display Port can be accessed with a USB-C to Display Port adaptor, it should be a adaptor that works via "alternate mode" such as the plugable cable [[2]](http://plugable.com/products/usbc-dp/) (known to work), there are other adaptors that did not work (KiWiBiRD USB 3.1 Type C THUNDERBOLT 3 to DisplayPort 4K Adapter), though why it didn't is unknown.

#### Multihead

The following instructions should help configure the laptop to display separate output on two external monitors. These instructions are similar in nature to the [instructions](/index.php/Bumblebee#xf86-video-intel-virtual-crtc_and_hybrid-screenclone "Bumblebee") on the [Bumblebee](/index.php/Bumblebee "Bumblebee") page, though recent advancements in virtual displays on Intel reduce the number of steps and packages needed.

*   First, follow the instructions in the previous section to install drivers for both Intel and Nvidia with Bumblebee.
*   Run `Xorg -configure` to generate a `xorg.conf` file. It may have a different filename, so watch the output and regardless of where it generates it, copy it to `/etc/X11/xorg.conf`. This should generate something like the following (for two external monitors):

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
	Identifier     "X.org Configured"
	Screen      0  "Screen0" 0 0
	Screen      1  "Screen1" RightOf "Screen0"
	InputDevice    "Mouse0" "CorePointer"
	InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Files"
	ModulePath   "/usr/lib/xorg/modules"
	FontPath     "/usr/share/fonts/misc/"
	FontPath     "/usr/share/fonts/TTF/"
	FontPath     "/usr/share/fonts/OTF/"
	FontPath     "/usr/share/fonts/Type1/"
	FontPath     "/usr/share/fonts/100dpi/"
	FontPath     "/usr/share/fonts/75dpi/"
EndSection

Section "Module"
	Load  "glx"
EndSection

Section "InputDevice"
	Identifier  "Keyboard0"
	Driver      "kbd"
EndSection

Section "InputDevice"
	Identifier  "Mouse0"
	Driver      "mouse"
	Option	    "Protocol" "auto"
	Option	    "Device" "/dev/input/mice"
	Option	    "ZAxisMapping" "4 5 6 7"
EndSection

Section "Monitor"
	Identifier   "Monitor0"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Monitor"
	Identifier   "Monitor1"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Device"
	Identifier  "Card0"
	Driver      "nvidia"
	BusID       "PCI:1:0:0"
EndSection

Section "Device"
	Identifier  "Card1"
	Driver      "intel"
	BusID       "PCI:0:2:0"
EndSection

Section "Screen"
	Identifier "Screen0"
	Device     "Card0"
	Monitor    "Monitor0"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection

Section "Screen"
	Identifier "Screen1"
	Device     "Card1"
	Monitor    "Monitor1"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection
```

*   Change the `bumblebee.conf` file to the following settings (these are scattered throughout the conf file):

 `/etc/bumblebee/bumblebee.conf` 
```
KeepUnusedXServer=true
Driver=nvidia
# In the [driver-nvidia] section,
XorgConfFile=/etc/X11/xorg.conf
```

*   Add the following to your `.xinitrc` file.

 `~/.xinitrc` 
```
# Start Bumblebee, create VIRTUAL display, and configure monitors.
optirun true
intel-virtual-output
xrandr --output VIRTUAL2 --left-of HDMI1 --mode 1920x1080 --auto

# Turn off the laptop display (optional of course, leave out if you want triple display).
xrandr --output LVDS1 --off

# Execute a window manager or desktop environment here.
# ex: exec awesome
```

*   Run `startx` and check that your displays are working.

The modifications to `.xinitrc` automate the configuration of the displays. First, `optirun` is launched to run [Bumblebee](/index.php/Bumblebee "Bumblebee"). Then, the `intel-virtual-output` utility (included with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) versions 2.99+) creates a few `VIRTUAL` displays; `VIRTUAL2` was the display mapping to my HDMI port, run `xrandr` to double check this for yourself. The remaining commands may vary for your configuration, note that `LVDS1` is the laptop screen and `HDMI1` is actually the Display Port.

### WLAN

Remember that [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) will be needed for using a network manager such as [NetworkManager](/index.php/NetworkManager "NetworkManager"), see [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") for more information.

### Bluetooth

Some users may need to run

```
hciconfig hci0 reset

```

to get blueman working

Using power management with [TLP](/index.php/TLP "TLP") might cause a problem. Excluding Bluetooth devices from USB autosuspend by setting:

 `/etc/default/tlp` 
```
…
USB_BLACKLIST_BTUSB=1

```

can resolve the issue.

### BIOS

**XPS 9550 with InfinityEdge 4K**

The XPS 9550 4K, with its current state, is unstable due to it's young age. A majority of the bugs stem from Dell's BIOS.

Listed below are you may encounter with the XPS 9550 4K:

**01.02.00**
• Brightness works with slow fade (XF86MonBrightnessUp / xbacklight -inc:-dec)
• Sleep resume working around 80% of the time
• Resume from sleep restarts the laptop

**01.02.10+**
• Increased speeds (faster boot, applications feel snappier when loading, especially in 01.02.13)
• Black screen upon resume (the computer will operate as if it's on, to get display to work, set brightness to max using keyboard shortcut)
• Brightness flickers/stutters when dimming or increasing the brightness (demonstrated in [i3wm](/index.php/I3wm "I3wm"))
• Screen flickers on low brightness settings
• Possible poor fan behavior (not confirmed)
• Battery will not charge beyond 60%. The fix is to download and flash [1.2.14 BIOS or later](http://downloads.dell.com/FOLDER03906323M/1/XPS_9550_1.2.14.exe) Flashing 01.02.00 will be pointless after, as the issue carries over to this version of BIOS.

**01.02.14** *[Download](http://downloads.dell.com/FOLDER03906910M/1/Precision_5510_1.2.14.exe)*
• User [report](https://www.reddit.com/r/Dell/comments/51wr31/dell_xps15_9550_bios_1214_fixes_battery_at_60/) that the issue with the battery is fixed
• Still has black screen upon resume issue. To turn screen on, increase brightness to maximum using keyboard. It is not possible to decrease brightness after resume, either maximum or off.
• Increasing the brightness (eg, with xbacklight) by less than 9% does not have any effect. Decreasing by less than 9% always results in a decrease of 9%.

**1.02.16** *[Download](http://downloads.dell.com/FOLDER04030973M/1/XPS_9550_1.2.16.exe)*
• "Black screen upon resume" issue appears to have been fixed!

Many users have recommend the 01.02.00 BIOS, as it proves to be the most balanced out of all of the updates.

### Webcam

If the camera seems that it does not work (black image), try to enable/disable auto-exposure (for example in Skype, the option is in the Video Settings and in guc). In reality, the camera tries to record at 0.5 fps and this is why it seems not to work, even if everything seems normal.

### Special Touch Keys

The special touch keys are strangely mapped by default. One changes brightness, one does next track. They seem to be linked to the same key sequences as the Fn+F# keys that do the same job. To fix this, make this new file:

 `/opt/dell_touchkeys_keymap` 
```
0x90 previoussong # Previous song
0xA2 playpause # Play/Pause
0x99 nextsong # Next song
0xDB computer # First touch key, Dell apparently uses a key sequence here where 0xDB is a modifer, 0x2D stands for the touch key and 0x19 for the monitor toggle
0x85 prog1 # Second touch key
0x84 media # Third touch key

```

and add this to /etc/rc.local:

 `/etc/rc.local` 
```
…
# Fix touch keys
/usr/lib/udev/keymap input/event0 /opt/dell_touchkeys_keymap

```

[Source](https://bbs.archlinux.org/viewtopic.php?id=131886)

#### Alternative method

For L502x model the above method can be improved:

1.  No need to remap Play/Pause, Previous song, Next song keys as they are mapped correctly by default.
2.  For the first (leftmost) touch key: it's wired in a weird way on the hardware level. It seems to be wired to both Super_L and x. Your best bet would be to remap this using your DE or something like xbindkeys. You may want to double-check with `xev` or `xbindkeys -mk` to see exactly what keys it is producing.

Thus the keymap file should be (I prefer standard location):

 `/usr/lib/udev/keymaps/dell-xps-l502x` 
```
0x85 prog1 # Second touch key
0x84 media # Third touch key

```

and add this to /etc/rc.local:

 `/etc/rc.local` 
```
…
# Fix touch keys
/usr/lib/udev/keymap input/event0 /usr/lib/udev/keymaps/dell-xps-l502x

```

OR make a udev rule (the former remaps keys on boot, this lets udev take care of the remapping):

 `/etc/udev/rules.d/99-local.rules` 
```
…
# Keymap Dell Touch keys
SUBSYSTEM=="input", KERNEL=="event0", RUN+="keymap $name dell-xps-l502x"

```

### Hidden Keyboard Keys

For L502X model: there are additional Fn+<Key> (sequences) that are not marked at all on the keyboard but underlying hardware generates them anyway. Here they are (if you find more add them to the table below):

<caption>Hidden Fn Keys</caption>
| Fn+<Key> | Resulting key (sequence) |
| Fn+Esc | Sleep |
| Fn+Super_L | Super_R |
| Fn+Ins | Pause/Break |
| Fn+Del | Ctrl + Pause/Break |
| Fn+PrntScr | Alt + PrtSc/SysRq |

### Touchpad Gestures

The 1.2.21 BIOS update has caused many users to lose mouse scrolling in Chromium. [A bug report has been opened about the issue.](https://bugs.chromium.org/p/chromium/issues/detail?id=647038) A workaround would be to disable Smooth Scrolling in chrome://flags

#### libinput

##### XPS 9550

Working, using libinput and libinput-gestures.

#### Synaptics

If using Synaptics, read [Synaptics](/index.php/Synaptics "Synaptics").

### Notes

*   Remember to turn on Wi-Fi and Bluetooth by pressing the F2 button.
*   Card reader is finnicky. Try booting with a card inserted or inserting a card after it is booted and running `sudo echo 1 > /sys/bus/pci/rescan`. Otherwise, card reader will not be detected. It seems that a certain kernel update results in the workaround not working as well. More info needed.

## Howtos & Helpful Info

*   [A fairly comprehensive writeup of running Arch Linux on an XPS 15 9530.](http://drwho.virtadpt.net/archive/2015/01/05/linux-on-the-dell-xps-15-9530)
*   [Comprehensive coverage of Arch Linux on XPS 15 9550](https://ahxxm.com/151.moew/)
*   [Multitouch gestures with libinput and libinput-gestures](https://blog.spirotot.com/2016/07/27/dell-xps-15-9550-arch-linux-trackpad-gestures/)
*   [Fixing 9550 screen flickering and black screen on resume from suspend](https://blog.spirotot.com/2016/08/11/xps-9550-arch-linux-fix-screen-flickering/)
*   [Arch on New XPS 15 (Late 2015)](https://bbs.archlinux.org/viewtopic.php?id=204739)