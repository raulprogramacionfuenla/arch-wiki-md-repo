## Contents

*   [1 Hardware Overview](#Hardware_Overview)
*   [2 Sound](#Sound)
*   [3 Display](#Display)
*   [4 Frozen CPU Frequency Scaling](#Frozen_CPU_Frequency_Scaling)
*   [5 Touchpad](#Touchpad)
*   [6 What does not work](#What_does_not_work)

## Hardware Overview

Output of `lspci -nn`:

```
00:00.0 Host bridge [0600]: Intel Corporation Skylake Host Bridge/DRAM Registers [8086:1904] (rev 08)
00:02.0 VGA compatible controller [0300]: Intel Corporation HD Graphics 520 [8086:1916] (rev 07)
00:04.0 Signal processing controller [1180]: Intel Corporation Skylake Processor Thermal Subsystem [8086:1903] (rev 08)
00:14.0 USB controller [0c03]: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller [8086:9d2f] (rev 21)
00:14.2 Signal processing controller [1180]: Intel Corporation Sunrise Point-LP Thermal subsystem [8086:9d31] (rev 21)
00:16.0 Communication controller [0780]: Intel Corporation Sunrise Point-LP CSME HECI #1 [8086:9d3a] (rev 21)
00:17.0 SATA controller [0106]: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] [8086:9d03] (rev 21)
00:1c.0 PCI bridge [0604]: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 [8086:9d14] (rev f1)
00:1c.5 PCI bridge [0604]: Intel Corporation Sunrise Point-LP PCI Express Root Port #6 [8086:9d15] (rev f1)
00:1d.0 PCI bridge [0604]: Intel Corporation Device [8086:9d1a] (rev f1)
00:1f.0 ISA bridge [0601]: Intel Corporation Sunrise Point-LP LPC Controller [8086:9d48] (rev 21)
00:1f.2 Memory controller [0580]: Intel Corporation Sunrise Point-LP PMC [8086:9d21] (rev 21)
00:1f.3 Audio device [0403]: Intel Corporation Sunrise Point-LP HD Audio [8086:9d70] (rev 21)
00:1f.4 SMBus [0c05]: Intel Corporation Sunrise Point-LP SMBus [8086:9d23] (rev 21)
00:1f.6 Ethernet controller [0200]: Intel Corporation Ethernet Connection I219-LM [8086:156f] (rev 21)
01:00.0 Network controller [0280]: Intel Corporation Wireless 8260 [8086:24f3] (rev 3a)
02:00.0 Network controller [0280]: Intel Corporation Device [8086:093c] (rev 3a)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader [10ec:525a] (rev 01)

```

Output of `lsusb`:

```
Bus 002 Device 006: ID 413c:81b6 Dell Computer Corp.
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 0a5c:5834 Broadcom Corp.
Bus 001 Device 002: ID 1bcf:28b8 Sunplus Innovation Technology Inc.
Bus 001 Device 006: ID 048d:1167 Integrated Technology Express, Inc.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Sound

Audio output via the headphone port does not work if the microphone is muted when the laptop is started. Unmuting the microphone fixes the issue, it can be savely muted afterwards.

## Display

According to `cat /sys/kernel/debug/dri/0/i915_edp_psr_status`:

```
Sink_Support: yes
Source_OK: no
Enabled: no
Active: no
Busy frontbuffer bits: 0x000
Re-enable work scheduled: no
Main link in standby mode: no
HW Enabled & Active bit: no

```

The FullHD panel supports psr, but the i915 psr implementation for skylake has [Known Bugs](https://bugs.freedesktop.org/show_bug.cgi?id=94126)

## Frozen CPU Frequency Scaling

If you experience frequency scaling freezing, i.e. your cpu stays at the lowest idle frequency follow these steps:

1.  shutdown your laptop
2.  remove back cover
3.  unplug battery
4.  hold power button for 20s (Count to 40 to be sure)
5.  replug battery
6.  attach back cover
7.  start laptop and retest

See also [FS#56866](https://bugs.archlinux.org/task/56866).

## Touchpad

Support for the ALPS touchpad included in Dell E7270 & E7470 was only added in Linux kernel 4.9, with some issues accidentally introduced in 4.13 and then refixed in 4.15\. The fixes were backported to Linux LTS kernels 4.9 & 4.14\. Earlier kernels didn't recognize the touchpad and used it in its emulated PS/2 mode, so changing options (like scroll direction, multi-touch gestures, etc.) was not possible.

## What does not work

*   Fingerprint Reader (0a5c:5834)
*   DW5811e stops working after suspend, presumably the UEFI does initial configuration, needs more testing
    *   Per [LKML](https://lkml.org/lkml/2016/11/4/117) runtime power management does not work for the chip (EM7455) used in the DW5811e, disabling runtime pm and reseting the device makes it usable.