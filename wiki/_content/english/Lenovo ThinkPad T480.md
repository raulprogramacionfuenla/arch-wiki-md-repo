| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Mobile internet](/index.php/ThinkPad_mobile_internet "ThinkPad mobile internet") | Yes¹ |
| Fingerprint Sensor |
| 

1.  No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.

 |

This article covers the installation and configuration of Arch Linux on a Lenovo T480 laptop. Everything seems to work pretty much out the box.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 Suspend / Hibernation](#Suspend_/_Hibernation)
*   [3 TrackPoint and Touchpad](#TrackPoint_and_Touchpad)
*   [4 Power management/Throttling issues](#Power_management/Throttling_issues)
*   [5 UEFI](#UEFI)
*   [6 Screen backlight](#Screen_backlight)
*   [7 Encryption and keyboard](#Encryption_and_keyboard)
*   [8 Special buttons](#Special_buttons)

## Hardware

Using kernel 4.16.8-1-ARCH

```
Version: ThinkPad T480
SKU Number: LENOVO_MT_20L5_BU_Think_FM_ThinkPad T480
Product Name: 20L5CTO1WW

```

`lspci` returns something like:

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
03:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
3d:00.0 Non-Volatile memory controller: Lenovo Device 0003

```

`lsusb` returns something like:

```
Bus 002 Device 005: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 06cb:009a Synaptics, Inc. 
Bus 001 Device 003: ID 04f2:b604 Chicony Electronics Co., Ltd 
Bus 001 Device 002: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

and for Product Name: `20L50007GE` something like:

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 002: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 001 Device 006: ID 06cb:009a Synaptics, Inc. 
Bus 001 Device 005: ID 13d3:56a6 IMC Networks 
Bus 001 Device 004: ID 8087:0a2b Intel Corp. 
Bus 001 Device 003: ID 2cb7:0210  
Bus 001 Device 002: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader

```

ID `2cb7:0210` is the 4G modem Fibocom L830-EB. Noted that devices come with 4G modem Fibocom L850-GL may not work.

## Suspend / Hibernation

Suspend and Hibernation work out of the box. The T480 does not have the same issues as the [X1 Carbon Gen 6](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#Suspend_issues "Lenovo ThinkPad X1 Carbon (Gen 6)")

## TrackPoint and Touchpad

TrackPoint and Touchpad work out of the box and do not seem to have the same issues as the [X1 Carbon Gen 6](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#TrackPoint_and_Touchpad_issues "Lenovo ThinkPad X1 Carbon (Gen 6)")

## Power management/Throttling issues

See

*   X1 Carbon Gen 6 [Power management/Throttling issues](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#Power_management.2FThrottling_issues "Lenovo ThinkPad X1 Carbon (Gen 6)")
*   ThinkPad T480s [Thermal Throttling Fix](/index.php/Lenovo_ThinkPad_T480s#Thermal_Throttling_Fix "Lenovo ThinkPad T480s")
*   [https://github.com/erpalma/throttled](https://github.com/erpalma/throttled)

## UEFI

Lenovo T480 is tied in with Microsoft and will only boot to windows efi file or default EFI fallback file. Verified on bios version 1.14

Sollution is to rename the .efi to that specific file.

```
 mount /dev/sdXY /mnt # replace XY with the letter & number of the Arch EFI system partition

 # Windows .efi file

```

```
 mkdir -p /mnt/EFI/Microsoft/Boot
 cp /mnt/EFI/grub/grubx64.efi /mnt/EFI/Microsoft/Boot/bootmgfw.efi

```

```
 # EFI fallback .efi file (As defined in the EFI standard.)

```

```
 mkdir -p /mnt/EFI/BOOT
 cp /mnt/EFI/grub/grub64.efi /mnt/EFI/BOOT/bootx64.efi

```

Source: [http://www.rodsbooks.com/efi-bootloaders/installation.html#alternative-naming](http://www.rodsbooks.com/efi-bootloaders/installation.html#alternative-naming)

## Screen backlight

Without the intel driver (xf86-video-intel), neither xbacklight or xrandr brightness control are working.

## Encryption and keyboard

Assuming encrypted installation, during boot process you are prompted to enter password to decrypt disk. In some cases you may not be able to enter password, because at this time keyboard driver is not loaded yet.

To fix this simply put `atkbd` module into `MODULES` in [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") config file:

 `/etc/mkinitcpio.conf` 
```
  MODULES = (... atkbd)

```

And generate new ramdisk environment:

```
 # mkinitcpio -p linux

```

## Special buttons

Some special buttons are not supported by X server due to keycode number limit.

| Key combination | Scancode | Keycode |
| `Fn+F11` | `0x49` | `374` `KEY_KEYBOARD` |
| `Fn+F12` | `0x45` | `364` `KEY_FAVORITES` |

You can remap unsupported keys using [udev hwdb](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes"):

 `/etc/udev/hwdb.d/90-thinkpad-keyboard.hwdb` 
```
evdev:name:ThinkPad Extra Buttons:dmi:bvn*:bvr*:bd*:svnLENOVO*:pn*
 KEYBOARD_KEY_45=prog1
 KEYBOARD_KEY_49=prog2

```

Update hwdb after editing the rule.

```
# udevadm hwdb --update
# udevadm trigger --sysname-match="event*"

```

Their names will be "XF86Launch2" (KEY_KEYBOARD) and "XF86Launch1" (KEY_FAVORITES)