Related articles

*   [openvpn](/index.php/Openvpn "Openvpn")

[ProtonVPN](https://www.protonvpn.com) is a VPN provider that utilizes the OpenVPN protocol.

In order to use this tutorial, one must have a protonvpn account.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Walkthrough](#Walkthrough)
    *   [1.1 Saving OpenVPN Authentication](#Saving_OpenVPN_Authentication)
    *   [1.2 Enable VPN on Boot](#Enable_VPN_on_Boot)
*   [2 Use ProtonVPN-cli](#Use_ProtonVPN-cli)

## Walkthrough

[Install](/index.php/Install "Install") [openvpn](https://www.archlinux.org/packages/?name=openvpn).

Log into ProtonVPN and download one or more OpenVPN configuration files.

Copy the *.ovpn files into `/etc/openvpn/client/`

Pick the corresponding **.ovpn** that will be used (ca.protonvpn.com.tcp443.ovpn is used as an example)

Copy the file with a new extension (this is just so you keep the original ovpn file intact)

```
# cp /etc/openvpn/client/ca.protonvpn.com.tcp443.ovpn /etc/openvpn/client/protonvpn.conf

```

Install the [openvpn-update-resolv-conf](https://github.com/masterkorp/openvpn-update-resolv-conf) script. It needs to be saved for example at `/etc/openvpn/update-resolv-conf` and made executable with [chmod](/index.php/Chmod "Chmod"). There is also an AUR package: [openvpn-update-resolv-conf-git](https://aur.archlinux.org/packages/openvpn-update-resolv-conf-git/) which will take care of the script installation for you. This script ensures that all traffic to/from the internet goes through the VPN and protects you against DNS leaks.

```
# chmod 755 /etc/openvpn/update-resolv-conf

```

Modify the **.conf** file to use the update-resolv-conf.sh script.

 `/etc/openvpn/client/protonvpn.conf` 
```
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf
down-pre

```

Start your VPN:

```
# openvpn /etc/openvpn/client/protonvpn.conf

```

Press `Ctrl+C` to close the VPN connection.

### Saving OpenVPN Authentication

If you get tired of punching in your username and password, you may save your OpenVPN credentials in a separate file and read them automatically.

 `/etc/openvpn/client/protonvpn.conf` 
```
auth-user-pass /etc/openvpn/client/login.conf

```
 `/etc/openvpn/client/login.conf` 
```
openvpn_username
openvpn_password

```

### Enable VPN on Boot

For systemd service configuration, see [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

## Use ProtonVPN-cli

ProtonVPN supplies a utility to access the VPN. Details can be found on [their website](https://protonvpn.com/support/linux-vpn-tool/) and the GitHub repository can be found [here](https://github.com/ProtonVPN/protonvpn-cli). This package can be installed directly from [AUR](https://aur.archlinux.org/packages/protonvpn-cli/).