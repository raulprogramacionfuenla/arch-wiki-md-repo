Related articles

*   [fstab (简体中文)](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")
*   [udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")
*   [LVM (简体中文)](/index.php/LVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LVM (简体中文)")

**翻译状态：** 本文是英文页面 [Persistent_block_device_naming](/index.php/Persistent_block_device_naming "Persistent block device naming") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-31，点击[这里](https://wiki.archlinux.org/index.php?title=Persistent_block_device_naming&diff=0&oldid=423674)可以查看翻译后英文页面的改动。

本文讲述如何为你的块设备提供持久化命名。udev的导入使之成为可能，也使之优于基于总线的命名法。如果你的机器上有不止一个 SATA, SCSI 或 IDE 磁盘控制器，那么它们所对应的设备节点将会依随机次序添加。这样就可能导致每次引导时设备的名字如 `/dev/**sda**` 与 `/dev/**sdb**` 互换了，最终导致系统不可引导、kernel panic、或者设备不可见。持久化命名法可以解决这些问题。

**注意:**

*   持久设备名有一些超出本文范围的限制，比如虽然 [mkinitcpio](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)") 支持某个方法，但 systemd 会对支持的设备名添加额外的限制(例如 [FS#42884](https://bugs.archlinux.org/task/42884))。
*   如果你使用 [LVM2](/index.php/LVM2 "LVM2")，本文将不适用。因为 LVM 自动处理这一问题。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 持久化命名的方法](#持久化命名的方法)
    *   [1.1 by-label](#by-label)
    *   [1.2 by-uuid](#by-uuid)
    *   [1.3 by-id 和 by-path](#by-id_和_by-path)
    *   [1.4 by-partlabel](#by-partlabel)
    *   [1.5 by-partuuid](#by-partuuid)
    *   [1.6 使用 Udev 静态设备名](#使用_Udev_静态设备名)
*   [2 使用持久名称](#使用持久名称)
    *   [2.1 fstab](#fstab)
    *   [2.2 引导管理器](#引导管理器)

## 持久化命名的方法

有四种持久化命名方案：[by-label](#by-label)、[by-uuid](#by-uuid)、[by-id 和 by-path](#by-id_和_by-path)。对于那些使用[GUID 分区表(GPT)](/index.php/GUID_Partition_Table "GUID Partition Table")的磁盘，还有额外的两种方案，[by-partlabel](#by-partlabel) 和 [by-partuuid](#by-partuuid)。你也可以[使用 Udev 静态设备名](#使用_Udev_静态设备名)方案。

下面讲解各种命名方案及其用法。

`lsblk -f` 命令用于以图示方式查看第一种方案：

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL  UUID                                 MOUNTPOINT
sda                                                       
├─sda1 vfat          CBB6-24F2                            /boot
├─sda2 ext4   SYSTEM 0a3407de-014b-458b-b5c1-848e92a327a3 /
├─sda3 ext4   DATA   b411dc99-f0a0-4c87-9e05-184977be8539 /home
└─sda4 swap          f9fe0b69-a280-415d-a03a-a32752370dee [SWAP]

```

[GPT 分区表](/index.php/GUID_Partition_Table "GUID Partition Table")的系统应改用 `blkid` 命令，这个命令更方便脚本使用但可读性低。

 `$ blkid` 
```
/dev/sda1: UUID="CBB6-24F2" TYPE="vfat" PARTLABEL="EFI SYSTEM PARTITION" PARTUUID="d0d0d110-0a71-4ed6-936a-304969ea36af" 
/dev/sda2: LABEL="SYSTEM" UUID="0a3407de-014b-458b-b5c1-848e92a327a3" TYPE="ext4" PARTLABEL="GNU/LINUX" PARTUUID="98a81274-10f7-40db-872a-03df048df366" 
/dev/sda3: LABEL="DATA" UUID="b411dc99-f0a0-4c87-9e05-184977be8539" TYPE="ext4" PARTLABEL="HOME" PARTUUID="7280201c-fc5d-40f2-a9b2-466611d3d49e" 
/dev/sda4: UUID="f9fe0b69-a280-415d-a03a-a32752370dee" TYPE="swap" PARTLABEL="SWAP" PARTUUID="039b6c1c-7553-4455-9537-1befbc9fbc5b"

```

### by-label

几乎每一个文件系统都可以有一个标签。所有有标签的分区都在 `/dev/disk/by-label` 目录中列出。这个目录随着分区标签的变动而被动态地创建和销毁。

 `$ ls -l /dev/disk/by-label` 
```

total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 DATA -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 SYSTEM -> ../../sda2

```

可以修改文件系统的标签。下面列出常见文件系统标签的修改方法：

	swap 

	`swaplabel -L <label> /dev/XXX` 用 [util-linux](https://www.archlinux.org/packages/?name=util-linux)

	ext2/3/4 

	`e2label /dev/XXX <label>` 用 [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

	btrfs 

	`btrfs filesystem label /dev/XXX <label>` 用 [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

	reiserfs 

	`reiserfstune -l <label> /dev/XXX` 用 [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

	jfs 

	`jfs_tune -L <label> /dev/XXX` 用 [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

	xfs 

	`xfs_admin -L <label> /dev/XXX` 用 [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

	fat/vfat 

	`dosfslabel /dev/XXX <label>` 用 [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

	fat/vfat 

	`mlabel -i /dev/XXX ::<label>` 用 [mtools](https://www.archlinux.org/packages/?name=mtools)

	ntfs 

	`ntfslabel /dev/XXX <label>` 用 [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

	zfs 

	这个文件系统不支持 `/dev/disk/by-label`, 但可以使用 [#by-partlabel](#by-partlabel)

**注意:**

*   Changing the filesystem label of the root partition has to be done from a "live" GNU/Linux distribution because the partition needs to be unmounted first.
*   标签必须是唯一的，以防止可能的冲突。
*   标签最多可以有16个字符。
*   标签是文件系统的一个属性，所以无法持久地表示单一磁盘阵列设备。

### by-uuid

[UUID](https://en.wikipedia.org/wiki/UUID "wikipedia:UUID") is a mechanism to give each filesystem a unique identifier. These identifiers are generated by filesystem utilities (e.g. `mkfs.*`) when the partition gets formatted and are designed so that collisions are unlikely. All GNU/Linux filesystems (including swap and LUKS headers of raw encrypted devices) support UUID. FAT and NTFS filesystems (*fat* and *windows* labels above) do not support UUID, but are still listed in `/dev/disk/by-uuid` with a shorter UID (unique identifier):

 `$ ls -l /dev/disk/by-uuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 0a3407de-014b-458b-b5c1-848e92a327a3 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 b411dc99-f0a0-4c87-9e05-184977be8539 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 CBB6-24F2 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 f9fe0b69-a280-415d-a03a-a32752370dee -> ../../sda4

```

The advantage of using the UUID method is that it is much less likely that name collisions occur than with labels. Further, it is generated automatically on creation of the filesystem. It will, for example, stay unique even if the device is plugged into another system (which may perhaps have a device with the same label).

The disadvantage is that UUIDs make long code lines hard to read and break formatting in many configuration files (e.g. fstab or crypttab). Also every time a partition is resized or reformatted a new UUID is generated and configs have to get adjusted (manually).

**Tip:** In case your swap partition does not have an UUID assigned, you will need to reset the swap partition using [mkswap](/index.php/Swap#Swap_partition "Swap") utility.

### by-id 和 by-path

`by-id` creates a unique name depending on the hardware serial number, `by-path` depending on the shortest physical path (according to sysfs). Both contain strings to indicate which subsystem they belong to (i.e. `-ide-` for `by-path`, and `-ata-` for `by-id`), so they are linked to the hardware controlling the device. This implies different levels of persistence: the `by-path` will already change when the device is plugged into a different port of the controller, the `by-id` will change when the device is plugged into a port of a hardware controller subject to another subsystem. [[1]](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/persistent_naming.html) Thus, both are not suitable to achieve persistent naming tolerant to hardware changes.

However, both provide important information to find a particular device in a large hardware infrastructure. For example, if you do not manually assign persistent labels (`by-label` or `by-partlabel`) and keep a directory with hardware port usage, `by-id` and `by-path` can be used to find a particular device.[[2]](http://linuxshellaccount.blogspot.in/2008/09/how-to-easily-find-wwns-of-qlogic-hba.html) [[3]](http://www.linuxquestions.org/questions/linux-server-73/how-to-find-wwn-for-dev-sdc-917269/)

### by-partlabel

**Note:** This method only concerns disks with [GUID Partition Table (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table").

Partition labels can be defined in the header of the partition entry on GPT disks.

See also [Wikipedia:GUID_Partition_Table#Partition_entries](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries "wikipedia:GUID Partition Table").

This method is very similar to the [filesystem labels](#by-label), excepted that the dynamic directory is `/dev/disk/by-partlabel`.

 `ls -l /dev/disk/by-partlabel/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 EFI\x20SYSTEM\x20PARTITION -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 GNU\x2fLINUX -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 HOME -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 SWAP -> ../../sda4

```

**Note:**

*   GPT partition labels have also to be different to avoid conflicts. To change your partition label, you can use `gdisk` or the ncurse-based version `cgdisk`. Both are available from the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package. See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").
*   According to the specification, GPT partition labels can be up to 72 characters long.

### by-partuuid

**Note:** This method only concerns disks with [GUID Partition Table (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table").

Like [GPT partition labels](#by-partlabel), GPT partition UUID are defined in the partition entry on GPT disks.

See also [Wikipedia:GUID_Partition_Table#Partition_entries](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries "wikipedia:GUID Partition Table").

The dynamic directory is similar to other methods and, like [UUID filesystems](#by-uuid), using UUIDs is prefered over labels.

 `ls -l /dev/disk/by-partuuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 039b6c1c-7553-4455-9537-1befbc9fbc5b -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 7280201c-fc5d-40f2-a9b2-466611d3d49e -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 98a81274-10f7-40db-872a-03df048df366 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 d0d0d110-0a71-4ed6-936a-304969ea36af -> ../../sda1

```

### 使用 Udev 静态设备名

参考 [设置静态设备名](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#设置静态设备名 "Udev (简体中文)")。

## 使用持久名称

有多种应用可以使用持久名称：

### fstab

参考 [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab")

### 引导管理器

要在引导管理器中使用持久化名称，需要满足下列先决条件：

*   使用 [mkinitcpio](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#配置 "Mkinitcpio (简体中文)") 初始化 RAM 磁盘镜像
*   在 `/etc/mkinitcpio.conf` 中启用了 udev

在上面的例子中，`/dev/sda1` 是引导分区。在 [GRUB](/index.php/GRUB "GRUB") 的 `grub.cfg` 文件中，*linux* 这行如下：

```
linux /boot/vmlinuz-linux root=/dev/sda1 rw quiet

```

根据选定的命名方案，将该行内容修改为如下之一：

```
linux /boot/vmlinuz-linux root=/dev/disk/by-label/root_myhost rw quiet

```

或者：

```
linux /boot/vmlinuz-linux root=UUID=2d781b26-0285-421a-b9d0-d4a0d3b55680 rw quiet

```

如果使用 [LILO](/index.php/LILO "LILO")，请勿使用 `root=...` 配置选项，它不会工作。而应代之以 `append="root=..."` 或 `addappend="root=..."`。详情参阅 LILO 的 man 文档中的 `append` 和 `addappend` 章节。

有一个替代的方法处理嵌入配置行中的文件系统标签。如上例中 `/dev/sda1` 文件系统标签为 `root_myhost`，可以在 GRUB 的 配置行中这样写：

```
linux /boot/vmlinuz-linux root=LABEL=root_myhost rw quiet

```