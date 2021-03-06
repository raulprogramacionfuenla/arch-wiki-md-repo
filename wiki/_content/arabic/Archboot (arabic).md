## Contents

*   [1 ما هو Archboot?](#ما_هو_Archboot?)
*   [2 إصدارات Archboot ISO](#إصدارات_Archboot_ISO)
    *   [2.1 حرق صورة القرص](#حرق_صورة_القرص)
    *   [2.2 أنماط الإقلاع المدعومة في وسيط تثبيت Archboot](#أنماط_الإقلاع_المدعومة_في_وسيط_تثبيت_Archboot)
    *   [2.3 نظام PXE للإقلاع/الإنقاذ](#نظام_PXE_للإقلاع/الإنقاذ)
    *   [2.4 أخبار](#أخبار)
        *   [2.4.1 أمور عامة](#أمور_عامة)
        *   [2.4.2 تغيرات النواة](#تغيرات_النواة)
        *   [2.4.3 تغييرات البيئة](#تغييرات_البيئة)
        *   [2.4.4 تغيرات الإعداد](#تغيرات_الإعداد)
        *   [2.4.5 تغيرات quickinst](#تغيرات_quickinst)
    *   [2.5 تاريخ](#تاريخ)
    *   [2.6 الاختلافات مع وسيط تثبيت archiso](#الاختلافات_مع_وسيط_تثبيت_archiso)
    *   [2.7 مميزات الإعداد التفاعلي](#مميزات_الإعداد_التفاعلي)
    *   [2.8 معاملات الإقلاع](#معاملات_الإقلاع)
        *   [2.8.1 المعاملات العامة للإقلاع](#المعاملات_العامة_للإقلاع)
        *   [2.8.2 خيارات الفيديو و framebuffer](#خيارات_الفيديو_و_framebuffer)
    *   [2.9 FAQ, القيود والمشكلات المعروفة](#FAQ,_القيود_والمشكلات_المعروفة)
    *   [2.10 تلميحات UEFI](#تلميحات_UEFI)
    *   [2.11 العِلل](#العِلل)
*   [3 روابط](#روابط)
*   [4 قرص USB للاستعادة](#قرص_USB_للاستعادة)
*   [5 إنشاء ملفات الصوة](#إنشاء_ملفات_الصوة)
    *   [5.1 Archboot Allinone ISO Howto](#Archboot_Allinone_ISO_Howto)
        *   [5.1.1 المتطلبات](#المتطلبات)
        *   [5.1.2 إنشاء بيئة محول الجذر في archboot](#إنشاء_بيئة_محول_الجذر_في_archboot)
        *   [5.1.3 تثبيت archboot والترقية ﻷحدث الحزم](#تثبيت_archboot_والترقية_ﻷحدث_الحزم)
        *   [5.1.4 توليد الصور](#توليد_الصور)

## ما هو Archboot?

*   Archboot is a set of scripts to generate bootable media for CD/USB/PXE.
*   It is designed for installation or rescue operation.
*   It only runs in RAM, without any special filesystems like squashfs, thus it is limited to the RAM which is installed in your system.

[Install](/index.php/Pacman "Pacman") [archboot](https://www.archlinux.org/packages/?name=archboot) from the [official repositories](/index.php/Official_repositories "Official repositories").

## إصدارات Archboot ISO

*   Hybrid image files and torrents are provided, which include i686 and/or x86_64 core repository.
*   Please read the according Changelog files for RAM limitations.
*   Please check md5sum before using it.
*   [Download 2013.03 „2k13-R1“](https://downloads.archlinux.de/iso/archboot/2013.03) / [Changelog](ftp://ftp.archlinux.org/iso/archboot/Changelog-2013.03-4.txt) / [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=159997)

### حرق صورة القرص

Hybrid image file is a standard CD-burnable image and also a raw disk image.

*   Can be burned to CD(RW) media using most CD-burning utilities.
*   Can be raw-written to a drive using 'dd' or similar utilities. This method is intended for use with USB thumb drives.

 `'dd if=<imagefile> of=/dev/<yourdevice> bs=1M'` 

### أنماط الإقلاع المدعومة في وسيط تثبيت Archboot

*   تدعم إقلع BIOS مع syslinux.
*   It supports UEFI booting with gummiboot and EFISTUB,

	for booting LTS kernels with efilinux-efi .

	(only UEFI USB is supported, UEFI CD booting is not supported!)

*   It supports grub's iso loopback support.

	variables used (below for example):

	iso_loop_dev=UUID=XXXX

	iso_loop_path=/blah/archboot.iso

*   It supports booting using syslinux's memdisk (only in BIOS mode).

### نظام PXE للإقلاع/الإنقاذ

[Download 2013.03 „2k13-R1“](https://downloads.archlinux.de/iso/archboot/2013.03/boot) needed files from the directory.

*   vmlinuz_i686 + initramfs_i686.img (i686)
*   vmlinuz_x86_64 + initramfs_x86_64.img(x86_64)
*   vmlinuz_i686_lts + initramfs_i686.img (i686 LTS kernel)
*   vmlinuz_x86_64_lts + initramfs_x86_64.img (x86_64 LTS kernel)
*   For PXE booting add the kernel and initrd to your tftp setup and you will get a running installation/rescue system.
*   For Rescue booting add an entry to your bootloader pointing to the kernel and initrd.

### أخبار

2013.03 „2k13-R1“

*   major update/cleanup on all components

#### أمور عامة

*   kernel 3.8.4 / LTS kernel 3.0.70
*   pacman 4.0.3 usage
*   RAM recommendations: 768 MB

#### تغيرات النواة

*   bump to latest 3.8.x series and bump lts to latest 3.0.x series

#### تغييرات البيئة

*   updated pacman mirrorlist
*   replaced netcfg with netctl
*   removed ide-legacy hook
*   replaced arch_virtio, arch_fw with block hook
*   replaced usbinput with keyboard hook
*   replaced dbus-core with dbus
*   bump to latest mkinitcpio code
*   bump syslinux from 4.x to 5.0
*   removed bind and dnsutils
*   blacklist floppy module during boot

#### تغيرات الإعداد

*   replaced netcfg network setup with netctl
*   always install netctl instead of netcfg
*   replaced gummiboot-efi with gummiboot
*   removed initscripts compat mode
*   always install systemd-sysvcompat
*   updated gummiboot install routine
*   updated refind install routine
*   removed persistent soundcard and network hack,

	systemd handles everything now.

*   no need to add hostname to /etc/hosts anymore

#### تغيرات quickinst

*   removed initscripts compat mode
*   removed rc.conf hint
*   removed double check on ntfs

### تاريخ

History of old releases can be found [here](ftp://ftp.archlinux.org/iso/archboot/history).

### الاختلافات مع وسيط تثبيت archiso

*   It provides an additional interactive setup and quickinst script.
*   It contains [core] repository on media.
*   It provides the long time support kernel as boot and installation option.
*   It runs a modified Arch Linux system in initramfs.
*   It is restricted to RAM usage, everything which is not necessary like

	man or info pages etc. is not provided.

*   It doesn't mount anything during boot process.

### مميزات الإعداد التفاعلي

*   Media and Network installation mode
*   Changing keymap and consolefont
*   Changing time and date
*   Setup network with netctl
*   Preparing storage disk, like auto-prepare, partitioning, GUID (gpt) support, 4k sector drive support etc.
*   Creation of software raid/raid partitions, lvm2 devices and luks encrypted devices
*   Supports standard linux,raid/raid_partitions,dmraid,lvm2 and encrypted devices
*   Filesystem support: ext2/3/4, btrfs, nilfs2, reiserfs,xfs,jfs,ntfs-3g,vfat
*   Name scheme support: PARTUUID, PARTLABEL, FSUUID, FSLABEL and KERNEL
*   Mount support of grub loopback and memdisk installation media
*   Package selection support
*   Signed package installation
*   hwdetect script is used for preconfiguration
*   Auto/Preconfiguration of framebuffer, uvesafb, kms mode, fstab, mkinitcpio.conf, systemd, crypttab and mdadm.conf
*   Configuration of basic system files
*   Setting root password
*   grub-bios, grub-efi-x86_64, grub-efi-i386, refind-efi-x86_64, gummiboot, efilinux-efi, lilo, extlinux/syslinux, bootloader support

### معاملات الإقلاع

#### المعاملات العامة للإقلاع

*   earlymodules

	load modules before hooks are executed

	Usage:

	earlymodules=<comma-separated-array>

	earlymodules=ahci,ehci-hcd

*   disablehooks

	disable a hook which is run during bootup

	Usage:

	disablehooks=<comma-separated-array>

	disablehooks=arch_floppy,arch_cdrom

*   root

	Using this option will boot you into your specified existing system.

	Usage:

	root=/dev/<your-root-of-installed-system>

	root=/dev/sda3

*   rootflags

	Using this option will pass special mount options for your root device

	Usage:

	rootflags=<comma-separated-array>

	rootflags=subvol=root,compress,ssd

*   advanced

	This will override advanced hooks running order for your system.

	Default order is arch_mdadm,arch_lvm2,arch_encrypt

	Advanced hooks are: arch_mdadm,arch_lvm2,arch_encrypt

	Usage:

	advanced=hook1,hook2,hook3

	advanced=arch_encrypt,arch_mdadm

*   arch-addons

	You want to load external addon packages or configs into the install environment.

	Place external addon packages in /packages directory of your external device.

	Place external configs in /config directory of your external device.

#### خيارات الفيديو و framebuffer

*   uvesafb

	enables uvesafb mode during boot and activates setup routine to use it later on installed system.

	you need to specify your supported resolution eg.:

	uvesafb=<resolution>-<depth>

	uvesafb=1024x768-16

*   fbmodule

	Loads the fb module you specify durin boot process and activates setup routine to use it later on installed system.

	Use it like this fbmodule=<yourmodule>, e.g. fbmodule=cirrusfb

### FAQ, القيود والمشكلات المعروفة

*   Release specific known issues and workarounds are posted in changelog files.
*   Check also the forum threads for posted fixes and workarounds.
*   Why screen stays blank or other weird screen issues happen?

	Some hardware doesn't like the KMS activation, use radeon.modeset=0 or i915.modeset=0 on boot prompt.

*   dmraid might be broken on some boards, support is not perfect here.

	The reason is there are so many different hardware components out there. At the moment 1.0.0rc16 is included, with latest fedora patchset.

*   grub2 cannot detect correct bios boot order:

	It may happen that hd(x,x) entries are not correct, thus first reboot may not work.

	Reason: grub cannot detect bios boot order.

	Fix: Either change bios boot order or change menu.lst to correct entries after successful boot. This cannot be fixed it is a restriction in grub/grub2!

*   Why is parted used in setup routine, instead of cfdisk in msdos partitiontable mode?

	parted is the only linux partition program that can handle all type of things the setup routine offers.

	cfdisk cannot handle GPT/GUID nor it can allign partitions correct with 1MB spaces for 4k sector disks.

	cfdisk is a nice tool but is too limited to be the standard partitioner anymore.

	cfdisk is still included but has to be run in an other terminal.

### تلميحات UEFI

*   [Create UEFI bootable USB from ISO](/index.php/Unified_Extensible_Firmware_Interface#Archboot "Unified Extensible Firmware Interface")
*   [Remove UEFI boot support from ISO](/index.php/Unified_Extensible_Firmware_Interface#Archboot_2 "Unified Extensible Firmware Interface")

### العِلل

[Arch Linux Bugtracker](https://bugs.archlinux.org)

## روابط

*   [GIT repository](https://projects.archlinux.org/archboot.git/)

## قرص USB للاستعادة

Take care about which device actually is your USB stick. The next command will render all data on /dev/sdX inaccessible.

*   First, wipe the bootsector of the USB stick:

 `dd if=/dev/zero of=/dev/sdX bs=512 count=1` 

*   Then, create a new FAT32 partition on the stick and write a FAT32 filesystem on it (vfat or type b in fdisk terminology):

```
fdisk /dev/sdX <<EOF
n
p
1

t
b
w
EOF

mkdosfs -F32 /dev/sdX1

```

## إنشاء ملفات الصوة

### Archboot Allinone ISO Howto

(Quick regeneration of installation media with latest available core packages)

#### المتطلبات

*   x86_64 architecture
*   archboot ISO
*   ~ 3GB free space on disk

#### إنشاء بيئة محول الجذر في archboot

```
# install archboot
pacman -S archboot
mkdir <x86_64_chroot>
pacman --root "<x86_64_chroot>" -S base --noconfirm --noprogressbar
mkdir <i686_chroot>
linux32 pacman --root "<i686_chroot>" -S base --noconfirm --noprogressbar

```

*   Mount and copy the following files to each chroot:

```
mount -o bind /dev <chrootpath>/dev
mount -o bind /tmp <chrootpath>/tmp
mount -o bind /sys <chrootpath>/sys
mount -o bind /proc <chrootpath>/proc
cp -a /etc/mtab <chrootpath>/etc/mtab
cp /etc/resolv.conf  <chrootpath>/etc/resolv.conf

```

*   Enter archboot x86_64 chroot:

```
chroot <chrootpath>

```

*   Enter archboot i686 chroot:

```
linux32 chroot <chrootpath>

```

#### تثبيت archboot والترقية ﻷحدث الحزم

```
# install in both chroots archboot:
pacman -S archboot
# update in both chroots to latest available packages
pacman -Syu

```

#### توليد الصور

```
# run in both chroots (needs quite some time ...)
archboot-allinone.sh -t
# put the generated tarballs in one directory and run (needs quite some time ...)
archboot-allinone.sh -g

```

*   Finished you get a burnable iso image, a rawwrite usb image and a hybrid image which is both in one.
*   Do not forget to unmount for each chroot after leaving:

```
umount <chrootpath>/dev
umount <chrootpath>/tmp
umount <chrootpath>/sys
umount <chrootpath>/proc

```

وقتا ممتعا! tpowa ( مطور Archboot )