From [AWStats - Free log file analyzer for advanced statistics](http://awstats.sourceforge.net/):

	*AWStats is a free powerful and featureful tool that generates advanced web, streaming, ftp or mail server statistics, graphically. This log analyzer works as a CGI or from command line and shows you all possible information your log contains, in few graphical web pages. It uses a partial information file to be able to process large log files, often and quickly. It can analyze log files from all major server tools like Apache log files (NCSA combined/XLF/ELF log format or common/CLF log format), WebStar, IIS (W3C log format) and a lot of other web, proxy, wap, streaming servers, mail servers and some ftp servers.*

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enable mod_perl for Apache](#Enable_mod_perl_for_Apache)
    *   [2.2 Configure Apache to log for AWStats](#Configure_Apache_to_log_for_AWStats)
    *   [2.3 Including AWStats configuration in Apache's configuration](#Including_AWStats_configuration_in_Apache's_configuration)
    *   [2.4 AWStats Configuration](#AWStats_Configuration)
*   [3 Nginx](#Nginx)
*   [4 Generating Statistics](#Generating_Statistics)
*   [5 GeoIP (optional)](#GeoIP_(optional))
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [awstats](https://www.archlinux.org/packages/?name=awstats) package. When [Apache](/index.php/Apache "Apache") is used as a web server, the [mod_perl](https://aur.archlinux.org/packages/mod_perl/) package is required as well.

## Configuration

### Enable mod_perl for Apache

To enable `mod_perl` in Apache, you should add following line to Apache configuration (`/etc/httpd/conf/httpd.conf`).

```
 LoadModule perl_module modules/mod_perl.so

```

### Configure Apache to log for AWStats

By default AWStats requires Apache to record access logs as 'combined'. Unless you want a different behavior, you should set your access log format as 'combined'. To do so, your Apache configuration should look like this:

```
 <VirtualHost *:80>
     ServerAdmin zxc@returnfalse.net
     DocumentRoot "/srv/http/xxx"
     ServerName www.returnfalse.net
     ErrorLog "/var/log/httpd/returnfalse-error_log"
     CustomLog "/var/log/httpd/returnfalse-access_log" combined
 </VirtualHost>

```

The important line here is:

```
 CustomLog "/var/log/httpd/returnfalse-access_log" combined

```

**Warning:** At this point, if apache has started to log access with different format, AWStats will complain about this because it cannot read. So if you are changing Apache's log format now, you probably should delete old log files not to confuse AWStats.

### Including AWStats configuration in Apache's configuration

If you set the log format, then next step is including AWStats config file in Apache. The package in the AUR has a default one, and it's working without any problem. But in case you want to create your own configuration, default one is this:

```
 Alias /awstatsclasses "/usr/share/webapps/awstats/classes/"
 Alias /awstatscss "/usr/share/webapps/awstats/css/"
 Alias /awstatsicons "/usr/share/webapps/awstats/icon/"
 ScriptAlias /awstats/ "/usr/share/webapps/awstats/cgi-bin/"

 <Directory "/usr/share/webapps/awstats">
     Options None
     AllowOverride None
     Require all granted
 </Directory>

```

Include this file (in AUR case, the path is `/etc/httpd/conf/extra/httpd-awstats.conf`) to Apache's main configuration:

```
 Include conf/extra/httpd-awstats.conf

```

Now if you have done all steps correctly, you should be able to see AWStats running on [http://localhost/awstats/awstats.pl](http://localhost/awstats/awstats.pl) **of course after restarting Apache**.

```
 # /etc/rc.d/httpd restart

```

One last thing, which is the actual aim, make AWStats read logs and convert them to stats.

### AWStats Configuration

The package comes with an script to update stats shown on AWStats. This script reads AWStats configuration files in `/etc/awstats` and updates the stats for the sites that are defined in these configuration files. Instead of creating these configuration files, you can use AWStats' configuration tool. Run:

```
 perl /usr/share/awstats/tools/awstats_configure.pl

```

and follow the instructions. If you successfully created config file there is one thing that you should modify manually. Open the configuration file created by `awstats_configure.pl` with your favorite text editor. Then find the line on which `LogFile` variable is defined, and set it as the path that Apache logs accesses (which you set to be logged as 'combined' format before):

```
 LogFile=/var/log/httpd/returnfalse-access_log

```

Now you can run the script to test the results, e.g. if you have a `/etc/awstats/awstats.apache.conf` then run

```
 /usr/share/awstats/tools/awstats_buildstaticpages.pl config=apache -update -awstatsprog=/usr/share/webapps/awstats/cgi-bin/awstats.pl -dir=/srv/http/awstats

```

**Warning:** With these settings anyone will be able to reach AWStats. Setting a authentication would help keeping these stats private.

## Nginx

If your web server software is nginx, follow steps below:

1\. Install awstats as described above. It is necessary to get the folders and files owned by user "http" and group "http" with the following command:

```
chown -R http:http /usr/share/webapps/awstats/

```

2\. Use awstats configuration tool to generate a site configuration file as described above. Make sure the following lines are set correctly:

```
LogFile="/var/log/nginx/access.log"
LogFormat=1

```

3\. To make the Perl scripts of awstats work on nginx, create /etc/nginx/cgi-bin.php script with the following code:

```
<?php
$descriptorspec = array(
   0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
   1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
   2 => array("pipe", "w")   // stderr is a file to write to
);
$newenv = $_SERVER;
$newenv["SCRIPT_FILENAME"] = $_SERVER["X_SCRIPT_FILENAME"];
$newenv["SCRIPT_NAME"] = $_SERVER["X_SCRIPT_NAME"];
if (is_executable($_SERVER["X_SCRIPT_FILENAME"])) {
   $process = proc_open($_SERVER["X_SCRIPT_FILENAME"], $descriptorspec, $pipes, NULL, $newenv);
   if (is_resource($process)) {
       fclose($pipes[0]);
       $head = fgets($pipes[1]);
       while (strcmp($head, "
")) {
           header($head);
           $head = fgets($pipes[1]);
       }
       fpassthru($pipes[1]);
       fclose($pipes[1]);
       fclose($pipes[2]);
       $return_value = proc_close($process);
   } else {
       header("Status: 500 Internal Server Error");
       echo("Internal Server Error");
   }
} else {
   header("Status: 404 Page Not Found");
   echo("Page Not Found");
}
?> 

```

4\. Add these directives to the domain nginx config file:

```
location ^~ /awstatsicons {
   alias /usr/share/webapps/awstats/icon/;
   access_log off;
}
location ^~ /awstatscss {
   alias /usr/share/webapps/awstats/examples/css/;
   access_log off;
}
location ^~ /awstatsclasses {
   alias /usr/share/webapps/awstats/examples/classes/;
   access_log off;
}
location ~ ^/cgi-bin/.*\.(cgi|pl|py|rb) {
   gzip off;
   fastcgi_pass  unix:/var/run/php-fpm/php-fpm.sock;
   fastcgi_index cgi-bin.php;
   fastcgi_param SCRIPT_FILENAME    /etc/nginx/cgi-bin.php;
   fastcgi_param SCRIPT_NAME        /cgi-bin/cgi-bin.php;
   fastcgi_param X_SCRIPT_FILENAME  /usr/share/webapps/awstats$fastcgi_script_name;
   fastcgi_param X_SCRIPT_NAME      $fastcgi_script_name;
   fastcgi_param QUERY_STRING       $query_string;
   fastcgi_param REQUEST_METHOD     $request_method;
   fastcgi_param CONTENT_TYPE       $content_type;
   fastcgi_param CONTENT_LENGTH     $content_length;
   fastcgi_param GATEWAY_INTERFACE  CGI/1.1;
   fastcgi_param SERVER_SOFTWARE    nginx;
   fastcgi_param REQUEST_URI        $request_uri;
   fastcgi_param DOCUMENT_URI       $document_uri;
   fastcgi_param DOCUMENT_ROOT      $document_root;
   fastcgi_param SERVER_PROTOCOL    $server_protocol;
   fastcgi_param REMOTE_ADDR        $remote_addr;
   fastcgi_param REMOTE_PORT        $remote_port;
   fastcgi_param SERVER_ADDR        $server_addr;
   fastcgi_param SERVER_PORT        $server_port;
   fastcgi_param SERVER_NAME        $server_name;
   fastcgi_param REMOTE_USER        $remote_user;
}

```

5\. You can access your awstats page of your site at **"http://your_domain.com/cgi-bin/awstats.pl?config=your_domain.com"** Optionally, you may want to add this rewrite rule to the nginx site config file:

```
location ~ ^/awstats {
   rewrite ^ http://your_domain.com/cgi-bin/awstats.pl?config=your_domain.com;
}

```

With this you can access your awstats page simply by typing **"http://your_domain.com/awstats"** in the address bar of your browser.

## Generating Statistics

You can generate the latest statistics of all your sites manually by issuing the following command:

```
/usr/share/awstats/tools/awstats_updateall.pl now -awstatsprog=/usr/share/webapps/awstats/cgi-bin/awstats.pl

```

This process can be automated by cron. See AWStats cron template: `/usr/share/doc/awstats-7.5/cron.hourly` However, if you are using logrotate, you have to make sure the cronjob starts right before logrotate runs. Otherwise, statistics will be lost because loratate will change the access log file name to a different name not accessible by awstats. A better way to deal with this is to use web server specific logrotate script normally located in */etc/logrotate.d* to trigger the awstats calculation. An example of nginx logrotate script is provided here. Note the addition of a *prerotate* directive:

```
/var/log/nginx/*log {
 daily
 missingok
 notifempty
 create 640 http log
 compress
 sharedscripts
 prerotate
   # Trigger awstats computation
   /usr/share/awstats/tools/awstats_updateall.pl now -awstatsprog=/usr/share/webapps/awstats/cgi-bin/awstats.pl
 endscript
 postrotate
    test ! -r /run/nginx.pid || kill -USR1 `cat /run/nginx.pid`
 endscript
}

```

## GeoIP (optional)

To add geo ip support, install Geo::IP module using cpan. (See [Perl#CPAN.pm](/index.php/Perl#CPAN.pm "Perl") for more details.) Alternatively, install [perl-geoip](https://aur.archlinux.org/packages/perl-geoip/) from [AUR](/index.php/AUR "AUR"). Add the following line to each of the awstats site configuration files located in /etc/awstats/:

```
LoadPlugin="geoip GEOIP_STANDARD /usr/share/GeoIP/GeoIP.dat"

```

## See also

*   [mod_perl](/index.php/Mod_perl "Mod perl") Apache + Perl