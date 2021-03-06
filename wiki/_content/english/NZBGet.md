[NZBGet](https://nzbget.net/) is an Usenet-client written in C++ and designed with performance in mind to achieve maximum download speed by using very little system resources.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuring NZBGet](#Configuring_NZBGet)
*   [3 Starting NZBGet](#Starting_NZBGet)
*   [4 Running NZBGet under a different user](#Running_NZBGet_under_a_different_user)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Default NZBGet credentials](#Default_NZBGet_credentials)
    *   [5.2 NZBGet crashes on start](#NZBGet_crashes_on_start)
    *   [5.3 Alternative systemd service](#Alternative_systemd_service)
    *   [5.4 Unable to extract archives](#Unable_to_extract_archives)
*   [6 See also](#See_also)

## Installation

Install the [nzbget](https://www.archlinux.org/packages/?name=nzbget) package and the optional [nzbget-systemd](https://aur.archlinux.org/packages/nzbget-systemd/) that provides a `nzbget` [systemd](/index.php/Systemd "Systemd") service. Alternatively, install the development version from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") ([nzbget-git](https://aur.archlinux.org/packages/nzbget-git/)), which also includes the [systemd](/index.php/Systemd "Systemd") service.

## Configuring NZBGet

Copy the template configuration file to a custom directory:

```
# cp /usr/share/nzbget/nzbget.conf /var/lib/nzbget/.nzbget

```

Update the configuration before starting NZBGet:

 `/var/lib/nzbget/.nzbget` 
```
..
WebDir=/usr/share/nzbget/webui
ScriptDir=${WebDir}/scripts
LockFile=/var/lib/nzbget/nzbget.lock
ConfigTemplate=/usr/share/nzbget/nzbget.conf
DaemonUsername=nzbget
..
```

Make sure the permissions are set correctly:

```
# chown -R nzbget:nzbget /var/lib/nzbget
# chmod -R 750 /var/lib/nzbget

```

## Starting NZBGet

**Note:** The official [nzbget](https://www.archlinux.org/packages/?name=nzbget) package doesn't provide a systemd service file. You will have to start NZBGet manually instead.

*   Running as root in console-mode: `# nzbget -c /var/lib/nzbget/.nzbget -s` 

*   Running as root in daemon-mode: `# nzbget -c /var/lib/nzbget/.nzbget -D` 

NZBGet should now be accessible on [http://localhost:6789](http://localhost:6789).

## Running NZBGet under a different user

**Note:** [nzbget-systemd](https://aur.archlinux.org/packages/nzbget-systemd/) and [nzbget-git](https://aur.archlinux.org/packages/nzbget-git/) already provide the `nzbget` [user](/index.php/User "User") and [user group](/index.php/User_group "User group").

See [system user](/index.php/Users_and_groups#Example_adding_a_system_user "Users and groups") for an example and reasons why it may be useful.

After adding a system user, update the main configuration file using the webinterface or by manually editing `/var/lib/nzbget/.nzbget`:

 `/var/lib/nzbget/.nzbget` 
```
..
DaemonUsername=nzbget # system user
MainDir=/home/myuser/Downloads/NZBGet
UMask=0002 # 775 for dirs - 664 for files
```

Create and set permissions for the desired directories:

```
# mkdir /home/myuser/Downloads/NZBGet
# chown -R nzbget:nzbget /home/myuser/Downloads/NZBGet
# chmod 775 /home/myuser/Downloads/NZBGet

```

The `/home/myuser/Downloads/NZBGet` will be accessible for the user `nzbget` and for the `nzbget` group. Making the target directory world read/writable is highly discouraged (i.e. do not *chmod* the directory to *777*). Instead, give individual users/groups appropriate permissions to the appropriate directories (e.g. by adding 'yourself' to the `nzbget` group).

Starting NZBGet as user `nzbget` in daemon-mode, or start NZBGet by using the `nzbget.service` if installed with the [nzbget-systemd](https://aur.archlinux.org/packages/nzbget-systemd/) instead:

```
$ sudo -u nzbget /usr/bin/nzbget -c /var/lib/nzbget/.nzbget -D

```

## Troubleshooting

### Default NZBGet credentials

The default credentials for NZBGet are `nzbget` as user and `tegbzn6789` as password. For security reasons it is recommended to change the default credentials.

### NZBGet crashes on start

This may happen when the user edited the NZBGet configuration by the Web-interface (located at [http://localhost:6789](http://localhost:6789)), corrupting the configuration-file. Clean-up the configuration-file and restart the server/daemon again.

### Alternative systemd service

The following `nzbget.service` provides an alternative solution for (re)starting NZBGet when using [systemd](/index.php/Systemd "Systemd"):

 `/usr/lib/systemd/system/nzbget.service` 
```
[Unit]
Description=NZBGet Daemon
Documentation=[http://nzbget.net/Documentation](http://nzbget.net/Documentation)
After=network.target

[Service]
User=nzbget
Group=nzbget
Type=forking
PIDFile=/var/lib/nzbget/nzbget.lock
ExecStart=/usr/bin/nzbget -c /var/lib/nzbget/.nzbget -D
ExecStop=/usr/bin/nzbget -Q
ExecReload=/usr/bin/nzbget -O
KillMode=process
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

### Unable to extract archives

Verify if [unzip](https://www.archlinux.org/packages/?name=unzip), [unrar](https://www.archlinux.org/packages/?name=unrar), [p7zip](https://www.archlinux.org/packages/?name=p7zip) and [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline) have been installed.

## See also

*   [NZBGet Documentation](http://nzbget.net/Documentation)
*   [Performance Tips](http://nzbget.net/Performance_tips)