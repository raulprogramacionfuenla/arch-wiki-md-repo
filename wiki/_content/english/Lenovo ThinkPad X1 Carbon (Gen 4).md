Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")
*   [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Model description](#Model_description)
    *   [1.1 UEFI](#UEFI)
    *   [1.2 Support](#Support)
    *   [1.3 Fingerprint Reader](#Fingerprint_Reader)
*   [2 Configuration](#Configuration)
    *   [2.1 Display](#Display)
    *   [2.2 OneLink+](#OneLink+)
        *   [2.2.1 Dock](#Dock)
    *   [2.3 WiFi](#WiFi)
        *   [2.3.1 Bluetooth](#Bluetooth)
    *   [2.4 WWAN](#WWAN)
*   [3 See also](#See_also)

## Model description

Lenovo ThinkPad X1 Carbon, Gen 4.

To ensure you have this version, run *dmidecode*:

```
# dmidecode -t system | grep Version

Version: ThinkPad X1 Carbon 4th

```

### UEFI

Updating the UEFI works like described here: [link ThinkWiki BIOS Upgrade/Using UEFI](https://www.thinkwiki.org/wiki/BIOS_Upgrade#Using_UEFI).

### Support

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes |
| Mobile broadband | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| Camera | Yes |
| Fingerprint Reader | No |
| [Power management](/index.php/Power_management "Power management") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| microSD card reader | Yes |

### Fingerprint Reader

An open source Linux driver prototype has been developed by reverse engineering the Windows driver. The project seems to have died while in early testing. [[1]](https://github.com/nmikhailov/Validity90)

The fingerprint reader included with this model `138a:0090 Validity Sensors, Inc` currently lacks an official linux driver. [libfprint bugreport](https://gitlab.freedesktop.org/libfprint/libfprint/issues/54). Synaptics (which has acquired 'Validity Sensors') has unofficially said that they cannot disclose the protocol, but may possibly release a binary driver.

## Configuration

### Display

There are two options for displays:

*   14" FHD IPS (1920 x 1080): Works
*   14" WQHD (2560 x 1440): Works

HDMI: Works

Mini DisplayPort: Works

### OneLink+

RJ45-Adapter: Works

#### Dock

Ethernet: Works

DisplayPort: Works

Audio: Works

VGA: Works

### WiFi

There are several cards used:

*   Intel Dual Band Wireless-AC 8260, 2x2
*   Intel WiGig 18260 AC 2x2

#### Bluetooth

All cards feature BT4.1 connectivity and should work out of the box when starting the bluetooth service

### WWAN

There are several cards used

*   4G LTE (Huawei ME906S) - Tested, stable and working.
*   Qualcomm Snapdragon X7 LTE-A (Sierra Wireless EM7455) - ??.

## See also

*   [Installing and configuring arch linux on thinkpad X1 Carbon (Gen 4), complete guide](https://kozikow.wordpress.com/2016/06/03/installing-and-configuring-arch-linux-on-thinkpad-x1-carbon/)