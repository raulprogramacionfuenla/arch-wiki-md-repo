Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

The Linux kernel supports EFISTUB booting which allows [EFI](/index.php/EFI "EFI") firmware to load the kernel as an EFI executable. The option is enabled by default on Arch Linux kernels, or if compiling a the kernel one can activate it by setting `CONFIG_EFI_STUB=y` in the Kernel configuration. See [The EFI Boot Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt) for more information.

With EFISTUB a kernel can be booted directly by a UEFI motherboard or indirectly using a [boot loader](/index.php/Boot_loader "Boot loader"). Using a boot loader is recommended if you have multiple kernel/initramfs pairs and your motherboard's UEFI boot menu is not easy to use.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparing for EFISTUB](#Preparing_for_EFISTUB)
*   [2 Booting EFISTUB](#Booting_EFISTUB)
    *   [2.1 Using a boot manager](#Using_a_boot_manager)
    *   [2.2 Using UEFI Shell](#Using_UEFI_Shell)
    *   [2.3 Using UEFI directly](#Using_UEFI_directly)
        *   [2.3.1 efibootmgr](#efibootmgr)
        *   [2.3.2 efibootmgr with .efi file](#efibootmgr_with_.efi_file)
        *   [2.3.3 UEFI Shell](#UEFI_Shell)
        *   [2.3.4 More tools](#More_tools)
        *   [2.3.5 Using a startup.nsh script](#Using_a_startup.nsh_script)
*   [3 See also](#See_also)

## Preparing for EFISTUB

First, you must create an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") and choose how it is mounted. See [EFI system partition#Mount the partition](/index.php/EFI_system_partition#Mount_the_partition "EFI system partition") for all available ESP mounting options.

**Tip:**

*   [pacman](/index.php/Pacman "Pacman") will directly update the kernel that the EFI firmware will read if you mount the ESP to `/boot`.
*   You can keep the kernel and initramfs off of the ESP if you use a boot manager which has a file system driver for the partition where they reside, e.g. [rEFInd](/index.php/REFInd "REFInd").

## Booting EFISTUB

**Note:** Linux Kernel EFISTUB initramfs path should be relative to the EFI System Partition's root and use backslashes (in accordance with EFI standards). For example, if the initramfs is located in `*esp*/EFI/arch/initramfs-linux.img`, the corresponding UEFI formatted line should be `initrd=\EFI\arch\initramfs-linux.img`. In the following examples we will assume that everything is under `*esp*/`.

### Using a boot manager

There are several UEFI boot managers which can provide additional options or simplify the process of UEFI booting - especially if you have multiple kernels/operating systems. See [Arch boot process#Boot loader](/index.php/Arch_boot_process#Boot_loader "Arch boot process") for more information.

### Using UEFI Shell

It is possible to launch an EFISTUB kernel from UEFI Shell as if it is a normal UEFI application. In this case the kernel parameters are passed as normal parameters to the launched EFISTUB kernel file.

```
> fs0:
> \vmlinuz-linux root=PARTUUID=3518bb68-d01e-45c9-b973-0b5d918aae96 rw initrd=\initramfs-linux.img

```

To avoid needing to remember all of your kernel parameters every time, you can save the executable command to a shell script such as `archlinux.nsh` on your UEFI System Partition, then run it with:

```
> fs0:
> archlinux

```

### Using UEFI directly

UEFI is designed to remove the need for an intermediate bootloader such as [GRUB](/index.php/GRUB "GRUB"). If your motherboard has a good UEFI implementation, it is possible to embed the kernel parameters within a UEFI boot entry and for the motherboard to boot Arch directly. You can use [efibootmgr](/index.php/Efibootmgr "Efibootmgr") or UEFI Shell v2 to modify your motherboard's boot entries.

#### efibootmgr

The command looks like

```
# efibootmgr --disk */dev/sdX* --part *Y* --create --label "Arch Linux" --loader /vmlinuz-linux --unicode 'root=PARTUUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* rw initrd=\initramfs-linux.img' --verbose

```

Where `*/dev/sdX*` and `*Y*` are the drive and partition number where the ESP is located. Change the `root=` parameter to reflect your Linux root partition. Note that the `-u`/`--unicode` argument in quotes is just the list of [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), so you may need to add additional parameters (e.g. for [suspend to disk](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate") or [microcode](/index.php/Microcode "Microcode")).

**Tip:** Save the command for creating your boot entry in a shell script somewhere, which makes it easier to modify (when changing kernel parameters, for example).

After adding the boot entry, you can verify the entry was added properly with:

```
# efibootmgr --verbose

```

**Note:** Some kernel and `efibootmgr` version combinations might refuse to create new boot entries. This could be due to lack of free space in the NVRAM. You can try deleting any EFI dump files
```
# rm /sys/firmware/efi/efivars/dump-*

```

Or, as a last resort, boot with the `efi_no_storage_paranoia` kernel parameter. You can also try to [downgrade](/index.php/Downgrade "Downgrade") your efibootmgr install to version 0.11.0\. This version works with Linux version 4.0.6\. See the bug discussion [FS#34641](https://bugs.archlinux.org/task/34641), in particular the [closing comment](https://bugs.archlinux.org/task/34641#comment111365), for more information.

To set the boot order, run:

```
# efibootmgr --bootorder *XXXX*,*XXXX* --verbose

```

where *XXXX* is the number that appears in the output of `efibootmgr` command against each entry.

The forum post titled [[Solved]The linux kernel with build in bootloader?](https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040%7C) might also be of interest.

#### efibootmgr with .efi file

If using [cryptboot](https://aur.archlinux.org/packages/cryptboot/) and [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/) to generate your own keys for [Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot") and sign the initramfs and kernel then create a bootable *.efi* image, [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) can be used directly to boot the *.efi* file:

```
# efibootmgr --create --disk /dev/sdX --part *partition_number* --label "*label*" --loader "EFI\*folder*\*file*.efi" --verbose

```

See [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8) for an explanation of the options.

#### UEFI Shell

Some UEFI implementations make it difficult to modify the NVRAM successfully using efibootmgr. If efibootmgr cannot successfully create an entry, you can use the [bcfg](/index.php/UEFI#bcfg "UEFI") command in UEFI Shell v2 (i.e., from the Arch Linux live iso).

First, find out the device number where your [ESP](/index.php/ESP "ESP") resides by using:

```
Shell> map

```

In this example, `1` is used as the device number. To list the contents of the [ESP](/index.php/ESP "ESP") do:

```
Shell> ls fs1:

```

To view the current boot entries do:

```
Shell> bcfg boot dump

```

To add an entry for your kernel, use:

```
Shell> bcfg boot add *N* fs1:\vmlinuz-linux "Arch Linux"

```

where `*N*` is the location where the entry will be added in the boot menu. 0 is the first menu item. Menu items already existing will be shifted in the menu without being discarded.

To add the necessary kernel options, first create a file on your ESP:

```
Shell> edit fs1:\options.txt

```

In the file add the boot line. For example:

```
root=/dev/sda2 ro initrd=\initramfs-linux.img

```

**Note:** Add extra spaces in the beginning of the line in the file. There is a [byte order mark](https://en.wikipedia.org/wiki/Byte_order_mark "wikipedia:Byte order mark") at the beginning of the line that will squash any character next to it which will cause an error when booting.

Press `F2` to save and then `F3` to exit.

To add these options to your previous entry do:

```
Shell> bcfg boot -opt *N* fs1:\options.txt

```

Repeat this process for any additional entries.

To remove a previously added item do:

```
Shell> bcfg boot rm *N*

```

#### More tools

Some of the tools above, and more, are briefly discussed in [rEFInd#Tools](/index.php/REFInd#Tools "REFInd").

#### Using a startup.nsh script

Some UEFI implementations do not retain EFI variables between cold boots (e.g. [VirtualBox](/index.php/VirtualBox "VirtualBox")) and anything set through the UEFI firmware interface is lost on poweroff.

The [UEFI Shell Specification 2.0](http://www.uefi.org/sites/default/files/resources/UEFI_Shell_Spec_2_0.pdf) establishes that a script called `startup.nsh` at the root of the ESP partition will always be interpreted and can contain arbitrary instructions; among those you can set a bootloading line. Make sure you mount the ESP partition on `/boot` and create a `startup.nsh` script that contains a kernel bootloading line. For example:

```
vmlinuz-linux rw root=/dev/sdX [rootfs=myfs] [rootflags=myrootflags] \
 [kernel.flag=foo] [mymodule.flag=bar] \
 [initrd=\intel-ucode.img] initrd=\initramfs-linux.img

```

This method will work with almost all UEFI firmware versions you may encounter in real hardware, you can use it as last resort. **The script must be a single long line.** Sections in brackets are optional and given only as a guide. Shell style linebreaks are for visual clarification only. FAT filesystems use the backslash as path separator and in this case, the backslash declares the initramfs is located in the root of the ESP partition. Only Intel microcode is loaded in the booting parameters line; AMD microcode is read from disk later during the boot process; this is done automatically by the kernel.

## See also

*   [Linux Kernel Documentation on EFISTUB](https://www.kernel.org/doc/Documentation/efi-stub.txt)
*   [Linux Kernel EFISTUB Git Commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=291f36325f9f252bd76ef5f603995f37e453fc60;hp=55839d515495e766605d7aaabd9c2758370a8d27)
*   [Rod Smith's page on EFISTUB](http://www.rodsbooks.com/efi-bootloaders/efistub.html)