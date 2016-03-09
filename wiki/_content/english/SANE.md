SANE ([Scanner Access Now Easy](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy "wikipedia:Scanner Access Now Easy")) provides a library and a command-line tool to use scanners under GNU/Linux. [Here](http://www.sane-project.org/sane-supported-devices.html) you can check if sane supports your scanner.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Installing a scanner driver](#Installing_a_scanner_driver)
    *   [3.1 Firmware](#Firmware)
*   [4 Install a frontend](#Install_a_frontend)
*   [5 Network scanning](#Network_scanning)
    *   [5.1 Sharing your scanner over a network](#Sharing_your_scanner_over_a_network)
    *   [5.2 Accessing your scanner from a remote workstation](#Accessing_your_scanner_from_a_remote_workstation)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Invalid argument](#Invalid_argument)
        *   [6.1.1 Missing firmware file](#Missing_firmware_file)
        *   [6.1.2 Wrong firmware file permissions](#Wrong_firmware_file_permissions)
        *   [6.1.3 Multiple backends claim scanner](#Multiple_backends_claim_scanner)
    *   [6.2 Slow startup](#Slow_startup)
    *   [6.3 Permission problem](#Permission_problem)

## Installation

[Install](/index.php/Install "Install") the [sane](https://www.archlinux.org/packages/?name=sane) package.

## Configuration

Now you can try to see if sane recognizes your scanner

```
$ scanimage -L

```

If that fails, check that your scanner is plugged into the computer. You also might have to unplug/plug your scanner for `/etc/udev/rules.d/sane.rules` to recognize your scanner.

Now you can see if it actually works

```
$ scanimage --format=tiff > test.tiff

```

If the scanning fails with the message `scanimage: sane_start: Invalid argument` you may need to specify the device.

 `$ scanimage -L` 
```
device `v4l:/dev/video0' is a Noname Video WebCam virtual device
device `pixma:04A91749_247936' is a CANON Canon PIXMA MG5200 multi-function peripheral
```

Then you would need to run

```
$ scanimage --device pixma:04A91749_247936 --format=tiff > test.tiff

```

Sane provides many special backend options for numerous scanner types. To see what these are for your device:

```
$ scanimage -A

```

## Installing a scanner driver

Most scanners should work out of the box. If yours does not, see [SANE/Scanner-specific problems](/index.php/SANE/Scanner-specific_problems "SANE/Scanner-specific problems") for installation instructions.

### Firmware

**Note:** This section is only needed if you need to upload firmware to your scanner.

Firmwares usually have the **`.bin`** extension.

Firstly you need to put the firmware someplace safe, it is recommended to put it in a subdirectory of `/usr/share/sane`.

Then you need to tell sane where the firmware is:

*   Find the name of the backend for your scanner from the [sane supported devices list](http://www.sane-project.org/sane-supported-devices.html).
*   Open the file `/etc/sane.d/<backend-name>.conf`.
*   Make sure the firmware entry is uncommented and let the file-path point to where you put the firmware file for your scanner. Be sure that members of the group `scanner` can access the `/etc/sane.d/<backend-name>.conf` file.

If the backend of your scanner is not part of the sane package (such as hpaio.conf which is part of hplip), you need to uncomment the relevant entry in /etc/sane.d/dll.d/hplip.

## Install a frontend

Many frontends exist for SANE, a non-exhaustive list of which can be found on the [sane-project website](http://www.sane-project.org/sane-frontends.html). Another way to find them is to use `pacman` to [search the repositories](/index.php/Pacman#Querying_package_databases "Pacman") for keywords such as "sane" or "scanner".

*   **[gscan2pdf](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#gscan2pdf "wikipedia:Scanner Access Now Easy")** — A GTK2-based GUI to produce PDFs, TIFFs or DjVus from scanned documents. It is also able to apply OCR in the process using different engines. Depends on a few Perl packages to build of which some are in the [AUR](/index.php/AUR "AUR") as well.

	[http://gscan2pdf.sourceforge.net/](http://gscan2pdf.sourceforge.net/) || [gscan2pdf](https://aur.archlinux.org/packages/gscan2pdf/)

*   **[Simple Scan](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#Simple_Scan "wikipedia:Scanner Access Now Easy")** — A simplified GUI that is intended to be easier to use and better integrated into the [GNOME](/index.php/GNOME "GNOME") desktop than XSane. It was initially written for Ubuntu and is maintained by Robert Ancell of Canonical Ltd. for GNU/Linux.

	[http://launchpad.net/simple-scan](http://launchpad.net/simple-scan) || [simple-scan](https://www.archlinux.org/packages/?name=simple-scan)

*   **[XSane](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy#XSane "wikipedia:Scanner Access Now Easy")** — A full-featured GTK-based frontend looking a bit old but providing extended functionalities.

	[http://www.xsane.org/](http://www.xsane.org/) || [xsane](https://www.archlinux.org/packages/?name=xsane)

**Note:** Scanning directly to PDF using XSane in 16bit color depth mode is known to produces [corrupted files](https://bugs.launchpad.net/ubuntu/+source/xsane/+bug/539162) and a note in `pacman` output warns so. 8bit mode is known to work.

## Network scanning

### Sharing your scanner over a network

You can share your scanner with other hosts on your network who use sane, xsane or xsane-enabled Gimp. To set up the server, first indicate which hosts on your network are allowed access.

Change the `/etc/sane.d/saned.conf` file to your liking, for example:

```
# required
localhost
# allow local subnet
192.168.0.0/24

```

If you use iptables, insert the `nf_conntrack_sane` module to let the firewall track saned connections.

Now start/enable `saned.socket` [using systemd](/index.php/Systemd#Using_units "Systemd"). Your scanner is now available over the network. For more information, see `man saned`.

### Accessing your scanner from a remote workstation

**Note:** Some network scanners require a different approach. See [SANE/Scanner-specific problems](/index.php/SANE/Scanner-specific_problems "SANE/Scanner-specific problems").

You can access your network-enabled scanner from a remote Arch Linux workstation.

First, specify the server's host name or IP address in the `/etc/sane.d/net.conf` file:

```
# static IP address
192.168.0.1
# or host name
stratus

```

Now test your workstation's connection:

```
$ scanimage -L

```

The network scanner should now also show up in any [front-end](#Install_a_frontend).

## Troubleshooting

	See also: [SANE/Scanner-specific problems](/index.php/SANE/Scanner-specific_problems "SANE/Scanner-specific problems")

### Invalid argument

If you get an "Invalid argument" error with xsane or another sane front-end, this could be caused by one of the following reasons:

#### Missing firmware file

No firmware file was provided for the used scanner (see above for details).

#### Wrong firmware file permissions

The permissions for the used firmware file are wrong. Correct them using

```
# chown root:scanner /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE
# chmod ug+r /usr/share/sane/SCANNER_MODEL/FIRMWARE_FILE

```

#### Multiple backends claim scanner

It may happen, that multiple backends support (or pretend to support) your scanner, and sane chooses one that doesn't do after all (the scanner won't be displayed by scanimage -L then). This has happend with older Epson scanners and the `epson2` resp. `epson` backends. In this case, the solution is to comment out the unwanted backend in `/etc/sane.d/dll.conf`. In the Epson case, that would be to change

```
 epson2
 #epson

```

to

```
 #epson2
 epson

```

### Slow startup

If you encounter slow startup issue (e.g. `xsane` or `scanimage -L` take a lot to find scanner) it may be that more than one driver supporting it is available.

Have a look at `/etc/sane.d/dll.conf` and try commenting out one (e.g. you may have epson, epson2 and epkowa enabled at the same time, try leaving only epson or epkowa uncommented)

You can also try to comment out "net" driver, if there are no network scanners.

### Permission problem

After systemd, the `scanner` and `lp` groups are deprecated. No need to add your user to those groups. See [Users and groups#Pre-systemd groups](/index.php/Users_and_groups#Pre-systemd_groups "Users and groups") for detail.

You can also try to change permissions of usb device but this is not recommended, a better solution is to fix the Udev rules so that your scanner is recognized.

First, as root, check connected usb devices with `lsusb`:

```
#Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 003 Device 003: ID 04d9:1603 Holtek Semiconductor, Inc. 
#Bus 003 Device 002: ID 04fc:0538 Sunplus Technology Co., Ltd 
#Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
#Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard 
#Bus 001 Device 002: ID 046d:0802 Logitech, Inc. Webcam C200
#Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

In our example we see the scanner: `Bus 001 Device 006: ID 03f0:2504 Hewlett-Packard`. Here `03f0` is the *vendorID* and `2504` is the *productID*.

Now open `/usr/lib/udev/rules.d/49-sane.rules` and see if there is there is a line with the vendorID and productID of your scanner. If there isn't any, create the new file `/etc/udev/rules.d/49-sane-missing-scanner.rules`, with the following contents:

```
ATTRS{idVendor}=="**vendorID**", ATTRS{idProduct}=="**productID**", MODE="0664", GROUP="scanner", ENV{libsane_matched}="yes"

```

Save the file, plug out and back in your scanner and the file permissions should be now correct.

Another tip, is that you can add your device (scanner) in backend file:

Add `usb 0x03f0 0x2504` to `/etc/sane.d/hp4200.conf` so it looks like this:

```
#
# Configuration file for the hp4200 backend
#
#
# HP4200
#usb 0x03f0 0x0105
usb 0x03f0 0x2504

```