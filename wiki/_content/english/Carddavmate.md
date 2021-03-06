[Carddavmate](http://www.inf-it.com/) is a CardDAV client that runs in a web browser using JavaScript. It is useful when you have a CardDAV server and want to access the contacts on this server with only a web browser.

This guide shows you how to install carddavmate to use with davical.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Password Protection](#Password_Protection)
    *   [2.2 Carddav server](#Carddav_server)
    *   [2.3 Apache](#Apache)
    *   [2.4 Testing](#Testing)
    *   [2.5 Security](#Security)
*   [3 Troubleshooting](#Troubleshooting)

## Installation

Install the [carddavmate](https://aur.archlinux.org/packages/carddavmate/) package.

After that, `config.js` needs to be configured, as well as `httpd-carddavmate.conf`. Then, `httpd-carddavmate.conf` needs to be included in the [Apache](/index.php/Apache "Apache") configuration, and Apache needs to be restarted.

## Configuration

### Password Protection

Password protection is implemented using apache's `htpasswd` facility. The relevant file that includes the authentification credentials is at `/srv/http/carddavmate/htpasswd`.

You may delete the file or remove the "test" account by deleting the line from the file.

To add your own user, run:

```
# htpasswd /srv/http/carddavmate/htpasswd

```

add `-c` after *htpasswd* if you deleted the `htpasswd` file.

### Carddav server

Add the carddav server to your config by editing `/srv/http/carddavmate/config.js`, for example:

```
var globalSettings=[{href: '[https://carddav.example.com:443/caldav.php/joe/'](https://carddav.example.com:443/caldav.php/joe/'), userAuth: {userName: 'joe', userPassword: 'secret', serverPassword: false}, timeOut: 14000}];

```

A better example, without insecure user clear passwords:

```
var globalSettings=[{href: '[https://carddav.example.com:443/caldav.php/USER'}](https://carddav.example.com:443/caldav.php/USER'})];

```

### Apache

To "serve" the `/srv/http/carddavmate` directory properly, include `/etc/httpd/conf/extra/httpd-carddavmate.conf` in your apache configuration. To do this, add the following line to `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-carddavmate.conf

```

Also, edit `httpd-carddavmate.conf` to reflect the url where carddavmate is installed, for example:

```
Header always set Access-Control-Allow-Origin "[https://carddavmate.example.com](https://carddavmate.example.com)"

```

Save this file and [restart](/index.php/Restart "Restart") Apache with `httpd.service`.

### Testing

To test your installation, browse to `[https://127.0.0.1/carddavmate](https://127.0.0.1/carddavmate)` and see if your carddav data shows up.

### Security

Since the client is a javascript program that runs in your browser, the username/password that is configured in `config.js` on the server is also in the browser and can be easily seen. To avoid issues, clear your browser cache to delete the compromising files after you are done.

## Troubleshooting

Troubleshooting is best done using chrome's built-in javascript console.