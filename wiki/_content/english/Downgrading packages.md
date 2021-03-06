Related articles

*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [pacman](/index.php/Pacman "Pacman")
*   [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")

Before downgrading a single or multiple packages, consider why you wish to do so. If it is due to a bug, search the [bug tracker](https://bugs.archlinux.org/) for existing tasks. If there is none, add a new task; it is better to correct bugs, or at least warn other users of possible issues.

**Warning:**

*   Downgrading one package may require that its dependencies be downgraded as well. When the number of packages to downgrade is large, consider using a snapshot. See [Arch Linux Archive#How to restore all packages to a specific date](/index.php/Arch_Linux_Archive#How_to_restore_all_packages_to_a_specific_date "Arch Linux Archive").
*   Be careful with changes to configuration files and scripts. For now pacman will handle this for us, as long as we do not bypass its safeguards.
*   If the downgrading involve a soname change, all dependency may need downgrading or [rebuild](/index.php/Frequently_asked_questions#What_if_I_run_a_full_system_upgrade_and_there_will_be_an_update_for_a_shared_library.2C_but_not_for_the_apps_that_depend_on_it.3F "Frequently asked questions") too.

## Contents

*   [1 Return to an earlier package version](#Return_to_an_earlier_package_version)
    *   [1.1 Using the pacman cache](#Using_the_pacman_cache)
    *   [1.2 Downgrading the kernel](#Downgrading_the_kernel)
    *   [1.3 Arch Linux Archive](#Arch_Linux_Archive)
    *   [1.4 Rebuild the package](#Rebuild_the_package)
    *   [1.5 Automation](#Automation)
*   [2 Return from [testing]](#Return_from_.5Btesting.5D)

## Return to an earlier package version

### Using the pacman cache

If a package was installed at an earlier stage, and the [pacman cache](/index.php/Pacman#Cleaning_the_package_cache "Pacman") was not cleaned, install an earlier version from `/var/cache/pacman/pkg/`.

This process will remove the current package and install the older version. Dependency changes will be handled, but [pacman](/index.php/Pacman "Pacman") will not handle version conflicts. If a library or other package needs to be downgraded with the packages, please be aware that you will have to downgrade this package yourself as well.

```
# pacman -U /var/cache/pacman/pkg/*package*-*old_version*.pkg.tar.xz

```

Once the package is reverted, temporarily add it to the [IgnorePkg section](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman") of `pacman.conf`, until the difficulty with the updated package is resolved.

### Downgrading the kernel

In case of issue with a new kernel, the Linux packages can be downgraded to the last working ones [#Using the pacman cache](#Using_the_pacman_cache). Go into the directory `/var/cache/pacman/pkg` and downgrade at least [linux](https://www.archlinux.org/packages/?name=linux), [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) and any kernel modules. For example:

```
# pacman -U linux-4.15.8-1-x86_64.pkg.tar.xz linux-headers-4.15.8-1-x86_64.pkg.tar.xz virtualbox-host-modules-arch-5.2.8-4-x86_64.pkg.tar.xz

```

**Tip:** If you are unable to boot after a kernel update, you can downgrade the kernel [chrooting](/index.php/Change_root "Change root") into the system. Boot using an Arch Linux [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media") and mount the partition where your system is installed to `/mnt`. If you have `/boot` or `/var` on separate partitions, also mount them to `/mnt` (e.g. `mount /dev/sdc3 /mnt/boot`). Then *chroot* into the system using: `# arch-chroot /mnt /bin/bash` Now you can go into the *pacman* cache directory and downgrade the Linux packages using the command indicated above. Once done, exit the chroot (with `exit`) and reboot.

### Arch Linux Archive

The [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") is a daily snapshot of the [official repositories](/index.php/Official_repositories "Official repositories"). It can be used to [install a previous package version](/index.php/Arch_Linux_Archive#How_to_downgrade_one_package "Arch Linux Archive"), or [restore the system to an earlier date](/index.php/Arch_Linux_Archive#How_to_restore_all_packages_to_a_specific_date "Arch Linux Archive").

### Rebuild the package

If the package is unavailable, find the correct [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and rebuild it with [makepkg](/index.php/Makepkg "Makepkg").

For packages from the [official repositories](/index.php/Official_repositories "Official repositories"), retrieve the PKGBUILD with [ABS](/index.php/ABS "ABS") and change the software version. Alternatively, find the package on the [Packages](https://www.archlinux.org/packages) website, click "View Changes", and navigate to the desired version. The files are available through a `.tar.gz` snapshot, and via the *Tree* view.

See also [Arch Build System#Checkout an older version of a package](/index.php/Arch_Build_System#Checkout_an_older_version_of_a_package "Arch Build System").

Old AUR packages can be built by checking out an old commit in the AUR package Git repository. For pre-2015 AUR3 PKGBUILDs, see [Arch User Repository#Git repositories for AUR3 packages](/index.php/Arch_User_Repository#Git_repositories_for_AUR3_packages "Arch User Repository").

### Automation

[downgrader](https://aur.archlinux.org/packages/downgrader/) is a tool which works with libalpm, supports the pacman log and downgrading packages using [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive"), local cache and [ARM](http://repo-arm.archlinuxcn.org).

The [downgrade](https://aur.archlinux.org/packages/downgrade/) package is a Bash script to downgrade one (or multiple) packages, by using the pacman cache or the [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine"). See `man downgrade` for details.

[agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/) quickly lists/gets/installs packages from the [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive").

## Return from [testing]

See [Official repositories#Disabling testing repositories](/index.php/Official_repositories#Disabling_testing_repositories "Official repositories").