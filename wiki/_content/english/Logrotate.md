From [https://fedorahosted.org/logrotate/](https://fedorahosted.org/logrotate/):

	*The logrotate utility is designed to simplify the administration of log files on a system which generates a lot of log files. Logrotate allows for the automatic rotation compression, removal and mailing of log files. Logrotate can be set to handle a log file daily, weekly, monthly or when the log file gets to a certain size.*

By default, logrotate's *rotation* consists of renaming existing log files with a numerical suffix, then recreating the original *empty* log file. For example, `/var/log/syslog.log` is renamed `/var/log/syslog.log.1`. If `/var/log/syslog.log.1` already exists from a previous rotation, it is first renamed `/var/log/syslog.log.2`. (The number of backlogs to keep can be configured.)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 exim log not rotated](#exim_log_not_rotated)
*   [4 See also](#See_also)

## Installation

Logrotate can be installed with the [logrotate](https://www.archlinux.org/packages/?name=logrotate) package. It is installed by default as it is member of the [base](https://www.archlinux.org/groups/x86_64/base/) group.

By default, logrotate runs daily using a [systemd timer](/index.php/Systemd/Timers "Systemd/Timers"): `logrotate.timer`.

## Configuration

The primary configuration file for logrotate is `/etc/logrotate.conf`; additional configuration files are included from the `/etc/logrotate.d` directory.

## Troubleshooting

### exim log not rotated

If you have set the `olddir` variable in `/etc/logrotate.conf`, you will get a message such as:

`error: failed to rename /var/log/exim/mainlog to /var/log/old/mainlog.1: Permission denied`

To fix this, add the user `exim` to the group `log`. Then change the group of the `olddir`, usually `/var/log/old`, to `log` instead of the default `root`.

## See also

*   [Logrotate on Gentoo Linux Wiki](http://wiki.gentoo.org/wiki/Logrotate)