[InspIRCd](http://www.inspircd.org/) (Inspire IRC daemon) is a modular and lightweight IRC daemon written in C++. As it is one of the few IRCd projects written from scratch, it avoids a number of design flaws and speed issues that plague other more established IRCd projects with the same or less features, such as UnrealIRCd 3\. It's the IRCd used by the [Chatspike IRC network](http://www.chatspike.net/).

## Contents

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
*   [3 Loading modules](#Loading_modules)
    *   [3.1 Third-party modules](#Third-party_modules)
*   [4 Starting/Stopping the daemon](#Starting.2FStopping_the_daemon)
*   [5 External links](#External_links)

## Installing

**Note:** Before you begin, check that you do not have any user or group named `inspircd` as the package will create and run using this user privileges (for security reasons).

[Install](/index.php/Install "Install") the [inspircd](https://aur.archlinux.org/packages/inspircd/) package.

## Configuring

The configuration file `/etc/inspircd/inspircd.conf` is **mandatory**, XML-formatted and needs to be created when installing.

How you set your configuration file will depend a lot on your needs and system configuration, reason why there's no configuration file set by default.

**Tip:** You can use the example (and very well documented) configuration file located at `/usr/share/inspircd/examples/inspircd.conf.example`. Copy this file to `/etc/inspircd/inspircd.conf`, read and edit it carefully to fit your needs.

Its HTML format may be somewhat different of what most of the people is used to. The format of an instruction within the configuration file looks like the following:

```
<tagname variable="value">

```

**Note:** The example file has some `<die value="anything here">` lines in the example file to make sure you read the entire thing. You must remove these entries otherwise the server will not start.

Make sure to set the pidfile to `/var/lib/inspircd/inspircd.pid`, as explained in the package's [install script](https://aur.archlinux.org/cgit/aur.git/tree/inspircd.install?h=inspircd).

Further information is available at the [InspIRCd configuration](http://wiki.inspircd.org/Configuration) wiki page.

## Loading modules

By default, InspIRCd loads no modules. As every feature outside of [RFC 1459](http://tools.ietf.org/html/rfc1459) is actually a module, by loading no modules your ircd really won't do anything impressive. You can load modules by adding for instance:

```
<module name="m_silence.so">

```

This will load the m_silence module (which provides the somewhat standard SILENCE list facility). You must restart the daemon for changes to take effect. A list of the available modules is available at the [InspIRCd modules](https://wiki.inspircd.org/2.0/Modules) wiki page.

### Third-party modules

To install a third-party module, save the `[module].cpp` within `[build-dir]/inspircd/src/inspircd/src/modules/` and continue the build process. If you have already built and installed InspIRCd and have the source files intact, compile the module with `./configure -modupdate; make` and copy to: `/usr/lib/inspircd/modules/`.

## Starting/Stopping the daemon

[Start](/index.php/Start "Start") or [stop](/index.php/Stop "Stop") the `inspircd` systemd unit.

The first start fails sometimes so try restarting until you get no errors. After this you shall have no further problems. The reason behind this is because of security reasons the daemon doesn't run as root as you normally would see, so the script must ensure that the user **irc** has permission to write/read the pid and log files.

## External links

*   [Inspire IRCd (website)](http://www.inspircd.org)
*   [Inspire IRCd (wiki)](http://wiki.inspircd.org/Main_Page)
*   [Inspire IRCd (irc channel)](irc://irc.inspircd.org/inspircd)