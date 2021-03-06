## Contents

*   [1 Known issues](#Known_issues)
    *   [1.1 Open issues](#Open_issues)
    *   [1.2 Has Workaround](#Has_Workaround)
    *   [1.3 Fixed](#Fixed)
    *   [1.4 Laptop Settings](#Laptop_Settings)

## Known issues

The following are known problems and workarounds for the Lenovo Thinkpad T430s, and likely also for the related models (X230, T430, T530).

### Open issues

*   The usual issue with laptop hard drives and disk head parking, which can be fixed with [hdparm's -B option](/index.php/Hdparm "Hdparm").
*   At least on one T430s, using QCad with [SNA](/index.php/Intel_graphics "Intel graphics") would reliably crash Xorg. A workaround is using UXA instead of SNA. ([FS#31617](https://bugs.archlinux.org/task/31617))
*   The accelerometer for [HDAPS](/index.php/HDAPS "HDAPS") isn't supported.

### Has Workaround

*   The system sometimes does not properly resume after being put into a suspended state. To fix configure [GRUB](/index.php/GRUB "GRUB")'s use of ACPI sleep functionality by adding "acpi_sleep=nonvs" in GRUB_CMDLINE_LINUX in /etc/default/grub

*   The brightness can't always be adjusted by default. Adding `acpi_osi\='!Windows 2012'` to `/etc/default/grub` under `GRUB_CMDLINE_LINUX_DEFAULT` and reconfiguring the grub config file fixes this.

### Fixed

*   Fixed accurately setting the brightness levels with the Fn + brightness up/down shortcut keys. The problem comes from Intel graphics, and the solution can be found from [here](/index.php/Intel#Backlight_not_fully_adjusting.2C_or_adjusting_at_all.2C_after_resume. "Intel").

### Laptop Settings

[Xbindkeys](/index.php/Xbindkeys "Xbindkeys") or [sxhkd](/index.php/Sxhkd "Sxhkd") can be used to create and modify keyboard bindings. The following example requires the [xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset) package, and turns the display off when the rectangular button to the right of the microphone mute button is pressed.

 `~/.xinbkeysrc` 
```
# Close display
"xset dpms force off"
    m:0x0 + c:156
    XF86Launch1

```

Other options can be found from [Lenovo ThinkPad T420#Volume up/down not changing volume](/index.php/Lenovo_ThinkPad_T420#Volume_up.2Fdown_not_changing_volume "Lenovo ThinkPad T420")