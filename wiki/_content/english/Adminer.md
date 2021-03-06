[Adminer](http://www.adminer.org/) is a web-based database management tool written in PHP. It is possible to manage [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [Sqlite3](/index.php/Sqlite3 "Sqlite3"), MS SQL, [Oracle](/index.php/Oracle "Oracle") and [Elasticsearch](/index.php/Elasticsearch "Elasticsearch").

It is a simpler alternative to [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin"). You can find more pieces of information about this project at the [official page](http://www.adminer.org/en/) or at [Wikipedia](https://en.wikipedia.org/wiki/Adminer "wikipedia:Adminer").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Apache](#Apache)
    *   [2.2 Nginx](#Nginx)
    *   [2.3 Hiawatha](#Hiawatha)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [adminer](https://aur.archlinux.org/packages/adminer/) package or [download Adminer](https://www.adminer.org/#download) and place it manually in the document-root instead.

When using the [adminer](https://aur.archlinux.org/packages/adminer/) package, Adminer will be installed as `/usr/share/webapps/adminer/index.php`.

Ensure the correct extensions in `/etc/php/php.ini` are uncommented, e.g. `extension=pdo_mysql` should provide [MySQL](/index.php/MySQL "MySQL") database management.

## Configuration

### Apache

Add the following line to `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-adminer.conf

```

Then [restart](/index.php/Restart "Restart") your [apache](/index.php/Apache "Apache") daemon.

Adminer can now be accessed by browsing to [http://localhost/adminer](http://localhost/adminer).

### Nginx

Ensure that the [PHP FastCGI interface](/index.php/Nginx#FastCGI "Nginx") is configured correctly.

Then add the following `server` block to your `/etc/nginx/nginx.conf` or place it in a file under `/etc/nginx/servers-available/` and [enable](/index.php/Nginx#Managing_server_entries "Nginx") it:

 `/etc/nginx/nginx.conf` 
```
server {
        listen 80;
        server_name db.domainname.dom;
        root /usr/share/webapps/adminer;

        # If you want to use a .htpass file, uncomment the three following lines.
        #auth_basic "Admin-Area! Password needed!";
        #auth_basic_user_file /usr/share/webapps/adminer/.htpass;
        #access_log /var/log/nginx/adminer-access.log;

        error_log /var/log/nginx/adminer-error.log;
        location / {
                index index.php;
                try_files $uri $uri/ /index.php?$args;
        }

       location ~ .php$ {
             include fastcgi.conf;
             #fastcgi_pass localhost:9000;
             fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
             fastcgi_index index.php;
             fastcgi_param SCRIPT_FILENAME /usr/share/webapps/adminer$fastcgi_script_name;
        }
}

```

Afterwards [restart](/index.php/Restart "Restart") [nginx](/index.php/Nginx "Nginx").

### Hiawatha

Ensure that the [PHP FastCGI interface](/index.php/Hiawatha#FastCGI "Hiawatha") is configured correctly.

Then add the following `VirtualHost` block to your `/etc/hiawatha/hiawatha.conf`.

 `/etc/hiawatha/hiawatha.conf` 
```
VirtualHost {

    # If you set WebsiteRoot to /usr/share/webapps/adminer you don't need followsymlinks
    # I symlinked the adminer folder to '/srv/http/adminer' so that I can easily remember where it's located but
    # still set 'WebsiteRoot' to the real source directory. You could point WebsiteRoot to the
    # symlinked directory, but you will have to set 'FollowSymlinks = yes' for that to function properly

    Hostname = db.domainname.dom
    #FollowSymlinks = yes
    #WebsiteRoot = /srv/http/adminer
    WebsiteRoot = /usr/share/webapps/adminer
    AccessLogfile = /var/log/hiawatha/adminer/access.log
    ErrorLogfile = /var/log/hiawatha/adminer/error.log
    StartFile = index.php
    UseFastCGI = PHP7

}
```

Then [restart](/index.php/Restart "Restart") the `hiawatha.service`.

## See also

*   [Official Adminer webpage](http://www.adminer.org/en/)
*   [Author's weblog](http://php.vrana.cz/)