[SystemTap](http://sourceware.org/systemtap/) provides free software (GPL) infrastructure to simplify the gathering of information about the running Linux system.

## Contents

*   [1 SystemTap](#SystemTap)
*   [2 Standard kernel](#Standard_kernel)
*   [3 Kernel rebuild](#Kernel_rebuild)
    *   [3.1 Prepare](#Prepare)
    *   [3.2 modify config](#modify_config)
    *   [3.3 Update checksum](#Update_checksum)
    *   [3.4 Build and Install](#Build_and_Install)
*   [4 Build custom kernel](#Build_custom_kernel)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Pass 4 fails when launching](#Pass_4_fails_when_launching)
    *   [5.2 System.map is missing](#System.map_is_missing)
    *   [5.3 Process return probes not available](#Process_return_probes_not_available)

## SystemTap

Simply install [systemtap](https://aur.archlinux.org/packages/systemtap/) or [systemtap-git](https://aur.archlinux.org/packages/systemtap-git/), all done. Compare it to the most recent upstream release at [[1]](https://sourceware.org/systemtap/wiki/SystemTapReleases).

Consider also building it from sources at [[2]](https://sourceware.org/git/?p=systemtap.git;a=summary), where support for newer kernels or distros makes first appearance.

## Standard kernel

You will need at least the [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) package installed.

Because Arch permanently strips debugging data from its distributed binaries (including the kernel), many normal/fancier systemtap capabilities are simply not available, so many examples at */usr/share/doc/systemtap/examples* will not work. However, see the [stapprobes man page](https://sourceware.org/systemtap/man/stapprobes.3stap.html) for the NON-DWARF and AUTO-DWARF probe types for what should still work, for example:

*   kernel tracepoints: kernel.trace("*")
*   user-space probes: process("...").function("...") (for programs you build yourself with -g)
*   user-space markers: process("...").mark("...") (if they were configured with the *<sys/sdt.h>* markers)
*   perfctr-based probes: perf.*
*   non-dwarf kernel probes: kprobe.function("...") and nd_syscall.* tapset (if a /boot/System.map* file is available, see below).

## Kernel rebuild

You may consider to build a *linux-custom* package to run SystemTap, but rebuilding the original [linux](https://www.archlinux.org/packages/?name=linux) package is easy and efficient. See also [Kernels/Traditional compilation](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation").

### Prepare

First, run `cd ~/ && mkdir build && cd build/ && asp checkout linux && cd linux/trunk` to get the original kernel build files. Then use `makepkg --verifysource` to get the additional files. By performing the verification, you can safely **skip** the steps on "Update checksum".

### modify config

Edit **config** (for 32-bit systems) or **config.x86_64** (for 64-bit systems), turn on these options:

*   CONFIG_KPROBES=y
*   CONFIG_KPROBES_SANITY_TEST=n
*   CONFIG_KPROBE_EVENT=y
*   CONFIG_NET_DCCPPROBE=m
*   CONFIG_NET_SCTPPROBE=m
*   CONFIG_NET_TCPPROBE=y
*   CONFIG_DEBUG_INFO=y
*   CONFIG_DEBUG_INFO_REDUCED=n
*   CONFIG_X86_DECODER_SELFTEST=n
*   CONFIG_DEBUG_INFO_VTA=y

By default only *CONFIG_DEBUG_INFO* and *CONFIG_DEBUG_INFO_REDUCED* are not set.

With current core/linux (tested with 3.15.2) you can simply append these lines into config.[x86_64]:

 `x86_64` 
```

echo '
CONFIG_DEBUG_INFO=y
CONFIG_DEBUG_INFO_REDUCED=n
' >> config.x86_64

```

*Note that if you want to put these lines into a self-maintained script, do not insert any space before CONFIG_* lines.*

### Update checksum

*You can safely skip this step if you believe the source files are correct*.

Run `sha256sum config[.x86_64]` to get a new sha256sum.

In **PKGBUILD** file, the `sha256sum=('sum-of-first' ... 'sum-of-last')` has the same order with `source=('first-source' ... 'last-source')`, put your new sha256sum in the right place.

### Build and Install

Optional: It is recommended to set `MAKEFLAGS="-j16"` in `/etc/makepkg.conf` to speed up the compilation.

You will need about 12 GB disk space for this build. Consider using an in-memory tmpfs if you have large DRAM. Run `makepkg` or `makepkg --skipchecksums` to compile, then simply `sudo pacman -U *.pkg.tar.gz` to install the packages. **pacman** will tell you **reinstall**, and you should say y.

[linux](https://www.archlinux.org/packages/?name=linux) and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) should be reinstalled, [linux-docs](https://www.archlinux.org/packages/?name=linux-docs) does not matter.

Via this method, external modules (e.g. [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [virtualbox](https://www.archlinux.org/packages/?name=virtualbox)) do not need to be rebuilt.

## Build custom kernel

Please reference this [README](http://sourceware.org/git/?p=systemtap.git;a=blob_plain;f=README;hb=HEAD)

## Troubleshooting

### Pass 4 fails when launching

If you have:

```
   /usr/share/systemtap/runtime/stat.c:214:2: error: 'cpu_possible_map' undeclared (first use in this function)

```

Try to install systemtap-git package

### System.map is missing

You can recover it where you build your linux kernel with DEBUG_INFO enabled

```
   cp src/linux-3.6/System.map /boot/System.map-3.6.7-1-ARCH

```

Alternately,

```
   sudo cp /proc/kallsyms /boot/System.map-`uname -r`

```

### Process return probes not available

If you are sure that your kernel configuration is correct, but on launching `stap` you get **both** of the following messages:

```
   WARNING: Kernel function symbol table missing [man warning::symbols]

```

```
   semantic error: process return probes not available [man error::inode-uprobes]

```

then SystemTap may have failed to verify support for this feature. You can fix this by following the steps in [System.map is missing](#System.map_is_missing).