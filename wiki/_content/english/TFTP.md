The [Trivial File Transfer Protocol](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol "wikipedia:Trivial File Transfer Protocol") (TFTP) provides a minimalistic means for transferring files. It is generally used as a part of [PXE](/index.php/PXE "PXE") booting or for updating configuration and firmware on devices which have limited memory such as routers and printers.

## Server

There are several TFTP server implementations, some are listed below and [iputils](https://www.archlinux.org/packages/?name=iputils) also includes a version of tftp.

**Note:** Make sure not to start different TFTP implementations at the same time. They will fail with an error `got more than one socket`, because only one may listen to the default TFTP port `69`.

### tftp-hpa

[Install](/index.php/Install "Install") [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) and then [start](/index.php/Start "Start") `tftpd.service`.

To modify service parameters edit `/etc/conf.d/tftpd`.

### atftp

[Install](/index.php/Install "Install") [atftp](https://www.archlinux.org/packages/?name=atftp) and then [start](/index.php/Start "Start") `atftpd.service`.

To modify service parameters edit `/etc/conf.d/atftpd`.