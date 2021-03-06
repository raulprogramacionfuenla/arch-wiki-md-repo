[Smokeping](https://oss.oetiker.ch/smokeping/index.en.html) allows you to probe a list of servers, store that data using RRDtool, and generate statistical charts based on RRDtool's output. Smokeping consists of two parts. A daemon runs in the background pinging and collecting data at set intervals. A web interface displays that data in the form of graphs.

This wiki page covers a basic setup of the smokeping daemon and the CGI webinterface.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Optional Prerequisites](#Optional_Prerequisites)
*   [2 Configuration](#Configuration)
    *   [2.1 Editing the config file](#Editing_the_config_file)
        *   [2.1.1 Notes on the smokeping configuration file syntax](#Notes_on_the_smokeping_configuration_file_syntax)
    *   [2.2 Setup the rest of the system](#Setup_the_rest_of_the_system)
    *   [2.3 Start and enable daemon](#Start_and_enable_daemon)
*   [3 Setup web frontend](#Setup_web_frontend)
    *   [3.1 Apache](#Apache)
    *   [3.2 Caddy](#Caddy)
    *   [3.3 Lighttpd](#Lighttpd)
    *   [3.4 Nginx](#Nginx)
*   [4 Advanced Configuration](#Advanced_Configuration)
*   [5 Notes](#Notes)
    *   [5.1 Smoketrace (Tr.cgi)](#Smoketrace_(Tr.cgi))

## Installation

This section covers the installation of [Smokeping](https://oss.oetiker.ch/smokeping/index.en.html) using the [smokeping](https://www.archlinux.org/packages/?name=smokeping) package. FastCGI on Apache will be setup as described in [Apache and FastCGI](/index.php/Apache_and_FastCGI "Apache and FastCGI").

The smokeping package consists of two parts:

*   The smokeping daemon and configs in `/etc/smokeping/`. This daemon performs the monitoring.
*   The smokeping "htdocs" in `/srv/http/smokeping`. These will be used by the web interface.

In addition to the [smokeping](https://www.archlinux.org/packages/?name=smokeping) package, you will need:

*   A tool that smokeping can use for monitoring. [fping](https://www.archlinux.org/packages/?name=fping) is the simplest and default method for simple ping probes.
*   [apache](https://www.archlinux.org/packages/?name=apache) and [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) for the web interface if you're using Apache.
*   [fcgiwrap](https://www.archlinux.org/packages/?name=fcgiwrap) and start and enable fcgiwrap.socket if you're using Nginx
*   An image cache directory that the FastCGI script can write to, e.g. `/srv/smokeping/imgcache`
*   A data directory that the smokeping daemon can write to, and the FastCGI script can read, e.g. `/srv/smokeping/data`
*   To ensure that the main config file is readable by the smokeping daemon.

### Optional Prerequisites

If you want to use other probes such as the DNS or http probe you will need other packages as shown below. The configuration of these will is not covered by this wiki page.

| Probe | Package Needed |
| Curl | [curl](https://www.archlinux.org/packages/?name=curl) |
| DNS | [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) (for the dig utility) |
| EchoPing | [echoping](https://www.archlinux.org/packages/?name=echoping) |
| SSH | [openssh](https://www.archlinux.org/packages/?name=openssh) |
| TelnetIOSPing | [perl-net-telnet](https://www.archlinux.org/packages/?name=perl-net-telnet) |
| AnotherDNS | [perl-net-dns](https://www.archlinux.org/packages/?name=perl-net-dns) |
| LDAP | [perl-ldap](https://www.archlinux.org/packages/?name=perl-ldap) |
| LDAP (tls) | [perl-io-socket-ssl](https://www.archlinux.org/packages/?name=perl-io-socket-ssl) |
| Authen | [perl-authen-radius](https://www.archlinux.org/packages/?name=perl-authen-radius) |

## Configuration

Smokeping requires you to edit a few files. The unedited files end with the `.dist` extension. Rename the `.dist` files in `/etc/smokeping` to remove the suffix. The *find* command does this and prints out each file that is being renamed and needs editing:

```
# cd /etc/smokeping
# find . -name '*.dist' -print -execdir sh -c 'mv {} $(basename {} .dist)' \;
# mv /srv/http/smokeping/smokeping.fcgi.dist /srv/http/smokeping/smokeping.fcgi

```

### Editing the config file

Next, edit the `/etc/smokeping/config` file; this is smokeping's main config file. A brief description of the sections is followed by a complete example.

The *General* section of the `/etc/smokeping/config` file is the easiest to edit. Personalize the top of the config file to match your information. The comments describe each field. Note that if you do not have the `sendmail` program installed (ie from postfix or sendmail) then use something else instead like `/bin/false`. The file you specify must exist or smokeping will error out.

The *Alerts* section is not needed in this minimal example, so it can be either commented out or removed.

The *Database* section does not require any changes.

In the *Presentation* section the path to the template filename needs to be updated.

The *Probes* section specifies which probes are active. By default only the *FPing* probe is enabled. This section does not require any changes.

The *Slaves* section is not needed in this minimal example, so it can be either commented out or removed. Note that if you use the `smokeping_secrets` setting in the *Slaves* section, you will have to make that file unreadable to the rest of the world, or else smokeping will error: `chmod 600 /etc/smokeping/smokeping_secrets`.

The *Targets* section specifies which hosts will be probed (pinged in our example). Customize it so that it probes the host(s) you would like to collect statistics on, as shown in the example below.

You can learn more about the Smokeping config file with the examples at [http://oss.oetiker.ch/smokeping/doc/smokeping_examples.en.html](http://oss.oetiker.ch/smokeping/doc/smokeping_examples.en.html)

 `/etc/smokeping/config` 
```
*** General ***

owner     = Your Name Here                            # your name
contact   = your.email@host.bla                       # your email
mailhost  = your.smtp.server.bla                      # your mail server
sendmail  = /bin/false                                # where the sendmail program is
imgcache  = /srv/smokeping/imgcache                   # filesystem directory where we store files
imgurl    = imgcache                                  # URL directory to find them
datadir   = /srv/smokeping/data                       # where we share data between the daemon and webapp
piddir    = /var/run                                  # filesystem directory to store PID file
cgiurl    = http://localhost/smokeping/smokeping.fcgi  # exterior URL
smokemail = /etc/smokeping/smokemail   
tmail     = /etc/smokeping/tmail
syslogfacility = local0
# each probe is now run in its own process
# disable this to revert to the old behaviour
# concurrentprobes = no

*** Database ***

step     = 300
pings    = 20

# consfn mrhb steps total

AVERAGE  0.5   1  1008
AVERAGE  0.5  12  4320
    MIN  0.5  12  4320
    MAX  0.5  12  4320
AVERAGE  0.5 144   720
    MAX  0.5 144   720
    MIN  0.5 144   720

*** Presentation ***

template = /etc/smokeping/basepage.html

+ charts

menu = Charts
title = The most interesting destinations
++ stddev
sorter = StdDev(entries=>4)
title = Top Standard Deviation
menu = Std Deviation
format = Standard Deviation %f

++ max
sorter = Max(entries=>5)
title = Top Max Roundtrip Time
menu = by Max
format = Max Roundtrip Time %f seconds

++ loss
sorter = Loss(entries=>5)
title = Top Packet Loss
menu = Loss
format = Packets Lost %f

++ median
sorter = Median(entries=>5)
title = Top Median Roundtrip Time
menu = by Median
format = Median RTT %f seconds

+ overview 

width = 600
height = 50
range = 10h

+ detail

width = 600
height = 200
unison_tolerance = 2

"Last 3 Hours"    3h
"Last 30 Hours"   30h
"Last 10 Days"    10d
"Last 400 Days"   400d

*** Probes ***

+ FPing

binary = /usr/bin/fping

*** Targets ***

probe = FPing

menu = Top
title = Network Latency Grapher
remark = Welcome to the SmokePing website of Arch User. \
         Here you will learn all about the latency of our network.

+ targets
menu = Targets

++ ArchLinux

menu = Arch Linux
title = Arch Linux Website
host = 66.211.214.131

++ GoogleDNS

menu = Google DNS
title = Google DNS server
host = 8.8.8.8

++ MultiHost

menu = Multihost example
title = Arch Wiki and Google DNS
host = /targets/ArchLinux /targets/GoogleDNS

```

#### Notes on the smokeping configuration file syntax

Each **+** character defines a section in the hierarchy. Spaces are not allowed in the section names. Period and forward slashes should probably also be avoided in section names. This is probably because the RRD files are stored under the data directory with the same exact names as the sections.

In the *Targets* section, you can define `host` as either a real host name or the path to another section to generate a multiple host chart, as shown in the `MultiHost` example above.

### Setup the rest of the system

Setup the extra directories referenced by the configuration file:

```
# mkdir -p /srv/smokeping/data
# mkdir -p /srv/smokeping/imgcache
# chown -R smokeping:smokeping /srv/smokeping
# chown -R http:http /srv/smokeping/imgcache
# chmod a+rx /srv/smokeping
# chmod -R a+rx /srv/smokeping/data

```

Since the smokeping configuration is read by both the smokeping daemon and the FastCGI scripts, so it needs to be readable:

```
# chmod a+rx /etc/smokeping
# chmod a+r /etc/smokeping/config

```

### Start and enable daemon

[Start](/index.php/Start "Start") and enable `smokeping.service`. Then check that it is running.

## Setup web frontend

### Apache

Edit `/etc/httpd/conf/httpd.conf` so that it includes:

```
LoadModule fcgid_module modules/mod_fcgid.so
<IfModule fcgid_module>
  AddHandler fcgid-script .fcgi
</IfModule>

Alias /smokeping/imgcache /srv/smokeping/imgcache
Alias /smokeping /srv/http/smokeping

<Directory "/srv/smokeping/imgcache">
  AllowOverride all
  Require all granted
</Directory>

<Directory "/srv/http/smokeping">
 Options FollowSymLinks ExecCGI
 AllowOverride all
 Require all granted
</Directory>

```

[Start](/index.php/Start "Start") Apache via the `httpd.service`.

Check that [http://localhost/smokeping/smokeping.fcgi](http://localhost/smokeping/smokeping.fcgi) loads. The first data should appear after a couple of minutes.

If the fonts in the graphs are unreadable, you may need to install the [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) package.

### Caddy

Thanks to the [Caddy community](https://caddy.community/t/smokeping-caddyfile/3560/8) and with this config file [/etc/smokeping/config](https://s.natalian.org/2018-03-27/config) and with `sudo systemctl enable fcgiwrap.socket`

 `/etc/caddy/caddy.conf.d/smokeping.conf` 
```
smokeping.example.com {

        log stdout
        errors

        tls john@example.com
        root /srv/http/smokeping

        fastcgi / unix:/var/run/fcgiwrap.sock {
                env SCRIPT_FILENAME /srv/http/smokeping/smokeping.fcgi.dist
        }
}

smokeping.example.com/js {
        root /srv/http/smokeping/js
}

smokeping.example.com/css {
        root /srv/http/smokeping/css
}

smokeping.example.com/cache {
        root /var/cache/smokeping
}

```

### Lighttpd

First install Lighttpd and FastCGI:

 `# pacman -S lighttpd fcgi` 

Edit the [Lighttpd](/index.php/Lighttpd "Lighttpd") configuration file and ensure you have at least all of the following configuration directives:

 `/etc/lighttpd/lighttpd.conf` 
```
server.document-root    = "/srv/http"
server.follow-symlink   = "enable"

server.modules += ("mod_fastcgi")
fastcgi.server = (
        ".fcgi" =>
        ((
                "bin-path" => "/srv/http/smokeping/smokeping.fcgi",
                "host" => "localhost",
                "port" => 8001,
        )),
)
```

Start and enable the server:

```
$ systemctl start lighttpd
$ systemctl enable lighttpd

```

[Systemd](/index.php/Systemd "Systemd") should show `smokeping_cgi` being managed by `lighttpd.service`.

 `$ systemctl status lighttpd` 
```
● lighttpd.service - Lighttpd Web Server
   Loaded: loaded (/usr/lib/systemd/system/lighttpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2018-12-26 14:34:42 PST; 1 day 7h ago
  Process: 17117 ExecReload=/bin/kill -HUP $MAINPID (code=exited, status=0/SUCCESS)
 Main PID: 28321 (lighttpd-angel)
    Tasks: 6 (limit: 4915)
   Memory: 128.9M
   CGroup: /system.slice/lighttpd.service
           ├─17119 /usr/bin/lighttpd -D -f /etc/lighttpd/lighttpd.conf
           ├─17126 /usr/bin/perl /usr/bin/smokeping_cgi /etc/smokeping/config
           ├─17127 /usr/bin/perl /usr/bin/smokeping_cgi /etc/smokeping/config
           ├─17128 /usr/bin/perl /usr/bin/smokeping_cgi /etc/smokeping/config
           ├─17129 /usr/bin/perl /usr/bin/smokeping_cgi /etc/smokeping/config
           └─28321 /usr/bin/lighttpd-angel -D -f /etc/lighttpd/lighttpd.conf
```

Finally, add a symbolic link to allow images to load:

```
# ln -s -t /srv/http/smokeping /srv/smokeping/imgcache

```

### Nginx

Ensure that `fcgiwrap.socket` and `nginx.service` are both running via systemctl.

Add a server block for smokeping to `/etc/nginx/nginx.conf`, following is an example for a TLS enabled block.

```
   server {
       server_name smokeping.example.com;
       listen 443 ssl http2;
       listen [::]:443 ssl http2;
       root /srv/http/smokeping/;
       index smokeping.fcgi;
       gzip off;
       location ~ \.fcgi$ {
           fastcgi_intercept_errors on;
           include /etc/nginx/fastcgi_params;
           fastcgi_param SCRIPT_FILENAME /srv/http/smokeping/smokeping.fcgi;
           fastcgi_pass unix:/var/run/fcgiwrap.sock;
       }
       location ^~ /smokeping/imgcache {
           alias /srv/smokeping/imgcache;
           gzip off;
       }
   }

```

Verify that your config is fine via `# nginx -t` and reload the configuration via `# nginx -s reload`.

## Advanced Configuration

Smokeping is a powerful tool that can be configured in many ways. You can setup many different types of probes. You can setup slave smokeping servers that can send their statistics and show you probes from other servers. You can also create your custom probes in perl. These options are currently not covered by this guide, please consult the documentation on the [Smokeping website](http://oss.oetiker.ch/smokeping/index.en.html) instead.

## Notes

### Smoketrace (Tr.cgi)

The [SmokeTraceroute](http://oss.oetiker.ch/smokeping/doc/smoketrace.en.html) utility is gone since v2.5.0 according to the [release notes](http://oss.oetiker.ch/smokeping/pub/CHANGES).