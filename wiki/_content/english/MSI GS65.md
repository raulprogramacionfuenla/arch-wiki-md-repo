| Wireless | Working | iwlwifi |
    *   [1.2 Video](#Video)
        *   [1.2.1 Backlight](#Backlight)
        *   [1.2.2 Drivers](#Drivers)
        *   [1.2.3 Multihead](#Multihead)
    *   [1.3 Webcam](#Webcam)
    *   [1.4 Power Management](#Power_Management)
    *   [1.5 Keyboard](#Keyboard)
        *   [1.5.1 Lights](#Lights)
        *   [1.5.2 Button Mapping](#Button_Mapping)
            *   [1.5.2.1 Unmapped Buttons](#Unmapped_Buttons)
    *   [1.6 Touchpad](#Touchpad)
The Steel Series lights on the keyboard cannot be configured with [msi-keyboard-git](https://aur.archlinux.org/packages/msi-keyboard-git/) or [msiklm-git](https://aur.archlinux.org/packages/msiklm-git/) probably due to the udev rules not matching the usb vendor_id and product_id [[1]](https://github.com/Gibtnix/MSIKLM/issues/19)[[2]](https://github.com/bparker06/msi-keyboard/issues/9).
The commit [[3]](https://github.com/systemd/systemd/commit/e05c8b44622afe4256f3bb361cfb2c7db32fff8e) to fix this in systemd has been merged and should be available in the next release of systemd (240).
Waking from suspend will have wifi in airplane mode. [[4]](https://askubuntu.com/questions/1043547/wifi-hard-blocked-after-suspend-in-ubuntu-on-gs65)
A way to mitigate this is by setting systemd to hibernate instead of suspending.

 `/etc/systemd/logind.conf` 
```
HandleSuspendKey=hibernate
HandleLidSwitch=hibernate

```
