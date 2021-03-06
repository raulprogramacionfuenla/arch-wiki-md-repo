## Contents

*   [1 Installation](#Installation)
*   [2 mod_fastcgi](#mod_fastcgi)
*   [3 mod_fcgid](#mod_fcgid)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

There are two FastCGI modules for Apache:

*   [mod_fastcgi](https://httpd.apache.org/mod_fcgid/)
*   [mod_fcgid](https://httpd.apache.org/mod_fcgid/)

They both have permissive licenses (custom for mod_fastcgi and GPL for mod_fcgid).

Apache 2.4 (available in the [official repositories](/index.php/Official_repositories "Official repositories") as [apache](https://www.archlinux.org/packages/?name=apache)) now provides an official module, [mod_proxy_fcgi](http://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html). See [configuration example for php-fpm](http://wiki.apache.org/httpd/PHP-FPM) and [wiki article on set-up using archlinux](/index.php/Apache_HTTP_Server#Using_php-fpm_and_mod_proxy_fcgi "Apache HTTP Server").

## mod_fastcgi

[Install](/index.php/Install "Install") [mod_fastcgi](https://www.archlinux.org/packages/?name=mod_fastcgi) from the official repositories.

First you need to load the fastcgi module. Make sure that the following is **present** and **uncommented** in your `httpd.conf`:

```
LoadModule fastcgi_module modules/mod_fastcgi.so

```

Then you need to tell Apache when to use FastCGI.

For example you can ask Apache to treat all .fcgi files as fastcgi applications:

```
<IfModule fastcgi_module>
  AddHandler fastcgi-script .fcgi # you can put whatever extension you want
</IfModule>

```

Remember that standard CGI restrictions apply, files must be in an ExecCGI enabled directory to execute.

## mod_fcgid

[Install](/index.php/Install "Install") the [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) package.

First you need to load the fastcgi module. Make sure that the following is **present** and **uncommented** in your `httpd.conf`:

```
LoadModule fcgid_module modules/mod_fcgid.so

```

Then you need to tell Apache when to use FastCGI.

For example you can ask Apache to treat all .fcgi files as fastcgi applications:

```
<IfModule fcgid_module>
  AddHandler fcgid-script .fcgi # you can put whatever extension you want
</IfModule>

```

Remember that standard CGI restrictions apply, files must be in an ExecCGI enabled directory to execute.

## Troubleshooting

It doesn't work? Apache error log (`/var/log/httpd/error_log`) should help you find the problem.

## See also

*   [lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd")
*   [Apache HTTP Server#Using php-fpm and mod_proxy_fcgi](/index.php/Apache_HTTP_Server#Using_php-fpm_and_mod_proxy_fcgi "Apache HTTP Server")