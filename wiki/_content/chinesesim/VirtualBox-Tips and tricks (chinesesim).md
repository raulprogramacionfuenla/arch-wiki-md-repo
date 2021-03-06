See [VirtualBox](/index.php/VirtualBox "VirtualBox") for the main article.

## Contents

*   [1 VirtualBox虚拟机从其他虚拟机导入/导出的管理](#VirtualBox虚拟机从其他虚拟机导入/导出的管理)
    *   [1.1 添加删除](#添加删除)
    *   [1.2 使用正确的虚拟磁盘格式](#使用正确的虚拟磁盘格式)
        *   [1.2.1 自动工具](#自动工具)
        *   [1.2.2 手动转换](#手动转换)
    *   [1.3 创建虚拟机的配置为你的虚拟机管理程序](#创建虚拟机的配置为你的虚拟机管理程序)
*   [2 虚拟机管理启动](#虚拟机管理启动)
    *   [2.1 启动虚拟机服务](#启动虚拟机服务)
    *   [2.2 启动虚拟机键盘快捷键](#启动虚拟机键盘快捷键)
*   [3 在虚拟机中使用特定的设备](#在虚拟机中使用特定的设备)
    *   [3.1 使用 USB 摄像头 / 麦克风](#使用_USB_摄像头_/_麦克风)
        *   [3.1.1 侦测摄像头和其他USB设备](#侦测摄像头和其他USB设备)
    *   [3.2 访问guest 服务](#访问guest_服务)
    *   [3.3 在Windows客户端中激活D3D加速](#在Windows客户端中激活D3D加速)
    *   [3.4 在USB key上使用VirtualBox](#在USB_key上使用VirtualBox)
    *   [3.5 Run a native Arch Linux installation inside VirtualBox](#Run_a_native_Arch_Linux_installation_inside_VirtualBox)
        *   [3.5.1 Make sure you have a persistent naming scheme](#Make_sure_you_have_a_persistent_naming_scheme)
        *   [3.5.2 Make sure your mkinitcpio image is correct](#Make_sure_your_mkinitcpio_image_is_correct)
        *   [3.5.3 Create a VM configuration to boot from the physical drive](#Create_a_VM_configuration_to_boot_from_the_physical_drive)
            *   [3.5.3.1 创建一个原始只读磁盘的.vmdk映像](#创建一个原始只读磁盘的.vmdk映像)
            *   [3.5.3.2 创建虚拟机配置文件](#创建虚拟机配置文件)
    *   [3.6 安装VirtualBox的本地Arch Linux系统](#安装VirtualBox的本地Arch_Linux系统)
    *   [3.7 将本机Windows安装到虚拟机](#将本机Windows安装到虚拟机)
        *   [3.7.1 Tasks on Windows](#Tasks_on_Windows)
        *   [3.7.2 Using Disk2vhd to clone Windows partition](#Using_Disk2vhd_to_clone_Windows_partition)
        *   [3.7.3 Tasks on GNU/Linux](#Tasks_on_GNU/Linux)
        *   [3.7.4 修复MBR和Microsoft引导](#修复MBR和Microsoft引导)
        *   [3.7.5 已知的限制](#已知的限制)

## VirtualBox虚拟机从其他虚拟机导入/导出的管理

If you plan to use your virtual machine on another hypervisor or want to import in VirtualBox a virtual machine created with another hypervisor, you might be interested in reading the following steps.

### 添加删除

Guest additions are available in most hypervisor solutions: VirtualBox comes with the Guest Additions, VMware with the VMware Tools, Parallels with the Parallels Tools, etc. These additional components are designed to be installed inside a virtual machine after the guest operating system has been installed. They consist of device drivers and system applications that optimize the guest operating system for better performance and usability [by providing these features](https://www.virtualbox.org/manual/ch04.html).

If you have installed the additions to your virtual machine, please uninstall them first. Your guest, especially if it is using an OS from the Windows family, might behave weirdly, crash or even might not boot at all if you are still using the specific drivers in another hypervisor.

### 使用正确的虚拟磁盘格式

这一步将取决于虚拟磁盘映像直接或不能转换的能力。

#### 自动工具

Some companies provide tools which offer the ability to create virtual machines from a Windows or GNU/Linux operating system located either in a virtual machine or even in a native installation. With such a product, you do not need to apply this and the following steps and can stop reading here.

*   *[Parallels Transporter](http://www.parallels.com/products/transporter)* which is non free, is a product from Parallels Inc. This solution basically consists in an piece of software called *agent* that will be installed in the guest you want to import/convert. Then, Parallels Transporter, <u>which only works on OS X</u>, will create a virtual machine from that *agent* which is contacted either by USB or Ethernet network.
*   *[VMware vCenter Converter](https://www.vmware.com/products/converter/)* which is free upon registration on the VMware webiste, works nearly the same way as Parallels Transporter, but the piece of software that will gather the data to create the virtual machine only works on a Windows platform.

#### 手动转换

First, familiarize yourself with the [#Formats supported by VirtualBox](#Formats_supported_by_VirtualBox) and [those supported by third-party hypervisors](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines").

*   Importing or exporting a virtual machine from/to a VMware solution is not a problem at all if you use the VMDK or OVF disk format, otherwise converting [#VMDK to VDI and VDI to VMDK](#VMDK_to_VDI_and_VDI_to_VMDK) is possible and the aforementioned VMware vCenter Converter tool is available.

*   Importing or exporting from/to QEMU is not a problem neither: some QEMU formats are supported directly by VirtualBox and conversion between [#QCOW2 to VDI and VDI to QCOW2](#QCOW2_to_VDI_and_VDI_to_QCOW2) is still available if needed.

*   Importing or exporting from/to Parallels hypervisor is the hardest way: Parallels does only support its own HDD format (even the standard and portable OVF format is not supported!).

*   To export your virtual machine to Parallels, you will need to use the Parallels Transporter tool described above.
*   To import your virtual machine to VirtualBox, you will need to use the VMware vCenter Converter described above to convert the VM to the VMware format first. Then, apply the solution to migrate from VMware.

### 创建虚拟机的配置为你的虚拟机管理程序

Each hypervisor have their own virtual machine configuration file: `.vbox` for VirtualBox, `.vmx` for VMware, a `config.pvs` file located in the virtual machine bundle (`.pvm` file), etc. You will have thus to recreate a new virtual machine in your new destination hypervisor and specify its hardware configuration as close as possible as your initial virtual machine.

Pay a close attention to the firmware interface (BIOS or UEFI) used to install the guest operating system. While an option is available to choose between these 2 interfaces on VirtualBox and on Parallels solutions, on VMware, you will have to add manually the following line to your *.vmx* file.

 `ArchLinux_vm.vmx`  `firmware = "efi"` 

Finally, ask your hypervisor to use the existing virtual disk you have converted and launch the virtual machine.

**Tip:**

*   On VirtualBox, if you do not want to browse the whole GUI to find the right location to add your new virtual drive device, you can [#Replace a virtual disk manually from the .vbox file](#Replace_a_virtual_disk_manually_from_the_.vbox_file), or use the `VBoxManage storageattach` described in [#Increase virtual disks](#Increase_virtual_disks) or in the [VirtualBox manual page](https://www.virtualbox.org/manual/ch08.html#vboxmanage-storageattach).
*   Similarly, in VMware products, you can replace the location of the current virtual disk location by adapting the *.vmdk* file location in your *.vmx* configuration file.

## 虚拟机管理启动

### 启动虚拟机服务

此后查找将用于考虑虚拟机作为服务systemd服务的实现。

 `/etc/systemd/system/vboxvmservice@.service` 
```
[Unit]
Description=VBox Virtual Machine %i Service
Requires=systemd-modules-load.service
After=systemd-modules-load.service

[Service]
User=*username*
Group=vboxusers
ExecStart=/usr/bin/VBoxHeadless -s %i
ExecStop=/usr/bin/VBoxManage controlvm %i savestate

[Install]
WantedBy=multi-user.target
```

**Note:** Replace `*username*` with a user that is a member of the `vboxusers` group. Make sure the user chosen is the same user that will create/import virtual machines, otherwise the user will not see the VM appliances.

**Note:** If you have multiple virtual machines managed by Systemd and they are not stopping properly, try to add `RemainAfterExit=true` and `KillMode=none` at the end of `[Service]` section.

To enable the service that will launch the virtual machine at next boot, use:

```
# systemctl enable vboxvmservice@*your_virtual_machine_name*

```

To start the service that will launch directly the virtual machine, use:

```
# systemctl start vboxvmservice@*your_virtual_machine_name*

```

VirtualBox 4.2 introduces [a new way](http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/) for UNIX-like systems to have virtual machines started automatically, other than using a systemd service.

### 启动虚拟机键盘快捷键

It can be useful to start virtual machines directly with a keyboard shortcut instead of using the VirtualBox interface (GUI or CLI). For that, you can simply define key bindings in `.xbindkeysrc`. Please refer to [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") for more details.

Example, using the `Fn` key of a laptop with an unused battery key (`F3` on the computer used in this example):

```
"VBoxManage startvm 'Windows 7'"
m:0x0 + c:244
XF86Battery

```

**Note:** If you have a space in the name of your virtual machine, then enclose it with single apostrophes like made in the example just above.

## 在虚拟机中使用特定的设备

### 使用 USB 摄像头 / 麦克风

**Note:** 在遵照下列步骤前，你需要安装 VirtualBox 扩展包。详见 [VirtualBox Extras#Extension pack](/index.php/VirtualBox_Extras#Extension_pack "VirtualBox Extras")。

1.  要确保没有在运行虚拟机，以及没有使用摄像头 / 麦克风。
2.  进入VirtualBox主界面并打开Arch系统的设置界面，到USB设备页。
3.  要确保勾选上“启用USB控制器”选项。 还要确保选择“启用USB 2.0(EHCI)控制器”选项。
4.  点击“从设备列表中添加筛选器”按钮 (就是那个有“+”图标的连接线).
5.  从列表中选择你的USB摄像头 / 麦克风设备。
6.  然后再点击OK，启动你的VM

**Note:** If your Microphone does not show up in the "Add filter from device" menu, try the USB 3.0 and 1.1 options instead (In Step 3).

#### 侦测摄像头和其他USB设备

**Note:** This will not do much if you are running a *NIX OS inside of your VM, as most do not have autodetection features.

If the device that you are looking for does not show up on any of the menus in the section above and you have tried all three USB controller options,

boot up your VM three seperate times. Once using the USB 1.1 controller, another using the USB 2.0 controller, etc. Leave the VM running for at least 5 minutes after startup. Sometimes Windows will autodetect the device for you. Be sure you filter any devices that are not a keyboard or a mouse so they do not start up at boot. This ensures that Windows will detect the device at start-up.

### 访问guest 服务

To access [Apache server](https://en.wikipedia.org/wiki/Apache_HTTP_Server "wikipedia:Apache HTTP Server") on a Virtual Machine from the host machine **only**, simply execute the following lines on the host:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/HostPort" *8888*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/GuestPort" *80*
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/*pcnet*/0/LUN#0/Config/Apache/Protocol" TCP

```

Where 8888 is the port the host should listen on and 80 is the port the VM will send Apache's signal on.

To use a port lower than 1024 on the host machine, changes need to be made to the firewall on that host machine. This can also be set up to work with SSH or any other services by changing "Apache" to the corresponding service and ports.

**Note:** `pcnet` refers to the network card of the VM. If you use an Intel card in your VM settings, change `pcnet` to `e1000`.

To communicate between the VirtualBox guest and host using ssh, the server port must be forwarded under Settings > Network. When connecting from the client/host, connect to the IP address of the client/host machine, as opposed to the connection of the other machine. This is because the connection will be made over a virtual adapter.

### 在Windows客户端中激活D3D加速

Recent versions of Virtualbox have support for accelerating OpenGL inside guests. This can be enabled with a simple checkbox in the machine's settings, right below where video ram is set, and installing the Virtualbox guest additions. However, most Windows games use Direct3D (part of DirectX), not OpenGL, and are thus not helped by this method. However, it is possible to gain accelerated Direct3D in your Windows guests by borrowing the d3d libraries from Wine, which translate d3d calls into OpenGL, which is then accelerated. These libraries are now part of Virtualbox guest additions software.

After enabling OpenGL acceleration as described above, reboot the guest into safe mode (press F8 before the Windows screen appears but after the Virtualbox screen disappears), and install Virtualbox guest additions, during install enable checkbox "Direct3D support". Reboot back to normal mode and you should have accelerated Direct3D.

**Note:** This hack may or may not work for some games depending on what hardware checks they make and what parts of D3D they use.

**Note:** This was tested on Windows XP, 7 and 8.1\. If method does not work on your Windows version please add data here.

### 在USB key上使用VirtualBox

When using VirtualBox on a USB key, for example to start an installed machine with an ISO image, you will manually have to create VDMKs from the existing drives. However, once the new VMDKs are saved and you move on to another machine, you may experience problems launching an appropriate machine again. To get rid of this issue, you can use the following script to launch VirtualBox. This script will clean up and unregister old VMDK files and it will create new, proper VMDKs for you:

```
#!/bin/bash

# Erase old VMDK entries
rm ~/.VirtualBox/*.vmdk

# Clean up VBox-Registry
sed -i '/sd/d' ~/.VirtualBox/VirtualBox.xml

# Remove old harddisks from existing machines
find ~/.VirtualBox/Machines -name \*.xml | while read file; do
  line=`grep -e "type\=\"HardDisk\"" -n $file | cut -d ':' -f 1`
  if [ -n "$line" ]; then
    sed -i ${line}d $file
    sed -i ${line}d $file
    sed -i ${line}d $file
  fi
  sed -i "/rg/d" $file
done

# Delete prev-files created by VirtualBox
find  ~/.VirtualBox/Machines -name \*-prev -exec rm '{}' \;

# Recreate VMDKs
ls -l /dev/disk/by-uuid | cut -d ' ' -f 9,11 | while read ln; do
  if [ -n "$ln" ]; then
    uuid=`echo "$ln" | cut -d ' ' -f 1`
    device=`echo "$ln" | cut -d ' ' -f 2 | cut -d '/' -f 3 | cut -b 1-3`

    # determine whether drive is mounted already
    checkstr1=`mount | grep $uuid`
    checkstr2=`mount | grep $device`
    checkstr3=`ls ~/.VirtualBox/*.vmdk | grep $device`
    if [[ -z "$checkstr1" && -z "$checkstr2" && -z "$checkstr3" ]]; then
      VBoxManage internalcommands createrawvmdk -filename ~/.VirtualBox/$device.vmdk -rawdisk /dev/$device -register
    fi
  fi
done

# Start VirtualBox
VirtualBox

```

Note that your user has to be added to the "disk" group to create VMDKs out of existing drives.

### Run a native Arch Linux installation inside VirtualBox

If you have a dual boot system between Arch Linux and another operating system, it can become rapidly tedious to switch back and forth if you need to work in both. Also, by using virtual machines, you just have a tiny fragment of your computer power, which can cause issues when working on projects requiring performance.

This guide will let you reuse, in a virtual machine, your native Arch Linux installation when you are running your second operating system. This way, you keep the ability to run each operating system natively, but have the option to run your Arch Linux installation inside a virtual machine.

#### Make sure you have a persistent naming scheme

Depending on your hard drive setup, device files representing your hard drives may appear differently when you will run your Arch Linux installation natively or in virtual machine. This problem occurs when using [FakeRAID](/index.php/RAID#Implementation "RAID") for example. The fake RAID device will be mapped in `/dev/mapper/` when you run your GNU/Linux distribution natively, while the devices are still accessible separately. However, in your virtual machine, it can appear without any mapping in `/dev/sdaX` for example, because the drivers controlling the fake RAID in your host operating system (e.g. Windows) are abstracting the fake RAID device.

To circumvent this problem, we will need to use an addressing scheme that is persistent to both systems. This can be achieved using [UUIDs](/index.php/Fstab#UUIDs "Fstab"). Make sure your [boot loader](/index.php/Boot_loader "Boot loader") and [fstab](/index.php/Fstab "Fstab") file is using UUIDs, otherwise fix this issue. Read [fstab](/index.php/Fstab "Fstab") and [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

**Warning:**

*   Make sure your host partition is only accessible in read only from your Arch Linux virtual machine, this will avoid risk of corruptions if you were to corrupt that host partition by writing on it due to lack of attention.
*   You should NEVER allow VirtualBox to boot from the entry of your second operating system, which, as a reminder, is used as the host for this virtual machine! Take thus a special care especially if your default boot loader/boot manager entry is your other operating system. Give a more important timeout or put it below in the order of preferences.

#### Make sure your mkinitcpio image is correct

Make sure your [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") configuration uses the [HOOK](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") `block`:

 `/etc/mkinitcpio.conf` 
```
[...]
HOOKS="base udev autodetect modconf *block* filesystems keyboard fsck"
[...]
```

If it is not present, add it and [regenerate your initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio"):

```
# mkinitcpio -p linux

```

#### Create a VM configuration to boot from the physical drive

##### 创建一个原始只读磁盘的.vmdk映像

Now, we need to create a new virtual machine which will use a [RAW disk](https://www.virtualbox.org/manual/ch09.html#rawdisk) as virtual drive, for that we will use a ~ 1Kio VMDK file which will be mapped to a physical disk. Unfortunately, VirtualBox does not have this option in the GUI, so we will have to use the console and use an internal command of `VBoxManage`.

Boot the host which will use the Arch Linux virtual machine. The command will need to be adapted according to the host you have.

	On a GNU/Linux host

There is 3 ways to achieve this: login as root, changing the access right of the device with `chmod`, adding your user to the `disk` group. The latter way is the more elegant, let us proceed that way:

```
# gpasswd -a *your_user* disk

```

Apply the new group settings with:

```
$ newgrp

```

Now, you can use the command:

```
$ VBoxManage internalcommands createrawvmdk -filename */path/to/file.vmdk* -rawdisk */dev/sdb* -register 

```

Adapt the above command to your need, especially the path and filename of the VMDK location and the raw disk location to map which contain your Arch Linux installation.

	On a Windows host

Open a command prompt must be run as administrator.
**Tip:** On Windows, open your start menu/start screen, type `cmd`, and type `Ctrl+Shift+Enter`, this is a shortcut to execute the selected program with admin rights.
On Windows, as the disk filename convention is different from UNIX, use this command to determine what drives you have in your Windows system and their location: `# wmic diskdrive get name,size,model` 
```
Model                               Name                Size
WDC WD40EZRX-00SPEB0 ATA Device     \\.\PHYSICALDRIVE1  4000783933440
KINGSTON SVP100S296G ATA Device     \\.\PHYSICALDRIVE0  96024821760
Hitachi HDT721010SLA360 ATA Device  \\.\PHYSICALDRIVE2  1000202273280
Innostor Ext. HDD USB Device        \\.\PHYSICALDRIVE3  1000202273280
```

In this example, as the Windows convention is `\\.\PhysicalDriveX` where X is a number from 0, `\\.\PHYSICALDRIVE1` could be analogous to `/dev/sdb` from the Linux disk terminology.

To use the `VBoxManage` command on Windows, you can either, change the current directory to your VirtualBox installation folder first with `cd C:\Program Files\Oracle\VirtualBox\`

```
# .\VBoxManage.exe internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

or use the absolute path name:

```
# "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

	On another OS host

There are other limitations regarding the aforementioned command when used in other operating systems like OS X, please thus [read carefully the manual page](https://www.virtualbox.org/manual/ch09.html#rawdisk), if you are concerned.

##### 创建虚拟机配置文件

**Note:**

*   To make use of the VBoxManage command on Windows, you need to change the current directory to your VirtualBox installation folder first: cd C:\Program Files\Oracle\VirtualBox\.
*   Windows makes use of backslashes instead of slashes, please replace all slashes / occurrences by backslashes \ in the commands that follow when you will use them.

After, we need to create a new machine (replace the *VM_name* to your convenience) and register it with VirtualBox.

```
$ VBoxManage createvm -name *VM_name* -register

```

Then, the newly raw disk needs to be attached to the machine. This will depend if your computer or actually the root of your native Arch Linux installation is on an IDE or a SATA controller.

If you need an IDE controller:

```
$ VBoxManage storagectl *VM_name* --name "IDE Controller" --add ide
$ VBoxManage storageattach *VM_name* --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

otherwise:

```
$ VBoxManage storagectl *VM_name* --name "SATA Controller" --add sata
$ VBoxManage storageattach *VM_name* --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

While you continue using the CLI, it is recommended to use the VirtualBox GUI, to personalise the virtual machine configuration. Indeed, you must specify its hardware configuration as close as possible as your native machine: turning on the 3D acceleration, increasing video memory, setting the network interface, etc.

Finally, you may want to seamlessly integrate your Arch Linux with your host operating system and allow copy pasting between both OSes. Please refer to [#Install the Guest Additions](#Install_the_Guest_Additions) for that, since this Arch Linux virtual machine is basically an Arch Linux guest.

**Warning:** For [Xorg](/index.php/Xorg "Xorg") to work in natively and in the virtual machine, since obviously it will be using different drivers, it is best if there is no `/etc/X11/xorg.conf`, so Xorg will pick up everything it needs on the fly. However, if you really do need your own Xorg configuration, maybe is it worth to set your default systemd target to `multi-user.target` with `systemctl isolate graphical.target` as root (more details at [Systemd#Targets table](/index.php/Systemd#Targets_table "Systemd") and [Systemd#Change current target](/index.php/Systemd#Change_current_target "Systemd")). In that way, the graphical interface is disabled (i.e. Xorg is not launched) and after you logged in, you can `startx`} manually with a custom `xorg.conf`.

### 安装VirtualBox的本地Arch Linux系统

In some cases it may be useful to install a native Arch Linux system while running another operating system: one way to accomplish this is to perform the installation through VirtualBox on a [raw disk](http://www.virtualbox.org/manual/ch09.html#rawdisk). If the existing operating system is Linux based, you may want to consider following [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") instead.

This scenario is very similar to [#Run a native Arch Linux installation inside VirtualBox](#Run_a_native_Arch_Linux_installation_inside_VirtualBox), but will follow those steps in a different order: start by [#Create a raw disk .vmdk image](#Create_a_raw_disk_.vmdk_image), then [#Create the VM configuration file](#Create_the_VM_configuration_file).

Now, you should have a working VM configuration whose virtual VMDK disk is tied to a real disk. The installation process is exactly the same as the steps described in [#Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests), but [#Make sure you have a persistent naming scheme](#Make_sure_you_have_a_persistent_naming_scheme) and [#Make sure your mkinitcpio image is correct](#Make_sure_your_mkinitcpio_image_is_correct).

**Warning:**

*   For BIOS systems and MBR disks, do not install a bootloader inside your virtual machine, this will not work since the MBR is not linked to the MBR of your real machine and your virtual disk is only mapped to a real partition without the MBR.
*   For UEFI systems without [CSM](https://en.wikipedia.org/wiki/Compatibility_Support_Module#CSM "wikipedia:Compatibility Support Module") and GPT disks, the installation will not work at all since:

*   the [ESP](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition") partition is not mapped to your virtual disk and Arch Linux requires to have the Linux kernel on it to boot as an EFI application (see [EFISTUB](/index.php/EFISTUB "EFISTUB") for details);
*   and the efivars, if you are installing Arch Linux using the EFI mode brought by VirtualBox, are not the one of your real system: the bootmanager entries will hence not be registered.

*   This is why, it is recommended to create your partitions in a native installation first, otherwize the partitions will not be taken into consideration in your MBR/GPT partition table.

After completing the installation, boot your computer natively with an GNU/Linux installation media (whether it be Arch Linux or not), [chroot](/index.php/Beginner%27s_Guide#Chroot_and_configure_the_base_system "Beginner's Guide") into your installed Arch Linux installation and [#Install and configure a bootloader](/index.php/Beginner%27s_Guide#Install_and_configure_a_bootloader "Beginner's Guide").

### 将本机Windows安装到虚拟机

If you want to migrate an existing native Windows installation to a virtual machine which will be used with VirtualBox on GNU/Linux, this use case is for you. This section only covers native Windows installation using the MSDOS/Intel partition scheme. Your Windows installation must reside on the first MBR partition for this operation to success. Operation for other partitions are available but have been untested (see [#Known limitations](#Known_limitations) for details).

**Warning:** If you are using an OEM version of Windows, this process is unauthorized by the end user license license. Indeed, the OEM license typically states the Windows install is tied with the hardware together. Transferring a Windows install to a virtual machine removes this link. Make thus sure you have a full Windows install or a volume license model before continuing. If you have a full Windows license but the latter is not coming in volume, nor as a special license for several PCs, this means you will have to remove the native installation after the transfer operation has been achieved.

A couple of tasks are required to be done inside your native Windows installation first, then on your GNU/Linux host.

#### Tasks on Windows

The first three following points comes from [this outdated VirtualBox wiki page](https://www.virtualbox.org/wiki/Migrate_Windows#HAL), but are updated here.

*   Remove IDE/ATA controllers checks (Windows XP only): Windows memorize the IDE/ATA drive controllers it has been installed on and will not boot if it detects these have changed. The solution proposed by Microsoft is to reuse the same controller or use one of the same serial, which is impossible to achieve since we are using a Virtual Machine. [MergeIDE](https://www.virtualbox.org/wiki/Migrate_Windows#HardDiskSupport), a German tool, developped upon another other solution proposed by Microsoft can be used. That solution basically consists in taking all IDE/ATA controller drivers supported by Windows XP from the initial driver archive (the location is hard coded, or specify it as the first argument to the `.bat` script), installing them and registering them with the regedit database.

*   Use the right type of Hardware Abstraction Layer (old 32 bits Windows versions): Microsoft ships 3 default versions: `Hal.dll` (Standard PC), `Halacpi.dll` (ACPI HAL) and `Halaacpi.dll` (ACPI HAL with IO APIC). Your Windows install could come installed with the first or the second version. In that way, please [disable the *Enable IO/APIC* VirtualBox extended feature](https://www.virtualbox.org/manual/ch08.html#idp56927888).

*   Disable any AGP device driver (only outdated Windows versions): If you have the files `agp440.sys` or `intelppm.sys` inside the `C:\Windows\SYSTEM32\drivers\` directory, remove it. As VirtualBox uses a PCI virtual graphic card, this can cause problems when this AGP driver is used.

*   Create a Windows recovery disk: In the following steps, if things turn bad, you will need to repair your Windows installation. Make sure you have an install media at hand, or create one with *Create a recovery disk* from Vista SP1, *Create a system repair disc* on Windows 7 or *Create a recovery drive* on Windows 8.x).

#### Using Disk2vhd to clone Windows partition

Boot into Windows, clean up the installation (with [CCleaner](http://www.piriform.com/ccleaner) for example), use [disk2vhd](https://technet.microsoft.com/en-us/library/ee656415.aspx) tool to create a VHD image. Include a reserved system partition (if present) and the actual Windows partition (usually disk C:). The size of Disk2vhd-created image will be the sum of the actual files on the partition (used space), not the size of a whole partition. If all goes well, the image should just boot in a VM and you will not have to go through the hassle with MBR and Windows bootloader, as in the case of cloning an entire partition.

#### Tasks on GNU/Linux

**Tip:** Skip the partition-related parts if you created VHD image with [Disk2vhd](#Using_Disk2vhd_to_clone_Windows_partition).

*   Reduce the native Windows partition size to the size Windows actually needs with `ntfsresize` available from [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). The size you will specify will be the same size of the VDI that will be created in the next step. If this size is too low, you may break your Windows install and the latter might not boot at all.

	Use the `--no-action` option first to run a test:

	 `# ntfsresize --no-action --size *52Gi* */dev/sda1*` 

	If only the previous test succeeded, execute this command again, but this time without the aforementioned test flag.

*   Install VirtualBox on your GNU/Linux host (see [#Installation steps for Arch Linux hosts](#Installation_steps_for_Arch_Linux_hosts) if your host is Arch Linux).

*   Create the Windows disk image from the beginning of the drive to the end of the first partition where is located your Windows installation. Copying from the beginning of the disk is necessary because the MBR space at the beginning of the drive needs to be on the virtual drive along with the Windows partition. In this example two following partitions `sda2` and `sda3`will be later removed from the partition table and the MBR bootloader will be updated.

	 `# sectnum=$(( $(cat /sys/block/''sda/sda1''/start) + $(cat /sys/block/''sda/sda1''/size) ))` 

	Using `cat /sys/block/*sda/sda1*/size` will output the number of total sectors of the first partition of the disk `sda`. Adapt where necessary.

	 `# dd if=''/dev/sda'' bs=512 count=$sectnum | VBoxManage convertfromraw stdin ''windows.vdi'' $(( $sectnum * 512 ))` 

	We need to display the size in byte, `$(( $sectnum * 512 ))` will convert the sector numbers to bytes.

*   Since you created your disk image as root, set the right ownership to the virtual disk image: `# chown *your_user*:*your_group* windows.vdi` 

*   Create your virtual machine configuration file and use the virtual disk created previously as the main virtual hard disk.

*   Try to boot your Windows VM, it may just work. First though remove and repair disks from the boot process as it may interfere (and likely will) booting into safe-mode.

*   Attempt to boot your Windows virtual machine in safe mode (press the F8 key before the Windows logo shows up)... if running into boot issues, read [#Fix MBR and Microsoft bootloader](#Fix_MBR_and_Microsoft_bootloader). In safe-mode, drivers will be installed likely by the Windows plug-and-play detection mechanism [view](http://i.imgur.com/hh1RrSp.png). Additionally, install the VirtualBox Guest Additions via the menu *Devices* > *Insert Guest Additions CD image...*. If a new disk dialog does not appear, navigate to the CD drive and start the installer manually.

*   You should finally have a working Windows virtual machine. Do not forget to read the [#Known limitations](#Known_limitations).

*   Performance tip: according to [VirtualBox manual](http://www.virtualbox.org/manual/ch05.html#harddiskcontrollers), SATA controller has a better performance than IDE. If you cannot boot Windows off virtual SATA controller right away, it is probably due to the lack of SATA drivers. Attach virtual disk to IDE controller, create an empty SATA controller and boot the VM - Windows should automatically install SATA drivers for the controller. You can then shutdown VM, detach virtual disk from IDE controller and attach it to SATA controller instead.

#### 修复MBR和Microsoft引导

如果您的Windows虚拟机拒绝引导, 你可能需要修复你的虚拟机.

*   Boot a GNU/Live live distribution inside your virtual machine before Windows starts up.

*   Remove other partitions entries from the virtual disk MBR. Indeed, since we copied the MBR and only the Windows partition, the entries of the other partitions are still present in the MBR, but the partitions are not available anymore. Use `fdisk` to achieve this for example.

```
fdisk ''/dev/sda''
Command (m for help): a
Partition number (''1-3'', default ''3''): ''1''
```

*   Write the updated partition table to the disk (this will recreate the MBR) using the `m` command inside `fdisk`.

*   Use [testdisk](https://www.archlinux.org/packages/?name=testdisk) (see [here](http://www.cgsecurity.org/index.html?testdisk.html) for details) to add a generic MBR:

	 `# testdisk > *Disk /dev/sda...'* > [Proceed] >  [Intel] Intel/PC partition > [MBR Code] Write TestDisk MBR to first sector > Write a new copy of MBR code to first sector? (Y/n) > Y > Write a new copy of MBR code, confirm? (Y/N) > A new copy of MBR code has been written. You have to reboot for the change to take effect. > [OK]` 

*   With the new MBR and updated partition table, your Windows virtual machine should be able to boot. If you are still encountering issues, boot your Windows recovery disk from on of the previous step, and inside your Windows RE environment, execute the commands [described here](http://support.microsoft.com/kb/927392).

#### 已知的限制

*   Your virtual machine can sometimes hang and overrun your RAM, this can be caused by conflicting drivers still installed inside your Windows virtual machine. Good luck to find them!
*   Additional software expecting a given driver beneath may either not be disabled/uninstalled or needs to be uninstalled first as the drivers that are no longer available.
*   Your Windows installation must reside on the first partition for the above process to work. If this requirement is not met, the process might be achieved too, but this had not been tested. This will require either copying the MBR and editing in hexadecimal see [VirtualBox: booting cloned disk](http://superuser.com/questions/237782/virtualbox-booting-cloned-disk/253417#253417) or will require to fix the partition table [manually](http://gparted.org/h2-fix-msdos-pt.php) or by repairing Windows with the recovery disk you created in a previous step. Let us consider our Windows installation on the second partition; we will copy the MBR, then the second partition where to the disk image. `VBoxManage convertfromraw` needs the total number of bytes that will be written: calculated thanks to the size of the MBR (the start of the first partition) plus the size of the second (Windows) partition. `{ dd if=/dev/sda bs=512 count=$(cat /sys/block/sda/sda1/start) ; dd if=/dev/sda2 bs=512 count=$(cat /sys/block/sda/sda2/size) ; } | VBoxManage convertfromraw stdin windows.vdi $(( ($(cat /sys/block/sda/sda1/start) + $(cat /sys/block/sda/sda2/size)) * 512 ))`.