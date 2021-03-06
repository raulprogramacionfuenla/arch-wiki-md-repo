**[SNMP](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol "wikipedia:Simple Network Management Protocol")** is a tool designed for the management and monitoring of network devices. The Net-SNMP package is one implementation of SNMP that is available for Arch Linux. This article discusses the configuration and testing of the snmpd daemon that ships with Arch's net-snmp package.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Daemon](#Daemon)
    *   [2.2 SNMP 1 and 2c](#SNMP_1_and_2c)
    *   [2.3 SNMP 3](#SNMP_3)
    *   [2.4 Start Daemon](#Start_Daemon)
*   [3 Testing](#Testing)

## Installation

There is a single package for net-snmp in Arch Linux which contains both the snmpd daemon, and the accompanying utilities.

[Install](/index.php/Install "Install") the [net-snmp](https://www.archlinux.org/packages/?name=net-snmp) package.

## Configuration

Note that if `/var/net-snmp/snmpd.conf` is modified while snmpd is running, any changes will be lost when the daemon is restarted. It is therefore crucial that the snmpd service is stopped while editing the configuration file.

### Daemon

[Enable](/index.php/Enable "Enable") `snmpd.service`.

### SNMP 1 and 2c

There are three versions of SNMP which are supported by net-snmp: 1, 2c and 3\. Versions 1 and 2c start with the same basic configuration, using `/etc/snmp/snmpd.conf`.

```
mkdir /etc/snmp/
echo rocommunity *read_only_community_string* >> /etc/snmp/snmpd.conf

```

The above commands will add a community string that can be used for monitoring. Optionally, you can add another community string used for management. This is not recommended unless you have a specific reason to do so.

```
echo rwcommunity *read_write_community_string* >> /etc/snmp/snmpd.conf

```

### SNMP 3

SNMP v3 adds security and encrypted authentication/communication. It uses a different configuration scheme in `/etc/snmp/snmpd.conf` and additional configuration in `/var/net-snmp/snmpd.conf`.

```
mkdir /etc/snmp/
echo rouser *read_only_user* >> /etc/snmp/snmpd.conf
# or use the wizard $ snmpconf -g basic_setup

```

```
mkdir -p /var/net-snmp/
echo createUser *read_only_user* SHA *password1* AES *password2* > /var/net-snmp/snmpd.conf
# or use the tool # net-snmp-create-v3-user -ro -a SHA -x AES

```

Note that once snmpd is restarted, `/var/net-snmp/snmpd.conf` will be rewritten, and the clear-text passwords that you have entered will be encrypted.

### Start Daemon

After configuring the daemon, start it

```
systemctl start snmpd

```

## Testing

If using SNMP 1 or 2c, use one of the following commands to test configuration:

```
# snmpwalk -v 1 -c *read_only_community_string* localhost | less
# snmpwalk -v 2c -c *read_only_community_string* localhost | less

```

If using SNMP 3, use the following command to test configuration:

```
# snmpwalk -v 3 -u *read_only_user* -a SHA -A *password1* -x AES -X *password2* -l authNoPriv localhost | less

```

Either way, you should see several lines of data looking something like:

```
SNMPv2-MIB::sysDescr.0 = STRING: Linux myhost 2.6.37-ARCH #1 SMP PREEMPT Sat Jan 29 20:00:33 CET 2011 x86_64
SNMPv2-MIB::sysObjectID.0 = OID: ccitt.1
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (307772) 0:51:17.72
SNMPv2-MIB::sysContact.0 = STRING: root@localhost
SNMPv2-MIB::sysName.0 = STRING: myhost
...SNIP...

```