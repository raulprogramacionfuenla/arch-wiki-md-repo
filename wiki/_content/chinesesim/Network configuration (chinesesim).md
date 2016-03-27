**翻译状态：** 本文是英文页面 [Network_configuration](/index.php/Network_configuration "Network configuration") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-19，点击[这里](https://wiki.archlinux.org/index.php?title=Network_configuration&diff=0&oldid=424907)可以查看翻译后英文页面的改动。

本页解释了如何配置 **有线** 网络连接。如果你需要设置 **无线** 网络，参见[无线配置](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)")页面。

## Contents

*   [1 检查连接](#.E6.A3.80.E6.9F.A5.E8.BF.9E.E6.8E.A5)
*   [2 设置计算机名](#.E8.AE.BE.E7.BD.AE.E8.AE.A1.E7.AE.97.E6.9C.BA.E5.90.8D)
*   [3 设备驱动程序](#.E8.AE.BE.E5.A4.87.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F)
    *   [3.1 检测驱动状态](#.E6.A3.80.E6.B5.8B.E9.A9.B1.E5.8A.A8.E7.8A.B6.E6.80.81)
    *   [3.2 加载设备模块](#.E5.8A.A0.E8.BD.BD.E8.AE.BE.E5.A4.87.E6.A8.A1.E5.9D.97)
*   [4 网络接口](#.E7.BD.91.E7.BB.9C.E6.8E.A5.E5.8F.A3)
    *   [4.1 设备名称](#.E8.AE.BE.E5.A4.87.E5.90.8D.E7.A7.B0)
    *   [4.2 获取当前网络名](#.E8.8E.B7.E5.8F.96.E5.BD.93.E5.89.8D.E7.BD.91.E7.BB.9C.E5.90.8D)
        *   [4.2.1 更改设备名称](#.E6.9B.B4.E6.94.B9.E8.AE.BE.E5.A4.87.E5.90.8D.E7.A7.B0)
        *   [4.2.2 使用传统网络命名规则](#.E4.BD.BF.E7.94.A8.E4.BC.A0.E7.BB.9F.E7.BD.91.E7.BB.9C.E5.91.BD.E5.90.8D.E8.A7.84.E5.88.99)
    *   [4.3 设定设备的 MTU 和队列长度](#.E8.AE.BE.E5.AE.9A.E8.AE.BE.E5.A4.87.E7.9A.84_MTU_.E5.92.8C.E9.98.9F.E5.88.97.E9.95.BF.E5.BA.A6)
    *   [4.4 启用和禁用网络接口](#.E5.90.AF.E7.94.A8.E5.92.8C.E7.A6.81.E7.94.A8.E7.BD.91.E7.BB.9C.E6.8E.A5.E5.8F.A3)
*   [5 配置 IP 地址](#.E9.85.8D.E7.BD.AE_IP_.E5.9C.B0.E5.9D.80)
    *   [5.1 动态 IP 地址](#.E5.8A.A8.E6.80.81_IP_.E5.9C.B0.E5.9D.80)
        *   [5.1.1 systemd-networkd](#systemd-networkd)
        *   [5.1.2 dhcpcd](#dhcpcd)
        *   [5.1.3 netctl](#netctl)
    *   [5.2 静态 IP 地址](#.E9.9D.99.E6.80.81_IP_.E5.9C.B0.E5.9D.80)
        *   [5.2.1 netctl](#netctl_2)
        *   [5.2.2 systemd-networkd](#systemd-networkd_2)
        *   [5.2.3 dhcpcd](#dhcpcd_2)
        *   [5.2.4 手动指定](#.E6.89.8B.E5.8A.A8.E6.8C.87.E5.AE.9A)
        *   [5.2.5 计算地址](#.E8.AE.A1.E7.AE.97.E5.9C.B0.E5.9D.80)
*   [6 更多设置](#.E6.9B.B4.E5.A4.9A.E8.AE.BE.E7.BD.AE)
    *   [6.1 笔记本电脑使用 Ifplugd](#.E7.AC.94.E8.AE.B0.E6.9C.AC.E7.94.B5.E8.84.91.E4.BD.BF.E7.94.A8_Ifplugd)
    *   [6.2 绑定和链路聚合](#.E7.BB.91.E5.AE.9A.E5.92.8C.E9.93.BE.E8.B7.AF.E8.81.9A.E5.90.88)
    *   [6.3 IP 别名](#IP_.E5.88.AB.E5.90.8D)
    *   [6.4 更改 MAC/硬件地址](#.E6.9B.B4.E6.94.B9_MAC.2F.E7.A1.AC.E4.BB.B6.E5.9C.B0.E5.9D.80)
    *   [6.5 共享网络连接](#.E5.85.B1.E4.BA.AB.E7.BD.91.E7.BB.9C.E8.BF.9E.E6.8E.A5)
    *   [6.6 路由配置](#.E8.B7.AF.E7.94.B1.E9.85.8D.E7.BD.AE)
    *   [6.7 局域网主机的名称解析](#.E5.B1.80.E5.9F.9F.E7.BD.91.E4.B8.BB.E6.9C.BA.E7.9A.84.E5.90.8D.E7.A7.B0.E8.A7.A3.E6.9E.90)
*   [7 疑难排解](#.E7.96.91.E9.9A.BE.E6.8E.92.E8.A7.A3)
    *   [7.1 更换了连接cable modem的计算机](#.E6.9B.B4.E6.8D.A2.E4.BA.86.E8.BF.9E.E6.8E.A5cable_modem.E7.9A.84.E8.AE.A1.E7.AE.97.E6.9C.BA)
    *   [7.2 TCP窗口扩缩（window scaling）故障](#TCP.E7.AA.97.E5.8F.A3.E6.89.A9.E7.BC.A9.EF.BC.88window_scaling.EF.BC.89.E6.95.85.E9.9A.9C)
        *   [7.2.1 如何诊断故障](#.E5.A6.82.E4.BD.95.E8.AF.8A.E6.96.AD.E6.95.85.E9.9A.9C)
        *   [7.2.2 如何修复（糟糕的方法）](#.E5.A6.82.E4.BD.95.E4.BF.AE.E5.A4.8D.EF.BC.88.E7.B3.9F.E7.B3.95.E7.9A.84.E6.96.B9.E6.B3.95.EF.BC.89)
        *   [7.2.3 如何修复（好点的方法）](#.E5.A6.82.E4.BD.95.E4.BF.AE.E5.A4.8D.EF.BC.88.E5.A5.BD.E7.82.B9.E7.9A.84.E6.96.B9.E6.B3.95.EF.BC.89)
        *   [7.2.4 如何修复（最佳的方法）](#.E5.A6.82.E4.BD.95.E4.BF.AE.E5.A4.8D.EF.BC.88.E6.9C.80.E4.BD.B3.E7.9A.84.E6.96.B9.E6.B3.95.EF.BC.89)
        *   [7.2.5 更多](#.E6.9B.B4.E5.A4.9A)
    *   [7.3 Realtek 没有连接/网络唤醒故障](#Realtek_.E6.B2.A1.E6.9C.89.E8.BF.9E.E6.8E.A5.2F.E7.BD.91.E7.BB.9C.E5.94.A4.E9.86.92.E6.95.85.E9.9A.9C)
        *   [7.3.1 方法一 还原/变更Win驱动](#.E6.96.B9.E6.B3.95.E4.B8.80_.E8.BF.98.E5.8E.9F.2F.E5.8F.98.E6.9B.B4Win.E9.A9.B1.E5.8A.A8)
        *   [7.3.2 方法二 启动Windows驱动里的网络唤醒功能](#.E6.96.B9.E6.B3.95.E4.BA.8C_.E5.90.AF.E5.8A.A8Windows.E9.A9.B1.E5.8A.A8.E9.87.8C.E7.9A.84.E7.BD.91.E7.BB.9C.E5.94.A4.E9.86.92.E5.8A.9F.E8.83.BD)
        *   [7.3.3 方法三 更新Realtek Linux驱动](#.E6.96.B9.E6.B3.95.E4.B8.89_.E6.9B.B4.E6.96.B0Realtek_Linux.E9.A9.B1.E5.8A.A8)
        *   [7.3.4 方法四 在 BIOS/CMOS 中启用 *LAN Boot ROM*](#.E6.96.B9.E6.B3.95.E5.9B.9B_.E5.9C.A8_BIOS.2FCMOS_.E4.B8.AD.E5.90.AF.E7.94.A8_LAN_Boot_ROM)
    *   [7.4 DLink G604T/DLink G502T DNS 故障](#DLink_G604T.2FDLink_G502T_DNS_.E6.95.85.E9.9A.9C)
        *   [7.4.1 如何诊断故障](#.E5.A6.82.E4.BD.95.E8.AF.8A.E6.96.AD.E6.95.85.E9.9A.9C_2)
        *   [7.4.2 如何修复](#.E5.A6.82.E4.BD.95.E4.BF.AE.E5.A4.8D)
        *   [7.4.3 更多](#.E6.9B.B4.E5.A4.9A_2)
    *   [7.5 检查 DHCP 问题先释放 IP 地址](#.E6.A3.80.E6.9F.A5_DHCP_.E9.97.AE.E9.A2.98.E5.85.88.E9.87.8A.E6.94.BE_IP_.E5.9C.B0.E5.9D.80)
    *   [7.6 Atheros AR8161 没有 eth0](#Atheros_AR8161_.E6.B2.A1.E6.9C.89_eth0)
    *   [7.7 Atheros AR9485 没有 eth0](#Atheros_AR9485_.E6.B2.A1.E6.9C.89_eth0)
    *   [7.8 待机后未接线缆 / 无连接](#.E5.BE.85.E6.9C.BA.E5.90.8E.E6.9C.AA.E6.8E.A5.E7.BA.BF.E7.BC.86_.2F_.E6.97.A0.E8.BF.9E.E6.8E.A5)
    *   [7.9 Broadcom BCM57780](#Broadcom_BCM57780)

## 检查连接

基本的安装过程已经创建了正确的网络配置。通过*ping*检查：

 `$ ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=50 time=437 ms

```

成功时会收到类似上面的 64 bytes 信息，按 `Control-C` 可以停止ping.

**小贴士:** 参数 `-c 3` 表示执行命令 `ping` 3次 。 参见 `man ping`。

如果上面的命令说 unknown hosts，意思是你的机器无法进行域名解析。这可能和你的服务提供商或者你的路由器/网关有关。你可以尝试 ping `8.8.8.8` 来验证你的电脑是否能访问 Internet。它是 Google 的主 DNS 服务器，因此它可以视为可信的，通常不会被过滤系统或代理屏蔽。

 `$ ping -c 3 8.8.8.8` 
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_req=1 ttl=53 time=52.9 ms

```

如果可以 ping `8.8.8.8` 但是不能 ping `www.google.com`, 参考 [resolv.conf](/index.php/Resolv.conf "Resolv.conf") 检查 DNS 配置。还需要查下 `/etc/nsswitch.conf` 中的 `hosts` 行。如果不能 ping 通，请检查网线问题。

## 设置计算机名

[主机名](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname") 是一个网络中唯一标识一台机器的名称。主机名通过文件 `/etc/hostname` 进行配置。这样设置主机名：

```
# hostnamectl set-hostname **myhostname**

```

这将会把 **myhostname** 写入 `/etc/hostname`。详情参见 `man 5 hostname` 和 `man 1 hostnamectl`。

建议同时在 `/etc/hosts` 中设置 hostname：

 `/etc/hosts` 
```
#
# /etc/hosts: static lookup table for host names
#

#<ip-address>	<hostname.domain.org>	<hostname>
127.0.0.1	localhost.localdomain	localhost	 *myhostname*
::1		localhost.localdomain	localhost	 *myhostname*
```

**注意:** [systemd](https://www.archlinux.org/packages/?name=systemd) 通过 `myhostname` nss 模块(在 `/etc/nsswitch.conf` 中默认启用)进行主机名解析，所以大部分情况下都不需要在 `/etc/hosts` 中设置主机名。但是有些用户反馈如果不设置，某些依赖网络的程序会碰到延迟问题。参考 [#Local network hostname resolution](#Local_network_hostname_resolution)。

要临时设置主机名（直到下次重启为止），使用 [inetutils](https://www.archlinux.org/packages/?name=inetutils) 中的 `hostname` 命令：

```
# hostname *myhostname*

```

## 设备驱动程序

### 检测驱动状态

[Udev](/index.php/Udev "Udev") 会探测网卡（[NIC](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller")）并在启动时自动载入必要的模块。 检查 `lspci -v` 输出中 "Ethernet controller" （或者类似的）条目，它会告诉你哪个内核模块包含了网络设备的驱动程序。例如：

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

接下来， 用 `dmesg | grep *module_name*` 来检查是否已经加载了驱动。例如：

```
$ dmesg |grep atl1
  ...
  atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

如果驱动加载成功，就跳过下一节，否则，你需要知道您特定型号的网络设备需要哪一个模块。

### 加载设备模块

用 Google 查找芯片组需要的模块/驱动。常见的驱动模块有用于 Realtek 芯片组网卡的 `8139too`，或者用于 Sis 芯片组网卡的 `sis900`。知道要使用什么模块之后，尝试 [手动加载它](/index.php/Kernel_modules#Manual_module_handling "Kernel modules")。如果你碰到了未找到模块的错误，可能驱动没有包括在 Arch 的内核中。你可以在 [AUR](/index.php/AUR "AUR") 中搜索模块名称。

如果 udev 在引导时不能自动侦测和加载适当的模块，参见 [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules")。

## 网络接口

### 设备名称

对于有多块网卡的电脑，固定设备名称很重要。许多配置问题都是由于网络接口名称变化引起的。

[udev](/index.php/Udev "Udev") 负责给设备命名。Systemd v197 引入了[可预测的网络接口名称](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames)自动给网络设备分配静态名称，网络接口现在是以前缀 `en`（以太网）、`wl`（WLAN）、或者 `ww`（WWAN）附上一个自动生成的标识符，产生了一个类似于 `enp0s25` 的条目。在 [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") 中添加 `net.ifnames=0` 可以禁用此功能.

**注意:** 当你改变接口命名规则时，不要忘记更新所有与网络相关的配置文件和自定义的 systemd unit 文件以反映变化。特别是当你启用了 [netctl 静态配置](/index.php/Netctl#Basic_method "Netctl") 时，要运行 `netctl reenable *profile*` 来更新生成的服务文件。

### 获取当前网络名

可以通过 sysfs 或 `ip link` 找到。

 `$ ls /sys/class/net` 
```

lo eth0 eth1 firewire0

```
 `$ ip link` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:23:6f:3a brd ff:ff:ff:ff:ff:ff

```

无线设备名称也可以通过 `iw dev` 查看，请参考 [Wireless network configuration#Getting some useful information](/index.php/Wireless_network_configuration#Getting_some_useful_information "Wireless network configuration").

#### 更改设备名称

你可以用 udev-rule 手动定义名称来更改设备名称。例如：

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"

```

值得注意的两点：

*   使用这条命令来获得每张网卡的 MAC 地址：`cat /sys/class/net/**设备名**/address`
*   确保你的 udev 规则中使用小写的十六进制值，而不是大写。

**注意:** 选择静态名称时，**应该避免使用形如 "eth*X*" 或 "wlan*X*" 的名称**，因为这可能在引导时导致内核与 udev 之间的竞争状态。相反，最好用内核默认不会使用的接口名称，例如：`net0`、`net1`、`wifi0`、`wifi1`。更多细节请查看 [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) 文档。

#### 使用传统网络命名规则

如果希望使用传统的命名方法 eth0,可以通过下面方法禁用 [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames):

1.  ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

### 设定设备的 MTU 和队列长度

你可以手动定义一条 udev 规则来改变队列的 MTU（最大传输单元）和队列长度You can change the device MTU and queue length by defining manually with an udev-rule。举例来说：

 `/etc/udev/rules.d/10-network.rules` 
```
ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1480", ATTR{tx_queue_len}="2000"

```

### 启用和禁用网络接口

可以通过如下命令启用或禁用接口：

```
# ip link set eth0 up
# ip link set eth0 down

```

查看结果：

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP mode DEFAULT qlen 1000
...

```

**Note:** 如果默认路由是通过 `eth0` 建立，禁用接口同时也会删除路由，再次启用也不会自动重新建立路由，要重新建立，请参考 [#手动分配](#.E6.89.8B.E5.8A.A8.E5.88.86.E9.85.8D).

## 配置 IP 地址

有两种配置方式：通过 [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol")，或者不变的*静态*地址。

**Tip:** In addition to the methods described below one can also use a [network manager](/index.php/List_of_applications#Network_managers "List of applications"). Network managers are especially useful for dynamic network connections and wifi networking.

### 动态 IP 地址

#### systemd-networkd

一种DHCP的简单配置方法是利用systemd提供的[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")服务。参见[systemd-networkd#Basic DHCP network](/index.php/Systemd-networkd#Basic_DHCP_network "Systemd-networkd")。

#### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") is the default client in Arch Linux to setup DHCP on the installation ISO. It is a powerful tool with many configurable DHCP client options. See [dhcpcd#Running](/index.php/Dhcpcd#Running "Dhcpcd") on how to activate it for an interface.

#### netctl

[netctl](/index.php/Netctl "Netctl")是利用用户创建的profiles进行网络配置的CTI-based工具，如何创建profile参见[netctl#Example profiles](/index.php/Netctl#Example_profiles "Netctl")，激活参见[netctl#Basic method](/index.php/Netctl#Basic_method "Netctl")。

### 静态 IP 地址

不管用什么方法设置静态 IP，都需要确定：

*   静态IP地址，
*   [子网掩码](https://en.wikipedia.org/wiki/Subnetwork "wikipedia:Subnetwork")，使用 [CIDR 表示法](https://en.wikipedia.org/wiki/CIDR_notation "wikipedia:CIDR notation")
*   Subnet mask in [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing"), for example `/24` is the CIDR notation of `255.255.255.0` netmask
*   [广播地址](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address")，
*   [网关](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway")的IP地址
*   Name server (DNS) IP addresses. See also [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

如果你想配置一个内部网络，可以将你的 IP 设置成 192.168.*.* ，子网掩码设置成 255.255.255.0 ，广播地址设置成 192.168.*.255 。网关通常是 192.168.*.1 或者 192.168.*.254。

**Warning:**

*   Make sure manually assigned IP addresses do not conflict with DHCP assigned ones. See [this forum thread](http://www.raspberrypi.org/forums/viewtopic.php?f=28&t=16797)
*   在不使用路由器的情况下和一台安装 Windows 的电脑分享你的网络连接，请确保两台电脑都使用静态 IP ，否则你的局域网将会有问题。

#### netctl

To create a [netctl](/index.php/Netctl "Netctl") profile with a static IP, set the `IP=static` option as well as `Address`, `Gateway`, and `DNS`. See [netctl#Wired](/index.php/Netctl#Wired "Netctl").

#### systemd-networkd

The [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") service provided by systemd can set up a static IP using a simple configuration file. See [systemd-networkd#Wired adapter using a static IP](/index.php/Systemd-networkd#Wired_adapter_using_a_static_IP "Systemd-networkd").

#### dhcpcd

See [dhcpcd#Static profile](/index.php/Dhcpcd#Static_profile "Dhcpcd").

#### 手动指定

It is possible to manually set up a static IP using only the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package. This is a good way to test connection settings since the connection will not persist across reboots. First enable the [network interface](#Network_interfaces):

```
 # ip link set *interface* up

```

在终端中指定一个静态 IP：

```
# ip addr add *IP_address*/*subnet_mask* broadcast *broadcast_address* dev *interface*

```

如此添加你的网关（用你的网关 IP 替换）：

```
# ip route add default via <默认网关的 IP 地址>

```

例如：

```
# ip link set eth0 up
# ip addr add 192.168.1.2/24 dev eth0
# ip route add default via 192.168.1.1

```

To undo these steps (e.g. before switching to a dynamic IP), first remove any assigned IP address:

```
# ip addr flush dev *interface*

```

然后删除指定的网关：

```
# ip route flush dev *interface*

```

最后禁用接口：

1.  ip link set *interface* down

更多选项参见：`man ip`，这些命令可以用 systemd 服务自动启动，请参考[systemd units](/index.php/Systemd#Writing_unit_files "Systemd").

#### 计算地址

可以用 [ipcalc](https://www.archlinux.org/packages/?name=ipcalc) 软件包提供的 `ipcalc` 工具自动计算 IP 广播、子网掩码、主机范围等。例如通过火线连接视窗系统主机到 Arch。为了安全和网络组织，将它们分到独立的网络中，然后配置子网掩码和广播地址，网络中只有2台主机。要找出掩码和广播地址，我使用了 ipcalc，提供了它 arch firewire nic 的 IP 地址10.66.66.1，并告诉 ipcalc 要建立一个只有2台主机的网络。

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
Address:   10.66.66.1

Netmask:   255.255.255.252 = 30
Network:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet

```

## 更多设置

### 笔记本电脑使用 Ifplugd

**Tip:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 也提供了同样的功能。

[官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库") 中的 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) 是一个守护进程，当网络适配器插入的时候自动配置网络，当网络断开的时候自动取消配置（比如某些3G的usb网络适配器）。这对于笔记本电脑这样的使用移动式的网络适配器的情况很有用，因为他只会在网络实际接入的时候才会配置网络接口。另外一个可能会用得着它的情况是，你需要重启你的网络，可是你既不想重启电脑也不想在 shell 中配置。

在默认情况下，它会检查 `eth0` 设备。要更改这个设置（以及更改其他设置，比如等待时间），可以编辑 `/etc/ifplugd/ifplugd.conf`。

启用 `net-auto-wired.service` 就会在开机时启动 ifplugd，否则，你可以使用 `ifplugd@eth0.service`。

**注意:** [Netctl](/index.php/Netctl "Netctl") 软件包包含了 `netctl-ifplugd@.service`，否则你可以使用 [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) 软件包中的 `ifplugd@.service`。例如 `systemctl enable ifplugd@eth0.service`。

### 绑定和链路聚合

参见 [netctl (简体中文)#Bonding（绑定）](/index.php/Netctl_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Bonding.EF.BC.88.E7.BB.91.E5.AE.9A.EF.BC.89 "Netctl (简体中文)") 或 [Wireless bonding](/index.php/Wireless_bonding "Wireless bonding").

### IP 别名

IP 别名是指给同一个网络接口分配多个 IP 地址。这样一个网络节点可以有多个网络连接，每个实现不同的作用。Typical uses are virtual hosting of Web and FTP servers, or reorganizing servers without having to update any other machines (this is especially useful for nameservers).

要手动设置别名，可以使用 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 执行：

```
# ip addr add 192.168.2.101/24 dev eth0 label eth0:1

```

要删除别名：

```
# ip addr del 192.168.2.101/24 dev eth0:1

```

发送到一个子网的软件不会使用主别名，如果目标 IP 属于子别名，原始 IP 也会被相应设置。如果有多个网卡，可以通过 `ip route` 查看默认路由。

### 更改 MAC/硬件地址

参见 [伪造 MAC 地址](/index.php/MAC_address_spoofing "MAC address spoofing")。

### 共享网络连接

参见 [共享网络连接](/index.php/Internet_sharing "Internet sharing")。

### 路由配置

参见 [路由](/index.php/Router "Router")。

### 局域网主机的名称解析

首先需要设置好主机名。

 `$ ping *myhostname*` 
```
PING myhostname (192.168.1.2) 56(84) bytes of data.
64 bytes from myhostname (192.168.1.2): icmp_seq=1 ttl=64 time=0.043 ms
```

如果希望其他机器通过主机名访问到这台机器，可以手动修改 `/etc/hosts` 文件或通过一个服务解析此主机名。使用 systemd 时，主机名解析可以通过 `myhostname` nss 模块提供。但是并不是所有的网络服务都被支持 (例如: [[1]](https://bbs.archlinux.org/viewtopic.php?id=176761), [[2]](https://bbs.archlinux.org/viewtopic.php?id=186967))，或者其它客户端使用不同的操作系统解析主机名，这个也无法被 systemd 支持。

第一个解决方法是修改 `/etc/hosts`:

```
127.0.1.1	*myhostname*.localdomain	*myhostname*	

```

这样系统可以同时解析两个主机名:

```
$ getent hosts 
127.0.0.1       localhost
127.0.1.1       myhostname.localdomain myhostname

```

如果使用固定 IP 地址，请用 IP 地址替换 `127.0.1.1`.

还有一个方法是架设 DNS 服务器例如 [BIND](/index.php/BIND "BIND") or [Unbound](/index.php/Unbound "Unbound"), 但是这些方法有点小提大作。小的网络可以使用 [zero-configuration networking](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") 服务。有两个选择：

*   [Samba](/index.php/Samba "Samba") 通过 Microsoft's **NetBIOS** 提供主机名称解析。这只需要安装 [samba](https://www.archlinux.org/packages/?name=samba) 并启用 `nmbd.service` 服务。运行 Windows、 OS X、或者运行着 `nmbd` 的 Linux，将能找到你的机器。

*   [Avahi](/index.php/Avahi "Avahi") 通过 **zeroconf**，提供主机名称解析, 它也被称称作 Avahi 或者 Bonjour。这需要比 Samba 再稍微复杂一点的配置：详细信息参见 [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi")。运行 OS X 的电脑，或者运行着 Avahi 守护进程的 Linux，将能找到你的机器。Windows 没有内置的 Avahi 客户端或者守护进程。

## 疑难排解

### 更换了连接cable modem的计算机

许多家庭有线电视的运营商（例如加拿大最大的有线电视公司Videotron,还有中国大陆的有线电视宽带公司）都使用记录网卡MAC地址的方法将cable modem配置为只能一台计算机使用。一旦cable modem获得第一台连接它的PC的MAC地址，就不会响应任何其它MAC地址。这样如果你换了台PC（或者路由器），由于新PC（或者路由器）的MAC地址和旧的不同，就没法连接cable modem了。这时候必须复位cable modem以使它重新辨认新的PC。 你得关闭cable modem电源，然后重新打开。一旦cable modem重启并再次登录在线完毕（指示灯熄灭），重启新连接的PC以使它发起一个DHCP请求，或者手动发起DHCP请求。

如果这个方法不能奏效，你需要克隆原来机器上的MAC地址。参见 [Change MAC/hardware address](/index.php/Configuring_Network#Change_MAC.2Fhardware_address "Configuring Network")。

### TCP窗口扩缩（window scaling）故障

TCP包头有个窗口（window）值表明其它主机可以发送多少数据回来。这个值只有16个bit，也就是说窗口打消最多只有64Kb。TCP包会被缓存一段时间（得被记录），如果内存限制（过去经常是）的话，主机很容易会用完内存。

回到1992年，内存逐渐增加，[RFC 1323](http://www.faqs.org/rfcs/rfc1323.html)被发布以改善情况:窗口扩缩(Window Scaling)。所有包里的窗口值，可以被初始连接时定义的一个缩放因子（Scale Factor）所改变。

8-bit的缩放因子使得窗口可以是初始64Kb的32倍。

但是Internet上有些有故障的路由器和防火墙会将缩放因子重写为0,这导致主机之间产生误解。

Linux内核2.6.17引入了新的计算方式生成更高的缩放因子，间接的使得这些有故障的路由器和防火墙引发的后果更明显。

这导致连接缓慢甚至中断。

#### 如何诊断故障

首先，我们要明白：这个问题很怪异。在某些案例中，你根本无法使用(HTTP, FTP, ...)，而有时候，你可以连接某些主机（很少）。

当你碰到这个故障时，`dmesg`的输出正确，日志也没问题，`ip a`报告状态正常— 实际上一切都正常。

如果你无法浏览任何网站，不过你能ping通少部分主机，很可能你是遇到了这个问题。：ping使用ICMP协议所以不受TCP问题的影响。

你可以尝试使用WireShark。你也许会看到UDP和ICMP通讯成功，但是TCP通讯不成功（仅对外国主机）。

#### 如何修复（糟糕的方法）

用比较糟糕的方法修复的话，你可以修改缩放因子计算所基于的tcp_rmem值。虽然它对大部分主机有效，但并不担保一定都有效，特别是某些很远的主机。

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### 如何修复（好点的方法）

只需要禁止窗口缩放。虽然窗口缩放是个不错的TCP特性，但它也可能令人不安，特别是当你没法修改除了问题的路由器的时候。有几种方法可以禁止窗口缩放，而看来最可靠的（适用于大部分内核）将下面一行加入到你的`/etc/sysctl.d/99-sysctl.conf`中 （见 [sysctl](/index.php/Sysctl "Sysctl")）

```
net.ipv4.tcp_window_scaling = 0

```

#### 如何修复（最佳的方法）

这个故障是由有毛病的路由器/防火墙引致的，所以最好换了它。有些用户报告说那些有故障的路由是他们自己的DSL路由。

#### 更多

本段内容是基于LWN文章[TCP window scaling and broken routers](http://lwn.net/Articles/92727/)和一个Kernel Trap 文章：[Window Scaling on the Internet](http://kerneltrap.org/node/6723)。

在LKML上也有几篇相关的帖子。

### Realtek 没有连接/网络唤醒故障

使用基于Realtek 8168 8169 8101 8111芯片网卡（独立网卡和板载）的用户也许会发现这个故障，启动时网卡不可用，网卡上的连接指示灯不亮。这通常会发生在安装了Windows的双启动系统上。在windows下使用realtek官方驱动（2007年5月后的版本）会引发故障。新驱动通过在Windows关机时禁止网卡来关闭网络唤醒功能，直到下一次Windows启动前网卡都会一直不可用。通过观察连接指示灯在Windows启动前一直熄灭，而Windows关机时也会熄灭，你可以发现它。正常操作应该是只要系统一直开着，即使在POST加电过程中，连接指示灯也应该一直亮着的。这个故障也会影响其它没有安装新驱动的操作系统（例如Live CD等）。这里给出几种解决方案：

#### 方法一 还原/变更Win驱动

你可以将你的Windows网卡驱动还原回Microsoft自带的驱动（如果有的话），或者安装2007年5月份以前的Realtek官方驱动（也许在网卡附带的CD上）。

#### 方法二 启动Windows驱动里的网络唤醒功能

也许最好最快的修复方法就是改变Windows驱动里的这个设置。这个方法可以解决很多其它操作系统而不仅仅是Arch的麻烦。在Windows的设备管理器里，找到你的Realtek网卡，双击它。在“高级”标签页中，开启"wake-on-lan after shutdown"选项。

```
 例如在Windows XP里
 右键点击我的电脑-->管理-->设备管理器-->网络适配器-->双击 Realtek ... --> 高级标签页--> Wake-On-Lan After Shutdown --> 启用。

```

**注意:** 新的 Realtek Windows 驱动程序中（已测试了 2009/01/22 GIGABYTE 上的 *Realtek 8111/8169 LAN Driver v5.708.1030.2008*）可能与这里的选项稍微有点不同，像 *Shutdown Wake-On-LAN --> Enable*。似乎把它切换成 `Disable` 没有效果（你仍然可以在Windows关闭时看到连接指示灯熄灭）。一个比较不好的解决方法是引导 Windows，然后立即重启系统（执行非正常重启/关机），不给予 Windows 驱动程序关闭 LAN 的机会。连接指示灯将会保持亮着，网卡也会在 POST 之后保持可用 - 直到你再次进入 Windows 并正常关机。

#### 方法三 更新Realtek Linux驱动

可以在realtek的官方网页上找到新的Linux驱动。(没有测试过，不过相信也能解决问题）。

#### 方法四 在 BIOS/CMOS 中启用 *LAN Boot ROM*

尽管 Windows 驱动程序在系统关闭时禁用了它，但在 BIOS/CMOS 中设置 *Integrated Peripherals --> Onboard LAN Boot ROM --> Enabled*，系统启动时会重新激活 Realtek LAN 芯片。

**注意:** 这个方法多次在 GIGABYTE GA-G31M-ES2L 主板，2009/02/05 发布的 BIOS 版本 F8 上测试成功。YMMV。

### DLink G604T/DLink G502T DNS 故障

使用 DLink G604T/DLink G502T 路由器和DHCP，并且固件是 v2.00+（通常是使用 AUS 固件）的用户可能会碰到的某些程序不同解析 DNS 的问题。不幸的是，pacman 就是这些程序其中之一。故障基本上是因为路由器在某些情况下不正确地发送 DNS 给 DHCP，导致程序尝试连接 IP 地址是 1.0.0.0 的服务器，然后因超时错误而失败。

#### 如何诊断故障

最好的诊断问题方法是使用 Firefox/Konqueror/links/seamonkey，并用 wget 作为 pacman 下载工具。如果问题发生在全新安装的 Arch Linux上，那么你可能要通过 live CD 来安装 `links`。

首先，用 wget 作为 pacman下载工具，它可以提供 pacman 下载软件包时的信息。 使用你喜欢的编辑器打开 `/etc/pacman.conf` 并取消下面这行的注释（如果前面有#的话，就移除它）

```
XferCommand=/usr/bin/wget --passive-ftp -c -O %o %u

```

当你编辑 `/etc/pacman.conf` 时，检查 pacman 用来下载软件包的默认镜像。

现在用网络浏览器打开默认镜像，检查镜像确实在工作。如果它很正常，那么运行 `pacman -Syy` （否则就选取另一个正常运行的镜像，并把它设置为 pacman 的默认镜像）。如果你看到类似于下面这样的信息（注意 1.0.0.0），

```
ftp://mirror.pacific.net.au/linux/archlinux/extra/os/i686/extra.db.tar.gz                                                            
            => '/var/lib/pacman/community.db.tar.gz.part'
Resolving mirror.pacific.net.au... 1.0.0.0

```

那么你很有可能有这个问题。 1.0.0.0 表示不能解析 DNS，因此我们必须把它添加到 `/etc/resolv.conf` 中。

#### 如何修复

基本上我们需要做的就是手动地在 `/etc/resolv.conf` 文件中添加 DNS 服务器。问题是 DHCP 会在启动时自动地删除和替换这个文件，所以我们需要编辑 `/etc/conf.d/dhcpcd` 并修改标志，阻止 DHCP 这么做。

当你打开 `/etc/conf.d/dhcpcd`，你应该看见类似下面的内容：

```
DHCPCD_ARGS="-t 30 -h $HOSTNAME"

```

在参数中添加 -R 参数，即，

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

**注意:** 如果你使用的 [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) >= 4.0.2，标志 `-R` 已被弃用。请参考 [Dhcpcd](/index.php/Dhcpcd "Dhcpcd") 中关于怎样使用自定义的 `/etc/resolv.conf` 文件的信息。

保存并关闭文件；现在打开 `/etc/resolv.conf`。你应该看到一行 nameserver（最有可能是 10.1.1.1）。这是你的路由器的网关，我们需要连接它来获取你的 ISP 的 DNS 服务器。在你的浏览器地址栏中粘贴这个IP地址，并登录你的路由器。转到 DNS 部分，然后你将在 Primary DNS Server 一栏中看到一个 IP 地址；复制并粘贴它，作为一行 nameserver 放在现有网关那行的 **上面**。

例如，`/etc/resolv.conf` 应该看上去是像这样的

```
nameserver 10.1.1.1

```

如果我的主 DNS 服务器是 211.29.132.12，那么修改 `/etc/resolv.conf` 为

```
nameserver 211.29.132.12
nameserver 10.1.1.1

```

现在执行`systemctl restart dhcpcd@<interface>`重启 network 守护进程并执行 `pacman -Syy`。如果它与服务器正常地同步了，那么问题就解决了。

#### 更多

这是 whirlpool 论坛（Australian ISP community）中对这个问题的讨论并给出了相同的解决办法。

```
[http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html](http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html)

```

### 检查 DHCP 问题先释放 IP 地址

当 DHCP 获得了错误的 IP 分配就可能产生这个问题。举例来说，当两个路由器通过VPN相连，通过VPN与我相连的路由器可能分配IP地址。要修复这个问题，在终端中以 root 权限释放 IP 地址：

```
# dhcpcd -k

```

然后请求一个新的地址：

```
# dhcpcd

```

可能你必须运行这两个命令好几次。

### Atheros AR8161 没有 eth0

对于 Atheros AR8161 Gigabit 以太网卡，以太网连接不能立即使用（2013年3月的安装介质）。它需要加载模块 "alx"，但其并不存在。

你需要安装 [compat-drives](https://backports.wiki.kernel.org/index.php/Releases) 中的驱动。后缀 "-u" 说明 Qualcomm 可以使用通用的 Driver 模块。

```
$ wget [https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5-u.tar.bz2](https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5-u.tar.bz2)
$ tar xjf compat*
$ cd compat*
$ ./scripts/driver-select alx
$ make
$ sudo make install
$ sudo modprobe alx

```

alx 驱动由于各种问题且不同内核版本之间的兼容性不佳而没有被加入 Linux 内核。要获得更好的支持，访问 [邮件列表](http://lists.infradead.org/mailman/listinfo/unified-drivers) 和 [alx 页面](http://www.linuxfoundation.org/collaborate/workgroups/networking/alx) 获得最新的 alx 可行方案。

每次内核发生变化时，这个驱动都必须重新编译和安装。

另外，你可以使用 [compat 驱动](https://aur.archlinux.org/packages/compat-drivers-patched/)的 AUR 软件包，它还会安装许多其它驱动。

### Atheros AR9485 没有 eth0

**注意:** 3.10.2-1-ARCH 内核更新的软件包中包括了 alx 以太网驱动模块。

Atheros AR9485 的以太网连接（eth0）不能立即使用（2013年3月的安装介质）。一个可行的解决方法是从 AUR 中安装 [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) 软件包。

### 待机后未接线缆 / 无连接

待机以后，接入网络电缆后仍找不到连接。这可能是由于 PCI 电源管理引起的。以下命令的输出

```
# ip link show eth0

```

如果网线接入 eth0 端口之后这一行仍含有，那么可能 the device was auto-suspended and the media sense feature doesn't work。要解决这个问题，首先你需要找到网卡控制器的 PCI 地址，通过

```
# lspci

```

结果应该类似于这样：

```
...
00:19.0 Ethernet controller: Intel Corporation 82577LM Gigabit Network Connection (rev 06)
...

```

所以这里的地址是 00:19.0。 现在这样检查设备的电源状态：

```
# cat "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

使用从 lspci 中获得的地址替换 00:19.0。 如果输出结果为 "auto"，你可以尝试让设备不再待机，输入

```
# echo on > "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

不要忘记再一次替换地址。

**注意:** 这是内核 3.8.4.1 的缺陷：[论坛讨论](https://bbs.archlinux.org/viewtopic.php?id=159837&p=2)。在 3.9 中应该会 [修复](https://lkml.org/lkml/2013/1/18/147)。在更新内核前，可以使用上述方法。

### Broadcom BCM57780

这个 Broadcom 芯片只有你指定模块的加载顺序后才能正常工作。这些模块是 `broadcom` 和 `tg3`，前者需要首先加载。

如果你的电脑有这个芯片，这些步骤应该有用：

```
$ lspci | grep Ethernet
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

如果你的有线网络不能工作，尝试断开网线，然后以 root 权限实施以下步骤：

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

现在接入网线。如果现在你的故障解决了，你可以把 `broadcom` 和 `tg3` （以此顺序）加入到 `/etc/mkinitcpio.conf` 的 `MODULES` 一行，使得变更持久化：

```
MODULES=".. broadcom tg3 .."

```

然后重新编译 initramfs:

```
# mkinitcpio -p linux

```

**注意:** 这些方法可能也适用于其它芯片，例如 BCM57760。