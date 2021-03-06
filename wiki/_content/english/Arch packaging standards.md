Related articles

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

When building packages for Arch Linux, **adhere to the package guidelines** below, especially if the intention is to **contribute** a new package to Arch Linux. You should also see the [PKGBUILD](https://archlinux.org/pacman/PKGBUILD.5.html) and [makepkg](https://archlinux.org/pacman/makepkg.8.html) manpages.

## Contents

*   [1 PKGBUILD prototype](#PKGBUILD_prototype)
*   [2 Package etiquette](#Package_etiquette)
*   [3 Package naming](#Package_naming)
*   [4 Directories](#Directories)
*   [5 Makepkg duties](#Makepkg_duties)
*   [6 Architectures](#Architectures)
*   [7 Licenses](#Licenses)
*   [8 Additional guidelines](#Additional_guidelines)

## PKGBUILD prototype

```
# Maintainer: Your Name <youremail@domain.com>
pkgname=NAME
pkgver=VERSION
pkgrel=1
pkgdesc=""
arch=()
url=""
license=('GPL')
groups=()
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #autofill using updpkgsums

build() {
  cd "$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}
```

Other prototypes are found in `/usr/share/pacman` from the pacman and abs packages.

## Package etiquette

*   Packages should **never** be installed to `/usr/local`
*   **Do not introduce new variables or functions** into `PKGBUILD` build scripts, unless the package cannot be built without doing so, as these could possibly **conflict** with variables and functions used in makepkg itself.
*   If a new variable or a new function is absolutely required, **prefix its name with an underscore** (`_`), e.g. `_customvariable=` 
*   **Avoid** using `/usr/libexec/` for anything. Use `/usr/lib/$pkgname/` instead.
*   The `packager` field from the package meta file can be **customized** by the package builder by modifying the appropriate option in the `/etc/makepkg.conf` file, or alternatively override it by creating `~/.makepkg.conf`.
*   All important messages should be echoed during install using an **.install file**. For example, if a package needs extra setup to work, directions should be included.
*   **Dependencies** are the most common packaging error. Please take the time to verify them carefully, for example by running `ldd` on dynamic executables, checking tools required by scripts or looking at the documentation of the software. The [namcap](/index.php/Namcap "Namcap") utility can help you in this regard. This tool can analyze both PKGBUILD and the resulting package tarball and will warn you about bad permissions, missing dependencies, redundant dependencies, and other common mistakes.
*   Any **optional dependencies** that are not needed to run the package or have it generally function should not be included in the **depends** array; instead the information should be added to the **optdepends** array:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')

```

	The above example is taken from the **wine** package in `extra`. The optdepends information is automatically printed out on installation/upgrade so one should **not** keep this kind of information in `.install` files.

*   When creating a **package description** for a package, do not include the package name in a self-referencing way. For example, "Nedit is a text editor for X11" could be simplified to "A text editor for X11". Also try to keep the descriptions to ~80 characters or less.
*   Try to keep the **line length** in the PKGBUILD below ~100 characters.
*   Where possible, **remove empty lines** from the `PKGBUILD` (`provides`, `replaces`, etc.)
*   It is common practice to **preserve the order** of the `PKGBUILD` fields as shown above. However, this is not mandatory, as the only requirement in this context is **correct bash syntax**.
*   **Quote** variables which may contain spaces, such as `"$pkgdir"` and `"$srcdir"`.
*   To ensure the **integrity** of packages, make sure that the [integrity variables](/index.php/PKGBUILD#Integrity "PKGBUILD") contain correct values. These can be updated using the `updpkgsums` tool.

## Package naming

*   Package names can contain only alphanumeric characters and any of `@`, `.`, `_`, `+`, `-`. Names are not allowed to start with hyphens or dots. All letters should be lowercase.
*   Package names should NOT be suffixed with the upstream major release version number (e.g. we don't want libfoo2 if upstream calls it libfoo v2.3.4) in case the library and its dependencies are expected to be able to keep using the most recent library version with each respective upstream release. However, for some software or dependencies, this can not be assumed. In the past this has been especially true for widget toolkits such as GTK and Qt. Software that depends on such toolkits can usually not be trivially ported to a new major version. As such, in cases where software can not trivially keep rolling alongside its dependencies, package names should carry the major version suffix (e.g. gtk2, gtk3, qt4, qt5). For cases where most dependencies can keep rolling along the newest release but some can't (for instance closed source that needs libpng12 or similar), a deprecated version of that package might be called libfoo1 while the current version is just libfoo.
*   Package versions **should be the same as the version released by the author**. Versions can include letters if need be (eg, nmap's version is 2.54BETA32). **Version tags may not include hyphens!** Letters, numbers, and periods only.
*   Package releases are **specific to Arch Linux packages**. These allow users to differentiate between newer and older package builds. When a new package version is first released, the **release count starts at 1**. Then as fixes and optimizations are made, the package will be **re-released** to the Arch Linux public and the **release number will increment**. When a new version comes out, the release count resets to 1\. Package release tags follow the **same naming restrictions as version tags**.

## Directories

*   **Configuration files** should be placed in the `/etc` directory. If there is more than one configuration file, it is customary to **use a subdirectory** in order to keep the `/etc` area as clean as possible. Use `/etc/{pkgname}/` where `{pkgname}` is the name of the package (or a suitable alternative, eg, apache uses `/etc/httpd/`).

*   Package files should follow these **general directory guidelines**:

| `/etc` | **System-essential** configuration files |
| `/usr/bin` | Binaries |
| `/usr/lib` | Libraries |
| `/usr/include` | Header files |
| `/usr/lib/{pkg}` | Modules, plugins, etc. |
| `/usr/share/doc/{pkg}` | Application documentation |
| `/usr/share/info` | GNU Info system files |
| `/usr/share/man` | Manpages |
| `/usr/share/{pkg}` | Application data |
| `/var/lib/{pkg}` | Persistent application storage |
| `/etc/{pkg}` | Configuration files for `{pkg}` |
| `/opt/{pkg}` | Large self-contained packages |

*   Packages should not contain any of the following directories:
    *   `/bin`
    *   `/sbin`
    *   `/dev`
    *   `/home`
    *   `/srv`
    *   `/media`
    *   `/mnt`
    *   `/proc`
    *   `/root`
    *   `/selinux`
    *   `/sys`
    *   `/tmp`
    *   `/var/tmp`
    *   `/run`

## Makepkg duties

When [makepkg](/index.php/Makepkg "Makepkg") is used to build a package, it does the following automatically:

1.  Checks if package **dependencies** and **makedepends** are installed
2.  **Downloads source** files from servers
3.  **Checks the integrity** of source files
4.  **Unpacks** source files
5.  Does any necessary **patching**
6.  **Builds** the software and installs it in a fake root
7.  **Strips** symbols from binaries
8.  **Strips** debugging symbols from libraries
9.  **Compresses** manual and, or info pages
10.  Generates the **package meta file** which is included with each package
11.  **Compresses** the fake root into the package file
12.  **Stores** the package file in the configured destination directory (cwd by default)

## Architectures

The `arch` array should contain `'x86_64'` if the compiled package is architecture-specific. Otherwise, use `'any'` for architecture independent packages.

## Licenses

See [PKGBUILD#license](/index.php/PKGBUILD#license "PKGBUILD").

## Additional guidelines

Be sure to read the above guidelines first - important points are listed on this page that will not be repeated in the following guideline pages. These specific guidelines are intended as an addition to the standards listed on this page.

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Packages submitted to the AUR must additionally comply with [Arch User Repository#Rules of submission](/index.php/Arch_User_Repository#Rules_of_submission "Arch User Repository").