Related articles

*   [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages")

The **Arch Linux Archive** (a.k.a **ALA**), formerly known as **Arch Linux Rollback Machine** (a.k.a **ARM**), stores *official repositories snapshots*, *iso images* and *bootstrap tarballs* across time.

**You can use it to**

*   Downgrade to a previous version of one package (last version is broken, I want the previous one)
*   Restore all your packages at a precise moment (my system is broken, I want to go back 2 months ago)
*   Find a previous version of an ISO image

Packages are only kept for a few years, afterwards they are moved to the [Arch Linux Historical Archive](#Historical_Archive) on archive.org.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Location](#Location)
*   [2 Directories](#Directories)
    *   [2.1 /repos](#/repos)
    *   [2.2 /packages](#/packages)
    *   [2.3 /iso](#/iso)
*   [3 FAQ](#FAQ)
    *   [3.1 How to downgrade one package](#How_to_downgrade_one_package)
    *   [3.2 How to restore all packages to a specific date](#How_to_restore_all_packages_to_a_specific_date)
*   [4 Historical Archive](#Historical_Archive)
    *   [4.1 Finding packages in the Historical Archive](#Finding_packages_in_the_Historical_Archive)
    *   [4.2 Downloading packages from the Historical Archive](#Downloading_packages_from_the_Historical_Archive)
*   [5 History](#History)

## Location

The Arch Linux Archive is available at [https://archive.archlinux.org/](https://archive.archlinux.org/).

The [source code](https://github.com/seblu/archivetools) is also available for setting up your own mirror.

## Directories

The **Archive** is split into 3 main directories detailed below.

```
├── iso
├── packages
└── repos

```

### /repos

The [repos](https://archive.archlinux.org/repos) directory contains daily snapshots of official mirror organized by date like in the following example.

```
repos
├── 2013
│   ├── 08
│   │   └── 31
│   │       ├── community
│   │       ├── community-staging
│   │       ├── community-testing
│   │       ├── core
│   │       ├── extra
│   │       ├── gnome-unstable
│   │       ├── kde-unstable
│   │       ├── lastsync
│   │       ├── multilib
│   │       ├── multilib-staging
│   │       ├── multilib-testing
│   │       ├── pool
│   │       ├── staging
│   │       └── testing
│   ├── 09
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │   ├── 21
│   │   └── 22
│   ├── 10
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 11
│   └── 12
├── 2014
│   ├── 01
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 02
│   ├── 03
│   ├── ...
│   └── 09
│       ├── 01
│       ├── ...
│       └── 28
├── last
├── month
└── week

```

Note: The last 3 special directories (**last**, **week** and **month**) which links respectively to the last synced repository, to the last monday and to the first of the current month.

### /packages

The [packages](https://archive.archlinux.org/packages) directory contains all versions of each package with their signatures. One directory by package and package directories are grouped by their first letter.

```
├── packages
│   ├── a
│   │   ├── awesome
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz.sig
│   │   │   ├── ...
│   │   │ 
│   │   ├── ...
│   │   ├── awstats
│   │   └── axel
│   │   
│   ├── b
│   ├── ...
│   └── z

```

You can use the magic subdirectory [.all](https://archive.archlinux.org/packages/.all) to access all packages by their name. It acts as a flat directory containing all versions of every package.

```
├── packages
│   ├── .all
│   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   ├── ...
│   │   ├── zsh-5.0.2-3-i686.pkg.tar.xz
│   │   ├── zsh-5.0.2-4-i686.pkg.tar.xz
│   │   └── ...

```

You can download the full package list (there are over a hundred thousand packages) as a compressed index: [index.0.xz](https://archive.archlinux.org/packages/.all/index.0.xz).

 `$ curl https://archive.archlinux.org/packages/.all/index.0.xz | unxz` 
```
0ad-a14-1-i686
0ad-a14-1-x86_64
0ad-a14-2-i686
...
zziplib-0.13.62-1-x86_64
zziplib-0.13.62-2-i686
zziplib-0.13.62-2-x86_64
```

### /iso

The [iso](https://archive.archlinux.org/iso) directory contains official ISO images and bootstrap tarballs sorted by release date.

```
├── 2014.09.03
├── 2014.10.01
├── 2014.11.01
├── 2014.12.01
├── 2015.07.01
├── 2015.08.01
├── 2015.09.01
└── 2017.04.01
    ├── arch
    ├── archlinux-2017.04.01-x86_64.iso
    ├── archlinux-2017.04.01-x86_64.iso.sig
    ├── archlinux-2017.04.01-x86_64.iso.torrent
    ├── archlinux-bootstrap-2017.04.01-x86_64.tar.gz
    ├── archlinux-bootstrap-2017.04.01-x86_64.tar.gz.sig
    ├── md5sums.txt
    └── sha1sums.txt

```

## FAQ

### How to downgrade one package

Find the package you want under [/packages](#/packages) and let pacman fetch it for installation. For example:

```
# pacman -U https://archive.archlinux.org/packages/ ... *packagename*.pkg.tar.xz

```

Letting pacman fetch it will automatically download the package's detached *.sig* file and verify it according to `/etc/pacman.conf` settings.

Alternatively, download and install the package manually using `pacman -U`.

See also [Downgrading packages#Automation](/index.php/Downgrading_packages#Automation "Downgrading packages") for tools that simplify the process.

### How to restore all packages to a specific date

To restore all packages to their version at a specific date, let's say 30 March 2014, you have to direct [pacman](/index.php/Pacman "Pacman") to this date, by editing your `/etc/pacman.conf` and use the following server directive:

```
[core]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[extra]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[community]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

or by replacing your `/etc/pacman.d/mirrorlist` with the following content:

```
##                                                                              
## Arch Linux repository mirrorlist                                             
## Generated on 2042-01-01                                                      
##
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

Then update the database and force downgrade:

```
# pacman -Syyuu

```

**Note:** It's [not safe](/index.php/Partial_upgrades "Partial upgrades") to mix Archive and up-to-date mirrors. In case of a download failure, you will fall-back on an upstream package and you will have packages not from the same epoch in the rest of the system.

## Historical Archive

Maintaining the Arch Linux Archive consumes significant amount of resources, so old packages are cleaned up from time to time.

Before removing them, old packages are uploaded to a [dedicated collection "Arch Linux Historical Archive" on archive.org](https://archive.org/details/archlinuxarchive).

The Historical Archive does not provide a way to access a "snapshot" of Arch packages at a given point in time. However, there is a redirection on `archive.archlinux.org` so that downloads for old packages are redirected to the Historical Archive on `archive.org`. There should be no visible impact from the user side, except from the fact that `archive.org` is generally quite slow for downloading.

### Finding packages in the Historical Archive

The **Arch Linux Historical Archive** collection has an index of all packages: [https://archive.org/details/archlinuxarchive](https://archive.org/details/archlinuxarchive)

It is also possible to directly access a package by its **identifier**. The general pattern for identifiers is:

```
archlinux_pkg_<sanitized package name>

```

To obtain the **sanitized** package name, simply replace any `@`, `+` or `.` character in the package name by an underscore `_`.

For instance, the identifier for [lucene++](https://www.archlinux.org/packages/?name=lucene%2B%2B) is `archlinux_pkg_lucene__`.

You can then access the details page of a package via its identifier, for instance: [https://archive.org/details/archlinux_pkg_lucene__](https://archive.org/details/archlinux_pkg_lucene__)

It is also possible to run searches with the [archive.org Python client](https://github.com/jjjake/internetarchive):

```
$ ia search subject:"archlinux package" subject:'mysql'                                                                                       
{"identifier": "archlinux_pkg_ejabberd-mod_mysql"}                                                                                                           
{"identifier": "archlinux_pkg_ejabberd-mod_mysql-svn"}
{"identifier": "archlinux_pkg_gambas3-gb-db-mysql"}
{"identifier": "archlinux_pkg_gambas3-gb-mysql"}
{"identifier": "archlinux_pkg_libgda-mysql"}

```

### Downloading packages from the Historical Archive

All available package versions (and their signature) can be accessed via the download page of a package: [https://archive.org/download/archlinux_pkg_lucene__](https://archive.org/download/archlinux_pkg_lucene__)

To download, verify and install a package using [pacman](/index.php/Pacman "Pacman"):

```
# pacman -U https://archive.org/download/archlinux_pkg_cjdns/cjdns-16.1-3-x86_64.pkg.tar.xz

```

Package verification is controlled by pacman's `RemoteFileSigLevel` option. Note that if you use pacman, you have to figure out the dependencies yourself.

It is also possible to use the [archive.org Python client](https://github.com/jjjake/internetarchive):

```
# Download a specific version of a package
$ ia download archlinux_pkg_cjdns cjdns-16.1-3-x86_64.pkg.tar.xz{,.sig}

# Download all x86_64 versions of a package, with signatures
$ ia download archlinux_pkg_cjdns --glob="*x86_64.pkg.tar.xz*"

```

## History

*   The original ARM (*Archlinux Rollback Machine*) was closed on 2013-08-18.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360)
*   The new one is hosted on [seblu.net](http://seblu.net) since 2013-08-31.
*   New URL and closing the old ARM hierarchy on 2015-10-13\. A new software, [agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/) was introduced.
*   Moved to [archive.archlinux.org](https://archive.archlinux.org) on 2015-12-19.[[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2015-December/027635.html)
*   Old packages from 2013-2016 uploaded to [archive.org](https://archive.org/details/archlinuxarchive) on 2018-06-05.