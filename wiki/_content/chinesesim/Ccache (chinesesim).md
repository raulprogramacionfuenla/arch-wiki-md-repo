**翻译状态：** 本文是英文页面 [Ccache](/index.php/Ccache "Ccache") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-27，点击[这里](https://wiki.archlinux.org/index.php?title=Ccache&diff=0&oldid=485957)可以查看翻译后英文页面的改动。

[Ccache](http://ccache.samba.org) 是一个编译工具，可以加速 gcc 对同一个程序的多次编译。尽管第一次编译会花费长一点的时间，有了`ccache`，后续的编译将变得非常非常快。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 为 makepkg 启用 ccache](#.E4.B8.BA_makepkg_.E5.90.AF.E7.94.A8_ccache)
    *   [2.2 启用命令行](#.E5.90.AF.E7.94.A8.E5.91.BD.E4.BB.A4.E8.A1.8C)
    *   [2.3 启用 colorgcc 支持](#.E5.90.AF.E7.94.A8_colorgcc_.E6.94.AF.E6.8C.81)
*   [3 Misc](#Misc)
    *   [3.1 修改缓存目录](#.E4.BF.AE.E6.94.B9.E7.BC.93.E5.AD.98.E7.9B.AE.E5.BD.95)
    *   [3.2 设置最大缓存大小](#.E8.AE.BE.E7.BD.AE.E6.9C.80.E5.A4.A7.E7.BC.93.E5.AD.98.E5.A4.A7.E5.B0.8F)
    *   [3.3 CLI](#CLI)
    *   [3.4 makechrootpkg](#makechrootpkg)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/Pacman "Pacman") 位于 [官方软件仓库](/index.php/Official_repositories "Official repositories") 的 [ccache](https://www.archlinux.org/packages/?name=ccache) 软件包。

## 配置

可以用配置文件修改默认行为，优先级由高到低为:

1.  环境变量
2.  单个 Cache 的配置文件(`$HOME/.ccache/ccache.conf`)
3.  系统配置文件 (`/etc/ccache.conf`)

### 为 makepkg 启用 ccache

要在 makepkg 启用 ccache，请编辑 `/etc/makepkg.conf`. 在 `BUILDENV` 中删除 ccache 前的感叹号：

```
 BUILDENV=(fakeroot !distcc color ccache !xdelta)

```

**Note:** 如果要编译 KDE ，需要不要导出 CPP 而是导出 CXX — 这将会避免一些错误。

### 启用命令行

如果从命令行编译而不是生成软件包，也可以使用`ccache`提高速度。

先修改 `$PATH`，添加`ccache`所在路径。

```
export PATH="/usr/lib/ccache/bin/:$PATH"

```

可以将其加入 `~/.bashrc`，这样以后可以一直使用。

如果使用此 PATH，makepkg 也会启用 ccache。

### 启用 colorgcc 支持

colorgcc 也是一个编译器外壳，所以需要确保外壳的调用顺序是正确的。

```
export PATH="/usr/lib/colorgcc/bin/:$PATH"    # As per usual colorgcc installation, leave unchanged (don't add ccache)
export CCACHE_PATH="/usr/bin"                 # Tell ccache to only use compilers here

```

colorgcc 需要调用 ccache 而不是真正的编译器。编辑`/etc/colorgcc/colorgccrc` 修改所有`/usr/bin` 路径为`/usr/lib/ccache/bin`：

 `/etc/colorgcc/colorgccrc` 
```
g++: /usr/lib/ccache/bin/g++
gcc: /usr/lib/ccache/bin/gcc
c++: /usr/lib/ccache/bin/g++
cc: /usr/lib/ccache/bin/gcc
g77:/usr/bin/g77
f77:/usr/bin/g77
gcj:/usr/bin/gcj
```

## Misc

### 修改缓存目录

可以将缓存目录 `~/.ccache` 配置到其它地方，例如 SSD 或 [ramdisk](/index.php/Ramdisk "Ramdisk"):

要在修改当前 shell 的缓存目录：

```
$ export CCACHE_DIR=/ramdisk/ccache

```

要修改默认缓存目录：

 `/home/*user*/.ccache/ccache.conf`  `cache_dir = /ramdisk/ccache` 

### 设置最大缓存大小

默认值是 5G，可以通过配置修改：

 `/home/<user>/.ccache/ccache.conf`  `max_size = 2.0G` 

### CLI

此外可以使用 ccache 命令行工具。

显示统计数据:

```
$ ccache -s

```

清空缓存:

```
$ ccache -C

```

### makechrootpkg

makechrootpkg 也可以使用 ccache，要在清理 chroot 后保留缓存，可以使用 makechrootpkg 的 `-d` 选项将 cache 目录从普通系统绑定到 chroot:

```
$ mkdir /path/of/chroot/ccache

```

```
$ makechrootpkg -d /path/to/cache/:/ccache -r /path/of/chroot -- CCACHE_DIR=/ccache

```

这样 chroot 中就可以和正常系统中一样配置和使用 ccache.

## 参阅

*   [ccache 手册](http://ccache.samba.org/manual.html)