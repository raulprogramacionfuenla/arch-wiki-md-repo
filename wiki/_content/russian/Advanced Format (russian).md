The [Advanced Format](https://en.wikipedia.org/wiki/Advanced_Format "wikipedia:Advanced Format") is a generic term pertaining to any disk sector format used to store data on magnetic disks in [hard disk drives](https://en.wikipedia.org/wiki/hard_disk_drives "w:hard disk drives") (HDDs) that uses 4 kilobyte sectors instead of the traditional 512 byte sectors. The main idea behind using 4096-byte sectors is to increase the bit density on each track by reducing the number of gaps which hold Sync/DAM and ECC (Error Correction Code) information between data sectors. The old format gave a format efficiency of 88.7%, whereas Advanced Format results in a format efficiency of 97.3%.

## Contents

*   [1 How to determine if HDD employ a 4k sector](#How_to_determine_if_HDD_employ_a_4k_sector)
*   [2 Aligning Partitions](#Aligning_Partitions)
    *   [2.1 Check your partitions alignment](#Check_your_partitions_alignment)
    *   [2.2 GPT (Recommended)](#GPT_.28Recommended.29)
*   [3 See also](#See_also)

## How to determine if HDD employ a 4k sector

The physical and logical sector size of hard disk /dev/sd*X* can be determined by reading the following sysfs entries:

```
$ cat /sys/class/block/sd*X*/queue/physical_block_size
$ cat /sys/class/block/sd*X*/queue/logical_block_size

```

Tools which will report the physical sector of a drive (provided the drive will report it correctly) includes

*   smartmontools (since 5.41 ; <tt>smartmontools -a</tt>, in information section)
*   hdparm (since 9.12 ; <tt>hdparm -I</tt>, in configuration section)

Note that both works even for USB-attached discs (if the USB bridge supports SAT aka SCSI/ATA Translation, ANSI INCITS 431-2007).

## Aligning Partitions

**Note:** This should no longer require manual intervention. Any tools using recent libblkid versions are capable of handling Advanced Format automatically.

Versions with this support include:

*   fdisk, since util-linux >= 2.15\. You should start with ‘-c -u’ to disable DOS compatibility and use sectors instead of cylinders.
*   parted, since parted >= 2.1.
*   mdadm, since util-linux >= 2.15
*   lvm2, since util-linux >= 2.15
*   mkfs.{ext,xfs,gfs2,ocfs2} all support libblkid directly.

Refer to [this page](https://www.tolaris.com/2011/07/21/libblkid-or-why-you-dont-need-to-worry-about-4k-disk-format/) for further information.

### Check your partitions alignment

**Note:** This only works with [MBR](/index.php/MBR "MBR"), not [GPT](/index.php/GPT "GPT").

```
# fdisk -lu /dev/sda
...
# Device     Boot      Start   End         Blocks      Id System
# /dev/sda1            2048    46876671    23437312    7  HPFS/NTFS

```

2048 (default since fdisk 2.17.2) means that your HDD is aligned correctly. Any other value divisible by 8 is good as well.

### GPT (Recommended)

When using [GPT](/index.php/GPT "GPT") partition tables, one need only use gdisk to create partitions which are aligned by default. For an example, see [SSD#Detailed Usage Example](/index.php/SSD#Detailed_Usage_Example "SSD").

## See also

*   [Western Digital’s Advanced Format: The 4K Sector Transition Begins](http://www.anandtech.com/Show/Index/2888)
*   [White paper entitled "Advanced Format Technology."](http://www.wdc.com/wdproducts/library/WhitePapers/ENG/2579-771430.pdf)
*   Failure to align one's HDD results in poor read/write performance. See [this article](http://www.linuxconfig.org/linux-wd-ears-advanced-format) for specific examples.