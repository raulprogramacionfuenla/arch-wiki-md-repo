**翻译状态：** 本文是英文页面 [MySQL](/index.php/MySQL "MySQL") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-29，点击[这里](https://wiki.archlinux.org/index.php?title=MySQL&diff=0&oldid=394453)可以查看翻译后英文页面的改动。

MySQL是一个广泛使用的多线程多用户式数据库。具体特性请参看[官方网站](http://www.mysql.com/)。

**注意:** MariaDB 现在是 Arch Linux 官方默认的 MySQL 实现。Oracle MySQL 已被移动到 [AUR](/index.php/AUR "AUR")，推荐所有用户[升级](#Upgrade_from_Oracle_MySQL_to_MariaDB)到 MariaDB。参见[这条公告](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 升级](#.E5.8D.87.E7.BA.A7)
    *   [1.2 由 Oracle MySQL 升级到 MariaDB](#.E7.94.B1_Oracle_MySQL_.E5.8D.87.E7.BA.A7.E5.88.B0_MariaDB)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 添加新用户](#.E6.B7.BB.E5.8A.A0.E6.96.B0.E7.94.A8.E6.88.B7)
    *   [2.2 配置文件](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [2.3 禁用远程访问](#.E7.A6.81.E7.94.A8.E8.BF.9C.E7.A8.8B.E8.AE.BF.E9.97.AE)
    *   [2.4 启用自动补全](#.E5.90.AF.E7.94.A8.E8.87.AA.E5.8A.A8.E8.A1.A5.E5.85.A8)
    *   [2.5 为数据库使用 UTF-8 编码](#.E4.B8.BA.E6.95.B0.E6.8D.AE.E5.BA.93.E4.BD.BF.E7.94.A8_UTF-8_.E7.BC.96.E7.A0.81)
    *   [2.6 使用内存作为临时文件存放点](#.E4.BD.BF.E7.94.A8.E5.86.85.E5.AD.98.E4.BD.9C.E4.B8.BA.E4.B8.B4.E6.97.B6.E6.96.87.E4.BB.B6.E5.AD.98.E6.94.BE.E7.82.B9)
*   [3 备份](#.E5.A4.87.E4.BB.BD)
*   [4 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [4.1 MySQL 守护进程无法启动](#MySQL_.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
    *   [4.2 执行 mysql_upgrade 后 MySQL 不能启动](#.E6.89.A7.E8.A1.8C_mysql_upgrade_.E5.90.8E_MySQL_.E4.B8.8D.E8.83.BD.E5.90.AF.E5.8A.A8)
    *   [4.3 重置 root 密码](#.E9.87.8D.E7.BD.AE_root_.E5.AF.86.E7.A0.81)
    *   [4.4 检查并修复所有数据表](#.E6.A3.80.E6.9F.A5.E5.B9.B6.E4.BF.AE.E5.A4.8D.E6.89.80.E6.9C.89.E6.95.B0.E6.8D.AE.E8.A1.A8)
    *   [4.5 优化所有数据表](#.E4.BC.98.E5.8C.96.E6.89.80.E6.9C.89.E6.95.B0.E6.8D.AE.E8.A1.A8)
    *   [4.6 OS error 22 when running on ZFS](#OS_error_22_when_running_on_ZFS)
    *   [4.7 无法通过命令行登陆, 但是 phpmyadmin 正常工作](#.E6.97.A0.E6.B3.95.E9.80.9A.E8.BF.87.E5.91.BD.E4.BB.A4.E8.A1.8C.E7.99.BB.E9.99.86.2C_.E4.BD.86.E6.98.AF_phpmyadmin_.E6.AD.A3.E5.B8.B8.E5.B7.A5.E4.BD.9C)
    *   [4.8 MySQL 日志文件占用太多空间](#MySQL_.E6.97.A5.E5.BF.97.E6.96.87.E4.BB.B6.E5.8D.A0.E7.94.A8.E5.A4.AA.E5.A4.9A.E7.A9.BA.E9.97.B4)
*   [5 更多资源](#.E6.9B.B4.E5.A4.9A.E8.B5.84.E6.BA.90)

## 安装

Archlinux 选择的 MySQL 实现被称为 MariaDB。 [安装](/index.php/Pacman "Pacman")位于[官方软件源](/index.php/Official_repositories "Official repositories")的[mariadb](https://www.archlinux.org/packages/?name=mariadb)、[libmariadbclient](https://www.archlinux.org/packages/?name=libmariadbclient) 和 [mariadb-clients](https://www.archlinux.org/packages/?name=mariadb-clients) 软件包。 其它实现有 [percona-server](https://www.archlinux.org/packages/?name=percona-server) 和 Oracle [mysql](https://aur.archlinux.org/packages/mysql/)。

**Tip:**

*   如果数据库 (位于 `/var/lib/mysql`) 运行在[Btrfs](/index.php/Btrfs "Btrfs")分区之上, 你应当在创建数据库之前禁用 [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") 特性。
*   如果数据库运行在 [ZFS](/index.php/ZFS "ZFS") 分区之上, 你应该在创建数据库之前参阅 [ZFS#Database](/index.php/ZFS#Database "ZFS") 。

安装Maria软件包之后，你必须运行下面这条命令：

```
# mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

```

启动 `mysqld` [守护进程](/index.php/Daemon "Daemon")，运行安装脚本，然后重新启动守护进程：

```
# systemctl start mysqld
# mysql_secure_installation
# systemctl restart mysqld

```

为了简化管理过程，可用的管理前端有 [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench) 和 [Adminer](/index.php/Adminer "Adminer")。

### 升级

升级了 MySQL 并启动之后，要运行这条命令：

```
# mysql_upgrade -u root -p

```

### 由 Oracle MySQL 升级到 MariaDB

想要切换的用户需要安装 [mariadb](https://www.archlinux.org/packages/?name=mariadb)，[libmariadbclient](https://www.archlinux.org/packages/?name=libmariadbclient) 以及 [mariadb-clients](https://www.archlinux.org/packages/?name=mariadb-clients)，然后执行 `mysql_upgrade` 来迁移系统：

```
# systemctl stop mysqld
# pacman -S mariadb libmariadbclient mariadb-clients
# systemctl start mysqld
# mysql_upgrade -p

```

**注意:** 在重新启动守护进程前，请先删除 `/var/lib/mysql` 中的 `ib_logfile0`, `ib_logfile1` 以及 `aria_log_control`。

## 配置

一旦你启动了MySQL服务器，你最好增加一个root账号来维护你的MySQL用户和数据库。如上面的初始化脚本输出的信息里所述，有手动或自动完成两种方法 ── 可以运行命令来设置root账号的密码，或者运行安全安装脚本。

现在可以使用你偏好的交互方式来进行进一步配置。例如可以用MySQL的命令行工具，以root账号登录你的MySQL服务器：

```
$ mysql -p -u root

```

### 添加新用户

以下是创建一个密码为'some_pass'的'monty'用户的示例。

 `$ mysql -u root -p` 
```
MariaDB> CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
MariaDB> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost'
   ->     WITH GRANT OPTION;
MariaDB> quit
```

### 配置文件

*MariaDB* 会按照以下顺序读取配置文件 (根据 `mysqld --help --verbose` 的输出):

```
/etc/my.cnf /etc/mysql/my.cnf ~/.my.cnf

```

请根据你需要的配置作用范围(对系统, 对用户...)来修改对应的配置文件。 点击 [这里](https://mariadb.com/kb/en/mariadb/documentation/getting-started/starting-and-stopping-mariadb/mysqld-configuration-files-and-groups/) 了解更多信息。

### 禁用远程访问

MySQL 服务器默认可从网络访问。如果只有本机需要 MySQL，可以通过不监听 TCP 端口 3306 来增强安全性。要拒绝远程连接，取消注释 `/etc/mysql/my.cnf` 中以下这行：

```
skip-networking

```

你仍能从本机登录。

### 启用自动补全

**注意:** 启用这项功能会增加客户端启动时间。

MySQL 默认禁用客户端自动补全功能。要在整个系统中启用它，编辑 `/etc/mysql/my.cnf`，将 `no-auto-rehash` 替换为 `auto-rehash`。下次客户端启动时就会启用自动补全。

### 为数据库使用 UTF-8 编码

在 `/etc/mysql/my.cnf` 的 `mysqld` 下, 添加:

```
[mysqld]
init_connect                = 'SET collation_connection = utf8_general_ci,NAMES utf8'
collation_server            = utf8_general_ci
character_set_client        = utf8
character_set_server        = utf8

```

### 使用内存作为临时文件存放点

MySQL 存储临时文件的目录名是 *tmpdir*。

创建一个临时目录:

```
# mkdir -pv /var/lib/mysqltmp
# chown mysql:mysql /var/lib/mysqltmp

```

通过命令找出 `mysql` 的id和gid:

```
$ id mysql
uid=27(mysql) gid=27(mysql) groups=27(mysql)

```

添加到 `/etc/fstab` 中。

```
 tmpfs   /var/lib/mysqltmp   tmpfs   rw,gid=27,uid=27,size=100M,mode=0750,noatime   0 0

```

将以下配置添加到 `/etc/mysql/my.cnf` 的 `mysqld` 组下:

```
 tmpdir      = /var/lib/mysqltmp

```

然后重启系统以使配置生效。

## 备份

数据库可以转储到文件以简化备份。以下 shell 脚本会替你在脚本所在目录创建一个 `db_backup.gz` 文件，包含数据库的转储：

```
#!/bin/bash

THISDIR=$(dirname $(readlink -f "$0"))

mysqldump --single-transaction --flush-logs --master-data=2 --all-databases \
 | gzip > $THISDIR/db_backup.gz
echo 'purge master logs before date_sub(now(), interval 7 day);' | mysql
```

参见 MySQL 手册的官方 `mysqldump` [页面](http://dev.mysql.com/doc/refman/5.6/en/mysqldump.html)。

## 故障排除

### MySQL 守护进程无法启动

如果 MySQL 无法启动且日志文件中没有任何信息，你可能需要检查 `/var/lib/mysql` 和 `/var/lib/mysql/mysql` 目录中文件的权限。如果这些目录中文件的所有者不是 `mysql:mysql`，你应该这样做：

```
# chown mysql:mysql /var/lib/mysql -R

```

如果你仍旧碰到了权限问题，确保已把 `my.cnf` 拷贝到 `/etc/` 目录：

```
# cp /etc/mysql/my.cnf /etc/my.cnf

```

然后尝试重新启动守护进程。

如果文件 `/var/lib/mysql/hostname.err` 中有如下错误：

```
[ERROR] Can't start server : Bind on unix socket: Permission denied
[ERROR] Do you already have another mysqld server running on socket: /var/run/mysqld/mysqld.sock ?
[ERROR] Aborting

```

`/var/run/mysqld` 的权限可能是罪魁祸首：

```
# chown mysql:mysql /var/run/mysqld -R

```

如果运行 mysqld 时出现了如下错误：

```
Fatal error: Can’t open and lock privilege tables: Table ‘mysql.host’ doesn’t exist

```

在 `/usr` 目录中运行下列命令来安装默认的表：

```
# cd /usr
# mysql_install_db --user=mysql --ldata=/var/lib/mysql/

```

### 执行 mysql_upgrade 后 MySQL 不能启动

试试安全模式下运行的 MySQL：

```
# mysqld_safe --datadir=/var/lib/mysql/

```

然后再运行:

```
# mysql_upgrade -u root -p

```

### 重置 root 密码

停止 *mysqld* [守护进程](/index.php/Daemon "Daemon")，再执行以下命令：

```
# mysqld_safe --skip-grant-tables &

```

连接到 MySQL 服务器，执行以下命令：

```
# mysql -u root mysql

```

修改 root 密码：

```
mysql> UPDATE mysql.user SET Password=PASSWORD('MyNewPass') WHERE User='root';
mysql> FLUSH PRIVILEGES;
mysql> exit

```

再启动 *mysqld* 守护进程。

### 检查并修复所有数据表

检查并自动修复所有数据库中的所有表，[查看更多](http://dev.mysql.com/doc/refman/5.7/en/mysqlcheck.html)

```
# mysqlcheck -A --auto-repair -u root -p

```

### 优化所有数据表

强制优化所有数据表，自动修复可能出现的数据表错误

```
# mysqlcheck -A --auto-repair -f -o -u root -p

```

### OS error 22 when running on ZFS

如果您正在使用 [ZFS](/index.php/ZFS "ZFS") 并且遇见了如下错误

```
InnoDB: Operating system error number 22 in a file operation.

```

那么就需要修改 `/etc/mysql/my.cnf` 中的设置来禁用 aio_writes

```
[mysqld]
...
innodb_use_native_aio = 0

```

但如果后续的安装脚本因为上述问题出错，那么 MySQL/MariaDB 可能会处于非法的状态中。可以执行以下命令从非法状态中恢复：

```
rm -rf /var/lib/mysql/*
mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
chown -R mysql:mysql /var/lib/mysql &>/dev/null
/usr/bin/systemd-tmpfiles --create mysql.conf

```

以上命令全部执行后，MySQL/MariaDB 应该就能正确安装了。

### 无法通过命令行登陆, 但是 phpmyadmin 正常工作

当使用了超长 (>70-75) 的密码后，这个问题有可能发生。 由于某些因素，5.5.36 版本的 mysql 的命令行不能在 readline 模式中处理那么多的字符。 所以如果打算使用推荐的密码输入方式：

```
$ mysql -u <user> -p
Password:

```

不妨考虑更换一个长度短一点的密码。

**注意:** 您依然可以通过在命令行参数中指定密码来登陆
```
$ mysql -u <user> -p"<some-veryveryveryveryveryveryveryveryveryveryveryveryveryveryvery-long-and-veryveryveryveryveryveryveryveryveryvery-strong-password>"

```

**警告:** 但这样做很危险，因为您的密码很可能会泄漏到某个地方，例如，日志。只有当遇到紧急情况才能考虑这么做，并且事后不要忘记更改密码。

### MySQL 日志文件占用太多空间

默认情况下， mysqld 会在 `/var/lib/mysql` 下创建二进制日志文件。这在某些场景下是很有用的。但是这些日志文件也可能耗光您的硬盘空间。如果需要，您可以在 `/etc/mysql/my.cnf` 中注释掉以下两行来禁用日志：

```
#log-bin=mysql-bin
#binlog_format=mixed

```

另外，您也可以执行以下命令来清除 `/var/lib/mysql` 里的一些日志文件来释放硬盘空间：

```
#mysql -u root -p"PASSWORD" -e "PURGE BINARY LOGS TO 'mysql-bin.0000xx';"

```

## 更多资源

*   [LAMP_(简体中文)](/index.php/LAMP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LAMP (简体中文)") - Arch wiki 文章，涵盖安装 LAMP 服务器 (Linux Apache MySQL PHP)
*   [http://mariadb.org/](http://mariadb.org/) - Community-driven 实现
*   [http://www.mysql.com/](http://www.mysql.com/) - Oracle 实现
*   [http://www.percona.com/software](http://www.percona.com/software) - Percona 实现
*   [MariaDB knowledge Base](https://mariadb.com/kb/en/)
*   [MySQL documentation](http://dev.mysql.com/doc/)
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") - ArchWiki article covering the web-based tool to help manage MySQL databases using an Apache/PHP front-end.
*   [PHP](/index.php/PHP "PHP") - ArchWiki article on PHP.
*   [MySQL Performance Tuning Scripts and Know-How](http://www.askapache.com/mysql/performance-tuning-mysql.html)