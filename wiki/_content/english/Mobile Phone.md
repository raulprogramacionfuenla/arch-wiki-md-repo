This page is going to express how to connect your mobile device.

## Contents

*   [1 Android](#Android)
    *   [1.1 To install a ".apk" file](#To_install_a_.22.apk.22_file)
*   [2 iPhone](#iPhone)
*   [3 CDMA](#CDMA)
*   [4 Samsung Galaxy SII](#Samsung_Galaxy_SII)

## Android

To manage your Android mobile file, please install [mtpfs](https://www.archlinux.org/packages/?name=mtpfs) .

1\. Connect your phone with data wire.

2\. Open the file manager. You will see your phone folder.(Remember to allow the computer to visit on the phone. )

3\. Manage your file.

### To install a ".apk" file

See Android [[1]](https://wiki.archlinux.org/index.php/Android#Android_Debug_Bridge_.28ADB.29)

## iPhone

You will need [libimobiledevice-git](https://aur.archlinux.org/packages/libimobiledevice-git/) and [libgpod-git](https://aur.archlinux.org/packages/libgpod-git/) compiled with afc support. You can use the [ifuse-git](https://aur.archlinux.org/packages/ifuse-git/) to mount your [iPod](/index.php/IPod "IPod") or if you use [GNOME](/index.php/GNOME "GNOME") you can compile [Gvfs](/index.php/Gvfs "Gvfs") with the option `--with-afc` [[2]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/gvfs).

For more info see the [iPod](/index.php/IPod#iPhone.2FiPod_Touch "IPod") page.

## CDMA

[CDMA](https://en.wikipedia.org/wiki/CDMA "wikipedia:CDMA") includes phones on Samsung, LG, Sanyo, and more.

Right now there is no easy way to use CDMA phones. The best option is Bitpim.

You can use the latest version of [bitpim-release](https://aur.archlinux.org/packages/bitpim-release/) for these phones. Make sure you run Bitpim as root and everything should work.

## Samsung Galaxy SII

Here are the steps to mount a Samsung Galaxy SII from command line:

From the smart phone: Go to settings > Wireless and network > USB utilities.

Click on the "Connect storage to PC" icon.

Now, Plug the cable into the phone and to the computer.

You will get a new screen that says "USB Connected". Click the "Connect USB storage" icon.

You will get a new colored andoid screen showing that the USB mass storage is active.

Then the device could be mounted as [USB storage devices](/index.php/USB_storage_devices "USB storage devices").

reverse out your steps when you unmount.

If you have some troubles, install [go-mtpfs](https://aur.archlinux.org/packages/go-mtpfs/). For more detail, check [go-mtpfs](/index.php/MTP#go-mtpfs "MTP").