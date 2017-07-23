**Состояние перевода:** На этой странице представлен перевод статьи [Overlay filesystem](/index.php/Overlay_filesystem "Overlay filesystem"). Дата последней синхронизации: 15 марта 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Overlay_filesystem&diff=0&oldid=470729).

From [the initial kernel commit](https://github.com/torvalds/linux/commit/e9be9d5e76e34872f0c37d72e25bc27fe9e2c54c)

	Overlayfs allows one, usually read-write, directory tree to be overlaid onto another, read-only directory tree. All modifications go to the upper, writable layer. This type of mechanism is most often used for live CDs but there's a wide variety of other uses.

	The implementation differs from other "union filesystem" implementations in that after a file is opened all operations go directly to the underlying, lower or upper, filesystems. This simplifies the implementation and allows native performance in these cases.

Overlayfs has been in the linux kernel since 3.18.[[1]](https://github.com/torvalds/linux/commit/e9be9d5e76e34872f0c37d72e25bc27fe9e2c54c)

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Read-only overlay](#Read-only_overlay)
*   [3 See also](#See_also)

## Installation

Overlayfs is enabled in the default kernel and the `overlay` module is automatically loaded upon issuing a mount command.

## Usage

To mount an overlay use the following `mount` options:

```
# mount -t overlay overlay -o lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* */merged*

```

**Note:** The working directory (*workdir*) needs to be on the same filesystem mount as the upper directory. There isn't any requirement on (*lowerdir*).

The lower directory can actually be a list of directories separated by `:`, all changes in the `merged` directory are still reflected in `upper`.

Example:

```
# mount -t overlay overlay -o lowerdir=*/lower1:/lower2:/lower3*,upperdir=*/upper*,workdir=*/work* */merged*

```

To add an overlayfs entry to `/etc/fstab` use the following format:

 `/etc/fstab`  `overlay */merged* overlay noauto,x-systemd.automount,lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* 0 0` 

The `noauto` and `x-systemd.automount` mount options are necessary to prevent systemd from hanging on boot because it failed to mount the overlay. The overlay is now mounted whenever it is first accessed and requests are buffered until it is ready. See [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab").

### Read-only overlay

Sometimes, it is only desired to create a read-only view of the combination of two or more directories. In that case, it can be created in a easier manner, as the directories `upper` and `work` are **not** required:

```
# mount -t overlay overlay -o lowerdir=*/lower1:/lower2* */merged*

```

When `upperdir` is not specified, the overlay is [automatically mounted as read-only](https://github.com/torvalds/linux/blob/352526f45387cb96671f13b003bdd5b249e509bd/fs/overlayfs/super.c#L897).

## See also

*   [Overlay Filesystem documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/overlayfs.txt)