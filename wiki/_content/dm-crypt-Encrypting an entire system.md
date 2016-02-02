# dm-crypt/Encrypting an entire system

Back to [dm-crypt](/index.php/Dm-crypt "Dm-crypt").

The following are examples of common scenarios of full system encryption with _dm-crypt_. They explain all the adaptations that need to be done to the normal [installation procedure](/index.php/Installation_guide "Installation guide"). All the necessary tools are on the [installation image](https://www.archlinux.org/download/).

## Contents

*   [1 Overview](#Overview)
*   [2 Simple partition layout with LUKS](#Simple_partition_layout_with_LUKS)
    *   [2.1 Preparing the disk](#Preparing_the_disk)
    *   [2.2 Preparing non-boot partitions](#Preparing_non-boot_partitions)
    *   [2.3 Preparing the boot partition](#Preparing_the_boot_partition)
    *   [2.4 Mounting the devices](#Mounting_the_devices)
    *   [2.5 Configuring mkinitcpio](#Configuring_mkinitcpio)
    *   [2.6 Configuring the boot loader](#Configuring_the_boot_loader)
*   [3 LVM on LUKS](#LVM_on_LUKS)
    *   [3.1 Preparing the disk](#Preparing_the_disk_2)
    *   [3.2 Preparing the logical volumes](#Preparing_the_logical_volumes)
    *   [3.3 Preparing the boot partition](#Preparing_the_boot_partition_2)
    *   [3.4 Configuring mkinitcpio](#Configuring_mkinitcpio_2)
    *   [3.5 Configuring the boot loader](#Configuring_the_boot_loader_2)
*   [4 LUKS on LVM](#LUKS_on_LVM)
    *   [4.1 Preparing the disk](#Preparing_the_disk_3)
    *   [4.2 Preparing the logical volumes](#Preparing_the_logical_volumes_2)
    *   [4.3 Preparing the boot partition](#Preparing_the_boot_partition_3)
    *   [4.4 Configuring mkinitcpio](#Configuring_mkinitcpio_3)
    *   [4.5 Configuring the boot loader](#Configuring_the_boot_loader_3)
    *   [4.6 Configuring fstab and crypttab](#Configuring_fstab_and_crypttab)
    *   [4.7 Encrypting logical volume /home](#Encrypting_logical_volume_.2Fhome)
*   [5 LUKS on software RAID](#LUKS_on_software_RAID)
*   [6 Plain dm-crypt](#Plain_dm-crypt)
    *   [6.1 Preparing the disk](#Preparing_the_disk_4)
    *   [6.2 Preparing the non-boot partitions](#Preparing_the_non-boot_partitions)
    *   [6.3 Preparing the boot partition](#Preparing_the_boot_partition_4)
    *   [6.4 Configuring mkinitcpio](#Configuring_mkinitcpio_4)
    *   [6.5 Configuring the boot loader](#Configuring_the_boot_loader_4)
    *   [6.6 Post-installation](#Post-installation)
*   [7 Encrypted boot partition (GRUB)](#Encrypted_boot_partition_.28GRUB.29)
    *   [7.1 Preparing the disk](#Preparing_the_disk_5)
    *   [7.2 Preparing the logical volumes](#Preparing_the_logical_volumes_3)
    *   [7.3 Preparing the boot partition](#Preparing_the_boot_partition_5)
    *   [7.4 Configuring mkinitcpio](#Configuring_mkinitcpio_5)
    *   [7.5 Configuring the boot loader](#Configuring_the_boot_loader_5)
    *   [7.6 Configuring fstab and crypttab](#Configuring_fstab_and_crypttab_2)

## Overview

Securing a root filesystem is where _dm-crypt_ excels, feature and performance-wise. Unlike selectively encrypting non-root filesystems, an encrypted root filesystem can conceal information such as which programs are installed, the usernames of all user accounts, and common data-leakage vectors such as [mlocate](/index.php/Mlocate "Mlocate") and `/var/log/`. Furthermore, an encrypted root filesystem makes tampering with the system far more difficult, as everything except the [boot loader](/index.php/Boot_loader "Boot loader") and (usually) the kernel is encrypted.

All scenarios illustrated in the following share these advantages, other pros and cons differentiating them are summarized below:

| Scenarios | Advantages | Disadvantages |
| [#Simple partition layout with LUKS](#Simple_partition_layout_with_LUKS)

shows a basic and straight-forward set-up for a fully LUKS encrypted root.

 | 

*   Simple partitioning and setup

 | 

*   Inflexible; disk-space to be encrypted has to be pre-allocated

 |
| [#LVM on LUKS](#LVM_on_LUKS)

achieves partitioning flexiblity by using LVM inside a single LUKS encrypted partition.

 | 

*   Simple partitioning with knowledge of LVM
*   Only one key required to unlock all volumes (e.g. easy resume-from-disk setup)
*   Volume layout not transparent when locked
*   Easiest method to allow [suspension to disk](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption")

 | 

*   LVM adds an additional mapping layer and hook
*   Less useful, if a singular volume should receive a separate key

 |
| [#LUKS on LVM](#LUKS_on_LVM)

uses dm-crypt only after the LVM is setup.

 | 

*   LVM can be used to have encrypted volumes span multiple disks
*   Easy mix of un-/encrypted volume groups

 | 

*   Complex; changing volumes requires changing encryption mappers too
*   Volumes require individual keys
*   LVM layout is transparent when locked

 |
| [#Plain dm-crypt](#Plain_dm-crypt)

uses dm-crypt plain mode, i.e. without a LUKS header and its options for multiple keys.
This scenario also employs USB devices for `/boot` and key storage, which may be applied to the other scenarios.

 | 

*   Data resilience for cases where a LUKS header may be damaged
*   Allows [deniable encryption](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption")

 | 

*   High care to all encryption parameters is required
*   Single encryption key and no option to change it

 |
| [#Encrypted boot partition (GRUB)](#Encrypted_boot_partition_.28GRUB.29)

shows how to encrypt the boot partition using the GRUB bootloader.
This scenario also employs an ESP partition, which may be applied to the other scenarios.

 | 

*   Same advantages as the scenario the installation is based on (LVM on LUKS for this particular example)
*   Less data is left unencrypted, i.e. the boot loader and the ESP partition, if present

 | 

*   Same disadvantages as the scenario the installation is based on (LVM on LUKS for this particular example)
*   More complicated configuration
*   Not supported by other boot loaders

 |

While all above scenarios provide much greater protection from outside threats than encrypted secondary filesystems, they also share a common disadvantage: any user in possession of the encryption key is able to decrypt the entire drive, and therefore can access other users' data. If that is of concern, it is possible to use a combination of blockdevice and stacked filesystem encryption and reap the advantages of both. See [Disk encryption](/index.php/Disk_encryption "Disk encryption") to plan ahead.

See [Dm-crypt/Drive preparation#Partitioning](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation") for a general overview of the partitioning strategies used in the scenarios.

Another area to consider is whether to set up an encrypted swap partition and what kind. See [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") for alternatives.

If you anticipate to protect the system's data not only against physical theft, but also have a requirement of precautions against logical tampering, see [Dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties") for further possibilities after following one of the scenarios.

## Simple partition layout with LUKS

This example covers a full system encryption with _dmcrypt_ + LUKS in a simple partition layout:

```
+--------------------+--------------------------+--------------------------+
|Boot partition      |LUKS encrypted system     |Optional free space       |
|                    |partition                 |for additional partitions |
|/dev/sdaY           |/dev/sdaX                 |or swap to be setup later |
+--------------------+--------------------------+--------------------------+

```

The first steps can be performed directly after booting the Arch Linux install image.

### Preparing the disk

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Then create the needed partitions, at least one for `/` (e.g. `/dev/sdaX`) and `/boot` (`/dev/sdaY`), see [Partitioning](/index.php/Partitioning "Partitioning").

### Preparing non-boot partitions

The following commands create and mount the encrypted root partition. They correspond to the procedure described in detail in [Dm-crypt/Encrypting a non-root file system#Partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") (which, despite the title, _can_ be applied to root partitions, as long as [mkinitcpio](#Configuring_mkinitcpio) and the [boot loader](#Configuring_the_boot_loader) are correctly configured). If you want to use particular non-default encryption options (e.g. cipher, key length), see the [encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") before executing the first command:

```
# cryptsetup -y -v luksFormat /dev/sdaX
# cryptsetup open /dev/sdaX cryptroot
# mkfs -t ext4 /dev/mapper/cryptroot
# mount -t ext4 /dev/mapper/cryptroot /mnt

```

Check the mapping works as intended:

```
# umount /mnt
# cryptsetup close cryptroot
# cryptsetup open /dev/sdaX cryptroot
# mount -t ext4 /dev/mapper/cryptroot /mnt

```

If you created separate partitions (e.g. `/home`), these steps have to be adapted and repeated for all of them, _except_ for `/boot`. See [Dm-crypt/Encrypting a non-root file system#Automated unlocking and mounting](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Automated_unlocking_and_mounting "Dm-crypt/Encrypting a non-root file system") on how to handle additional partitions at boot.

Note that each blockdevice requires its own passphrase. This may be inconvenient, because it results in a separate passphrase to be input during boot. An alternative is to use a keyfile stored in the system partition to unlock the separate partition via `crypttab`. See [Dm-crypt/Device encryption#Using LUKS to Format Partitions with a Keyfile](/index.php/Dm-crypt/Device_encryption#Using_LUKS_to_Format_Partitions_with_a_Keyfile "Dm-crypt/Device encryption") for instructions.

### Preparing the boot partition

What you do have to setup is a non-encrypted `/boot` partition, which is needed for a crypted root. For a standard [MBR/non-EFI](/index.php/EFI "EFI") `/boot` partition, for example, execute:

```
# mkfs -t ext4 /dev/sdaY
# mkdir /mnt/boot
# mount -t ext4 /dev/sdaY /mnt/boot

```

### Mounting the devices

At [Installation guide#Mount the partitions](/index.php/Installation_guide#Mount_the_partitions "Installation guide") you will have to mount the mapped devices, not the actual partitions. Of course `/boot`, which is not encrypted, will still have to be mounted directly.

Afterwards continue with the installation procedure up to the mkinitcpio step.

### Configuring mkinitcpio

Add the `encrypt` hook to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `etc/mkinitcpio.conf`  `HOOKS="... **encrypt** ... filesystems ..."` 

Depending on which other hooks are used, the order may be relevant. See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=UUID=_<device-UUID>_:cryptroot root=/dev/mapper/cryptroot

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

The `_<device-UUID>_` refers to the UUID of `/dev/sdaX`, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

## LVM on LUKS

The straight-forward method is to set up [LVM](/index.php/LVM "LVM") on top of the encrypted partition instead of the other way round. Technically the LVM is setup inside one big encrypted blockdevice. Hence, the LVM is not transparent until the blockdevice is unlocked and the underlying volume structure is scanned and mounted during boot.

The disk layout in this example is:

```
+-----------------------------------------------------------------------+ +----------------+
| Logical volume1       | Logical volume2       | Logical volume3       | |                |
|/dev/MyStorage/swapvol |/dev/MyStorage/rootvol |/dev/MyStorage/homevol | | Boot partition |
|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _| | (may be on     |
|                                                                       | | other device)  |
|                        LUKS encrypted partition                       | |                |
|                          /dev/sdaX                                    | | /dev/sdbY      |
+-----------------------------------------------------------------------+ +----------------+

```

This method does not allow you to span the logical volumes over multiple disks, even in the future. The [#LUKS on LVM](#LUKS_on_LVM) method does not have this limitation.

**Tip:** Two variants of this setup:

*   Instructions at [Dm-crypt/Specialties#Encrypted system using a remote LUKS header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_remote_LUKS_header "Dm-crypt/Specialties") use this setup with a remote LUKS header on a USB device to achieve a two factor authentication with it.
*   Instructions at [Pavel Kogan's blog](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/) show how to encrypt the `/boot` partition while keeping it on the main LUKS partition when using GRUB, but be aware of [FS#43663](https://bugs.archlinux.org/task/43663).

### Preparing the disk

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

When using the [GRUB](/index.php/GRUB "GRUB") bootloader together with [GPT](/index.php/GPT "GPT"), create a BIOS Boot Partition as explained in [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB").

Create a partition to be mounted at `/boot` of type `8300` with a size of 100 MB or more.

Create a partition of type `8E00`, which will later contain the encrypted container.

Create the LUKS encrypted container at the "system" partition. Enter the chosen password twice.

```
# cryptsetup luksFormat /dev/_sdaX_

```

For more information about the available cryptsetup options see the [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") prior to above command.

Open the container:

```
# cryptsetup open --type luks /dev/_sdaX_ lvm

```

The decrypted container is now available at `/dev/mapper/lvm`.

### Preparing the logical volumes

Create a physical volume on top of the opened LUKS container:

```
# pvcreate /dev/mapper/lvm

```

Create the volume group named `MyStorage`, adding the previously created physical volume to it:

```
# vgcreate MyStorage /dev/mapper/lvm

```

Create all your logical volumes on the volume group:

```
# lvcreate -L 8G MyStorage -n swapvol
# lvcreate -L 15G MyStorage -n rootvol
# lvcreate -l +100%FREE MyStorage -n homevol

```

Format your filesystems on each logical volume:

```
# mkfs.ext4 /dev/mapper/MyStorage-rootvol
# mkfs.ext4 /dev/mapper/MyStorage-homevol
# mkswap /dev/mapper/MyStorage-swapvol

```

Mount your filesystems:

```
# mount /dev/MyStorage/rootvol /mnt
# mkdir /mnt/home
# mount /dev/MyStorage/homevol /mnt/home
# swapon /dev/MyStorage/swapvol

```

### Preparing the boot partition

The bootloader loads the kernel, [initramfs](/index.php/Initramfs "Initramfs"), and its own configuration files from the `/boot` directory. This directory must be located on a separate unencrypted filesystem.

Create an Ext2 filesystem on the partition intended for `/boot`. Any filesystem that can be read by the bootloader is eligible.

```
# mkfs.ext2 /dev/_sdbY_

```

Create the directory `/mnt/boot`:

```
# mkdir /mnt/boot

```

Mount the partition to `/mnt/boot`:

```
# mount /dev/_sdbY_ /mnt/boot

```

Afterwards continue with the installation procedure up to the mkinitcpio step.

### Configuring mkinitcpio

Add the `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS="... **encrypt** **lvm2** ... filesystems ..."` 

**Note:** The order of both hooks no longer matters with the current implementation of `lvm2`.

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=UUID=_<device-UUID>_:MyStorage root=/dev/mapper/MyStorage-rootvol

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

The `_<device-UUID>_` refers to the UUID of `/dev/sdaX`, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

## LUKS on LVM

To use encryption on top of [LVM](/index.php/LVM "LVM"), the LVM volumes are set up first and then used as the base for the encrypted partitions. This way, a mixture of encrypted and non-encrypted volumes/partitions is possible as well. Unlike [#LVM on LUKS](#LVM_on_LUKS), this method allows normally spanning the logical volumes over multiple disks.

The following short example creates a LUKS on LVM setup and mixes in the use of a key-file for the /home partition and temporary crypt volumes for `/tmp` and `/swap`. The latter is considered desirable from a security perspective, because no potentially sensitive temporary data survives the reboot, when the encryption is re-initialised. If you are experienced with LVM, you will be able to ignore/replace LVM and other specifics according to your plan. If you want to span a logical volume over multiple disks during setup already, a procedure to do so is described in [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

### Preparing the disk

Partitioning scheme:

*   `/dev/sda1` -> `/boot`
*   `/dev/sda2` -> LVM

Randomise `/dev/sda2` according to [Dm-crypt/Drive preparation#dm-crypt wipe before installation](/index.php/Dm-crypt/Drive_preparation#dm-crypt_wipe_before_installation "Dm-crypt/Drive preparation").

### Preparing the logical volumes

```
# lvm pvcreate /dev/sda2
# lvm vgcreate lvm /dev/sda2
# lvm lvcreate -L 10G -n lvroot lvm
# lvm lvcreate -L 500M -n swap lvm
# lvm lvcreate -L 500M -n tmp lvm
# lvm lvcreate -l 100%FREE -n home lvm

```

```
# cryptsetup luksFormat -c aes-xts-plain64 -s 512 /dev/lvm/lvroot
# cryptsetup open --type luks /dev/lvm/lvroot root
# mkfs -t ext4 /dev/mapper/root
# mount /dev/mapper/root /mnt

```

More information about the encryption options can be found in [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption"). Note that `/home` will be encrypted in [#Encrypting logical volume /home](#Encrypting_logical_volume_.2Fhome). Further, note that if you ever have to access the encrypted root from the Arch-ISO, the above `open` action will allow you to after the [LVM shows up](/index.php/LVM#Logical_Volumes_do_not_show_up "LVM").

### Preparing the boot partition

```
# dd if=/dev/zero of=/dev/sda1 bs=1M
# mkfs -t ext4 /dev/sda1
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

Now after setup of the encrypted LVM partitioning, it would be time to install: [Arch Install Scripts](/index.php/Installation_guide#Mount_the_partitions "Installation guide").

### Configuring mkinitcpio

Add the `lvm2` and `encrypt` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `etc/mkinitcpio.conf`  `HOOKS="... **block _''_encrypt** **lvm2** ... filesystems ..."` 

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=/dev/lvm/lvroot:cryptoroot root=/dev/mapper/cryptoroot

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

### Configuring fstab and crypttab

 `/etc/fstab` 

```
 /dev/mapper/root        /       ext4            defaults        0       1
 /dev/sda1               /boot   ext4            defaults        0       2
 /dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
 /dev/mapper/swap        none    swap            sw              0       0
```

The following [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") options will re-encrypt the temporary filesystems each reboot:

 `/etc/crypttab` 

```
 swap	/dev/lvm/swap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256
 tmp	/dev/lvm/tmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256
```

### Encrypting logical volume /home

Since this scenario uses LVM as the primary and dm-crypt as secondary mapper, each encrypted logical volume requires its own encryption. Yet, unlike the temporary filesystems configured with volatile encryption above, the logical volume for `/home` should be persistent, of course. The following assumes you have rebooted into the installed system, otherwise you have to adjust paths. To safe on entering a second passphrase at boot for it, a [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") is created:

```
mkdir -m 700 /etc/luks-keys
dd if=/dev/random of=/etc/luks-keys/home bs=1 count=256

```

The logical volume is encrypted with it:

```
cryptsetup luksFormat -v -s 512 /dev/lvm/home /etc/luks-keys/home
cryptsetup -d /etc/luks-keys/home open --type luks /dev/lvm/home home
mkfs -t ext4 /dev/mapper/home
mount /dev/mapper/home /home

```

The encrypted mount is configured in [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration"):

 `/etc/crypttab`  `home	/dev/lvm/home   /etc/luks-keys/home`  `/etc/fstab`  `/dev/mapper/home        /home   ext4        defaults        0       2` 

and setup is done.

If you want to expand the logical volume for `/home` (or any other volume) at a later point, it is important to note that the LUKS encrypted part has to be resized as well. For a procedure see [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

## LUKS on software RAID

## Plain dm-crypt

This scenario sets up a system on a dm-crypt a full disk with _plain_ mode encryption. Note that for most use cases, the methods using LUKS described above are the better options for both system encryption and encrypted partitions. LUKS features like key management with multiple pass-phrases/key-files are unavailable with _plain_ mode.

dm-crypt _plain_ mode does not require a header on the encrypted disk: this means that an unpartitioned, encrypted disk will be indistinguishable from a disk filled with random data, which is the desired attribute for this scenario, see also [Wikipedia:Deniable encryption](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption").

_Plain_ dm-crypt encrypted disks can be more resilient to damage than LUKS encrypted disks, because it does not rely on an encryption master-key which can be a single-point of failure if damaged. However, using _plain_ mode also requires more manual configuration of encryption options to achieve the same cryptographic strength. See also [Disk encryption#Cryptographic metadata](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption").

**Tip:** If headerless encryption is your goal but you are unsure about the lack of key-derivation with _plain_ mode, then two alternatives are:

*   [tcplay](/index.php/Tcplay "Tcplay") which offers headerless encryption but with the PBKDF2 function, or
*   dm-crypt LUKS mode by using the _cryptsetup_ `--header` option. It cannot be used with the standard _encrypt_ hook, but the hook [may be modified](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_remote_LUKS_header "Dm-crypt/Specialties").

The scenario uses a USB stick for the boot device and another one to store the encryption key. The disk layout is:

```
+--------------------+------------------+--------------------+ +---------------+ +---------------+
|Volume 1:           |Volume 2:         |Volume 3:           | |Boot device    | |Encryption key |
|                    |                  |                    | |               | |file storage   |
|root                |swap              |home                | |/boot          | |(unpartitioned |
|                    |                  |                    | |               | |in example)    |
|/dev/store/root     |/dev/store/swap   |/dev/store/home     | |/dev/sdY1      | |/dev/sdZ       |
|--------------------+------------------+--------------------| |---------------| |---------------|
|disk drive /dev/sdaX encrypted using plain mode and LVM     | |USB stick 1    | |USB stick 2    |
+------------------------------------------------------------+ +---------------+ +---------------+

```

`/boot` and the boot loader cannot be kept on the encrypted drive, or it will defeat the purpose of using _plain_ mode for deniable encryption. This also allows storing the options required to open/unlock the plain encrypted device in the boot loader configuration, since typing them on each boot would be error prone.

This scenario also uses a key file, assuming it stored as raw bits on a second USB stick, so that to the eyes of an unaware attacker who might get the usbkey the encryption key will appear as random data instead of being visible as a normal file. See also [Wikipedia:Security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity"), follow [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") to prepare the keyfile.

**Tip:**

*   It is also possible to use a single usb key by copying the keyfile to the initram directly. An example keyfile `/etc/keyfile` gets copied to the initram image by setting `FILES="/etc/keyfile"` in `/etc/mkinitcpio.conf`. The way to instruct the `encrypt` hook to read the keyfile in the initram image is using `rootfs:` prefix before the filename, e.g. `cryptkey=rootfs:/etc/keyfile`.
*   Another option is using a passphrase with good [entropy](/index.php/Disk_encryption#Choosing_a_strong_passphrase "Disk encryption").

### Preparing the disk

It is vital that the mapped device is filled with data. In particular this applies to the scenario usecase we apply here.

See [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") and [Dm-crypt/Drive preparation#dm-crypt specific methods](/index.php/Dm-crypt/Drive_preparation#dm-crypt_specific_methods "Dm-crypt/Drive preparation")

### Preparing the non-boot partitions

See [Dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") for details.

Using the device `/dev/sd_X_`, with the twofish-xts cipher with a 512 bit key size and using a keyfile we have the following options for this scenario:

 `# cryptsetup --hash=sha512 --cipher=twofish-xts-plain64 --offset=0 --key-file=/dev/sd_Z_ --key-size=512 open --type=plain /dev/sdX enc` 

Unlike encrypting with LUKS, the above command must be executed _in full_ whenever the mapping needs to be re-established, so it is important to remember the cipher, hash and key file details.

We can now check a mapping entry has been made for `/dev/mapper/enc`:

```
# fdisk -l

```

Next, we setup [LVM](/index.php/LVM "LVM") logical volumes on the mapped device, see [LVM#Installing Arch Linux on LVM](/index.php/LVM#Installing_Arch_Linux_on_LVM "LVM") for further details:

```
# pvcreate /dev/mapper/enc
# vgcreate store /dev/mapper/enc
# lvcreate -L 20G store -n root
# lvcreate -L 10G store -n swap
# lvcreate -l +100%FREE store -n home

```

We format and mount them and activate swap, see [File systems#Format a device](/index.php/File_systems#Format_a_device "File systems") for further details:

```
# mkfs.ext4 /dev/store/root
# mkfs.ext4 /dev/store/home
# mount /dev/store/root /mnt
# mkdir /mnt/home
# mount /dev/store/home /mnt/home
# mkswap /dev/store/swap
# swapon /dev/store/swap

```

### Preparing the boot partition

The `/boot` partition can be installed on the standard vfat partition of a USB stick, if required. But if manual partitioning is needed, then a small 200MB partition is all that is required. Create the partition using a [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning") of your choice.

We choose a non-journalling file system to preserve the flash memory of the `/boot` partition, if not already formatted as vfat:

```
# mkfs.ext2 /dev/sd_Y_1
# mkdir /mnt/boot
# mount /dev/sd_Y_1 /mnt/boot

```

### Configuring mkinitcpio

Add the `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `etc/mkinitcpio.conf`  `HOOKS="... **encrypt** **lvm2** ... filesystems ..."` 

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to boot the encrypted root partition, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=/dev/sd_X_:enc cryptkey=/dev/sd_Z_:0:512 crypto=sha512:twofish-xts-plain64:512:0:

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details and other parameters that you may need.

**Tip:** If using GRUB, you can install it on the same USB as the `/boot` partition with:

```
# grub-install --recheck /dev/sd_Y_

```

### Post-installation

You may wish to remove the USB sticks after booting. Since the `/boot` partition is not usually needed, the `noauto` option can be added to the relevant line in `/etc/fstab`:

 `/etc/fstab` 

```
# /dev/sd_Yn_
/dev/sd_Yn_ /boot ext2 **noauto**,rw,noatime 0 2
```

However, when an update to the kernel or bootloader is required, the `/boot` partition must be present and mounted. As the entry in `fstab` already exists, it can be mounted simply with:

```
# mount /boot

```

## Encrypted boot partition (GRUB)

This setup utilizes the same partition layout and configuration for the system's root partition as the previous [#LVM on LUKS](#LVM_on_LUKS) section, with two distinct differences:

1.  The setup is performed for an [UEFI](/index.php/UEFI "UEFI") system and
2.  A special feature of the [GRUB](/index.php/GRUB "GRUB") bootloader is used to additionally encrypt the boot partition `/boot`. See also [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB").

The disk layout in this example is:

```
+---------------+----------------+----------------+----------------+----------------+
|ESP partition: |Boot partition: |Volume 1:       |Volume 2:       |Volume 3:       |
|               |                |                |                |                |
|/boot/efi      |/boot           |root            |swap            |home            |
|               |                |                |                |                |
|               |                |/dev/store/root |/dev/store/swap |/dev/store/home |
|/dev/sdaX      |/dev/sdaY       +----------------+----------------+----------------+
|**un**encrypted    |LUKS encrypted  |/dev/sdaZ encrypted using LVM on LUKS             |
+---------------+----------------+--------------------------------------------------+

```

**Tip:** All scenarios are intended as examples. It is, of course, possible to apply both of the two above distinct installation steps with the other scenarios as well. See also the variants linked in [#LVM on LUKS](#LVM_on_LUKS).

### Preparing the disk

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Create an [EFI System Partition (ESP)](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") with an appropriate size, it will later be mounted at `/boot/efi`.

Create a partition to be mounted at `/boot` of type `8300` with a size of 100 MB or more.

**Tip:** When using the [GRUB](/index.php/GRUB "GRUB") bootloader together with a BIOS/[GPT](/index.php/GPT "GPT"), create a BIOS Boot Partition as explained in [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB") instead of the ESP.

Create a partition of type `8E00`, which will later contain the encrypted container.

Create the LUKS encrypted container at the "system" partition.

```
# cryptsetup luksFormat /dev/_sdaZ_

```

For more information about the available cryptsetup options see the [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") prior to above command.

Your partition layout should look similar to this:

 ` gdisk /dev/sda ` 

```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem
   3         1460224        41943006   19.3 GiB    8E00  Linux LVM

```

Open the container:

```
# cryptsetup open --type luks /dev/_sdaZ_ lvm

```

The decrypted container is now available at `/dev/mapper/lvm`.

### Preparing the logical volumes

The LVM logical volumes of this example follow the exact layout as the previous scenario. Therefore, please follow [Preparing the logical volumes](#Preparing_the_logical_volumes) above or adjust as required.

### Preparing the boot partition

The bootloader loads the kernel, [initramfs](/index.php/Initramfs "Initramfs"), and its own configuration files from the `/boot` directory.

First, create the LUKS container where the files will be located and installed into:

```
# cryptsetup luksFormat /dev/sda_Y_ 

```

Next, open it:

```
# cryptsetup open /dev/sda_Y_ cryptboot 

```

Create a filesystem on the partition intended for `/boot`. Any filesystem that can be read by the bootloader is eligible:

```
# mkfs.ext2 /dev/mapper/_cryptboot_

```

Create the directory `/mnt/boot`:

```
# mkdir /mnt/boot

```

Mount the partition to `/mnt/boot`:

```
# mount /dev/mapper/_cryptboot_ /mnt/boot

```

Create a mountpoint for the [ESP](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") at `/boot/efi` for compatibility with `grub-install` and mount it:

```
# mkdir /mnt/boot/efi
# mount /dev/_sdaX_ /mnt/boot/efi

```

At this point, you should have the following partitions and logical volumes inside of `/mnt`:

 `lsblk` 

```
NAME              	  MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                       8:0      0   200G  0 disk  
├─sda1                    8:1      0   512M  0 part  /boot/efi
├─sda2                    8:2      0   200M  0 part  
│ └─boot		  254:0    0   198M  0 crypt /boot
└─sda3                    8:3      0   100G  0 part  
  └─lvm                   254:1    0   100G  0 crypt 
    ├─MyStorage-swapvol   254:2    0     8G  0 lvm   [SWAP]
    ├─MyStorage-rootvol   254:3    0    15G  0 lvm   /
    └─MyStorage-homevol   254:4    0    77G  0 lvm   /home

```

Afterwards continue with the installation procedure up to the mkinitcpio step.

### Configuring mkinitcpio

Add the `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS="... **encrypt** **lvm2** ... filesystems ..."` 

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=UUID=_<device-UUID>_:MyStorage root=/dev/mapper/MyStorage-rootvol

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

The `_<device-UUID>_` refers to the UUID of `/dev/sdaX`, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

Now we prepare the GRUB bootloader installation to recognize the LUKS encrypted `/boot` partition according to [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB").

Open `/etc/default/grub` and add the parameter to the end:

`GRUB_ENABLE_CRYPTODISK=y`

Create the GRUB menu configuration file:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

[Install GRUB](/index.php/GRUB#Installation_2 "GRUB") to the mounted ESP:

```
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub --recheck

```

If this finished without errors, GRUB should prompt for the passphrase to unlock the `/boot` partition after the next reboot.

### Configuring fstab and crypttab

This section deals with extra configuration to let the system **mount** the encrypted `/boot`.

While GRUB asks for a passphrase to unlock the encrypted `/boot` after above instructions, the partition unlock is not passed on to the initramfs. Hence, `/boot` will not be available after the system has re-/booted, because the `encrypt` hook only unlocks the system's root.

If you used the _genfstab_ script during installation, it will have generated `/etc/fstab` entries for the `/boot` and `/boot/efi` mount points already, but the system will fail to find the generated device mapper for the boot partition. To make it available, add it to [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration"). For example:

 `/etc/crypttab`  `cryptboot  /dev/sdaY      none        luks` 

will make the system ask for the passphrase again (i.e. you have to enter it twice at boot: once for GRUB and once for systemd init). To avoid the double entry for unlocking `/boot`, follow the instructions at [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") to:

1.  Create a [randomtext keyfile](/index.php/Dm-crypt/Device_encryption#Storing_the_keyfile_on_a_filesystem "Dm-crypt/Device encryption"),
2.  Add the keyfile to the (`/dev/sdaY`) [boot partition's LUKS header](/index.php/Dm-crypt/Device_encryption#Configuring_LUKS_to_make_use_of_the_keyfile "Dm-crypt/Device encryption") and
3.  Check the `/etc/fstab` entry and add the `/etc/crypttab` line to [unlock it automatically at boot](/index.php/Dm-crypt/Device_encryption#Unlocking_a_secondary_partition_at_boot "Dm-crypt/Device encryption").

If for some reason the keyfile fails to unlock the boot partition, systemd will fallback to ask for a passphrase to unlock and, in case that is correct, continue booting.

**Tip:** Optional post-installation steps:

*   It may be worth considering to add the GRUB bootloader to the ignore list of `/etc/pacman.conf` in order to take particular control of when the bootloader (which includes its own encryption modules) is updated.
*   If you want to encrypt the `/boot` partition to protect against offline tampering threats, the [mkinitcpio-chkcryptoboot](/index.php/Dm-crypt/Specialties#mkinitcpio-chkcryptoboot "Dm-crypt/Specialties") hook has been contributed to help.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_an_entire_system&oldid=415497](https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_an_entire_system&oldid=415497)"