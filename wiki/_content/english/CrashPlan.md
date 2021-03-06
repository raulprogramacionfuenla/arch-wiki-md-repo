[CrashPlan](https://www.crashplan.com/en-us/) is a [backup program](/index.php/Backup_program "Backup program") that backs up data to remote servers, other computers, or hard drives. Backing up to the cloud servers requires a monthly subscription.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Basic Usage](#Basic_Usage)
*   [3 Running Crashplan on a headless server](#Running_Crashplan_on_a_headless_server)
    *   [3.1 X11 forwarding over SSH](#X11_forwarding_over_SSH)
    *   [3.2 Local client](#Local_client)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Waiting for connection](#Waiting_for_connection)
    *   [4.2 Waiting for Backup](#Waiting_for_Backup)
    *   [4.3 Desktop GUI Crashes on startup](#Desktop_GUI_Crashes_on_startup)
    *   [4.4 Out of Memory](#Out_of_Memory)
    *   [4.5 Real time protection](#Real_time_protection)
    *   [4.6 JRE Version Update](#JRE_Version_Update)
*   [5 See also](#See_also)

## Installation

Install [crashplan](https://aur.archlinux.org/packages/crashplan/) from the [AUR](/index.php/AUR "AUR"). There is also [crashplan-pro](https://aur.archlinux.org/packages/crashplan-pro/) and [crashplan-pro-e](https://aur.archlinux.org/packages/crashplan-pro-e/) available which are the paid enterprise packages.

## Basic Usage

Before accessing CrashPlan's graphical user interface, you should [start](/index.php/Start "Start") the `crashplan.service` unit.

CrashPlan can be configured entirely through its graphical user interface. To start the graphical interface:

```
$ CrashPlanDesktop

```

To make CrashPlan automatically start upon system startup, [enable](/index.php/Enable "Enable") the systemd unit.

## Running Crashplan on a headless server

Running CrashPlan on a headless server is not officially supported. However, it is possible to do so.

The CrashPlan daemon's configuration files (in `/opt/crashplan/conf`) are in an obscure XML format, and they are meant to be edited programmatically by the CrashPlan client.

CrashPlan 5 introduced a new client app which unfortunately dropped support for configuring a remote server with a local client, so you'll need to use X11 forwarding.

### X11 forwarding over SSH

Ensure that `X11Forwarding` is set to `yes` in the headless server's `/etc/ssh/sshd_config` and from another machine running X11, SSH to the headless machine with `-Y`, and from the remote shell run `CrashPlanDesktop`. The headless machine's windows will appear on the local X11 server. If you have problems, check `/opt/crashplan/log/ui_error.log`.

### Local client

On CrashPlan v4.x and below, the client and daemon communicate on port 4243 by default. Thus, an easy way of configuring the CrashPlan daemon on a headless server is to create an SSH tunnel:

1.  [Start](/index.php/Start "Start") the CrashPlan daemon on the server.
2.  Create an SSH tunnel. On the client: `ssh -N -L 4243:localhost:4243 headless.example.com`.
3.  Start the CrashPlan client. (Again, the executable is named `CrashPlanDesktop`.)

Note that the authentication token (located in `/var/lib/crashplan/.ui_info`) on the local and remote servers must match. More ideas can be found on these websites:

*   The CrashPlan support site [details](http://support.code42.com/CrashPlan/Latest/Configuring/Configuring_A_Headless_Client) a slightly more complicated method of tunneling traffic from the client (CrashPlan Desktop) to the daemon (CrashPlan Engine) through an SSH tunnel.
*   A [post by Bryan Ross](http://www.liquidstate.net/how-to-manage-your-crashplan-server-remotely/) details how to make CrashPlan Desktop connect directly to CrashPlan Engine. Note that this method can be less secure than tunneling traffic through an SSH tunnel.

## Troubleshooting

### Waiting for connection

On some systems it can happen that CrashPlan does not wait until an internet connection is established. If using [NetworkManager](/index.php/NetworkManager "NetworkManager"), you can install [networkmanager-dispatcher-crashplan-systemd](https://aur.archlinux.org/packages/networkmanager-dispatcher-crashplan-systemd/) which will automatically restart the CrashPlan service once a connection is successfully established.

### Waiting for Backup

If the backup is stuck on «Waiting for Backup» even after you engage it manually, it might be that CrashPlan cannot access the tempdir or it is mounted as `noexec`. It uses the default Java tmp dir which is normally `/tmp`. You can either remove the `noexec` mount option (not recommended) or change the tmpdir CrashPlan is using.

To change the tmpdir CrashPlan uses, open `/opt/crashplan/bin/run.conf` and insert `-Djava.io.tmpdir=/new-tempdir` to `SRV_JAVA_OPTS`, for example:

```
SRV_JAVA_OPTS="-Djava.io.tmpdir=/var/tmp/crashplan -Dfile.encoding=UTF-8 …

```

Make sure to create the new tmpdir and verify CrashPlan's user has access to it.

```
# mkdir /var/tmp/crashplan

```

[Restart](/index.php/Restart "Restart") CrashPlan.

### Desktop GUI Crashes on startup

On systems with Gnome 3 installed, or with libwebkit-gtk installed, there may be an issue where the GUI crashes on launch. This can be fixed by following the instructions [here](https://support.code42.com/CrashPlan/Latest/Troubleshooting/CrashPlan_Client_Closes_In_Some_Linux_Installations).

### Out of Memory

For backup sets containing large numbers of files (more than 100,000 or so), the default maximum heap size of 512M may be too small. If this is filled, the server will silently restart, and will usually get stuck restarting as it continually reaches the memory limit. The only sign of this happening is the creation of many small log files in `/opt/crashplan/bin` for each service restart (potentially hundreds of thousands, depending on how long it takes to notice the problem). To increase the heap size limit, adjust the `-Xmx` option in `/opt/crashplan/bin/run.conf` to a reasonable value for your system.

### Real time protection

If you use real time protection for your backup set and have a lot of files to backup, the default system configuration might not be able to allocate all required handles to follow all files in real time. This issue can manifest itself with logs like "inotify_add_watch: No space left on device" in the syslog journal. CrashPlan Support has instructions [here](https://support.crashplan.com/Troubleshooting/Real-Time_Backup_For_Network-Attached_Drives) describing how to modify inotify max_user_watches to a bigger value to fix the issue. **You cannot follow their instructions directly though**, you need to create a new file in /etc/sysctl.d as /etc/sysctl.conf is now ignored by systemd. See [sysctl#Configuration](/index.php/Sysctl#Configuration "Sysctl") for more information.

### JRE Version Update

If, during upgrade, CrashPlan is attempting to upgrade the self-installed JRE version and the upgrade never gets passed downloading the JRE from CrashPlan (checking in logs/upgrade<unique_number>.log, the last message is a curl/wget for the "latest" JRE tgz), it's possible to stop CrashPlan, download the JRE (from the ugprade log) manually and replace the jre folder in the CrashPlan install with the upgrade version. This should allow CrashPlan to get past being stuck trying to upgrade the JRE.

```
 cd <crashplan/install/dir>
 ./bin/CrashPlanEngine stop
 rm -rf jre
 curl <jre url from crashplan log>
 tar xzvf <jre.tgz>
 ./bin/CrashPlanEngine start

```

## See also

*   [CrashPlan home page](http://www.code42.com/crashplan/)
*   [CrashPlan On A Headless Server - Code42Support](http://support.code42.com/CrashPlan/Latest/Configuring/Using_CrashPlan_On_A_Headless_Computer)
*   [Wikipedia:CrashPlan](https://en.wikipedia.org/wiki/CrashPlan "wikipedia:CrashPlan")