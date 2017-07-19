Currently there are three methods of suspending available: **suspend to RAM** (usually called just **suspend**), **suspend to disk** (usually known as **hibernate**), and **hybrid suspend** (sometimes aptly called **suspend to both**):

*   **Suspend to RAM** method cuts power to most parts of the machine aside from the RAM, which is required to restore the machine's state. Because of the large power savings, it is advisable for laptops to automatically enter this mode when the computer is running on batteries and the lid is closed (or the user is inactive for some time).

*   **Suspend to disk** method saves the machine's state into [swap space](/index.php/Swap_space "Swap space") and completely powers off the machine. When the machine is powered on, the state is restored. Until then, there is zero power consumption.

*   **Suspend to both** method saves the machine's state into swap space, but does not power off the machine. Instead, it invokes usual suspend to RAM. Therefore, if the battery is not depleted, the system can resume from RAM. If the battery is depleted, the system can be resumed from disk, which is much slower than resuming from RAM, but the machine's state has not been lost.

There are multiple low level interfaces (backends) providing basic functionality, and some high level interfaces providing tweaks to handle problematic hardware drivers/kernel modules (e.g. video card re-initialization).

## Contents

*   [1 Low level interfaces](#Low_level_interfaces)
    *   [1.1 kernel (swsusp)](#kernel_.28swsusp.29)
    *   [1.2 uswsusp](#uswsusp)
    *   [1.3 tuxonice](#tuxonice)
*   [2 High level interfaces](#High_level_interfaces)
    *   [2.1 systemd](#systemd)
    *   [2.2 pm-utils](#pm-utils)
*   [3 Hibernation](#Hibernation)
    *   [3.1 About swap partition/file size](#About_swap_partition.2Ffile_size)
    *   [3.2 Required kernel parameters](#Required_kernel_parameters)
        *   [3.2.1 Hibernation into swap file](#Hibernation_into_swap_file)
    *   [3.3 Configure the initramfs](#Configure_the_initramfs)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 ACPI_OS_NAME](#ACPI_OS_NAME)
    *   [4.2 VAIO Users](#VAIO_Users)
    *   [4.3 Suspend/hibernate doesn't work, or not consistently](#Suspend.2Fhibernate_doesn.27t_work.2C_or_not_consistently)
    *   [4.4 Wake-on-LAN](#Wake-on-LAN)
    *   [4.5 Instantaneous wakeups from suspend](#Instantaneous_wakeups_from_suspend)

## Low level interfaces

Though these interfaces can be used directly, it is advisable to use some of [high level interfaces](#High_level_interfaces) to suspend/hibernate. Using low level interfaces directly is significantly faster than using any high level interface, since running all the pre- and post-suspend hooks takes time, but hooks can properly set hardware clock, restore wireless etc.

### kernel (swsusp)

The most straightforward approach is to directly inform the in-kernel software suspend code (swsusp) to enter a suspended state; the exact method and state depends on the level of hardware support. On modern kernels, writing appropriate strings to `/sys/power/state` is the primary mechanism to trigger this suspend.

See [kernel documentation](https://www.kernel.org/doc/Documentation/power/states.txt) for details.

### uswsusp

The uswsusp ('Userspace Software Suspend') is a wrapper around the kernel's suspend-to-RAM mechanism, which performs some graphics adapter manipulations from userspace before suspending and after resuming.

See main article [Uswsusp](/index.php/Uswsusp "Uswsusp").

### tuxonice

TuxOnIce is a fork of the kernel implementation of suspend/hibernate that provides kernel patches to improve the default implementation. It requires a custom kernel to achieve this purpose.

See main article [TuxOnIce](/index.php/TuxOnIce "TuxOnIce").

## High level interfaces

**Note:** The end goal of these packages is to provide binaries/scripts that can be invoked to perform suspend/hibernate. Actually hooking them up to power buttons or menu clicks or laptop lid events is usually left to other tools. To automatically suspend/hibernate on certain power events, such as laptop lid close or battery depletion percentage, you may want to look into running [Acpid](/index.php/Acpid "Acpid").

### systemd

[systemd](/index.php/Systemd "Systemd") provides native commands for suspend, hibernate and a hybrid suspend, see [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management") for details. This is the default interface used in Arch Linux.

See [Power management#Sleep hooks](/index.php/Power_management#Sleep_hooks "Power management") for additional information on configuring suspend/hibernate hooks. Also see `man systemctl`, `man systemd-sleep`, and `man systemd.special`.

### pm-utils

pm-utils is a set of shell scripts that encapsulate the backend's suspend/hibernate functionality. It comes with a set of pre- and post-suspend tweaks and various hooks to customize the process.

See main article [pm-utils](/index.php/Pm-utils "Pm-utils").

## Hibernation

In order to use hibernation, you need to create a [swap](/index.php/Swap "Swap") partition or file. You will need to point the kernel to your swap using the `resume=` kernel parameter, which is configured via the boot loader. You will also need to [configure the initramfs](#Configure_the_initramfs). This tells the kernel to attempt resuming from the specified swap in early userspace. These three steps are described in detail below.

### About swap partition/file size

Even if your swap partition is smaller than RAM, you still have a big chance of hibernating successfully. According to [kernel documentation](https://www.kernel.org/doc/Documentation/power/interface.txt):

	*`/sys/power/image_size` controls the size of the image created by the suspend-to-disk mechanism. It can be written a string representing a non-negative integer that will be used as an upper limit of the image size, in bytes. The suspend-to-disk mechanism will do its best to ensure the image size will not exceed that number. However, if this turns out to be impossible, it will try to suspend anyway using the smallest image possible. In particular, if "0" is written to this file, the suspend image will be as small as possible. Reading from this file will display the current image size limit, which is set to 2/5 of available RAM by default.*

You may either decrease the value of `/sys/power/image_size` to make the suspend image as small as possible (for small swap partitions), or increase it to possibly speed up the hibernation process.

### Required kernel parameters

The kernel parameter `resume=*swap_partition*` has to be used. Either the name the kernel assigns to the partition or its [UUID](/index.php/UUID "UUID") can be used as `*swap_partition*`. For example:

*   `resume=/dev/sda1`
*   `resume=UUID=4209c845-f495-4c43-8a03-5363dd433153`
*   `resume=/dev/mapper/archVolumeGroup-archLogicVolume` -- example if using LVM

Generally, the naming method used for the `resume` parameter should be the same as used for the `root` parameter.

The configuration depends on the used [boot loader](/index.php/Boot_loader "Boot loader"), refer to [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for details.

#### Hibernation into swap file

**Warning:** [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") does not support swap files. Failure to heed this warning may result in file system corruption. While a swap file may be used on Btrfs when mounted through a loop device, this will result in severely degraded swap performance.

Using a swap file instead of a swap partition requires an additional kernel parameter `resume_offset=*swap_file_offset*`.

The value of `*swap_file_offset*` can be obtained by running `filefrag -v *swap_file*`, the output is in a table format and the required value is located in the first row of the `physical_offset` column. For example:

 `# filefrag -v /swapfile` 
```
Filesystem type is: ef53
File size of /swapfile is 4294967296 (1048576 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..       0:      38912..     38912:      1:            
   1:        1..   22527:      38913..     61439:  22527:             unwritten
   2:    22528..   53247:     899072..    929791:  30720:      61440: unwritten
...

```

In the example the value of `*swap_file_offset*` is the first `38912` with the two periods.

The value of `*swap_file_offset*` can also be obtained by running `swap-offset *swap_file*`. The *swap-offset* binary is provided by package [uswsusp-git](https://aur.archlinux.org/packages/uswsusp-git/).

**Note:**

*   The `resume` kernel parameter specifies the device of the partition that contains the swap file, not swap file itself! The parameter `resume_offset` informs the system where the swap file starts on the resume device. Before the first hibernation a reboot is required for them to be active.
*   If using [uswsusp](/index.php/Uswsusp "Uswsusp"), then these two parameters have to be provided in `/etc/suspend.conf` via the keys `resume device` and `resume offset`. No reboot is required in this case.

**Tip:** You might want to decrease the [Swap#Swappiness](/index.php/Swap#Swappiness "Swap") for your swapfile if the only purpose is to be able to hibernate and not expand RAM.

### Configure the initramfs

*   When an [initramfs](/index.php/Initramfs "Initramfs") with the `base` hook is used, which is the default, the `resume` hook is required in `/etc/mkinitcpio.conf`. Whether by label or by UUID, the swap partition is referred to with a udev device node, so the `resume` hook must go *after* the `udev` hook. This example was made starting from the default hook configuration:

	 `HOOKS="base udev **resume** autodetect modconf block filesystems keyboard fsck"` 

	Remember to [rebuild the initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") for these changes to take effect.

**Note:** [LVM](/index.php/LVM "LVM") users should add the `resume` hook after `lvm2`.

*   When an initramfs with the `systemd` hook is used, a resume mechanism is already provided, and no further hooks need to be added.

## Troubleshooting

### ACPI_OS_NAME

You might want to tweak your **DSDT table** to make it work. See [DSDT](/index.php/DSDT "DSDT") article

### VAIO Users

Add acpi_sleep=nonvs kernel flag to your loader, and you are done!

### Suspend/hibernate doesn't work, or not consistently

There have been many reports about the screen going black without easily viewable errors or the ability to do anything when going into and coming back from suspend and/or hibernate. These problems have been seen on both laptops and desktops. This is not an official solution, but switching to an older kernel, especially the LTS-kernel, will probably fix this.

Sometimes the screen goes black due to device initialization from within the initramfs. Removing any modules you might have in [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") and rebuilding the initramfs, can possibly solve this issue, specially graphics drivers for [early KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"). Initializing such devices before resuming can cause inconsistencies that prevents the system resuming from hibernation. This does not affect resuming from RAM. Also, check this [article](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues) for the best practices to debug suspend/hibernate issues.

For Intel graphics drivers, enabling early KMS may help to solve the blank screen issue. Refer to [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for details.

### Wake-on-LAN

If [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") is active, the network interface card will consume power even if the computer is hibernated.

### Instantaneous wakeups from suspend

For some Intel Haswell systems with the LynxPoint and LynxPoint-LP chipset, instantaneous wakeups after suspend are reported. They are linked to erroneous BIOS ACPI implementations and how the `xhci_hcd` module interprets it during boot. As a work-around reported affected systems are added to a blacklist (named `XHCI_SPURIOUS_WAKEUP`) by the kernel case-by-case.[[1]](https://bugzilla.kernel.org/show_bug.cgi?id=66171#c6)

Instantaneous resume may happen, for example, if a USB device is plugged during suspend and ACPI wakeup triggers are enabled. A viable work-around for such a system, if it is not on the blacklist yet, is to disable the wakeup triggers. An example to disable wakeup through USB is described as follows.[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1575617)

To view the current configuration:

 `$ cat /proc/acpi/wakeup` 
```
Device  S-state   Status   Sysfs node
...
EHC1      S3    *enabled  pci:0000:00:1d.0
EHC2      S3    *enabled  pci:0000:00:1a.0
XHC       S3    *enabled  pci:0000:00:14.0
...

```

The relevant devices are `EHC1`, `EHC1` and `XHC` (for USB 3.0). To toggle their state you have to echo the device name to the file as root.

```
# echo EHC1 > /proc/acpi/wakeup
# echo EHC2 > /proc/acpi/wakeup
# echo XHC > /proc/acpi/wakeup

```

This should result in suspension working again. However, this settings are only temporary and would have to be set at every reboot. To automate this take a look at [systemd#Writing unit files](/index.php/Systemd#Writing_unit_files "Systemd"). See [BBS thread](https://bbs.archlinux.org/viewtopic.php?pid=1575617#p1575617) for a possible solution and more information.