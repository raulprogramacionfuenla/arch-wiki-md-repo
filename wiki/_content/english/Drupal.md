Related articles

*   [LAMP](/index.php/LAMP "LAMP")
*   [LAPP](/index.php/LAPP "LAPP")
*   [LASP](/index.php/LASP "LASP")
*   [MySQL](/index.php/MySQL "MySQL")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [SQLite](/index.php/SQLite "SQLite")
*   [Sendmail](/index.php/Sendmail "Sendmail")
*   [PostFix](/index.php/PostFix "PostFix")
*   [Exim](/index.php/Exim "Exim")

"Drupal is a free and open source content management system (CMS) and Content Management framework (CMF) written in PHP and distributed under the GNU General Public License." - [Wikipedia](https://en.wikipedia.org/wiki/Drupal "wikipedia:Drupal")

This article describes how to setup Drupal and configure [Apache](/index.php/Apache "Apache"), [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [PHP](/index.php/PHP "PHP"), and [Postfix](/index.php/Postfix "Postfix") to work with it. It is assumed that you have some sort of [LAMP](/index.php/LAMP "LAMP") (Linux, Apache, MySQL, PHP), LAPP (Linux, Apache, PostgreSQL, PHP) or LASP (Linux, Apache, SQLite, PHP) server already setup.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 Apache](#Apache)
    *   [2.3 Drupal](#Drupal)
*   [3 Commandline tools](#Commandline_tools)
    *   [3.1 Drush](#Drush)
    *   [3.2 Drupalconsole](#Drupalconsole)
    *   [3.3 PHP-Codesniffer-Drupal](#PHP-Codesniffer-Drupal)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Sending Mail](#Sending_Mail)
    *   [4.2 Scheduling with Cron](#Scheduling_with_Cron)
    *   [4.3 Upload progress not enabled](#Upload_progress_not_enabled)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [drupal](https://www.archlinux.org/packages/?name=drupal) package.

## Configuration

### PHP

Edit `/etc/php/php.ini`:

*   To enable support for image manipulation uncomment the line `extension=gd`

For database support enable a PDO extension for your database

*   To enable support for [SQLite](/index.php/SQLite "SQLite") uncomment the line `extension=pdo_sqlite`
*   To enable support for [MySQL](/index.php/MySQL "MySQL") uncomment the line `extension=pdo_mysql`
*   To enable support for [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") uncomment the line `extension=pdo_pgsql`

Apache will fail to start with an error finding php_admin_value, below fixes this:

[Install](/index.php/Install "Install") the [php-apache](https://www.archlinux.org/packages/?name=php-apache) package.

In `/etc/httpd/conf/httpd.conf`, comment the line:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so

```

and uncomment the line:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

Place this at the end of the `LoadModule` list:

```
LoadModule php7_module modules/libphp7.so
AddHandler php7-script .php

```

Place this at the end of the `Include` list:

```
Include conf/extra/php7_module.conf

```

Restart `httpd.service` using [systemd](/index.php/Systemd#Using_units "Systemd").

Apache will fail to start with an error finding open_basedir, below fixes this:

In `/etc/php/php.ini`, uncomment and suffix `open_basedir` to look like this:

```
open_basedir = /etc/webapps

```

### Apache

Copy the example Apache configuration file:

```
# cp /etc/webapps/drupal/apache.example.conf /etc/httpd/conf/extra/drupal.conf

```

And include it at the bottom of `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/drupal.conf

```

In `/etc/httpd/conf/httpd.conf`, also uncomment the `LoadModule rewrite_module modules/mod_rewrite.so` line.

### Drupal

Edit `/usr/share/webapps/drupal/.htaccess` and replace `Require all denied` by `Require all granted`.

Finally, [restart](/index.php/Restart "Restart") Apache (`httpd.service`). You can now access the Drupal installation at [http://localhost/drupal](http://localhost/drupal) .

## Commandline tools

### Drush

[Drush](http://www.drush.org/) is a command line shell and Unix scripting interface for Drupal. Drush core ships with lots of useful commands for interacting with code like modules/themes/profiles. Similarly, it runs update.php, executes sql queries and DB migrations, and misc utilities like run cron or clear cache. Drush can be extended by 3rd party commandfiles. It can be installed with the [drush](https://aur.archlinux.org/packages/drush/) package.

### Drupalconsole

[Drupalconsole](https://drupalconsole.com/) is a CLI tool to generate boilerplate code, interact and debug Drupal 8. It can be installed with the [drupalconsole](https://aur.archlinux.org/packages/drupalconsole/) package.

### PHP-Codesniffer-Drupal

[PHP-Codesniffer-Drupal](https://www.drupal.org/project/coder) checks your Drupal code against coding standards and other best practices. It can be installed with the [php-codesniffer-drupal](https://aur.archlinux.org/packages/php-codesniffer-drupal/) package.

## Tips and tricks

### Sending Mail

Drupal needs a Sendmail-compatible MTA like [Sendmail](/index.php/Sendmail "Sendmail"), [Postfix](/index.php/Postfix "Postfix") or [Exim](/index.php/Exim "Exim") if you plan to send mail from your local setup. Alternatively there are multiple solutions to send mail via external mail servers through SMTP or other means like [SMTP](https://drupal.org/project/smtp) or [PHPMailer](https://drupal.org/project/phpmailer). Use the [search page](https://www.drupal.org/search/site/mail) to find more possibilities.

### Scheduling with Cron

Drupal recommends running cron jobs hourly. Cron can be executed from the browser by visiting [http://localhost/drupal/cron](http://localhost/drupal/cron). It is also possible to run cron via script by copying the appropriate file from the "scripts" folder into `/etc/cron.hourly` and making it executable.

### Upload progress not enabled

Upon successful installation you may see the following message in the Status Report:

 `Your server is capable of displaying file upload progress, but does not have the required libraries. It is recommended to install the PECL uploadprogress library (preferred) or to install APC.` 

First, install the [php-pear](https://aur.archlinux.org/packages/php-pear/) package. Next, use the **pecl** command to automatically download, compile and install the library:

```
# pecl install uploadprogress

```

Finally, add to `/etc/php/php.ini`

```
extension=uploadprogress

```

Restart Apache.

## See also

*   [Official Drupal documentation](http://drupal.org/handbook)
*   [Simple guide to install Drupal on Xampp](http://drupal.org/node/307956)