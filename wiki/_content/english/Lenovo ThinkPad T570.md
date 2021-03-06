Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 BIOS Update](#BIOS_Update)
    *   [2.2 Bumblebee](#Bumblebee)
    *   [2.3 Bluetooth](#Bluetooth)

## Installation

Use the [Installation guide](/index.php/Installation_guide "Installation guide"). Make sure that Secure Boot is disable in BIOS Setup.

## Configuration

### BIOS Update

Install [this BIOS update](https://support.lenovo.com/de/en/downloads/ds120370) (or a newer one) to fix a [serious bug concerning hyperthreading](https://lists.debian.org/debian-devel/2017/06/msg00308.html) and issues with thunderbolt [[1]](https://forums.lenovo.com/t5/ThinkPad-T400-T500-and-newer-T/ThinkPad-T470s-BIOS-bug-WOL-and-Thunderbolt-3/m-p/3707059) [[2]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1708043/) , which can affect you even if you don't use thunderbolt. [[3]](https://github.com/linrunner/TLP/issues/308) See [Flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux "Flashing BIOS from Linux") for details on how to install the BIOS without an optical drive; the [geteltorito](https://aur.archlinux.org/packages/geteltorito/) method is known to work on the T570.

Note: before flashing, you have to disable the Intel BIOS guard or risk bricking your laptop. If you corrupt your BIOS, you can fix it by flashing a working ROM directly into the EEPROM chip either with [a Raspberry Pi](http://posts.nadim.computer/2018/10/26/repairing-a-thinkpad.html) or [a specialized programming device](https://www.flashrom.org/Flashrom/1.0/Supported_Hardware#USB_Devices).

### Bumblebee

[Until bbswitch is updated to support the new power management method](/index.php/Bumblebee#Broken_power_management_with_kernel_4.8 "Bumblebee"), add `pcie_port_pm=off` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Bluetooth

If you have a very weak bluetooth signal when using wifi, make sure you have a recent [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware). See [https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1721271](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1721271) for more information.