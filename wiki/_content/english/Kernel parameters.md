There are three ways to pass options to the kernel and thus control its behaviour:

1.  When building the kernel. See [Kernel#Compilation](/index.php/Kernel#Compilation "Kernel") for details.
2.  When starting the kernel (usually, when invoked from a boot loader).
3.  At runtime (through the files in `/proc` and `/sys`). See [sysctl](/index.php/Sysctl "Sysctl") for details.

This page explains in more detail the second method and shows a list of the most used kernel parameters in Arch Linux.

Not all parameters are always available. Most are associated with subsystems and work only if the kernel is configured with those subsystems built in. They also depend on the presence of the hardware they are associated with.

Parameters either have the format `parameter` or `parameter=value`.

**Note:** All kernel parameters are case-sensitive. Most of them are lower case, writing those in upper case does not work.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Syslinux](#Syslinux)
    *   [1.2 systemd-boot](#systemd-boot)
    *   [1.3 GRUB](#GRUB)
    *   [1.4 GRUB Legacy](#GRUB_Legacy)
    *   [1.5 LILO](#LILO)
    *   [1.6 rEFInd](#rEFInd)
    *   [1.7 EFISTUB](#EFISTUB)
    *   [1.8 Hijacking cmdline](#Hijacking_cmdline)
*   [2 Parameter list](#Parameter_list)
*   [3 See also](#See_also)

## Configuration

**Note:**

*   You can check the parameters your system was booted up with by running `cat /proc/cmdline` and see if it includes your changes.
*   The Arch Linux [installation medium](https://www.archlinux.org/download/) uses [Syslinux](/index.php/Syslinux "Syslinux") for [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") systems, and [systemd-boot](/index.php/Systemd-boot "Systemd-boot") for [UEFI](/index.php/UEFI "UEFI") systems.

Kernel parameters can be set either temporarily by editing the boot menu when it shows up, or by modifying the boot loader's configuration file.

The following examples add the `quiet` and `splash` parameters to [Syslinux](/index.php/Syslinux "Syslinux"), [systemd-boot](/index.php/Systemd-boot "Systemd-boot"), [GRUB](/index.php/GRUB "GRUB"), [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), [LILO](/index.php/LILO "LILO"), and [rEFInd](/index.php/REFInd "REFInd").

### Syslinux

*   Press `Tab` when the menu shows up and add them at the end of the string:

	 `linux /boot/vmlinuz-linux root=/dev/sda3 initrd=/boot/initramfs-linux.img *quiet splash*` 

	Press `Enter` to boot with these parameters.

*   To make the change persistent after reboot, edit `/boot/syslinux/syslinux.cfg` and add them to the `APPEND` line:

	 `APPEND root=/dev/sda3 *quiet splash*` 

For more information on configuring Syslinux, see the [Syslinux](/index.php/Syslinux "Syslinux") article.

### systemd-boot

*   Press `e` when the menu appears and add the parameters to the end of the string:

	 `initrd=\initramfs-linux.img root=/dev/sda2 *quiet splash*` 

	Press `Enter` to boot with these parameters.

**Note:** If you have not set a value for menu timeout, you will need to hold `Space` while booting for the systemd-boot menu to appear.

**Note:** If you can't edit the parameters from the boot menu, you may need to edit `/boot/loader/loader.conf` and add "editor 1" to enable editing.

*   To make the change persistent after reboot, edit `/boot/loader/entries/arch.conf` (assuming you set up your [EFI system partition](/index.php/EFI_system_partition "EFI system partition")) and add them to the `options` line:

	 `options root=/dev/sda2 *quiet splash*` 

For more information on configuring systemd-boot, see the [systemd-boot](/index.php/Systemd-boot "Systemd-boot") article.

### GRUB

*   Press `e` when the menu shows up and add them on the `linux` line:

	 `linux /boot/vmlinuz-linux root=UUID=978e3e81-8048-4ae1-8a06-aa727458e8ff *quiet splash*` 

	Press `Ctrl+x` to boot with these parameters.

*   To make the change persistent after reboot, while you *could* manually edit `/boot/grub/grub.cfg` with the exact line from above, the best practice is to:

	Edit `/etc/default/grub` and append your kernel options to the `GRUB_CMDLINE_LINUX_DEFAULT` line:

	 `GRUB_CMDLINE_LINUX_DEFAULT="*quiet splash*"` 

	And then automatically re-generate the `grub.cfg` file with:

	 `# grub-mkconfig -o /boot/grub/grub.cfg` 

For more information on configuring GRUB, see the [GRUB](/index.php/GRUB "GRUB") article.

### GRUB Legacy

*   Press `e` when the menu shows up and add them on the `kernel` line:

	 `kernel /boot/vmlinuz-linux root=/dev/sda3 *quiet splash*` 

	Press `b` to boot with these parameters.

*   To make the change persistent after reboot, edit `/boot/grub/menu.lst` and add them to the `kernel` line, exactly like above.

For more information on configuring GRUB Legacy, see the [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") article.

### LILO

*   Add them to `/etc/lilo.conf`:

```
image=/boot/vmlinuz-linux
        ...
        *quiet splash*
```

For more information on configuring LILO, see the [LILO](/index.php/LILO "LILO") article.

### rEFInd

*   Press `+`, `F2`, or `Insert` on the desired menu entry and press it again on the submenu entry. Add kernel parameters at the end of the string:

	 `root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff rw initrd=\boot\initramfs-linux.img *quiet splash*` 

	Press `Enter` to boot with these parameters.

*   To make the change persistent after reboot, edit `/boot/refind_linux.conf` and append them to all/required lines, for example

	 `"Boot using default options"   "root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff rw *quiet splash*"` 

*   If you have disabled auto-detection of OSes in rEFInd and are defining OS stanzas instead in `*esp*/EFI/refind/refind.conf` to load your OSes, you can edit it like:

```
menuentry "Arch Linux" {
	...
	options  "root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff rw *quiet splash*"
	...
}

```

For more information on configuring rEFInd, see the [rEFInd](/index.php/REFInd "REFInd") article.

### EFISTUB

See [EFISTUB#Using UEFI directly](/index.php/EFISTUB#Using_UEFI_directly "EFISTUB").

### Hijacking cmdline

Even without access to your bootloader it is possible to change your kernel parameters to enable debugging (if you have root access). This can be accomplished by overwriting `/proc/cmdline` which stores the kernel parameters. However `/proc/cmdline` is not writable even as root, so this hack is accomplished by using a bind mount to mask the path.

First create a file containing the desired kernel parameters

 `/root/cmdline`  `root=/dev/disk/by-label/ROOT ro console=tty1 logo.nologo debug` 

Then use a bind mount to overwrite the parameters

```
# mount -n --bind -o ro /root/cmdline /proc/cmdline

```

The `-n` option skips adding the mount to `/etc/mtab`, so it will work even if root is mounted read-only. You can `cat /proc/cmdline` to confirm that your change was successful.

## Parameter list

This list is not comprehensive. For a complete list of all options, please see the [kernel documentation](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt).

| parameter | Description |
| root= | Root filesystem. |
| rootflags= | Root filesystem mount options. |
| ro | Mount root device read-only on boot (default). |
| rw | Mount root device read-write on boot. |
| initrd= | Specify the location of the initial ramdisk. |
| init= | Run specified binary instead of `/sbin/init` (symlinked to [systemd](/index.php/Systemd "Systemd") in Arch) as init process. |
| init=/bin/sh | Boot to shell. |
| systemd.unit= | Boot to a [specified target](/index.php/Systemd#Targets "Systemd"). |
| resume= | Specify a swap device to use when waking from [hibernation](/index.php/Hibernation "Hibernation"). |
| nomodeset | Disable [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). |
| zswap.enabled | Enable [Zswap](/index.php/Zswap "Zswap"). |
| panic= | Time before automatic reboot on kernel panic. |
| debug | Enable kernel debugging (events log level). |
| mem= | Force usage of a specific amount of memory to be used. |
| maxcpus= | Maximum number of processors that an SMP kernel will bring up during bootup. |
| selinux= | Disable or enable SELinux at boot time. |
| netdev= | Network devices parameters. |
| video=<videosetting> | Override framebuffer video defaults. |

 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") uses `ro` as default value when neither `rw` or `ro` is set by the [boot loader](/index.php/Boot_loader "Boot loader"). Boot loaders may set the value to use, for example GRUB uses `rw` by default (see [FS#36275](https://bugs.archlinux.org/task/36275) as a reference).

## See also

*   [Linux "Kernel Parameters" documentation](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt)
*   [Power saving#Kernel parameters](/index.php/Power_saving#Kernel_parameters "Power saving")
*   [List of kernel parameters with further explanation and grouped by similar options](http://files.kroah.com/lkn/lkn_pdf/ch09.pdf)