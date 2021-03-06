[uWSGI](https://uwsgi-docs.readthedocs.io/en/latest/) is a fast, self-healing and developer/sysadmin-friendly application container server coded in pure C.

There are alternatives written in Python such as [gunicorn](https://www.archlinux.org/packages/?name=gunicorn).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Web applications](#Web_applications)
        *   [2.1.1 Python](#Python)
        *   [2.1.2 PHP](#PHP)
    *   [2.2 Web server](#Web_server)
        *   [2.2.1 Nginx](#Nginx)
        *   [2.2.2 Nginx (in chroot)](#Nginx_(in_chroot))
*   [3 Running uWSGI](#Running_uWSGI)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Socket activation](#Socket_activation)
    *   [4.2 Hardening uWSGI](#Hardening_uWSGI)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Apache httpd](#Apache_httpd)
        *   [5.1.1 AH00957: uwsgi: attempt to connect to 127.0.0.1:0 (*) failed](#AH00957:_uwsgi:_attempt_to_connect_to_127.0.0.1:0_(*)_failed)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [uwsgi](https://www.archlinux.org/packages/?name=uwsgi) package. Plugins need to be installed separately (their package names start with `uwsgi-plugin-`).

## Configuration

[Web applications](/index.php/Web_applications "Web applications") served by uWSGI are configured in `/etc/uwsgi/`, where each of them requires its own configuration file (ini-style). Details can be found [in the uWSGI documentation](http://uwsgi-docs.readthedocs.org/en/latest/).

Alternatively, you can run uWSGI in [Emperor mode](http://uwsgi-docs.readthedocs.org/en/latest/Emperor.html) (configured in `/etc/uwsgi/emperor.ini`). It enables a single uWSGI instance to run a set of different apps (called vassals) using a single main supervisor (called emperor).

**Note:** The plugins must be explicitly loaded before their options can be used, otherwise the options will not be recognized. This can be done with the `--plugins` command-line option or with the `plugins` variable in the config file.

### Web applications

uWSGI supports many different languages and thus also many web applications. As an example the configuration file `/etc/uwsgi/example.ini` and the prior installation of the plugin needed for your web application is assumed.

#### Python

The following is a simple example for a [Python](/index.php/Python "Python") application.

 `/etc/uwsgi/example.ini` 
```
[uwsgi]
chdir = /srv/http/example
module = example
plugins = python
```

It is also possible to run uWSGI separately with the following syntax for instance:

```
$ uwsgi --socket 127.0.0.1:3031 --plugin python2 --wsgi-file ~/foo.py --master --processes 4 --threads 2 --stats 127.0.0.1:9191 --uid --gid

```

You should avoid running this command as root.

**Note:** Pay attention to operational mode in use, preforking without --lazy-apps may cause non-obvious behavior. By default the Python plugin does not initialize the GIL. This means your app-generated threads will not run. If you need threads, remember to enable them with enable-threads. Running uWSGI in multithreading mode (with the threads options) will automatically enable threading support. This "strange" default behaviour is for performance reasons, no shame in that. [[1]](https://uwsgi-docs.readthedocs.io/en/latest/ThingsToKnow.html)

#### PHP

The following is a simple example for a [PHP](/index.php/PHP "PHP") based website.

 `/etc/uwsgi/example.ini` 
```
[uwsgi]
; maximum number of worker processes
processes = 4
; the user and group id of the process once it’s started
uid = http
gid = http
socket = /run/uwsgi/%n.sock
master = true
chdir = /srv/http/%n
; php
plugins = php
; jail our php environment
php-docroot = /srv/http/%n
php-index = index.php
; clear environment on exit
vacuum = true
```

### Web server

uWSGI can be the backend to many web servers, that support the forwarding of access. The following are examples for configurations.

**Note:** It is recommended to read through the uWSGI documentation to understand the configuration from both performance and security point of view.

#### Nginx

[nginx](/index.php/Nginx "Nginx") can redirect access towards unix sockets or ports (on localhost or remote machine), depending on your web application.

 `/etc/nginx/example.conf` 
```
# ...
# forward all access to / towards 
location / {
  root /usr/share/nginx/html;
  index index.html index.htm;
  include uwsgi_params;
  # this is the correct uwsgi_modifier1 parameter for a php based application
  uwsgi_modifier1 14;
  # uncomment the following if you want to use the unix socket instead
  # uwsgi_pass unix:/var/run/uwsgi/example.sock;
  # access is redirected to localhost:3031
  uwsgi_pass 127.0.0.1:3031;
}
# ...

```

**Tip:** Have a look at [the documentation](https://uwsgi-docs.readthedocs.io/en/latest/Protocol.html#packet-descriptions) for the list of `uwsgi_modifier1` parameters fitting to your web application.

#### Nginx (in chroot)

**Note:** This section assumes that you have deployed Nginx as described in [Nginx#Installation in a chroot](/index.php/Nginx#Installation_in_a_chroot "Nginx"). It is assumed that the Nginx chroot is located in `/srv/http`.

First create ini file that will point to your application:

 `/etc/uwsgi/application1.ini` 
```
[uwsgi]
chroot = /srv/http
chdir = /www/application1
wsgi-file = application1.py
plugins = python
socket = /run/application1.sock
uid = http
gid = http
threads = 2
stats = 127.0.0.1:9191
vacuum = true

```

Since we are chrooting to `/srv/http` above configuration will result in following unix socket being created `/srv/http/run/application1.sock`

**Note:**

*   Your application must be placed within `/srv/http/www/application1` before service is started. Depending on configuration your application may be cached so you may need to restart the service when you modify it.
*   If you are deploying python application you may need to copy standard python libraries - if you develop under python 3 then you can copy them from `/usr/lib/python3.6` to `/srv/http/lib/python3.6`.

You can try to run following:

```
# cp -r -p /usr/lib/python3.6 /srv/http/lib
# cp -r -p /usr/lib/*python*so /srv/http/lib

```

You will need to disable notifications within your service file:

 `/etc/systemd/system/multi-user.target.wants/uwsgi\@application1.service` 
```
[Unit]
Description=uWSGI service unit
After=syslog.target

[Service]
PIDFile=/run/%I.pid
RemainAfterExit=yes
ExecStart=/usr/bin/uwsgi --ini /etc/uwsgi/%I.ini
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -INT $MAINPID
Restart=always
StandardError=syslog
KillSignal=SIGQUIT

[Install]
WantedBy=multi-user.target

```

**Note:** PID file will be created within `/run` rather than `/srv/http/run`

After modification make sure to [reload](/index.php/Reload "Reload") to incorporate the new or changed units.

You are then free to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `uwsgi@application1.service`.

Edit `/srv/http/etc/nginx/nginx.conf` and add new `server` section within it that would contain at least following:

 `/srv/http/etc/nginx/nginx.conf` 
```
...
    server
    {
        listen       80;
        server_name  127.0.0.1;
        location /
        {
            root   /www/application1;
            include uwsgi_params;
            uwsgi_pass unix:/run/application1.sock;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html
        {
            root   /usr/share/nginx/html;
        }
    }
...

```

Make sure to now [restart](/index.php/Restart "Restart") `nginx.service` to have your `application1` be served at `127.0.0.1`.

## Running uWSGI

**Note:** This assumes the used web application has been properly configured, is being served by your web server, which redirects towards the socket or port it is using and was configured in `/etc/uwsgi/`. For simplicity, the configuration file names should contain only alphanumeric characters and `_` to avoid problems with escaping, see [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5#STRING_ESCAPING_FOR_INCLUSION_IN_UNIT_NAMES).

If you plan on using a web application all the time (without it being activated on demand), you can simply [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `uwsgi@example`.

If you plan on having your web application be started on demand you can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `uwsgi@example.socket`.

To use the Emperor mode, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `emperor.uwsgi.service`.

To use socket activation of this mode [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `emperor.uwsgi.socket`.

## Tips and tricks

Some functionality, that uWSGI offers is not accessible by using the [systemd](/index.php/Systemd "Systemd") service files provided in the [official repositories](/index.php/Official_repositories "Official repositories"). Changes to them are explained in the following sections. For further information see [[2]](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/).

### Socket activation

Using socket activation, you want to

*   direct your web server to a unix socket and thereby start your uWSGI instance running the application
*   you most likely want to have the application be closed by uWSGI after a certain idle time
*   you want your web server be able to start the application again, once it is accessed

uWSGI offers settings, with which you can have the instance close the application:

 `/etc/uwsgi/example.ini` 
```
[uwsgi]
# ...

# set idle time in seconds
idle = 600
# kill the application after idle time was reached
kill-on-idle = true

# ...

```

The current `uwsgi@.service` file however does not allow this, because [systemd](/index.php/Systemd "Systemd") treats non-zero exit codes as failure and thereby marking the unit as failed and additionally the `Restart=always` directive makes a closing after idle time useless. A fix for this is to add the exit codes, that uWSGI may provide after closing an application by itself to a list, that [systemd](/index.php/Systemd "Systemd") will treat as success by using the `SuccessExitStatus` directive (for further information see [[3]](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/)).

 `/etc/systemd/system/uwsgi-socket@.service` 
```
[Unit]
Description=uWSGI service unit
After=syslog.target

[Service]
ExecStart=/usr/bin/uwsgi --ini /etc/uwsgi/%I.ini
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -INT $MAINPID
Type=notify
SuccessExitStatus=15 17 29 30
StandardError=syslog
NotifyAccess=all
KillSignal=SIGQUIT

[Install]
WantedBy=multi-user.target

```

This will allow for proper socket activation with kill-after-idle functionality.

### Hardening uWSGI

Web applications are exposed to the wild and depending on their quality and the security of their underlying languages, some are more dangerous to run, than others. A good way to start dealing with possible unsafe web applications is to jail them. [systemd](/index.php/Systemd "Systemd") has some functionality, that can be put to use. Have a look at the following example (and for further information see [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5) and [[4]](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/)):

 `/etc/systemd/system/uwsgi-secure@.service` 
```
[Unit]
Description=uWSGI service unit
After=syslog.target

[Service]
ExecStart=/usr/bin/uwsgi --ini /etc/uwsgi/%I.ini
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -INT $MAINPID
Type=notify
SuccessExitStatus=15 17 29 30
StandardError=syslog
NotifyAccess=all
KillSignal=SIGQUIT
PrivateDevices=yes
PrivateTmp=yes
ProtectSystem=full
ReadWriteDirectories=/etc/webapps /var/lib/
ProtectHome=yes
NoNewPrivileges=yes

[Install]
WantedBy=multi-user.target

```

**Note:**

*   Using `NoNewPrivileges=yes` does not work with [Mailman](/index.php/Mailman "Mailman")'s cgi frontend! Remove this setting, if you want to use it in conjunction with it.
*   If you want to harden your uWSGI app further, the use of namespaces is advisable. You can get a first glance on that topic in the [uWSGI namespaces documentation](http://uwsgi-docs.readthedocs.io/en/latest/Namespaces.html).

## Troubleshooting

### Apache httpd

#### AH00957: uwsgi: attempt to connect to 127.0.0.1:0 (*) failed

The default uWSGI port (3031) does not work (currently?) with Apache httpd server. See [[5]](https://github.com/unbit/uwsgi/issues/1491) for details.

## See also

*   [Official Documentation](http://uwsgi-docs.readthedocs.org/en/latest)
*   [uWSGI Github](https://github.com/unbit/uwsgi-docs)
*   [Securely serving webapps using uWSGI](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/)
*   [Fluffy White Stuff Benchmark](http://blog.kgriffs.com/)
*   [Flask uWSGI deploying](http://flask.pocoo.org/docs/deploying/uwsgi/)
*   [Django and uWSGI](https://docs.djangoproject.com/en/dev/howto/deployment/wsgi/uwsgi/)
*   [Apache and uWSGI](http://uwsgi-docs.readthedocs.org/en/latest/Apache.html)