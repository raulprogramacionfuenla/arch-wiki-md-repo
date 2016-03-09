From the project [home page](https://tox.chat/):

	*Tox is a distributed, secure messenger with audio and video chat capabilities.*

## Installation

Install one of many [Tox clients](https://wiki.tox.chat/clients). [toxcore](https://www.archlinux.org/packages/?name=toxcore) is installed as a dependency.

Currently two clients are available in the official repositories:

*   **qTox** — Powerful Tox client written in QT

	[https://wiki.tox.chat/clients/qtox](https://wiki.tox.chat/clients/qtox) || [qtox](https://www.archlinux.org/packages/?name=qtox)

*   **Toxic** — ncurses-based CLI

	[https://wiki.tox.chat/clients/toxic](https://wiki.tox.chat/clients/toxic) || [toxic](https://www.archlinux.org/packages/?name=toxic)

Alternatively, select a client from the AUR:

*   **gTox** — GTK3-Style Tox-Client

	[https://github.com/KoKuToru/gTox/](https://github.com/KoKuToru/gTox/) || [gtox-git](https://aur.archlinux.org/packages/gtox-git/)

*   **µTox (uTox)** — Lightweight Tox client

	[https://github.com/GrayHatter/utox/](https://github.com/GrayHatter/utox/) || [utox-git](https://aur.archlinux.org/packages/utox-git/)

*   **Ratox** — FIFO based client

	[http://ratox.2f30.org/](http://ratox.2f30.org/) || [ratox-git](https://aur.archlinux.org/packages/ratox-git/)

*   **qTox** — Powerful Tox client written in QT

	[https://wiki.tox.chat/clients/qtox](https://wiki.tox.chat/clients/qtox) || [qtox-git](https://aur.archlinux.org/packages/qtox-git/)

*   **Ricin** — Lightweight and fully-Hackable Tox client powered by Vala & Gtk3

	[https://ricin.im/](https://ricin.im/) || [ricin-git](https://aur.archlinux.org/packages/ricin-git/)

*   **Tox Pidgin Protocol Plugin** — a plugin for Pidgin which allows the use of the Tox protocol within Pidgin

	[http://tox.dhs.org/](http://tox.dhs.org/) || [tox-prpl-git](https://aur.archlinux.org/packages/tox-prpl-git/)

*   **Toxic** — ncurses-based CLI

	[https://wiki.tox.chat/clients/toxic](https://wiki.tox.chat/clients/toxic) || [toxic-git](https://aur.archlinux.org/packages/toxic-git/)

## Run a node

To be able to connect to others, Tox needs to connect to a [DHT node](https://wiki.tox.chat/users/nodes) first. All DHT nodes are connected to each other, and since everyone is connected to at least one DHT node, you can connect to others one way or the other.

Move the service file to the correct location

By default, the service file for the tox bootstrap is in /usr/lib/systemd/system, where systemd cannot locate it, so it must be moved to /etc/systemd/system

```
# mv /usr/lib/systemd/system/tox-bootstrapd.service /etc/systemd/system

```

Create user for running the daemon and configuration folder.

```
# useradd --no-create-home --shell /bin/false --user-group tox-bootstrapd
# mkdir --verbose /etc/tox
# chown --recursive --verbose tox-bootstrapd:tox-bootstrapd /etc/tox

```

Reload *systemd*, scanning for new units:

```
# systemctl daemon-reload

```

Create the configuration file

Copy the file below to /etc/tox-bootstrapd.conf

 `/etc/tox-bootstrapd.conf` 
```
// Tox DHT bootstrap daemon configuration file.

// Listening port (UDP).
port = 33445

// A key file is like a password, so keep it where no one can read it.
// If there is no key file, a new one will be generated.
// The daemon should have permission to read/write it.
keys_file_path = "/var/lib/tox-bootstrapd/keys"

// The PID file written to by the daemon.
// Make sure that the user that daemon runs as has permissions to write to the
// PID file.
pid_file_path = "/var/run/tox-bootstrapd/tox-bootstrapd.pid"

// Enable IPv6.
enable_ipv6 = true

// Fallback to IPv4 in case IPv6 fails.
enable_ipv4_fallback = true

// Automatically bootstrap with nodes on local area network.
enable_lan_discovery = true

enable_tcp_relay = true

// While Tox uses 33445 port by default, 443 (https) and 3389 (rdp) ports are very
// common among nodes, so it's encouraged to keep them in place.
tcp_relay_ports = [443, 3389, 33445]

// Reply to MOTD (Message Of The Day) requests.
enable_motd = true

// Just a message that is sent when someone requests MOTD.
// Put anything you want, but note that it will be trimmed to fit into 255 bytes.
motd = "tox-bootstrapd"

// Any number of nodes the daemon will bootstrap itself off.
//
// Remember to replace the provided example with your own node list.
// There is a maintained list of bootstrap nodes on Tox's wiki, if you need it
// ([https://wiki.tox.chat/doku.php?id=users:nodes](https://wiki.tox.chat/doku.php?id=users:nodes)).
//
// You may leave the list empty or remove "bootstrap_nodes" completely,
// in both cases this will be interpreted as if you don't want to bootstrap
// from anyone.
//
// address = any IPv4 or IPv6 address and also any US-ASCII domain name.
bootstrap_nodes = (
  { // Example Node 1 (IPv4)
    address = "127.0.0.1"
    port = 33445
    public_key = "728925473812C7AAC482BE7250BCCAD0B8CB9F737BF3D42ABD34459C1768F854"
  },
  { // Example Node 2 (IPv6)
    address = "::1/128"
    port = 33445
    public_key = "3E78BACF0F84235B30054B54898F56793E1DEF8BD46B1038B9D822E8460FAB67"
  },
  { // Example Node 3 (US-ASCII domain name)
    address = "example.org"
    port = 33445
    public_key = "8CD5A9BF0A6CE358BA36F7A653F99FA6B258FF756E490F52C1F98CC420F78858"
  }
)
```

Then edit the config file above to select a node from the [Tox wiki](https://wiki.tox.chat/users/nodes)

[Enable](/index.php/Enable "Enable") and start tox-bootstrapd service, and check if it is running fine and port has been bound:

 `# ss --listening --numeric --processes | grep *node_port*`  `udp        0      0 *:*node_port*                 *:*                                 576/DHT_bootstrap`