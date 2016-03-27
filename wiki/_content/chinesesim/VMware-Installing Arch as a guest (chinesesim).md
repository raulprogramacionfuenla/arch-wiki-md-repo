**翻译状态：** 本文是英文页面 [Installing_Arch_Linux_in_VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-05，点击[这里](https://wiki.archlinux.org/index.php?title=Installing_Arch_Linux_in_VMware&diff=0&oldid=390025)可以查看翻译后英文页面的改动。

这篇文章是关于如何在[VMware](/index.php/VMware "VMware")产品，比如[Player (Plus)](http://www.vmware.com/products/player/)，[Fusion](http://www.vmware.com/products/fusion/)或[Workstation](http://www.vmware.com/products/workstation/)中安装ArchLinux。

## Contents

*   [1 内核驱动程序](#.E5.86.85.E6.A0.B8.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F)
*   [2 VMware Tools versus Open-VM-Tools](#VMware_Tools_versus_Open-VM-Tools)
*   [3 Open-VM-Tools](#Open-VM-Tools)
    *   [3.1 Utilities](#Utilities)
    *   [3.2 Modules](#Modules)
    *   [3.3 安装](#.E5.AE.89.E8.A3.85)
        *   [3.3.1 Multi-User Target](#Multi-User_Target)
        *   [3.3.2 Graphical Target](#Graphical_Target)
*   [4 官方 VMware Tools](#.E5.AE.98.E6.96.B9_VMware_Tools)
    *   [4.1 模块](#.E6.A8.A1.E5.9D.97)
    *   [4.2 安装（从客户机）](#.E5.AE.89.E8.A3.85.EF.BC.88.E4.BB.8E.E5.AE.A2.E6.88.B7.E6.9C.BA.EF.BC.89)
*   [5 Xorg配置](#Xorg.E9.85.8D.E7.BD.AE)
*   [6 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [6.1 共享文件夹](#.E5.85.B1.E4.BA.AB.E6.96.87.E4.BB.B6.E5.A4.B9)
        *   [6.1.1 在引导时启用](#.E5.9C.A8.E5.BC.95.E5.AF.BC.E6.97.B6.E5.90.AF.E7.94.A8)
            *   [6.1.1.1 fstab](#fstab)
            *   [6.1.1.2 Systemd](#Systemd)
        *   [6.1.2 Prune mlocate DB](#Prune_mlocate_DB)
    *   [6.2 3D加速](#3D.E5.8A.A0.E9.80.9F)
    *   [6.3 时间同步](#.E6.97.B6.E9.97.B4.E5.90.8C.E6.AD.A5)
        *   [6.3.1 Host machine as time source](#Host_machine_as_time_source)
        *   [6.3.2 External server as time source](#External_server_as_time_source)
    *   [6.4 Performance Tips](#Performance_Tips)
        *   [6.4.1 Paravirtual SCSI adapter](#Paravirtual_SCSI_adapter)
        *   [6.4.2 Paravirtual Network Adapater](#Paravirtual_Network_Adapater)
        *   [6.4.3 Virtual Machine Settings](#Virtual_Machine_Settings)
*   [7 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [7.1 鼠标问题](#.E9.BC.A0.E6.A0.87.E9.97.AE.E9.A2.98)
        *   [7.1.1 按钮丢失](#.E6.8C.89.E9.92.AE.E4.B8.A2.E5.A4.B1)
    *   [7.2 Boot problems](#Boot_problems)
        *   [7.2.1 Slow boot time](#Slow_boot_time)
        *   [7.2.2 Shutdown/Reboot hangs](#Shutdown.2FReboot_hangs)
    *   [7.3 Autofit problems](#Autofit_problems)
    *   [7.4 拖拽，复制/粘贴](#.E6.8B.96.E6.8B.BD.EF.BC.8C.E5.A4.8D.E5.88.B6.2F.E7.B2.98.E8.B4.B4)
    *   [7.5 Problems when running as a shared VM on Workstation 11](#Problems_when_running_as_a_shared_VM_on_Workstation_11)
    *   [7.6 Shared folder not mounted after system upgrade](#Shared_folder_not_mounted_after_system_upgrade)

## 内核驱动程序

*   `vmw_balloon` - 物理内存管理驱动. It acts like a "balloon" that can be inflated to reclaim physical pages by reserving them in the guest and invalidating them in the monitor, freeing up the underlying machine pages so they can be allocated to other guests. It can also be deflated to allow the guest to use more physical memory. Deallocated Virtual Machine memory can be reused in the host without terminating the guest.
*   `vmw_pvscsi` - For VMware's Paravirtual SCSI (PVSCSI) HBA.
*   `vmw_vmci` - 虚拟机通信接口. It enables high-speed communication between host and guest in a virtual environment via the VMCI virtual device.
*   `vmwgfx` - 3D加速. This is a KMS enabled DRM driver for the VMware SVGA2 virtual hardware.
*   `vmxnet3` - For VMware's vmxnet3 virtual ethernet NIC.

These drivers are only needed if you are running Arch Linux on a hypervisor like [VMware vSphere Hypervisor](http://www.vmware.com/products/vsphere-hypervisor)

*   `vsock` - 虚拟套接字协议. It is similar to the TCP/IP socket protocol, allowing communication between Virtual Machines and hypervisor or host.
*   `vmw_vsock_vmci_transport` - Implements a VMCI transport for Virtual Sockets.

**注意:** 以上模块只有少量会被 Arch的[Udev](/index.php/Udev "Udev") 自动检测并启用。一些附加模块，比如`vmw_balloon`, 可能需要添加到[Mkinitcpio](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")的`MODULES`列表。例如: ` # cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmw_balloon vmw_pvscsi vmware_vmhgfs vsock vmw_vsock_vmci_transport ..."
```

Make sure to rebuild with:

```
 # mkinitcpio -p linux

```

Some modules, such as `vmware_vmhgfs`, will require additional work to manually `compile` and systemd `enable` in order to function properly.

## VMware Tools versus Open-VM-Tools

In 2007, VMware released large partitions of the [VMware Tools](http://kb.vmware.com/kb/340) under the LGPL as [Open-VM-Tools](http://sourceforge.net/projects/open-vm-tools/). The official Tools are not available [separately](http://packages.vmware.com/tools/esx/latest/repos/index.html) for Arch Linux.

Originally, VMware Tools provided the best drivers for network and storage, combined with the functionality for other features such as time synchronization. However, for quite a while now the drivers for the network/SCSI adapter are part of the Linux kernel, and VMware Tools is only needed for extra features like Unity mode.

## Open-VM-Tools

### Utilities

The [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) package comes namely with the following utilities:

*   `vmtoolsd` - Service responsible for the Virtual Machine status report.
*   `vmware-checkvm` - Tool to check whether a program is running in the guest.
*   `vmware-toolbox-cmd` - Tool to obtain Virtual Machine information of the host.
*   `vmware-user-suid-wrapper` - Tool to enable clipboard sharing (copy/paste) between host and guest.
*   `vmware-vmblock-fuse` - Filesystem utility. Enables drag & drop functionality between host and guest through [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (Filesystem in Userspace).
*   `vmware-xferlogs` - Dumps logging/debugging information to the Virtual Machine logfile.

### Modules

The [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) package comes with the following modules:

*   `vmhgfs` - Filesystem driver. Enables sharing between host and guest.
*   `vmxnet` - for the old VMXNET network adapter.

### 安装

从[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools)包。如果您想要使用文件共享就需要安装[open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/)。

Open-VM-Tools在`/etc/arch-release`读取版本信息，但这是空的:

```
# cat /proc/version > /etc/arch-release

```

#### Multi-User Target

If your booting into the `multi-user.target` then follow the steps mentioned here. If your booting into the graphical.target then please skip this section and read the instructions for the `graphical.target`.

[Start](/index.php/Start "Start") `vmtoolsd.service` and enable it on boot, if desired.

**Note:** There is a bug in `vmtoolsd`, where the service is not able to properly shut down and hangs for 60 seconds. A quick workaround is described in [the forums](https://bbs.archlinux.org/viewtopic.php?pid=1206006#p1206006).

#### Graphical Target

如果您启动后进入一个图形环境，那么按照以下步骤启动VMware tools

```
#systemctl enable vmware-vmblock-fuse.service

```

If you have installed [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) then you should enable the `dkms.service` Systemd service which automatically recompiles the kernel modules after a kernel update.

## 官方 VMware Tools

### 模块

*   `vmblock` - Filesystem driver. Enables drag & drop functionality between host and guest ([superseded](https://www.mail-archive.com/open-vm-tools-devel@lists.sourceforge.net/msg00213.html) by the `vmware-vmblock-fuse` utility).
*   `vmci` - High performance communication interface between host and guest.
*   `vmmon` - Virtual Machine Monitor.
*   `vmnet` - Networking driver.
*   `vsock` - VMCI sockets.

**Note:** There is no module for `vmware-vmblock-fuse`, and `vmblock` has been removed from the kernel unless you disable `fuse`. Instead, systemd services need to be `enabled` to allow these functions. See instructions below.

### 安装（从客户机）

安装依赖项：[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) (for building), [net-tools](https://www.archlinux.org/packages/?name=net-tools) (for `ifconfig`, used by the installer) and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (for kernel headers).

然后，为安装程序创建假的init目录:

```
# for x in {0..6}; do mkdir -p /etc/init.d/rc$x.d; done

```

挂载安装程序：

```
# mount /dev/cdrom /mnt

```

解压(例如解压到`/root`):

```
# tar xf /mnt/VMwareTools*.tar.gz -C /root

```

开始安装

```
# perl /root/vmware-tools-distrib/vmware-install.pl

```

您可以安全地忽略下列构建失败：

*   VMNEXT 3 virtual network card
*   "Warning: This script could not find mkinitrd or update-initramfs and cannot remake the initrd file!"
*   Fuse components not found on the system.

启用`vmware-vmblock-fuse`服务:

```
 # abs community/open-vm-tools
 # cp /var/abs/community/open-vm-tools/vmware-* /usr/lib/systemd/system
 # systemctl enable vmware-vmblock-fuse.service

```

重新启动虚拟机：

```
# systemctl reboot

```

登录并启动VMware Tools:

```
# /etc/init.d/rc6.d/K99vmware-tools start

```

**Tip:** 在GitHub中[[1]](https://github.com/rasa/vmware-tools-patches)能够自动处理这些。

## Xorg配置

**Note:** 在虚拟机中运行Xorg，必须有至少32MB的VGA内存

安装依赖项:[xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse)，[xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware)和[mesa](https://www.archlinux.org/packages/?name=mesa).

If booting into a `graphical target` you are almost done. `/etc/xdg/autostart/vmware-user.desktop` will get started which will setup most of the things needed to work with the Virtual Machine.

However, if booting into `multi-user.target` or using an uncommon setup (e.g. multiple monitors), then `vmtoolsd.service` needs to be [enabled](/index.php/Enable "Enable"). In addition to this, edit:

 `/etc/X11/Xwrapper.config`  `needs_root_rights=yes` 

to give permission for loading drivers.

## 提示与技巧

### 共享文件夹

**Note:** 这个功能只能在VMware Workstation/Fusion里使用

选择*虚拟机设置 > 选项 > 共享文件夹 > 总是启用*,并添加共享.来共享一个文件夹。

请确保`vmhgfs`驱动已加载：

```
# modprobe vmhgfs

```

You should be able to see the shared folders by running vmware-hgfsclient command:

```
$ vmware-hgfsclient

```

Now you can mount the folder:

```
# mkdir /home/user1/shares
# mount -n -t vmhgfs .host:/*<shared_folder>* /home/user1/shares

```

#### 在引导时启用

编辑`mkinitcpio.conf`就像这样:

 ` # cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmhgfs"
...
```

and then update your ramdisk:

```
# mkinitcpio -p linux

```

##### fstab

为每个共享添加规则：

 `/etc/fstab` 
```
.host:/*<shared_folder>* */home/user1/shares* vmhgfs defaults 0 0

```

创建并挂载共享文件夹：

```
# mkdir /home/user1/shares
# mount /home/user1/shares

```

##### Systemd

For shared folders to be working you need to have loaded the `vmhgfs` driver. Simply create the following `.service`s:

 `/etc/systemd/system/mnt-hgfs.mount` 
```
[Unit]
Description=Load VMware shared folders
ConditionPathExists=.host:/*<shared_folder>*
ConditionVirtualization=vmware

[Mount]
What=.host:/*<shared_folder>*
Where=*<shared folders root directory>*/*<shared_folder>*
Type=vmhgfs
Options=defaults,noatime

[Install]
WantedBy=multi-user.target
```
 `/etc/systemd/system/mnt-hgfs.automount` 
```
[Unit]
Description=Load VMware shared folders
ConditionPathExists=.host:/*<shared_folder>*
ConditionVirtualization=vmware

[Automount]
Where=*<shared folders root directory>*/*<shared_folder>*

[Install]
WantedBy=multi-user.target
```

Make sure the `*<shared folders root directory>*` folder exists on your system. If this folder does not exist then you have to create it as the systemd scripts depend on it:

```
# mkdir -p *<shared folders root directory>*

```

[Enable](/index.php/Enable "Enable") the `mnt-hgfs.automount` mount target.

If you want to mount all shared folders automatically then omit *<shared_folder>*.

#### Prune mlocate DB

When using [mlocate](/index.php/Mlocate "Mlocate"), it is useless to index the shared directories in the `locate DB`. Therefore, add the directories to `PRUNEPATHS` in `/etc/updatedb`.

### 3D加速

3D加速功能如果在创建客户机时没有选择, 可以勾选: *编辑虚拟机设置 > 硬件 > 显示器 > 加速3D图形*.

### 时间同步

Configuring time synchronization in a Virtual Machine is important; fluctuations are bound to occur more easily in a guest, compared to a physical host. This is mostly due to the CPU being shared by more than one guest.

There are 2 options to set up time synchronization: the host or an external source.

#### Host machine as time source

To use the host as a time source, ensure `vmtoolsd.service` is [started](/index.php/Start "Start"). Then enable the time synchronization:

```
# vmware-toolbox-cmd timesync enable

```

To synchronize the guest after suspending the host:

```
# hwclock --hctosys --localtime

```

#### External server as time source

See [NTP](/index.php/NTP "NTP").

### Performance Tips

You can try the followings tips to improve the performance of your virtual machine.

#### Paravirtual SCSI adapter

[VMware Paravirtual SCSI (PVSCSI) adapters](http://kb.vmware.com/kb/1010398) are high-performance storage adapters for VMware ESXi that can result in greater throughput and lower CPU utilization. PVSCSI adapters are best suited for environments, where hardware or applications drive a very high amount of I/O throughput.

The SCSI adapter type `VMware Paravirtual` is available in the Virtual Machine settings.

If you do not have these settings in your virtual machine configuration you can still use the paravirtual SCSI adapter like this: Make sure that the paravirtual SCSI adapter is included in your kernel image. For this you have to modify your `mkinitcpio.conf`

 ` cat /etc/mkinitcpio.conf` 
```
`...`
MODULES="`...` vmw_pvscsi"
`...`
```

Rebuild your ramdisk:

```
# mkinitcpio -p linux

```

Shutdown your virtual machine and change the SCSI adapter your `.vmx` to the following:

```
scsi0.virtualDev = "pvscsi"

```

#### Paravirtual Network Adapater

VMware offers [multiple network adapters](http://kb.vmware.com/kb/1001805) for the guest OS. The default adapter used is usually the `e1000` adapter, which emulates an Intel 82545EM Gigabit Ethernet NIC. This Intel adapter is generally compatible with the built-in drivers across most operating systems, include Arch.

For [much more performance and additional features](http://rickardnobel.se/vmxnet3-vs-e1000e-and-e1000-part-1/) (such as multiqueue support), the VMware native `vmxnet3` network adapter can be used.

Arch has the `vmxnet3` kernel module available with a default install. Once enabled in [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") (or if it is auto-detected, check by running `$ lsmod | grep vmxnet3` to see if it is loaded), shutdown and change the network adapter type in your *.vmx* file to the following:

```
ethernet0.virtualDev = "vmxnet3"

```

After changing network adapters, you will need to update your network and [dhcpcd](/index.php/Dhcpcd "Dhcpcd") settings to use the new adapter name and mac address.

```
# dhcpcd *new_interface_name*
# systemctl enable dhcpcd@*new_interface_name*.service

```

You can get the new interface name by running `ip link`

#### Virtual Machine Settings

These settings could help improve the responsiveness of your virtual machine:

```
mainMem.useNamedFile = "FALSE"
MemTrimRate = "0"
prefvmx.useRecommendedLockedMemSize = "TRUE"
MemAllowAutoScaleDown = "FALSE"
sched.mem.pshare.enable = "FALSE"

```

*   **mainMem.useNamedFile**: This will only work for Windows hosts and you can use this parameter if you experience high disk activity on shutting down the virtual machine. This will prevent VMware from creating a *.vmem* file. Use *mainmem.backing = "swap"* on Linux hosts instead.
*   **MemTrimRate**: This setting prevents that memory whichc was released by the guest is released on the host also.
*   **prefvmx.useRecommendedLockedMemSize**: Unfortunately there does not seem to exist a proper explanation for this setting. This setting seems to prevent the host system from swapping parts of the guest memory.
*   **MemAllowAutoScaleDown**: Prevents that VMware adjusts the memory size of the virtual machine in case it cannot allocate enough memory.
*   **sched.mem.pshare.enable**: If several virtual machines are running simultaneously VMware will try to locate identical pages and share these between the virtual machines. This can be very I/O intensive.

The following settings could also be set in the configuration dialog of VMware Workstation(*Edit -> Preferences... -> Memory/Priority*).

```
prefvmx.minVmMemPct = "100"
mainMem.partialLazySave = "FALSE"
mainMem.partialLazyRestore = "FALSE"

```

*   **prefvmx.minVmMemPct**: Sets amount of RAM in percent which should be reserved by the virtual machine on the host system. If you set this to a lower value it is possible to assign the virtual machine more memory than available in the host system. Be careful though in this case as this will most likely lead to excessive hard drive usage. If you have enough RAM then leave this value at 100.
*   **mainMem.partialLazySave** and **mainMem.partialLazyRestore**: These two parameters will prevent the virtual machine from creating partial snapshots for suspends. When you use these parameters and you suspend your virtual machine it will take a little bit longer, but there should be less hard disk activity from VMware trying to store this information.

## 疑难解答

### 鼠标问题

鼠标可能会发生这些问题：

*   The automatic grab/ungrab feature will not automatically grab input when cursor enters the window
*   输入延迟
*   Clicks are not registered in some applications
*   当光标进入/离开虚拟机时跳动
*   光标跳转到它离开VM客户机的地方

您可以尝试卸载[xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse)。[xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse)和[xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)足以处理鼠标与键盘输入。

您可以尝试添加这些设置到`.vmx`配置文件([光标跳转到它离开VM客户机的地方](https://forums.mageia.org/en/viewtopic.php?f=7&t=7977)):

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx` 
```
mouse.vusb.enable = "TRUE"
mouse.vusb.useBasicMouse = "FALSE"
usb.generic.allowHID = "TRUE"

VMware attempts to automatically optimize mouse for gaming. If experiencing problems, disabling it is recommended: *Edit > Preferences > Input > Optimize mouse for games: Never*
```

Alternatively, attempting to [disable](http://www.spinics.net/lists/xorg/msg53932.html) the `catchall` event in `10-evdev.conf` may be needed:

 `/etc/X11/xorg.conf.d/10-evdev.conf` 
```
#Section "InputClass"
#        Identifier "evdev pointer catchall"
#        MatchIsPointer "on"
#        MatchDevicePath "/dev/input/event*"
#        Driver "evdev"
#EndSection

```

#### 按钮丢失

If not by default, all mouse buttons should be working after adding `[mouse.vusb.useBasicMouse = "FALSE"](https://communities.vmware.com/thread/457313?start=15&tstart=0)` to the `.vmx`.

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx`  `mouse.vusb.useBasicMouse = "FALSE"` 

### Boot problems

#### Slow boot time

You may see the following errors if VMWare's memory hot-add feature is enabled.

*   add_memory failed
*   acpi_memory_enable_device() error

Disable the memory hot-add feature by setting `mem.hotadd = "FALSE"` to the `.vmx`.

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx`  `mem.hotadd = "FALSE"` 

#### Shutdown/Reboot hangs

Adjust the timeout for the vmtoolsd service (defaults to 90 seconds).

 `/etc/systemd/system/vmtoolsd.service.d/timeout.conf` 
```
[Service]
TimeoutStopSec=1
```

### Autofit problems

If VMWare is stretching instead of changing the resolution even with the system service enabled, you may need to add the modules to mkinitcpio.conf.

 `/etc/mkinitcpio.conf`  `MODULES="vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx"` 

Do not forget to run:

 `# mkinitcpio -p linux` 

### 拖拽，复制/粘贴

`/etc/xdg/autostart/vmware-user.desktop` may try to start *vmware-user-suid-wrapper* properly when you log in, but there is an unspecified relationship between it and *gtkmm* that causes it to silently fail. This is documented in [FS#43159](https://bugs.archlinux.org/task/43159).

### Problems when running as a shared VM on Workstation 11

Workstation 11 has a bug where vmware-hostd crashes if an Arch guest is running as a shared VM and vmtoolsd is running in the guest. A patch to open-vm-tools to work around the bug is [here](https://github.com/vmware/open-vm-tools/issues/31).

### Shared folder not mounted after system upgrade

This is probably only happens to [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). Since the vmhgfs module belongs to [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) which belongs to AUR repositiory, therefore would not get's updated automatically by the `pacman -Syu` command. Always update the [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) manually before the system upgrade.

If you happened to get in to this situation, you need to remove the automount for shared file system, upgrade and do a `mkinitcpio -p linux`.