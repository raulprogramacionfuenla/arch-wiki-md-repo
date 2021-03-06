[Rygel](https://wiki.gnome.org/Projects/Rygel) is a streaming media server compatible with many [DLNA](https://en.wikipedia.org/wiki/Digital_Living_Network_Alliance "wikipedia:Digital Living Network Alliance")/[UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play "wikipedia:Universal Plug and Play") clients including the Sony PlayStation 3, Microsoft Xbox 360, smart televisions, DLNA speakers and many smartphones. Rygel will automatically transcode media to a format compatible with the client device. It can also utilise published media hierarchies from external applications like [Rhythmbox](/index.php/Rhythmbox "Rhythmbox") and DVB Daemon through the D-Bus MediaServer specification. It is under active development and is a part of the [GNOME](/index.php/GNOME "GNOME") project.

## Installation

Install the [rygel](https://www.archlinux.org/packages/?name=rygel) package.

## Configuration

After having installed Rygel on a GNOME environment, the "Share media" option will be available along the Sharing settings.

Rygel can be configured globally (`/etc/rygel.conf`) or per-user (`~/.config/rygel.conf`). The default `/etc/rygel.conf` is well documented.

More information on these and other configuration options can be found with [rygel.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rygel.conf.5).

## Troubleshooting

When starting Rygel from the command line, there are several options that might help you troubleshoot any strange behaviour. Find out more about these options with [rygel(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rygel.1).