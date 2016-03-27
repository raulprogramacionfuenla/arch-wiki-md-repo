**翻译状态：** 本文是英文页面 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-06，点击[这里](https://wiki.archlinux.org/index.php?title=PKGBUILD&diff=0&oldid=363576)可以查看翻译后英文页面的改动。

**PKGBUILD**是一个shell脚本，包含 [Arch Linux](/index.php/Arch_Linux "Arch Linux") 在构建软件包时需要的信息。本页面讨论PKGUILD中使用的变量。若要获取PKGBUILD中函数的信息，请参考[创建软件包](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)").

Arch Linux 用 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 创建软件包。当 **makepkg** 运行时，它会在当前目录寻找 `PKGBUILD` 文件，并依照其中的指令去获取依赖文件，编译出 `pkgname.pkg.tar.xz` 文件。生成的包内有二进制文件和安装指令，可以使用 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 进行安装。

`pkgname`，`pkgver`，`pkgrel`和`arch`是必须包含的变量。`license`在构建包时并不强制要求，但若要分享 PKGBUILD文件，推荐加上该变量，否则 `makepkg` 会有警告。

一般来说，这些变量按下面的顺序出现在 PKGBUILD 文件中，但这并不是强制性的，只要使用正确的 [Bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)") 语法就行了。

## Contents

*   [1 软件包 名称变量](#.E8.BD.AF.E4.BB.B6.E5.8C.85_.E5.90.8D.E7.A7.B0.E5.8F.98.E9.87.8F)
    *   [1.1 pkgbase](#pkgbase)
    *   [1.2 pkgname](#pkgname)
*   [2 版本变量](#.E7.89.88.E6.9C.AC.E5.8F.98.E9.87.8F)
    *   [2.1 pkgver](#pkgver)
    *   [2.2 pkgrel](#pkgrel)
    *   [2.3 epoch](#epoch)
*   [3 一般变量](#.E4.B8.80.E8.88.AC.E5.8F.98.E9.87.8F)
    *   [3.1 pkgdesc](#pkgdesc)
    *   [3.2 arch](#arch)
    *   [3.3 url](#url)
    *   [3.4 license](#license)
    *   [3.5 groups](#groups)
*   [4 依赖关系变量](#.E4.BE.9D.E8.B5.96.E5.85.B3.E7.B3.BB.E5.8F.98.E9.87.8F)
    *   [4.1 depends](#depends)
    *   [4.2 optdepends](#optdepends)
    *   [4.3 makedepends](#makedepends)
    *   [4.4 checkdepends](#checkdepends)
*   [5 软件相关性](#.E8.BD.AF.E4.BB.B6.E7.9B.B8.E5.85.B3.E6.80.A7)
    *   [5.1 provides](#provides)
    *   [5.2 conflicts](#conflicts)
    *   [5.3 replaces](#replaces)
*   [6 其它变量](#.E5.85.B6.E5.AE.83.E5.8F.98.E9.87.8F)
    *   [6.1 backup](#backup)
    *   [6.2 options](#options)
    *   [6.3 install](#install)
    *   [6.4 changelog](#changelog)
*   [7 源码变量](#.E6.BA.90.E7.A0.81.E5.8F.98.E9.87.8F)
    *   [7.1 source](#source)
    *   [7.2 noextract](#noextract)
*   [8 完整性变量](#.E5.AE.8C.E6.95.B4.E6.80.A7.E5.8F.98.E9.87.8F)
    *   [8.1 md5sums](#md5sums)
    *   [8.2 sha1sums](#sha1sums)
    *   [8.3 sha256sums](#sha256sums)
    *   [8.4 sha224sums, sha384sums, sha512sums](#sha224sums.2C_sha384sums.2C_sha512sums)
    *   [8.5 validpgpkeys](#validpgpkeys)
*   [9 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 软件包 名称变量

### pkgbase

构建拆分包时，可以使用一个可选的全局参考值。pkgbase可以在 makepkg 输出和纯源代码包中指定软件包组。若该变量未被设置，则用pkgname数组的第一个元素充当。此变量不允许以下划线开头。拆分软件包中的所有变量都默认使用全局 PKGBUILD 设置的值。除了`makedepends,source variables, integrity variables`, 其他变量都可以在拆分包的 `package()` 函数中进行额外设置。

### pkgname

软件包的名称，名称由小写字母、数字和任意以下字符组成：`@ . _ + -` (at 符号, 点, 下划线, 加号, 连字符)。字母均为小写且不能以连字符开头。为了保证一致性，`pkgname` 应该匹配源文件 tar 包的名称，比如：源文件包名为 `foobar-2.5.tar.gz`，那么 `pkgname` 应该使用 `pkgname=foobar`。除此之处，`PKGBUILD` 文件所在工作目录也应该与 `pkgname` 想匹配。

拆分包中应该使用数组：`pkgname=('foo' 'bar')`.

## 版本变量

### pkgver

软件包的版本号，应该与软件原作者发布的版本号一致。它由字母、数字和'.'组成，但*不能*包含连字符'-'，如果原作者在他的版本号中使用了连字符'-'，那么用下划线'_'来替代。举个例子：原版本号“0.99-10”，改写成“0.99_10”。在之后的 PKGBUILD 指令中 `pkgver` 中的下划线可以用下面这个方法替代为连接符：

```
source=("$pkgname-${pkgver//_/-}.tar.gz")

```

**注意:** 如果上游使用时间戳格式的版本，例如 *05102014*，请修改为年份在前的格式 *20141005* (ISO 8601). 否则新版本判断会失效。

**Tip:** 在 PKGBUILD 中定义`pkgver()`，[makepkg](/index.php/Makepkg "Makepkg") 就可以自动 [更新](http://allanmcrae.com/2013/04/pacman-4-1-released/) 此变量。详情参阅 [VCS_package_guidelines#The pkgver() 函数](/index.php/VCS_package_guidelines#The_pkgver.28.29_.E5.87.BD.E6.95.B0 "VCS package guidelines").

### pkgrel

这个值用来区分同一版本软件的多次构建。当软件包随着 `PKGBUILD` 的调整与优化变化时，**释出号**递增 1。

而当这个软件包发布一个新版本时，释出号重置为 1。

### epoch

**注意:** 若非必要，不要使用此变量

当一个软件的版本编号方式改变，打破正常的版本比较逻辑时, 使用此数值进行强制升级。只要此数值比安装的版本大，就会视作新版本进行升级。更多信息参见[pacman(8)](https://www.archlinux.org/pacman/pacman.8.html)。

示例：

```
pkgver=5.13
pkgrel=2
epoch=1
```
 `1:5.13-2` 

## 一般变量

### pkgdesc

软件包描述，建议最多80个字符，不要重复软件的名字，除非软件包名和程序名不相同。合理使用关键字以方便搜索。

比如："Nedit is a text editor for X11"应该写成"A text editor for X11"。

### arch

主机架构数组。当前，它应该包含 `i686`、`x86_64` 或`any`. `arch=('i686' 'x86_64')`。

在构建过程中，甚至是定义其它变量时都可以使用变量 `$CARCH` 来取得当前主机架构。

### url

软件官方站点的网址

### license

软件发布许可证。软件包仓库 `[core]` 中的 [licenses](https://www.archlinux.org/packages/?name=licenses) 包存放了通用的许可证协议，安装后能在 `/usr/share/licenses/common` 中找到这些许可证协议，比如 `/usr/share/licenses/common/GPL`。如果软件包是发布在这些许可证中的任何一个，这个值应该被设定成许可证的目录名，比如：`license=('GPL')`。如果软件包中没有适用的许可证，可以按下的方法执行：

1.  许可证安装到： `/usr/share/licenses/**pkgname**/` 目录下，例如：`/usr/share/licenses/foobar/LICENSE`。
2.  如果许可证的内容仅保存在网站上，那么你需要单独保存一个版本。
3.  把 `custom` 添加到 `license` 列表。或者你可以用 `custom:name of license` 替代 `custom`。一旦某个许可证被官方仓库用于两个以上软件包（包括 `[community]`），它将成为 [licenses](https://www.archlinux.org/packages/?name=licenses) 的一个组成部分。

*   [BSD](https://en.wikipedia.org/wiki/BSD_License "wikipedia:BSD License")、[MIT](https://en.wikipedia.org/wiki/MIT_License "wikipedia:MIT License")、[zlib/png](https://en.wikipedia.org/wiki/ZLIB_license "wikipedia:ZLIB license") 和 [Python](https://en.wikipedia.org/wiki/Python_License "wikipedia:Python License") 是几个例外的情况，它们不能加入 [licenses](https://www.archlinux.org/packages/?name=licenses) 包。在 `license` 列表中还是把它们当成通用协议来对待(`license=('BSD')`, `license=('MIT')`, `license=('ZLIB')` and `license=('Python')`)，但是实际上它们都是私有协议，因为它们都包括了各自的版权条款。任何发布于这四个许可协议的软件包都应该在 `/usr/share/licenses/**pkgname**` 存放它们独有的许可证文件。一些软件包可能不止一个许可证，这种情况下，在 `license` 列表中置入多个值，像`license=('GPL' 'custom:name of license')`。
*   另外，(L)GPL 拥有多个版本。对那个 (L)GPL 软件，约定如下：
    *   (L)GPL - 指代 (L)GPLv2 或之后的任意版本
    *   (L)GPL2 - 仅 (L)GPL2
    *   (L)GPL3 - 指代 (L)GPL3 或之后的任意版本
*   如果最终无法决定使用哪种许可证，[PKGBUILD.proto](https://projects.archlinux.org/pacman.git/tree/proto/PKGBUILD.proto) 建议使用 `unknown`。这种情况下应该联系上游的软件发布者。

**小贴士:** 有些软件作者没有提供单独的版权文件，而是在 ReadMe.txt 中声明。可以在 `build` 阶段将这些声明提取为单独文件：`sed -n '/**This software**/,/ **thereof.**/p' ReadMe.txt > LICENSE`.

### groups

软件包所在的组。例如：当你安装 [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/)，它会安装属于 [kde](https://www.archlinux.org/groups/x86_64/kde/) 组里的所有包。

## 依赖关系变量

**注意:** 架构相关的变量可以通过下划线加架构的方式指定：`depends_x86_64=()`, `optdepends_x86_64=()`.

### depends

软件的运行时依赖列表。可以使用比较运算符来描述版本限制，如：`depends=('foobar>=1.8.0')`。如有多重限制，你可以重复设置它们[[1]](https://mailman.archlinux.org/pipermail/arch-general/2012-July/029022.html)，像这样：`depends=('foobar>=1.8.0' 'foobar<2.0.0')`

不需要列出你的软件包的二次依赖，比如说：[gtk2](https://www.archlinux.org/packages/?name=gtk2)依赖[glib2](https://www.archlinux.org/packages/?name=glib2)和[glibc](https://www.archlinux.org/packages/?name=glibc)；然而[glib2](https://www.archlinux.org/packages/?name=glib2)本就依赖于[glibc](https://www.archlinux.org/packages/?name=glibc)，那么在[gtk2](https://www.archlinux.org/packages/?name=gtk2)中就不需要把[glibc](https://www.archlinux.org/packages/?name=glibc)加入 depends 列表。

### optdepends

一组不影响软件主要功能，但能提供额外特性的软件包。应该简要说明每个包所能提供的额外功能。有些可选依赖如果不安装，软件包的个别程序可能无法正常使用。

`optdepends`看起来像这样：

```
optdepends=(
  'cups: printing support'
  'sane: scanners support'
  'libgphoto2: digital cameras support'
  'alsa-lib: sound support'
  'giflib: GIF images support'
  'libjpeg: JPEG images support'
  'libpng: PNG images support'
)

```

### makedepends

仅在软件编译时需要的软件包列表。可以像`depends`序列里提到的一样指定最小版本依赖。

在使用makepkg构建软件包时，[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)组被视为已安装。该组的成员**不应该**出现在`makedepends`列表中。用下面程序查看一个依赖关系是否已经包含在 base-devel 中：

```
$ pacman -Si $(pactree -rl *package*) 2>/dev/null | grep -q "^Groups *:.*base-devel"

```

### checkdepends

运行测试组件时需要，而运行时不需要的包列表。该列表中的包遵循和`depends`相同的格式。这些依赖只在[check()](/index.php/Creating_packages#The_check.28.29_function "Creating packages")函数存在且被makepkg运行时被考虑。

**注意:** 在使用makepkg构建软件包时，[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)组被视为已安装。该组的成员**不应该**出现在`checkdepends`列表中。

## 软件相关性

**注意:** 架构相关的变量可以通过下划线加架构的方式指定：`provides_x86_64=()`, `conflicts_x86_64=()`.

### provides

这个变量说明当前包能提供的功能（或者像 cron、sh 这样的虚拟包）。只要没有标记为 conflicts，提供相同功能的软件包可以同时安装，

如果你使用这个变量，应当加上所替代软件的版本号（`pkgver`，可能的话还有`pkgrel`）。举例来说，如果你提供一个修改过的 *qt* 包其版本号为 3.3.8，命名为 *qt-foobar*，那么 `provides` 应该写成 `provides=('qt=3.3.8')`。只写成 `provides=('qt')` 会使对 *qt* 有版本依赖的包编译失败。不要把 `pkgname` 加入 provides 序列，它会自动完成的。

### conflicts

与当前软件包发生冲突的包列表。安装此软件时，所有有冲突的软件都会被删除。可以像 depends 那样指定冲突包的版本号。

### replaces

会因安装当前包而取代的包列表，比如：[wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk)中的`replaces=('wireshark')`。`pacman -Sy` 同步软件数据库后，会立刻用软件库中的另一个包替换掉 `replaces`中已安装的包。如果你只是提供已存在包的一个替代品，或者上传到 [AUR](/index.php/AUR "AUR"), 使用`conflicts`和`provides`变量——它们仅在安装冲突包时被检查。

## 其它变量

### backup

当包被升级或卸载时，应当备份的文件（的名字）。这些文件一般是用户会更改的文件，如（主要是）放置在`/etc`中的配置文件。

列表中的文件应该使用相对路径(如 `etc/pacman.conf`)，而不是绝对路径(如 `/etc/pacman.conf`)。

在升级时，新版本会被命名为`file.pacnew`以避免覆盖旧有且被用户修改过的文件。类似地，当卸载包时，用户修改过的文件会以`file.pacsave`为名而保留下来——除非用`pacman -Rn`命令卸载。

参见[Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files")获取更多信息。

### options

这个变量允许你重置`makepkg`的部分默认（定义在`/etc/makepkg.conf`中的）行为。要设置一个选项必须指定选项名。要反转一个默认行为，在选项前加上**`!`** 。 参见[PKGBUILD(5)](https://www.archlinux.org/pacman/PKGBUILD.5.html) 以获取所有可用选项。

### install

`.install` 脚本的名称, 应该和 pkgname 相同。 *pacman* 可以在安装、卸载或升级一个软件包时存储及执行一些特定的脚本。在不同的情况下，脚本会执行下面几个函数。

*   ***pre_install*** - 安装前运行的脚本，可以传递版本号为参数。
*   ***post_install*** - 安装后运行的脚本，可以传递版本号为参数。
*   ***pre_upgrade*** - 升级前运行的脚本，可以按`新版本号`，`旧版本号`的顺序传递参数。
*   ***post_upgrade*** - 升级后运行的脚本，可以按`新版本号`，`旧版本号`的顺序传递参数。
*   ***pre_remove*** - 卸载前运行的脚本，可以传递版本号为参数。
*   ***post_remove*** - 卸载后运行的脚本，可以传递版本号为参数。

每一个函数都是在 pacman 安装目录下通过 chroot 运行。参见[这个帖子](https://bbs.archlinux.org/viewtopic.php?pid=913891).

**小贴士:** 一个 `.install` 文件模板（原型）位于[/usr/share/pacman/proto.install 这里](https://projects.archlinux.org/pacman.git/plain/proto/proto.install)。

### changelog

软件包 changelog 的名称，要查看安装软件的 changelog：

```
$ pacman -Qc *pkgname*

```

## 源码变量

**注意:** 架构相关的变量可以通过下划线加架构的方式指定：`source_x86_64=()`. 记得要同时提供对应的校验和：`sha256sums_x86_64=()`

### source

构建软件包时需要的文件列表。它必须包含软件源的位置信息，大多数情况下是一个完整的 HTTP 或 FTP 地址。可以在软件源信息中很好的调用前面提到的变量 `pkgname` 和 `pkgver`(如 `source=("https://example.com/$pkgname-$pkgver.tar.gz")`)。

文件也可以放到 `PKGBUILD` 相同目录中，把文件名添加到这个列表中，以相对 `PKGBUILD` 的路径记录。在实际的编译过程开始之前，所有该列表中引用的文件都会被下载或检查是否存在，如果有文件丢失 `makepkg` 就不会继续。

**小贴士:** 你可以为下载的文件指定不同的文件名（如将下载的文件出于某些原因有不同的文件名，像 URL 有一个 GET 参数时）。使用如下语法：`*filename*::*fileuri*`。

例如：

`$pkgname-$pkgver.zip::http://199.91.152.193/7pd0l2tpkidg/jg2e1cynwii/Warez_collection_16.4.exe`

### noextract

一些列举于 `source` 中，但不需要在运行`makepkg`时解包的文件。在碰到不能被`/usr/bin/bsdtar`处理的文件或不需要解压的文件时使用。在这些情况下，额外的解包工具（如`unzip`、`p7zip`，[lrzip](https://www.archlinux.org/packages/?name=lrzip)等）应该加入 `makedepends` 序列，并且用[prepare()](/index.php/Creating_packages#The_prepare.28.29_function "Creating packages")函数手动解包。例如：

```
  prepare() {
  lrzip -d *source*.tar.lrz
}

```

注意当 `source` 是一些 URL 时，`noextract` **仅仅**取文件名部分：

```
source=("https://ftp.archlinux.org/other/grub2/grub2_extras_lua_r20.tar.xz")
noextract=('grub2_extras_lua_r20.tar.xz')

```

不提取任何东西时，可以像这样：

```
noextract=("${source[@]%%::*}")

```

## 完整性变量

*   *碰撞漏洞* 意味着不同的内容可以产生相同的校验和。
*   *Preimage 漏洞* 意味着已知校验和的情况下，可以生成一段字符串产生相同的校验和。

| 算法 | 碰撞漏洞 | Preimage 漏洞 |
| MD5 | 严重. | 理论可行. |
| SHA-1 | 理论可行. | 未发现. |
| SHA-2 | 未发现. | 未发现. |

### md5sums

`source` 列表文件中的 128 位 MD5 校验和。

*   MD5 算法已被发现有 [碰撞漏洞](https://en.wikipedia.org/wiki/MD5 "wikipedia:MD5")。2 = 2.6 × 10 次运算就可以破解，一般的机器上只需要不到一秒。
*   理论上通过 2 ≈ 1.4 × 10 次计算可以进行 Preimage。

### sha1sums

`source` 列表文件中 SHA-1 160位校验和。

**注意:** SHA-1算法已被发现有漏洞。

### sha256sums

256 位 SHA-2 校验和，目前未发现明显漏洞。一旦 `source` 序列中的所有文件都存在了，每个文件的 SHA-2 校验和会自动的计算出来，并与对应 `source` 列表位置的值进行比较。在包含 `PKGBUILD` 文件的目录中，使用指令 `updpkgsums` 可以生成 MD5 序列。

为了启用自动校验和生成，请在 `/etc/makepkg.conf` 设置 `INTEGRITY_CHECK` 选项。参见 [makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html).

### sha224sums, sha384sums, sha512sums

SHA-2 校验和列表，有224，384 和 512位。它们都可以替代上述的 `sha256sums`，并且有更少的已知弱点。

### validpgpkeys

PGP 指纹列表。如果使用，*makepkg* 仅接受这里定义的签名，并且忽略密钥环中的值。如果源代码用子密钥加密，*makepkg* 会使用主键进行比较。

仅接受完整签名，必须是大写字母而且不能有空白字符。

## 更多信息

*   [PKGBUILD(5) 手册页](https://www.archlinux.org/pacman/PKGBUILD.5.html)
*   [PKGBUILD 示例](http://ix.io/66p)