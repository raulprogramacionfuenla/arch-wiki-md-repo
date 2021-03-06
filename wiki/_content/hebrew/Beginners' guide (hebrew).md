| **Summary**  |
| Provides a highly detailed, explanatory guide to installing, configuring and using a full-featured Arch Linux system. |
| **Related** |
| [Category:Accessibility](/index.php/Category:Accessibility "Category:Accessibility") |
| [Installation guide](/index.php/Installation_guide "Installation guide") |
| [General Recommendations](/index.php/General_Recommendations "General Recommendations") |

## Contents

*   [1 הקדמה](#.D7.94.D7.A7.D7.93.D7.9E.D7.94)
    *   [1.1 הכרות](#.D7.94.D7.9B.D7.A8.D7.95.D7.AA)
    *   [1.2 רשיון](#.D7.A8.D7.A9.D7.99.D7.95.D7.9F)
    *   [1.3 הדרך של Arch](#.D7.94.D7.93.D7.A8.D7.9A_.D7.A9.D7.9C_Arch)
    *   [1.4 על המדריך הזה](#.D7.A2.D7.9C_.D7.94.D7.9E.D7.93.D7.A8.D7.99.D7.9A_.D7.94.D7.96.D7.94)
*   [2 חלק I: התקנת מערכת הבסיס](#.D7.97.D7.9C.D7.A7_I:_.D7.94.D7.AA.D7.A7.D7.A0.D7.AA_.D7.9E.D7.A2.D7.A8.D7.9B.D7.AA_.D7.94.D7.91.D7.A1.D7.99.D7.A1)
    *   [2.1 Step 1: Obtain the latest Installation media](#Step_1:_Obtain_the_latest_Installation_media)
        *   [2.1.1 Install from an Existing GNU/Linux Distro](#Install_from_an_Existing_GNU.2FLinux_Distro)
        *   [2.1.2 CD installer](#CD_installer)
        *   [2.1.3 USB stick](#USB_stick)
    *   [2.2 Step 2: Boot Arch Linux Installer](#Step_2:_Boot_Arch_Linux_Installer)
        *   [2.2.1 Changing the keymap](#Changing_the_keymap)
        *   [2.2.2 Documentation](#Documentation)
    *   [2.3 Step 3: Start the Installation](#Step_3:_Start_the_Installation)
    *   [2.4 A: Select an installation source](#A:_Select_an_installation_source)
        *   [2.4.1 Configure Network (Netinstall)](#Configure_Network_.28Netinstall.29)
            *   [2.4.1.1 (A)DSL Quickstart for the Live Environment (If you have a pure modem (or router in bridge mode) to connect to your ISP)](#.28A.29DSL_Quickstart_for_the_Live_Environment_.28If_you_have_a_pure_modem_.28or_router_in_bridge_mode.29_to_connect_to_your_ISP.29)
            *   [2.4.1.2 Wireless Quickstart For the Live Environment (If you need wireless connectivity during the installation process)](#Wireless_Quickstart_For_the_Live_Environment_.28If_you_need_wireless_connectivity_during_the_installation_process.29)
                *   [2.4.1.2.1 Does the Wireless Chipset require Firmware?](#Does_the_Wireless_Chipset_require_Firmware.3F)
    *   [2.5 B: Set Clock](#B:_Set_Clock)
    *   [2.6 C: Prepare Hard Drive](#C:_Prepare_Hard_Drive)
        *   [2.6.1 Partition Hard Drives](#Partition_Hard_Drives)
            *   [2.6.1.1 Partition Info](#Partition_Info)
            *   [2.6.1.2 Swap Partition](#Swap_Partition)
            *   [2.6.1.3 Partition Scheme](#Partition_Scheme)
            *   [2.6.1.4 How big should my partitions be?](#How_big_should_my_partitions_be.3F)
            *   [2.6.1.5 Create Partition:cfdisk](#Create_Partition:cfdisk)
        *   [2.6.2 Set Filesystem Mountpoints](#Set_Filesystem_Mountpoints)
            *   [2.6.2.1 Filesystem Types](#Filesystem_Types)
            *   [2.6.2.2 A note on Journaling](#A_note_on_Journaling)
    *   [2.7 D: Select Packages](#D:_Select_Packages)
    *   [2.8 E: Install Packages](#E:_Install_Packages)
    *   [2.9 F: Configure the System](#F:_Configure_the_System)
        *   [2.9.1 Can the installer handle this more automatically?](#Can_the_installer_handle_this_more_automatically.3F)
        *   [2.9.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [2.9.2.1 LOCALIZATION section](#LOCALIZATION_section)
            *   [2.9.2.2 HARDWARE Section](#HARDWARE_Section)
            *   [2.9.2.3 NETWORKING Section](#NETWORKING_Section)
                *   [2.9.2.3.1 Example, using a dynamically assigned IP address (**DHCP**)](#Example.2C_using_a_dynamically_assigned_IP_address_.28DHCP.29)
                *   [2.9.2.3.2 Example, using a **static** IP address](#Example.2C_using_a_static_IP_address)
            *   [2.9.2.4 DAEMONS Section](#DAEMONS_Section)
                *   [2.9.2.4.1 About DAEMONS](#About_DAEMONS)
        *   [2.9.3 /etc/fstab](#.2Fetc.2Ffstab)
            *   [2.9.3.1 An example /etc/fstab](#An_example_.2Fetc.2Ffstab)
        *   [2.9.4 **/etc/mkinitcpio.conf**](#.2Fetc.2Fmkinitcpio.conf)
        *   [2.9.5 /etc/resolv.conf (for Static IP)](#.2Fetc.2Fresolv.conf_.28for_Static_IP.29)
        *   [2.9.6 /etc/hosts](#.2Fetc.2Fhosts)
        *   [2.9.7 /etc/hosts.deny and /etc/hosts.allow](#.2Fetc.2Fhosts.deny_and_.2Fetc.2Fhosts.allow)
        *   [2.9.8 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [2.9.9 Pacman-Mirror](#Pacman-Mirror)
        *   [2.9.10 Root password](#Root_password)
    *   [2.10 Install and configure a bootloader](#Install_and_configure_a_bootloader)
        *   [2.10.1 For BIOS motherboards](#For_BIOS_motherboards)
            *   [2.10.1.1 Syslinux](#Syslinux)
            *   [2.10.1.2 GRUB](#GRUB)
        *   [2.10.2 For UEFI motherboards](#For_UEFI_motherboards)
            *   [2.10.2.1 Gummiboot](#Gummiboot)
            *   [2.10.2.2 GRUB](#GRUB_2)
    *   [2.11 H: Reboot](#H:_Reboot)
*   [3 Part II: Configure & Update the New Arch Linux base system](#Part_II:_Configure_.26_Update_the_New_Arch_Linux_base_system)
    *   [3.1 Step 1: Configuring the network (if necessary)](#Step_1:_Configuring_the_network_.28if_necessary.29)
        *   [3.1.1 Wired LAN](#Wired_LAN)
        *   [3.1.2 Wireless LAN](#Wireless_LAN)
        *   [3.1.3 Analog Modem](#Analog_Modem)
        *   [3.1.4 ISDN](#ISDN)
        *   [3.1.5 DSL (PPPoE)](#DSL_.28PPPoE.29)
    *   [3.2 Step 2: Update, Sync, and Upgrade the system with pacman](#Step_2:_Update.2C_Sync.2C_and_Upgrade_the_system_with_pacman)
        *   [3.2.1 What is pacman ?](#What_is_pacman_.3F)
        *   [3.2.2 Package Repositories and /etc/pacman.conf](#Package_Repositories_and_.2Fetc.2Fpacman.conf)
        *   [3.2.3 /etc/pacman.d/mirrorlist](#.2Fetc.2Fpacman.d.2Fmirrorlist)
        *   [3.2.4 Mirrorcheck for up-to-date packages](#Mirrorcheck_for_up-to-date_packages)
        *   [3.2.5 Ignoring packages](#Ignoring_packages)
        *   [3.2.6 Ignoring Configuration Files](#Ignoring_Configuration_Files)
        *   [3.2.7 Get familiar with pacman](#Get_familiar_with_pacman)
    *   [3.3 Step 3: Update System](#Step_3:_Update_System)
        *   [3.3.1 The Arch rolling release model](#The_Arch_rolling_release_model)
        *   [3.3.2 Network Time Protocol](#Network_Time_Protocol)
    *   [3.4 Step 4: Add a user and setup groups](#Step_4:_Add_a_user_and_setup_groups)
    *   [3.5 Step 5: Install and setup Sudo (Optional)](#Step_5:_Install_and_setup_Sudo_.28Optional.29)
*   [4 Part III: Install X and configure ALSA](#Part_III:_Install_X_and_configure_ALSA)
    *   [4.1 Step 1: Configure sound with alsamixer](#Step_1:_Configure_sound_with_alsamixer)
        *   [4.1.1 Sound test](#Sound_test)
        *   [4.1.2 Saving the Sound Settings](#Saving_the_Sound_Settings)
    *   [4.2 Step 2: Install X](#Step_2:_Install_X)
    *   [4.3 Step 3: Configure X (Optional)](#Step_3:_Configure_X_.28Optional.29)
        *   [4.3.1 B: Input hotplugging](#B:_Input_hotplugging)
            *   [4.3.1.1 Using input hotplugging](#Using_input_hotplugging)
            *   [4.3.1.2 Disable input hotplugging](#Disable_input_hotplugging)
                *   [4.3.1.2.1 Set the keyboard layout if not using a standard US keyboard](#Set_the_keyboard_layout_if_not_using_a_standard_US_keyboard)
        *   [4.3.2 C: Test X](#C:_Test_X)
            *   [4.3.2.1 Prepare for the test by configuring ~/.xinitrc](#Prepare_for_the_test_by_configuring_.7E.2F.xinitrc)
            *   [4.3.2.2 Perform the test](#Perform_the_test)
            *   [4.3.2.3 In case of errors](#In_case_of_errors)
            *   [4.3.2.4 Need Help?](#Need_Help.3F)
*   [5 Part IV: Installing and configuring a Desktop Environment](#Part_IV:_Installing_and_configuring_a_Desktop_Environment)
    *   [5.1 Step 1: Install Fonts](#Step_1:_Install_Fonts)
    *   [5.2 Step 2: ~/.xinitrc (again)](#Step_2:_.7E.2F.xinitrc_.28again.29)
    *   [5.3 Step 3: Install a Desktop Environment](#Step_3:_Install_a_Desktop_Environment)
        *   [5.3.1 GNOME](#GNOME)
            *   [5.3.1.1 About GNOME](#About_GNOME)
            *   [5.3.1.2 Installation](#Installation)
            *   [5.3.1.3 Useful DAEMONS for GNOME](#Useful_DAEMONS_for_GNOME)
            *   [5.3.1.4 Eye Candy](#Eye_Candy)
        *   [5.3.2 KDE](#KDE)
            *   [5.3.2.1 About KDE](#About_KDE)
            *   [5.3.2.2 Installation](#Installation_2)
            *   [5.3.2.3 Useful KDE DAEMONS](#Useful_KDE_DAEMONS)
            *   [5.3.2.4 Eye candy](#Eye_candy_2)
        *   [5.3.3 Xfce](#Xfce)
            *   [5.3.3.1 אודות Xfce](#.D7.90.D7.95.D7.93.D7.95.D7.AA_Xfce)
            *   [5.3.3.2 התקנה](#.D7.94.D7.AA.D7.A7.D7.A0.D7.94)
            *   [5.3.3.3 Daemons שימושיים](#Daemons_.D7.A9.D7.99.D7.9E.D7.95.D7.A9.D7.99.D7.99.D7.9D)
        *   [5.3.4 LXDE](#LXDE)
            *   [5.3.4.1 About LXDE](#About_LXDE)
            *   [5.3.4.2 Installation](#Installation_3)
        *   [5.3.5 *box](#.2Abox)
            *   [5.3.5.1 Fluxbox](#Fluxbox)
            *   [5.3.5.2 Openbox](#Openbox)
        *   [5.3.6 FVWM2](#FVWM2)
        *   [5.3.7 Tiling WMs](#Tiling_WMs)
*   [6 מולטימדיה](#.D7.9E.D7.95.D7.9C.D7.98.D7.99.D7.9E.D7.93.D7.99.D7.94)
    *   [6.1 קודקים, פלאגינים וג'אווה](#.D7.A7.D7.95.D7.93.D7.A7.D7.99.D7.9D.2C_.D7.A4.D7.9C.D7.90.D7.92.D7.99.D7.A0.D7.99.D7.9D_.D7.95.D7.92.27.D7.90.D7.95.D7.95.D7.94)
*   [7 נספח](#.D7.A0.D7.A1.D7.A4.D7.97)

## הקדמה

##### הכרות

ברוכים הבאים. מסמך הוויקי הזה ידריך אתכם בהתקנה וקינפוג של [Arch Linux](/index.php/Arch_Linux "Arch Linux"); הפצת גנו\לינוקס פשוטה, קלה המכוונת למשתמש. המדריך הזה מכוון עבור משתמשים חדשים בארצ', אבל יכול לשמש כמקור טוב למידע באופן כללי.

**נקודות עיקריות שמנחות את ארצ'**

*   [פשטות](/index.php/The_Arch_Way "The Arch Way") ברעיון ובמעשה
*   כל החבילות מהודרות לi686 ו x86_64
*   [סגנון BSD](/index.php/Arch_boot_process "Arch boot process") בתסריטי init, כאשר ההגדרות מרוכזות בקובץ מרכזי אחד.
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"): יוצר initramfs פשוט.
*   [Pacman](/index.php/Pacman "Pacman") מנהל חבילות קל וזריז, עם חתימת זיכרון נמוכה.
*   מערכת ה [Arch Build System](/index.php/Arch_Build_System "Arch Build System"): מערכת דמוית הפורטים של BSD, המהווה מסגרת פשוטה להתקנת חבילות של ארצ' מקוד מקור.
*   מערכת ה [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"): המציעה אלפי חבילות שנוצרו על ידי המשתמשים, ואפשרות לחלוק גם את שלך!

##### רשיון

ארצ' לינוקס, פאקמן, התיעוד והתסריטים שמורים בזכויות יוצרים ל ©2002-2007 by Judd Vinet, ©2007-2010 by Aaron Griffin והם תחת ה GNU General Public License Version 2.

##### הדרך של Arch

***העיקרון המעצב מאחורי ארצ' לינוקס הוא להשאיר את הדברים [פשוטים](/index.php/The_Arch_Way "The Arch Way").***

'פשוט', בהקשר הזה, משמעותו ללא תוספות לא הכרחיות, שינויים וכד' בקיצור - גישה אלגנטית.

**כמה נקודות לתשומת ליבכם, כאשר מדברים על פשטות:**

*   *" 'פשטות' מוגדרת מנקודת מבט טכנית, ולא מנקודת המבט של השמישות. עדיף להיות בעלי אלגנטיות טכנית ועקומת למידה גבוה, מאשר להיות קל לשימוש ונחות בשימוש." -אארון גריפין*
*   *Entia non sunt multiplicanda praeter necessitatem* or "יש להניח את ההנחות הפשוטות ביותר." - התער של אוקום.

המונח *תער* מתיחס לכך שיש לגלח החוצה כל דרך מיותרת

*   *"החלק היוצא דופן של השיטה שלי טמון בפשטות..הדרגה הגבוה ביותר של טיפוח תמיד מגיעה לפשטות."* - ברוס לי

##### על המדריך הזה

הוויקי של ארצ' הוא מקור מעולה למידע, ולכן יש קודם כל להתיעץ [איתו](/index.php/Main_page "Main page"). חדר הIRC (בשרת freenode #archlinux), וה[פורומים](https://bbs.archlinux.org/) גם יכולים לשמש לעזרה, מבמקרה ולא נמצאה תשובה במקום אחר..

**Note:** מעקב אחר המדריך הזה באופן המדויק ביותר היא הנוסחה להצלחה בהתקנה של ארצ' כראוי, לכן, *אנא* קראו את הכל כראוי. מומלץ מאוד לקרוא <u>קודם כל</u> את הפרק העוסק במה שיש לעשות ורק אחרי כן לבצע אותו..

מאחר והפצות גנו\לינוקס הן 'מודלריות' בהגדרתן, מדריך זה מחולק לארבעה שלבים, כפי שמורכבת מערכת לשולחן העבודה של תחנות דמויות <tt>UNIX</tt>:

**[חלק I: התקנה של מערכת הבסיס](#Part_I:_Install_the_Base_System)**

**[חלק II: קינפוג ועידכון של מערכת ארצ *בסיסית*](#Part_II:_Configure_.26_Update_the_New_Arch_Linux_base_system)**

**[חלק III: התקנת שרת X וקינפוג של ALSA](#Part_III:_Install_X_and_configure_ALSA)**

**[Part IV: התקנת סביבת שולחן עבודה](#Part_IV:_Installing_and_configuring_a_Desktop_Environment)**

## חלק I: התקנת מערכת הבסיס

### Step 1: Obtain the latest Installation media

You can obtain Arch's official installation media from [here](https://archlinux.org/download/). The latest version is 2010.05

*   Both the Core and the Netinstall images provide only the necessary packages to create an **Arch Linux base system**. *Note that the Base System does not include a GUI. It is mainly comprised of the GNU toolchain (compiler, assembler, linker, libraries, shell, and utilities), the Linux kernel, and a few extra libraries and modules.*
*   Core images facilitate both installing from CD and Net.
*   Netinstall images are smaller and provide no packages themselves; the entire system is retrieved via internet.
*   [The Arch64 FAQ](/index.php/Arch64_FAQ "Arch64 FAQ") can help you choose between the 32- and 64-bit versions.

#### Install from an Existing GNU/Linux Distro

Arch is flexible enough to be installed to another partition *from within* an existing distro or Live CD. See [this wiki article](/index.php/Install_from_Existing_Linux "Install from Existing Linux") for steps to do this. This can be useful particularly if you plan to install Arch via vnc or ssh remotely.

#### CD installer

Burn the .iso image file to a CD with your preferred CD burner drive and software, and continue with [Step 2: Boot Arch Linux Installer](#Step_2:_Boot_Arch_Linux_Installer)

**Note:** The quality of optical drives, as well as the CD media itself, vary greatly. Generally, using a slow burn speed is recommended for reliable burns; Some users recommend speeds ***as low as 4x or 2x.*** If you are experiencing unexpected behavior from the CD, try burning at the minimum speed supported by your system.

#### USB stick

**Warning:** This procedure will irrevocably destroy all data on your USB stick!

**<tt>UNIX</tt> Method:**

Insert an empty or expendable USB stick, determine its path, and write the .iso to the USB stick with the `/bin/dd` program:

```
dd if=archlinux-2010.05-*{core|netinstall}*-*{i686|x86_64|dual}*.iso of=/dev/sd*x*

```

where `if=` is the path to the img file and `of=` is your USB device. Make sure to use `/dev/sd**x**` and not `/dev/sd**x1**`. You will need a usb stick large enough to accomodate the image which, at the time of this writing is 381MB.

**Check md5sum:**

Make a note of the number of records (blocks) read in and written out, then perform the following check:

```
dd if=/dev/sd*x* count=*number_of_records* status=noxfer | md5sum

```

The md5sum returned should match the [md5sum of the downloaded archlinux image file](ftp://ftp.archlinux.org/iso/2010.05/md5sums.txt); they both should match the md5sum of the image as listed in the md5sums file in the mirror distribution site. A typical run will look like this:

```
$ [sudo] dd if=archlinux-2010.05-core-i686.iso of=/dev/sdc
744973+0 records in
744973+0 records out
381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s
$ [sudo] dd if=/dev/sdc count=744973 status=noxfer | md5sum
4850d533ddd343b80507543536258229  -
744973+0 records in
744973+0 records out

```

**Microsoft Windows Method:**

Download Disk Imager from [https://launchpad.net/win32-image-writer/+download](https://launchpad.net/win32-image-writer/+download). Insert flash media. Start the Disk Imager and select the image file. Select the Drive letter associated with the flash drive. Click "write".

Continue with [Step 2: Boot Arch Linux Installer](#Step_2:_Boot_Arch_Linux_Installer)

### Step 2: Boot Arch Linux Installer

Insert the CD or USB stick and boot from it. You may have to change the boot order in your computer BIOS or press a key (usually DEL, F1, F2, F11 or F12) during the BIOS POST (Power On Self-Test) phase.

**Tip:** The memory requirements for a basic install are:

*   Core : 128 MB RAM x86_64/i686 (all packages selected, with swap partition)
*   Netinstall : 128 MB RAM x86_64/i686 (all packages selected, with swap partition)

The main menu should be displayed at this point. Select the preferred choice by using the arrow keys to highlight your choice, and then by pressing Enter.

Usually, the first item, Boot Archlive, is the preferred selection. However, choose Boot Archlive [legacy IDE] if you have trouble with libata/PATA, or have no SATA (Serial ATA) drives.

To change GRUB boot options, press **e**. Many users may wish to change the resolution of the framebuffer, for more readable console output. Append:

```
vga=773

```

to the kernel line, followed by <ENTER>, for a 1024x768 framebuffer. When done, press **b** to boot into that selection.

The system will now boot and present a login prompt. Login as 'root', without the quotes.

If your system has errors trying to boot from the live CD or there are other **hardware** errors, refer to the [Installation Troubleshooting](/index.php?title=Installation_Troubleshooting&action=edit&redlink=1 "Installation Troubleshooting (page does not exist)") wiki page.

#### Changing the keymap

If you have a non-US keyboard layout you can interactively choose your keymap/console font with the command:

```
# km

```

or use the loadkeys command:

```
# loadkeys *layout*

```

(replace *layout* with your keyboard layout such as "`fr`" or "`be-latin1`")

#### Documentation

The official install guide is conveniently available right on the live system! To access it, change to vc/2 (virtual console #2) with <ALT>+F2, and then invoke `/usr/bin/less` by typing in the following at the # prompt:

```
# less /arch/docs/official_installation_guide_en

```

`less` will allow you to page through the document. Change back to vc/1 with <ALT>+F1 to follow the rest of the install process.

Change back to vc/2 at any time if you need to reference the Official Guide as you progress through the installation process.

**Tip:** Please note that the official guide only covers installation and configuration of the base system. Once that is installed, it is strongly recommended that you come back here to the wiki to find out more about post-installation considerations and other related issues.

### Step 3: Start the Installation

As root, run the installer script from vc/1:

```
# /arch/setup

```

### A: Select an installation source

After a welcome screen, you will be prompted for an installation source. Choose the appropriate source for the installer you are using.

*   If you chose the CORE installer, continue below with [B: Set Clock](#B:_Set_Clock).
*   Netinstall only: You shall be prompted to load ethernet drivers manually, if desired. Udev is quite effective at loading the required modules, so you may assume it has already done so. You may verify this by invoking ifconfig -a from vc/3\. (Select OK to continue.)

#### Configure Network (Netinstall)

Available Interfaces will be presented. If an interface and HWaddr (**H**ard**W**are **addr**ess) is listed, then your module has already been loaded. If your interface is not listed, you may probe it from the installer, or manually do so from another virtual console.

The following screen will prompt you to *Select the interface, Probe,* or *Cancel*. Choose the appropriate interface and continue.

The installer will then ask if you wish to use DHCP. Choosing Yes will run **dhcpcd** to discover an available gateway and request an IP address; Choosing No will prompt you for your static IP, netmask, broadcast, gateway DNS IP, HTTP proxy, and FTP proxy. Lastly, you will be presented with an overview to ensure your entries are correct.

##### (A)DSL Quickstart for the Live Environment (If you have a pure modem (or router in bridge mode) to connect to your ISP)

Switch to another virtual console (<Alt> + F2), login as root and invoke

```
# pppoe-setup

```

If everything is well configured in the end you can connect to your ISP with

```
# pppoe-start

```

Return to first virtual console with <ALT>+F1\. Continue with [B: Set Clock](#B:_Set_Clock)

##### Wireless Quickstart For the Live Environment (If you need wireless connectivity during the installation process)

The wireless drivers and utilities are now available to you in the live environment of the installation media. A good knowledge of your wireless hardware will be of key importance to successful configuration. Note that the following quickstart procedure *executed at this point in the installation* will initialize your wireless hardware for use *in the live environment*. These steps (or some other form of wireless management) must be repeated from the actual installed system after booting into it.

Also note that these steps are optional if wireless connectivity is unnecessary at this point in the installation; wireless functionality may always be established later.

The basic procedure will be:

*   Switch to a free virtual console, e.g.: <ALT>+F3
*   Login as root
*   (Optional) Identify the wireless interface and driver module:

```
# lsmod | grep -i net

```

*   Ensure udev has loaded the driver, and that the driver has created a usable wireless kernel interface with `/usr/sbin/iwconfig`:

```
# iwconfig

```

Example output:

```
lo no wireless extensions.
eth0 no wireless extensions.
wlan0    unassociated  ESSID:""
         Mode:Managed  Channel=0  Access Point: Not-Associated   
         Bit Rate:0 kb/s   Tx-Power=20 dBm   Sensitivity=8/0  
         Retry limit:7   RTS thr:off   Fragment thr:off
         Power Management:off
         Link Quality:0  Signal level:0  Noise level:0
         Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
         Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

`wlan0` is the available wireless interface in the example.

*   Bring the interface up with `/sbin/ifconfig <interface> up`.

An example using the wlan0 interface:

```
# ifconfig wlan0 up

```

(Remember, your interface may be named something else, depending on your module (driver) and chipset: wlan0, eth1, etc.)

*   If the essid has been forgotten or is unknown, use `/sbin/iwlist <interface> scan` to scan for nearby networks.

```
# iwlist wlan0 scan

```

*   Associate your wireless device with the access point you want to use. Depending on the encryption (none, WEP, or WPA), the procedure may differ. You need to know the name of the chosen wireless network (ESSID), e.g. 'linksys' in the following examples:
*   An example using a *non-encrypted* network:

```
# iwconfig wlan0 essid "linksys"

```

*   An example using *WEP and a hexadecimal key*:

```
# iwconfig wlan0 essid "linksys" key 0241baf34c

```

*   An example using *WEP and an ASCII passphrase*:

```
# iwconfig wlan0 essid "linksys" key s:pass1

```

*   Using *WPA*, the procedure requires a bit more work. Check [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for more information and troubleshooting (or try using [netcfg](/index.php/Netcfg "Netcfg") instead):

```
# wpa_passphrase linksys "secretpassphrase" > /etc/wpa_supplicant.conf
# wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf

```

*   Confirm you have successfully associated to the access point before continuing:

```
# iwconfig wlan0

```

*   Request an IP address with `/sbin/dhcpcd <interface>` . e.g.:

```
# dhcpcd wlan0

```

*   Ensure you can route using `/bin/ping`:

```
# ping -c 3 www.google.com

```

You should have a working network connection. For troubleshooting, check the detailed [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup") page.

###### Does the Wireless Chipset require Firmware?

A small percentage of wireless chipsets also require firmware, in addition to a corresponding driver. If unsure, invoke `/usr/bin/dmesg` to query the kernel log for a firmware request from the wireless chipset:

```
# dmesg | grep firmware

```

Example output from an Intel chipset which requires and has requested firmware from the kernel at boot:

```
firmware: requesting iwlwifi-5000-1.ucode

```

If there is no output, it may be concluded that the system's wireless chipset does not require firmware.

**Note:** **Wireless chipset firmware packages (for cards which require them) are pre-installed under /lib/firmware in the live environment, (on CD/USB stick) *but must be explicitly installed to your actual system to provide wireless functionality after you reboot into it!* Package selection and installation is covered below. Ensure installation of both your wireless module and firmware during the package selection step! See [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") if you are unsure about the requirement of corresponding firmware installation for your particular chipset. This is a very common error.**

After the initial Arch installation is complete, you may wish to refer to [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") to ensure a permanent configuration solution for your installed system.

Return to vc/1 with <ALT>+F1\. Continue with [B: Set Clock](#B:_Set_Clock)

### B: Set Clock

*   UTC - Choose UTC if running only <tt>UNIX</tt>-like operating system(s).

*   localtime - Choose local if multi-booting with a Microsoft Windows OS.

### C: Prepare Hard Drive

**Warning:** Partitioning hard drives can destroy data. You are strongly cautioned and advised to backup your critical data if applicable.

**Note:** Partitioning may be performed before initiating the Arch installation if desired, by utilizing [GParted](http://gparted.sourceforge.net/download.php) or other available tools. If the installation drive has already been partitioned to the required specifications, continue with [Set Filesystem Mountpoints](#Set_Filesystem_Mountpoints)

Verify current disk identities and layout by invoking `/sbin/fdisk` with the `-l` (lower-case L) switch.

Open another virtual console (<ALT>+F3) and enter:

```
# fdisk -l

```

Take note of the disk(s)/partition(s) to utilize for the Arch installation.

Switch back to the installation script with <ALT>+F1

Select the first menu entry "Prepare Hard Drive".

*   Option 1: Auto Prepare

Auto-Prepare divides the disk into the following configuration:

*   ext2 /boot partition, default size 32MB. *You will be prompted to modify the size to your requirement.*
*   swap partition, default size 256MB. *You will be prompted to modify the size to your requirement.*
*   A Separate / and /home partition, (sizes can also be specified). Available filesystems include ext2, ext3, ext4, reiserfs, xfs and jfs, but note that *both / and /home shall share the same fs type* if choosing the Auto Prepare option.

Be warned that Auto-prepare will completely erase the chosen hard drive. Read the <font color="red">warning</font> presented by the installer very carefully, and make sure the correct device is about to be partitioned.

*   Option 2: **(Recommended)** Partition Hard Drives (with cfdisk)

This option will allow for the most robust and customized partitioning solution for your personal needs.

*At this point, more advanced GNU/Linux users who are familiar and comfortable with manually partitioning may wish to skip down to **[D: Select Packages](#D:_Select_Packages)** below.*

**Note:** If you are installing to a USB flash key, see "[Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")".

#### Partition Hard Drives

##### Partition Info

Partitioning a hard disk drive defines specific areas (the partitions) within the disk, that will each appear and behave as a separate disk and upon which a filesystem may be created (formatted).

*   There are 3 types of disk partitions:

1.  Primary
2.  Extended
3.  Logical

**Primary** partitions can be bootable, and are limited to 4 partitions per disk or raid volume. If a partitioning scheme requires more than 4 partitions, an **extended** partition which will contain **logical** partitions will be required.

Extended partitions are not usable by themselves; they are merely a "container" for logical partitions. If required, a hard disk shall contain only one extended partition; which shall then be sub-divided into logical partitions.

When partitioning a disk, one can observe this numbering scheme by creating primary partitions sda1 through sda3 followed by creating an extended partition, sda4, and subsequently creating logical partition(s) within the extended partition; sda5, sda6, and so on.

##### Swap Partition

A swap partition is a place on the drive where virtual ram resides, allowing the kernel to easily use disk storage for data that does not fit into physical RAM.

Historically, the general rule for swap partition size was 2x the amount of physical RAM. Over time, as computers have gained ever larger memory capacities, this rule has become increasingly deprecated. Generally, on machines with up to 512MB RAM, the 2x rule is usually quite sufficient. If the installation machine provides gratuitous amounts of RAM (more than 1024 MB) it may be possible to completely forget a swap partition altogether, since the option to create a [swap file](/index.php/HOW_TO:_Create_swap_file "HOW TO: Create swap file") is always available later. A 1 GB swap partition will be used in this example.

**Note:** If using suspend-to-disk, (hibernate) a swap partition at least **equal** in size to the amount of physical RAM is required. Some Arch users even recommend oversizing it beyond the amount of physical RAM by 10-15%, to allow for possible bad sectors.

##### Partition Scheme

A disk partitioning scheme is a very personalized preference. Each user's choices will be unique to their own computing habits and requirements. If you would like to dual boot Arch Linux and a Windows operating system please see [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot").

Filesystem candidates for separate partitions include:

**/** (root) *The root filesystem is the primary filesystem from which all other filesystems stem; the top of the hierarchy. All files and directories appear under the root directory "/", even if they are stored on different physical devices. The contents of the root filesystem must be adequate to boot, restore, recover, and/or repair the system. Therefore, certain directories under / are not themselves candidates for separate partitions. (See warning below).*

**/boot** *This directory contains the kernel and ramdisk images as well as the bootloader configuration file, and bootloader stages. /boot also stores data that is used before the kernel begins executing userspace programs. This may include saved master boot sectors and sector map files. /boot is essential for booting, but is unique in that it may still be kept on its own separate partition (if required).*

**/home** *Provides subdirectories, each named for a system user, for miscellaneous personal data storage as well as user-specific configuration files for applications.*

**/usr** *While root is the primary filesystem, /usr is the secondary hierarchy for all system users' data, including the majority of multi-user utilities and applications. /usr is shareable, read-only data. This means that /usr shall be shareable between various hosts and must not be written to, except in the case of system update/upgrade. Any information that is host-specific or varies with time is stored elsewhere.*

**/tmp** *directory for programs that require temporary files such as '.lck' files, which can be used to prevent multiple instances of their respective program until a task is completed, at which point the '.lck' file will be removed. Programs must not assume that any files or directories in /tmp are preserved between invocations of the program and files and directories located under /tmp will typically be deleted whenever the system is booted.*

**/var** *contains variable data; spool directories and files, administrative and logging data, pacman's cache, the ABS tree, etc. /var exists in order to make it possible to mount /usr as read-only. Everything that historically went into /usr that is written to during system operation (as opposed to installation and software maintenance) must reside under /var.*

**Warning:** Besides /boot, directories essential for booting are: '***/bin', '/etc', '/lib', and '/sbin'. Therefore, they must not reside on a separate partition from /.***

***There are several advantages for using discrete filesystems, rather than combining all into one partition***:

*   Security: Each filesystem may be configured in /etc/fstab as 'nosuid', 'nodev', 'noexec', 'readonly', etc.
*   Stability: A user, or malfunctioning program can completely fill a filesystem with garbage if they have write permissions for it. Critical programs, which reside on a different filesystem remain unaffected.
*   Speed: A filesystem which gets written to frequently may become somewhat fragmented. (An effective method of avoiding fragmentation is to ensure that each filesystem is never in danger of filling up completely.) Separate filesystems remain unaffected, and each can be defragmented separately as well.
*   Integrity: If one filesystem becomes corrupted, separate filesystems remain unaffected.
*   Versatility: Sharing data across several systems becomes more expedient when independent filesystems are used. Separate filesystem types may also be chosen based upon the nature of data and usage.

In this example, we shall use separate partitions for /, /var, /home, and a swap partition.

**Note:** /var contains many small files. This should be taken into consideration when choosing a filesystem type for it, (if creating its own separate partition).

##### How big should my partitions be?

This question is best answered based upon individual needs. You may wish to simply create **one partition for root and one partition for swap or only one root partition without swap** or refer to the following examples and consider these guidelines to provide a frame of reference:

*   The root filesystem (/) in the example will contain the /usr directory, which can become moderately large, depending upon how much software is installed. 15-20 GB should be sufficient for most users.

*   The /var filesystem will contain, among other data, the [ABS](/index.php/ABS "ABS") tree and the pacman cache. Keeping cached packages is useful and versatile; it provides the ability to downgrade packages if needed. /var tends to grow in size; the pacman cache can grow large over long periods of time, but can be safely cleared if needed. If you are using an SSD, you may wish to locate your /var on an HDD and keep the / and /home partitions on your SSD to avoid needless read/writes to the SSD. 8-12 Gigs on a desktop system should be sufficient for /var, depending largely upon how much software you intend to install. Servers tend to have relatively larger /var filesystems.

*   The /home filesystem is typically where user data, downloads, and multimedia reside. On a desktop system, /home is typically the largest filesystem on the drive by a large margin. Remember that if you chose to reinstall Arch, all the data on your /home partition will be untouched (so long as you have a separate /home partition).

*   An extra 25% of space added to each filesystem will provide a cushion for unforeseen occurrence, expansion, and serve as a preventive against fragmentation.

***From the guidelines above, the example system shall contain a ~15GB root (/) partition, ~10GB /var, 1GB swap, and a /home containing the remaining disk space.***

##### Create Partition:cfdisk

Start by creating the primary partition that will contain the **root**, (/) filesystem.

Choose **N**ew -> Primary and enter the desired size for root (/). Put the partition at the beginning of the disk.

Also choose the **T**ype by designating it as '83 Linux'. The created / partition shall appear as sda1 in our example.

Now create a primary partition for /var, designating it as **T**ype 83 Linux. The created /var partition shall appear as sda2

Next, create a partition for swap. Select an appropriate size and specify the **T**ype as 82 (Linux swap / Solaris). The created swap partition shall appear as sda3.

Lastly, create a partition for your /home directory. Choose another primary partition and set the desired size.

Likewise, select the **T**ype as 83 Linux. The created /home partition shall appear as sda4.

Example:

```
Name    Flags     Part Type    FS Type           [Label]         Size (MB)
-------------------------------------------------------------------------
sda1               Primary     Linux                             15440 #root
sda2               Primary     Linux                             10256 #/var
sda3               Primary     Linux swap / Solaris              1024  #swap
sda4               Primary     Linux                             140480 #/home

```

Choose **W**rite and type '**yes'**. Beware that this operation may destroy data on your disk. Choose **Q**uit to leave the partitioner. Choose Done to leave this menu and continue with "Set Filesystem Mountpoints".

**Note:** Since the latest developments of the Linux kernel which include the libata and PATA modules, all IDE, SATA and SCSI drives have adopted the sd*x* naming scheme. This is perfectly normal and should not be a concern.

#### Set Filesystem Mountpoints

First you will be asked for your swap partition. Choose the appropriate partition (sda3 in this example). You will be asked if you want to create a swap filesystem; select yes. Next, choose where to mount the / (root) directory (sda1 in the example). At this time, you will be asked to specify the filesystem type.

##### Filesystem Types

Again, a filesystem type is a very subjective matter which comes down to personal preference. Each has its own advantages, disadvantages, and unique idiosyncrasies. Here is a very brief overview of supported filesystems:

1\. **ext2** *Second Extended Filesystem*- Old, reliable GNU/Linux filesystem. Very stable, but *without journaling support*. May be inconvenient for root (/) and /home, due to very long fsck's. *An ext2 filesystem can easily be converted to ext3.* Generally regarded as a good choice for /boot/.

2\. **ext3** *Third Extended Filesystem*- Essentially the ext2 system, but with journaling support. ext3 is backward compatible with ext2\. Extremely stable, mature, and by far the most widely used, supported and developed GNU/Linux FS.

**High Performance Filesystems:**

3\. **ext4** *Fourth Extended Filesystem*- Backward compatible with ext2 and ext3\. Introduces support for volumes with sizes up to 1 exabyte and files with sizes up to 16 terabytes. Increases the 32,000 subdirectory limit in ext3 to 64,000\. Offers online defragmentation ability.

4\. **ReiserFS** (V3)- Hans Reiser's high-performance journaling FS uses a very interesting method of data throughput based on an unconventional and creative algorithm. ReiserFS is touted as very fast, especially when dealing with many small files. ReiserFS is fast at formatting, yet comparatively slow at mounting. Quite mature and stable. ReiserFS is not actively developed at this time (Reiser4 is the new Reiser filesystem). Generally regarded as a good choice for /var/.

5\. **JFS** - IBM's **J**ournaled **F**ile**S**ystem- The first filesystem to offer journaling. JFS had many years of use in the IBM AIX® OS before being ported to GNU/Linux. JFS currently uses the least CPU resources of any GNU/Linux filesystem. Very fast at formatting, mounting and fsck's, and very good all-around performance, especially in conjunction with the deadline I/O scheduler. (See [JFS](/index.php/JFS "JFS").) Not as widely supported as ext or ReiserFS, but very mature and stable.

6\. **XFS** - Another early journaling filesystem originally developed by Silicon Graphics for the IRIX OS and ported to GNU/Linux. XFS offers very fast throughput on large files and large filesystems. Very fast at formatting and mounting. Generally benchmarked as slower with many small files, in comparison to other filesystems. XFS is very mature and offers online defragmentation ability.

*   JFS and XFS filesystems cannot be *shrunk* by disk utilities (such as gparted or parted magic)

##### A note on Journaling

All above filesystems, except ext2, utilize [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling file systems are fault-resilient file systems that use a journal to log changes before they are committed to the file system to avoid metadata corruption in the event of a crash. Note that not all journaling techniques are alike; specifically, only ext3 and ext4 offer *data-mode journaling*, (though, not by default), which journals *both* data *and* meta-data (but with a significant speed penalty). The others only offer *ordered-mode journaling*, which journals meta-data only. While all will return your filesystem to a valid state after recovering from a crash, *data-mode journaling* offers the greatest protection against file system corruption and data loss but can suffer from performance degradation, as all data is written twice (first to the journal, then to the disk). Depending upon how important your data is, this may be a consideration in choosing your filesystem type.

***Moving on...***

Choose and create the filesystem (format the partition) for / by selecting **yes**. You will now be prompted to add any additional partitions. In our example, sda2 and sda4 remain. For sda2, choose a filesystem type and mount it as /var. Finally, choose the filesystem type for sda4, and mount it as /home.

**Note:** If you have not created and do not need a separate /boot partition, you may safely ignore the warning that it does not exist.
Return to the main menu.

### D: Select Packages

*   Core ISO: Choose CD as source and select the appropriate CD drive if more than one exist on the installation machine.
*   Netinstall: Select an FTP/HTTP [mirror](https://www.archlinux.de/?page=MirrorStatus). *Note that archlinux.org is throttled to 50KB/s*.
*   All packages during installation are from the [core] repository. They are further divided into **Base**, and **Base-devel**.
*   Package information and brief descriptions are available [here](https://www.archlinux.org/packages/?repo=Core&arch=i686&limit=all&sort=pkgname).

Package selection is split into two stages. First, select the package category:

**Note:** For expedience, all packages in **base** are selected by default. Use the space-bar to select and de-select packages.

*   **Base**: Packages from the [core] repo to provide the minimal base environment. *Always select it and only remove packages that will not be used.*
*   **Base-devel**: Extra tools from [core] such as **make**, and **automake**. *Most beginners should choose to install it, and will probably need it later.*

After category selection, you will be presented with the full lists of packages, allowing you to fine-tune your selections. Use the space bar to select and unselect.

**Note:** If connection to a wireless network is required, remember to select and install the **wireless_tools** package. Some wireless interfaces also need [**ndiswrapper**](/index.php/Wireless_network_configuration#ndiswrapper "Wireless network configuration") and/or a specific [**firmware**](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration"). If you plan to use WPA encryption, you will need [**wpa_supplicant**](/index.php/WPA_supplicant "WPA supplicant"). The [Wireless Setup page](/index.php/Wireless_Setup "Wireless Setup") will help you choose the correct packages for your wireless device. Also strongly consider installing [**netcfg**](/index.php/Netcfg "Netcfg"), which will help you set up your network connection and profiles.

After selecting the needed packages, leave the selection screen and continue to the next step, Install Packages.

### E: Install Packages

Next, choose 'Install Packages'. You will be asked if you wish to keep the packages in the pacman cache. If you choose 'yes', you will have the flexibility to [downgrade](/index.php/Downgrade_packages "Downgrade packages") to previous package versions in the future, so this is recommended (you can always clear the cache in the future). The installer script will now install the selected packages, as well as the default Arch 2.6 kernel, to your system.

*   Netinstall: The [Pacman](/index.php/Pacman "Pacman") package manager will now download and install your selected packages. (See vc/5 for output, vc/1 to return to the installer)
*   Core image: The packages will be installed from the CD/USB stick.

### F: Configure the System

*Closely following and understanding these steps is of key importance to ensure a properly configured system.*

*   At this stage of the installation, you will configure the primary configuration files of your Arch Linux base system.

*   Previous versions of the installer included [hwdetect](/index.php/Hwdetect "Hwdetect") to gather information for your configuration. This has been deprecated, and **[udev](/index.php/Udev "Udev")** should handle most module loading automatically at boot.

Now you will be asked which text editor you want to use; choose [nano](/index.php/Nano "Nano"), [joe](http://joe-editor.sourceforge.net/) or [vi](/index.php/Vim "Vim"), (**nano** is generally considered easiest of the 3). You will be presented with a menu including the main configuration files for your system.

**Note:** *It is very important at this point to edit, or at least verify by opening, every configuration file.* The installer script relies on your input to create these files on your installation. A common error is to skip over these critical steps of configuration.

##### Can the installer handle this more automatically?

Hiding the process of system configuration is in direct opposition to ***[The Arch Way](/index.php/The_Arch_Way "The Arch Way")***. While it is true that recent versions of the kernel and hardware probing tools offer excellent hardware support and auto-configuration, Arch presents the user all pertinent configuration files during installation for the purposes of *transparency and system resource control*. By the time you have finished modifying these files to your specifications, you will have learned the simple method of manual Arch Linux system configuration and become more familiar with the base structure, leaving you better prepared to use and maintain your new installation productively.

***Moving on...***

#### /etc/rc.conf

Arch Linux uses the file `/etc/rc.conf` as the principal location for system configuration. This one file contains a wide range of configuration information, principally used at system startup. As its name directly implies, it also contains settings for and invokes the /etc/rc* files, and is, of course, sourced *by* these files.

##### LOCALIZATION section

*   **LOCALE**=: This sets your system locale, which will be used by all i18n-aware applications and utilities. You can get a list of the available locales by running `locale -a` from the command line. This setting's default is fine for US English users.
*   **HARDWARECLOCK**=: Specifies whether the hardware clock, which is synchronized on boot and on shutdown, stores **UTC** time, or **localtime**. UTC makes sense because it greatly simplifies changing timezones and daylight savings time. localtime is necessary if you dual boot with an operating system such as Windows, that only stores localtime to the hardware clock.
*   **USEDIRECTISA**=: Use direct I/O request instead of `/dev/rtc` for hwclock
*   **TIMEZONE**=: Specify your TIMEZONE. (All available zones are under `/usr/share/zoneinfo/`).
*   **KEYMAP**=: The available keymaps are in `/usr/share/kbd/keymaps`. Please note that this setting is only valid for your TTYs, not any graphical window managers or **X**.
*   **CONSOLEFONT**=: Available console fonts reside under `/usr/share/kbd/consolefonts/` if you must change. The default (blank) is safe.
*   **CONSOLEMAP**=: Defines the console map to load with the setfont program at boot. Possible maps are found in `/usr/share/kbd/consoletrans`, if needed. The default (blank) is safe.
*   **USECOLOR**=: Select "yes" if you have a color monitor and wish to have colors in your consoles.

```
LOCALE="en_US.utf8"
HARDWARECLOCK="localtime"
USEDIRECTISA="no"
TIMEZONE="US/Eastern"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

```

##### HARDWARE Section

*   **MOD_AUTOLOAD**=: Setting this to "yes" will use **udev** to automatically probe hardware and load the appropriate modules during boot, (convenient with the default modular kernel). Setting this to "no" will rely on the user's ability to specify this information manually, or compile their own custom kernel and modules, etc.
*   **MOD_BLACKLIST**=: This has become deprecated in favor of adding blacklisted modules directly to the **MODULES=** line below.
*   **MODULES**=: Specify additional MODULES if you know that an important module is missing. If your system has any floppy drives, add "floppy". If you will be using loopback filesystems, add "loop". Also specify any blacklisted modules by prefixing them with a bang (!). Udev will be forced NOT to load blacklisted modules. In the example, the IPv6 module as well as the annoying pcspeaker are blacklisted.

```
# Scan hardware and load required modules at boot
MOD_AUTOLOAD="yes"
# Module Blacklist - Deprecated
MOD_BLACKLIST=()
#
MODULES=(!net-pf-10 !snd_pcsp !pcspkr loop)

```

##### NETWORKING Section

*   **HOSTNAME**=:Set your HOSTNAME to your liking.
*   **eth0**=: 'Ethernet, card 0'. Adjust the interface IP address, netmask and broadcast address *if* you are using **static IP**. Set eth0="dhcp" if you want to use **DHCP**
*   **INTERFACES**=: Specify all interfaces here. Multiple interfaces should be separated with a space as in:

```
(eth0 wlan0)

```

*   **gateway**=: If you are using **static IP**, set the gateway address. If using **DHCP**, you can usually ignore this variable, though some users have reported the need to define it.
*   **ROUTES**=: If you are using static **IP**, remove the **!** in front of 'gateway'. If using **DHCP**, you can usually leave this variable commented out with the bang (!), but again, some users require the gateway and ROUTES defined. If you experience networking issues with pacman, for instance, you may want to return to these variables.

###### Example, using a dynamically assigned IP address (**DHCP**)

```
HOSTNAME="arch"
#eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
eth0="dhcp"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(!gateway)

```

###### Example, using a **static** IP address

```
HOSTNAME="arch"
eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(gateway)

```

Modify `/etc/resolv.conf` to specify the DNS servers of choice. Example:

```
search my.isp.net.
nameserver 4.2.2.1
nameserver 4.2.2.2
nameserver 4.2.2.3

```

Various processes can overwrite the contents of `/etc/resolv.conf`. For example, by default Arch Linux uses the **dhcpcd** DHCP client, which will overwrite the file when it starts. [Various methods](/index.php/Resolv.conf "Resolv.conf") may be used to preserve the nameserver settings in `/etc/resolv.conf`. For example, dhcpcd's configurations file may be edited to prevent the dhcpcd daemon from overwriting the file. To do this, you will need to append this to the end of `/etc/dhcpcd.conf`:

```
nohook resolv.conf

```

**Tip:** If using a non-standard MTU size (a.k.a. jumbo frames) is desired AND the installation machine hardware supports them, see the [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames") wiki article for further configuration.

##### DAEMONS Section

This array simply lists the names of those scripts contained in /etc/rc.d/ which are to be started during the boot process, and the order in which they start. Asynchronous initialization by backgrounding is also supported and useful for speeding up boot.

```
DAEMONS=(network @syslog-ng netfs @crond)

```

*   If a script name is prefixed with a bang (!), it is not executed.
*   If a script is prefixed with an "at" symbol (@), it shall be executed in the background; the startup sequence will not wait for successful completion of each daemon before continuing to the next. (Useful for speeding up system boot). Do not background daemons that are needed by other daemons. For example "mpd" depends on "network", therefore backgrounding network may cause mpd to break.
*   Edit this array whenever new system services are installed, if starting them automatically during boot is desired.

**Note:** This 'BSD-style' init, is the Arch way of handling what other distributions handle with various symlinks to an /etc/init.d directory.

###### About DAEMONS

The [daemons](/index.php/Daemons "Daemons") line need not be changed at this time, but it is useful to explain what daemons are, as they will be addressed later in this guide. A *daemon* is a program that runs in the background, waiting for events to occur and offering services. A good example is a webserver that waits for a request to deliver a page (e.g.:httpd) or an SSH server waiting for a user login (e.g.:sshd). While these are full-featured applications, there are also daemons whose work is not that visible. Examples are a daemon which writes messages into a log file (e.g. syslog, metalog), a daemon which lowers the CPU frequency if the system has nothing to do (e.g.:cpufreq), and a daemon which provides a graphical login (e.g.: gdm, kdm). All these programs can be added to the daemons line and will be started when the system boots. Useful daemons will be presented during this guide.

Historically, the term *daemon* was coined by the programmers of MIT's Project MAC. They took the name from *Maxwell's demon*, an imaginary being from a famous thought experiment that constantly works in the background, sorting molecules. <tt>UNIX</tt> systems inherited this terminology and created the backronym **d**isk **a**nd **e**xecution **mon**itor.

**Tip:** All Arch daemons reside under /etc/rc.d/

#### /etc/fstab

The **fstab** (for **f**ile **s**ystems **tab**le) is part of the system configuration listing all available disks and disk partitions, and indicating how they are to be initialized or otherwise integrated into the overall system's filesystem. The **/etc/fstab** file is most commonly used by the **mount** command. The mount command takes a filesystem on a device, and adds it to the main system hierarchy that you see when you use your system. **mount -a** is called from /etc/rc.sysinit, about 3/4 of the way through the boot process, and reads /etc/fstab to determine which options should be used when mounting the specified devices therein. If **noauto** is appended to a filesystem in /etc/fstab, **mount -a** will not mount it at boot.

##### An example /etc/fstab

```
# <file system>        <dir>        <type>        <options>                 <dump>    <pass>
none                   /dev/pts     devpts        defaults                       0         0
none                   /dev/shm     tmpfs         defaults                       0         0
#/dev/cdrom            /media/cdrom   auto        ro,user,noauto,unhide          0         0
#/dev/dvd              /media/dvd     auto        ro,user,noauto,unhide          0         0
#/dev/fd0              /media/fl      auto        user,noauto                    0         0
/dev/sda1                   /          jfs        defaults,noatime               0         1
/dev/sda2                   /var     reiserfs     defaults,noatime,notail        0         2
/dev/sda3                    swap     swap        defaults                       0         0
/dev/sda4                   /home      jfs        defaults,noatime               0         2

```

**Note:** The 'noatime' option disables writing read access times to the metadata of files and may safely be appended to / and /home regardless of your specified filesystem type for increased speed, performance, and power efficiency (see [here](http://kerneltrap.org/node/14148) for more). 'notail' disables the ReiserFS tailpacking feature, for added performance at the cost of slightly less efficient disk usage.

*   **<file system>**: describes the block device or remote filesystem to be mounted. For regular mounts, this field will contain a link to a block device node (as created by mknod which is called by udev at boot) for the device to be mounted; for instance, '/dev/cdrom' or '/dev/sda1'.

**Note:** If your system has more than one hard drive, the installer will default to using UUID rather than the sd*x* naming scheme, for consistent device mapping. Due to active developments in the kernel and also udev, the ordering in which drivers for storage controllers are loaded may change randomly, yielding an unbootable system/kernel panic. Nearly every motherboard has several controllers (onboard SATA, onboard IDE), and due to the aforementioned development updates, /dev/sda may become /dev/sdb on the next reboot. (See [this wiki article](/index.php/Persistent_block_device_naming "Persistent block device naming") for more information on persistent block device naming. )

*   **<dir>**: describes the mount point for the filesystem. For swap partitions, this field should be specified as 'swap'; (Swap partitions are not actually mounted.)

*   **<type>**: describes the type of the filesystem. The Linux kernel supports many filesystem types. (For the filesystems currently supported by the running kernel, see /proc/filesystems). An entry 'swap' denotes a file or partition to be used for swapping. An entry 'ignore' causes the line to be ignored. This is useful to show disk partitions which are currently unused.

*   **<options>**: describes the mount options associated with the filesystem. It is formatted as a comma separated list of options with no intervening spaces. It contains at least the type of mount plus any additional options appropriate to the filesystem type. For documentation on the available options for non-nfs file systems, see mount(8).

*   **<dump>**: used by the dump(8) command to determine which filesystems are to be dumped. dump is a backup utility. If the fifth field is not present, a value of zero is returned and dump will assume that the filesystem does not need to be backed up. *Note that dump is not installed by default.*

*   **<pass>**: used by the fsck(8) program to determine the order in which filesystem checks are done at boot time. The root filesystem should be specified with a <pass> of 1, and other filesystems should have a <pass> of 2 or 0\. Filesystems within a drive will be checked sequentially, but filesystems on different drives will be checked at the same time to utilize parallelism available in the hardware. If the sixth field is not present or zero, a value of zero is returned and fsck will assume that the filesystem does not need to be checked.

*   If you plan on using **hal** to automount media such as DVDs, you may wish to comment out the cdrom and dvd entries in preparation for **hal**, which will be installed later in this guide.

Expanded information available in the [Fstab](/index.php/Fstab "Fstab") wiki entry.

#### **[/etc/mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio").conf**

*Most users will not need to modify this file at this time, but please read the following explanatory information.*

This file allows further fine-tuning of the initial ram filesystem, or initramfs, (also historically referred to as the initial ramdisk or "initrd") for your system. The initramfs is a gzipped image that is read by the kernel during boot. The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem. This means it has to load any modules that are required for devices like IDE, SCSI, or SATA drives (or USB/FW, if you are booting from a USB/FW drive). Once the initrramfs loads the proper modules, either manually or through udev, it passes control to the kernel and your boot continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem. It does not need to contain every module you would ever want to use. The majority of common kernel modules will be loaded later on by udev, during the init process.

**mkinitcpio** is the next generation of **initramfs creation**. It has many advantages over the old **mkinitrd** and **mkinitramfs** scripts.

*   It uses "glibc" and "busybox" to provide a small and lightweight base for early userspace.
*   It can use **udev** for hardware autodetection at runtime, thus prevents you from having tons of unnecessary modules loaded.
*   Its hook-based init script is easily extendable with custom hooks, which can easily be included in pacman packages without having to modifiy mkinitcpio itself.
*   It already supports **lvm2**, **dm-crypt** for both legacy and luks volumes, **raid**, **swsusp** and **suspend2** resuming and booting from **usb mass storage** devices.
*   Many features can be configured from the kernel command line without having to rebuild the image.
*   The **mkinitcpio** script makes it possible to include the image in a kernel, thus making a self-contained kernel image is possible.
*   Its flexibility makes recompiling a kernel unnecessary in many cases.

If using RAID or LVM on the root filesystem, the appropriate HOOKS must be configured. See the wiki pages for [RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") and [/etc/mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio") for more info. If using a non-US keyboard. add the "`keymap`" hook to load your local keymap during boot. Add the "`usbinput`" hook if using a USB keyboard, e.g.:

```
HOOKS="base udev autodetect pata scsi sata filesystems keymap usbinput"

```

(Otherwise, if boot fails for some reason you will be asked to enter root's password for system maintenance but will be unable to do so.)

If you need support for booting from USB devices, FireWire devices, PCMCIA devices, NFS shares, software RAID arrays, LVM2 volumes, encrypted volumes, or DSDT support, configure your HOOKS accordingly.

If doing a CF or SD card install, you may need to add the `usbinput` HOOK for your system to boot properly.

*If you are using a US keyboard, and have no need for any of the above HOOKS, editing this configuration should be unnecessary at this point.*

**mkinitcpio** is an Arch innovation developed by Aaron Griffin and Tobias Powalowski with some help from the community.

#### /etc/resolv.conf (for Static IP)

The *resolver* is a set of routines in the C library that provide access to the Internet Domain Name System (DNS). One of the main functions of DNS is to translate domain names into IP addresses, to make the Web a friendlier place. The resolver configuration file, or /etc/resolv.conf, contains information that is read by the resolver routines the first time they are invoked by a process.

*   *If you are using DHCP, you may safely ignore this file, as by default, it will be dynamically created and destroyed by the dhcpcd daemon. You may change this default behavior if you wish. (See [Network](/index.php/Network#For_DHCP_IP "Network")]).*

If you use a static IP, set your DNS servers in /etc/resolv.conf (nameserver <ip-address>). You may have as many as you wish. An example, using OpenDNS:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

If you are using a router, you will probably want to specify your DNS servers in the router itself, and merely point to it from your **/etc/resolv.conf**, using your router's IP (which is also your gateway from **/etc/rc.conf**), e.g.:

```
nameserver 192.168.1.1

```

If using **DHCP**, you may also specify your DNS servers in the router, or allow automatic assignment from your ISP, if your ISP is so equipped.

#### /etc/hosts

This file associates IP addresses with hostnames and aliases, one line per IP address. For each host a single line should be present with the following information:

```
<IP-address> <hostname> [aliases...]

```

Add your *hostname*, coinciding with the one specified in /etc/rc.conf, as an alias, so that it looks like this:

```
127.0.0.1   localhost.localdomain   localhost ***yourhostname***

```

**Note:** *This format, **including the 'localhost' and your actual host name**, is required for program compatibility! So, if you have named your computer "arch", then that line above should look like this:*
```
127.0.0.1   localhost.localdomain   localhost arch

```
Errors in this entry may cause poor network performance and/or certain programs to open very slowly, or not work at all. This is a very common error for beginners.

If you use a static IP, add another line using the syntax: <static-IP> <hostname.domainname.org> <hostname> e.g.:

```
192.168.1.100 ***yourhostname***.domain.org  ***yourhostname***

```

**Tip:** For convenience, you may also use /etc/hosts aliases for hosts on your network, and/or on the Web, e.g.:
```
64.233.169.103   www.google.com   g
192.168.1.90   media
192.168.1.88   data

```
The above example would allow you to access google simply by typing 'g' into your browser, and access to a media and data server on your network by name and without the need for typing out their respective IP addresses.

#### /etc/hosts.deny and /etc/hosts.allow

Modify these configurations according to your needs if you plan on using the [ssh](/index.php/SSH "SSH") daemon. The default configuration will reject all incoming connections, not only ssh connections. Edit your **/etc/hosts.allow** file and add the appropriate parameters:

*   let everyone connect to you

```
sshd: ALL

```

*   restrict it to a certain ip

```
sshd: 192.168.0.1

```

*   restrict it to your local LAN network (range 192.168.0.0 to 192.168.0.255)

```
sshd: 192.168.0.

```

*   OR restrict for an IP range

```
sshd: 10.0.0.0/255.255.255.0

```

If you do not plan on using the [ssh](/index.php/SSH "SSH") daemon, leave this file at the default, (empty), for added security.

#### /etc/locale.gen

The **/usr/sbin/locale-gen** command reads from **/etc/locale.gen** to generate specific locales. They can then be used by **glibc** and any other locale-aware program or library for rendering text, correctly displaying regional monetary values, time and date formats, alphabetic idiosyncrasies, and other locale-specific standards.

By default /etc/locale.gen is an empty file with commented documentation. Once edited, the file remains untouched. **locale-gen** runs on every **glibc** upgrade, generating all the locales specified in /etc/locale.gen.

Choose the locale(s) you need (remove the # in front of the lines you want), e.g.:

```
en_US ISO-8859-1
en_US.UTF-8	

```

The installer will now run the locale-gen script, which will generate the locales you specified. You may change your locale in the future by editing /etc/locale.gen and subsequently running 'locale-gen' as root.

**Note:** ***If you fail to choose your locale, this will lead to a "The current locale is invalid..." error. This is perhaps the most common mistake by new Arch users, and also leads to the most commonly asked questions on the forum.***

#### Pacman-Mirror

Choose a mirror repository for **pacman**.

*   *archlinux.org is throttled, limiting downloads to 50KB/s*

#### Root password

Finally, set a root password and make sure that you remember it later. Return to the main menu and continue with installing bootloader.

### Install and configure a bootloader

#### For BIOS motherboards

For BIOS systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [Syslinux](/index.php/Syslinux "Syslinux") is (currently) limited to loading only files from the partition where it was installed. Its configuration file is considered to be easier to understand. An example configuration can be found in the [syslinux](/index.php/Syslinux#Examples "Syslinux") article.
*   [GRUB](/index.php/GRUB "GRUB") is more feature-rich and supports more complex scenarios. Its configuration file(s) is more similar to 'sh' scripting language, which may be difficult for beginners to manually write. It is recommended that they automatically generate one.

##### Syslinux

If you opted for a GUID partition table (GPT) for your hard drive earlier, you need to install the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package now for the installation of *syslinux* to work:

```
# pacman -S gptfdisk

```

Install the [syslinux](https://www.archlinux.org/packages/?name=syslinux) package and then use the `syslinux-install_update` script to automatically *install* the bootloader (`-i`), mark the partition *active* by setting the boot flag (`-a`), and install the *MBR* boot code (`-m`):

```
# pacman -S syslinux
# syslinux-install_update -iam

```

After installing Syslinux, configure `syslinux.cfg` to point to the right root partition. This step is vital. If it points to the wrong partition, Arch Linux will not boot. Change `/dev/sda3` to reflect your root partition (if you partitioned your drive as in [the example](#Prepare_the_storage_drive), your root partition is `/dev/sda1`).

 `# nano /boot/syslinux/syslinux.cfg` 
```
...
LABEL arch
        ...
        APPEND root=**/dev/sda3** rw
        ...
```

If adding [UUID](/index.php/UUID "UUID") rather than partition number the syntax is `APPEND root=UUID=*partition_uuid* rw`.

Do the same for the fallback entry.

For more information on configuring and using Syslinux, see [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) package and then run `grub-install` to install the bootloader:

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

**Note:**

*   Change `/dev/sda` to reflect the drive you installed Arch on. Do not append a partition number (do not use `sda*X*`).
*   For GPT-partitioned drives on BIOS motherboards, you also need a "BIOS Boot Partition". See [GPT-specific instructions](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") in the GRUB page.
*   A sample `/boot/grub/grub.cfg` gets installed as part of the [grub](https://www.archlinux.org/packages/?name=grub) package, and subsequent `grub-*` commands may not over-write it. Ensure that your intended changes are in `grub.cfg`, rather than in `grub.cfg.new` or some such file.

While using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`) before running the next command.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** It is possible that multiple redundant menu entries will be generated. See [GRUB#Redundant_menu_entries](/index.php/GRUB#Redundant_menu_entries "GRUB").

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

#### For UEFI motherboards

For UEFI systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [gummiboot](/index.php/Gummiboot "Gummiboot") is a minimal UEFI Boot Manager which provides a menu for [EFISTUB](/index.php/EFISTUB "EFISTUB") kernels and other UEFI applications.
*   [GRUB](/index.php/GRUB "GRUB") is a more complete bootloader, useful if you run into problems with Gummiboot.

No matter which one you choose, first install the [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) package, so you can manipulate your EFI System Partition after installation:

```
# pacman -S dosfstools

```

**Note:** For UEFI boot, the drive needs to be GPT-partitioned and an [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (512 MiB or larger, gdisk type `EF00`, formatted with FAT32) must be present. In the following examples, this partition is assumed to be mounted at `/boot`. If you have followed this guide from the beginning, you have already done all of these.

##### Gummiboot

Install the [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) package and run `gummiboot install` to install the bootloader to the EFI System Partition:

```
# pacman -S gummiboot
# gummiboot install

```

**Warning:** Gummiboot and the Linux Kernel will not automatically update if your EFI System Partition is not mounted at `/boot`.

You will need to manually create a configuration file to add an entry for Arch Linux to the gummiboot manager. Create `/boot/loader/entries/arch.conf` and add the following contents, replacing `/dev/sdaX` with your **root** partition, usually `/dev/sda2`:

 `# nano /boot/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

For more information on configuring and using gummiboot, see [gummiboot](/index.php/Gummiboot "Gummiboot").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) and [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) packages and run `grub-install` to install the bootloader:

```
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

Next, while using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) before running the next command. However *os-prober* is not known to properly detect UEFI OSes.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

### H: Reboot

That's it; You have configured and installed your Arch Linux base system. Exit the install, and reboot:

```
# reboot

```

(Be sure to remove the installer CD)

## Part II: Configure & Update the New Arch Linux base system

Your new Arch Linux system will boot up and finish with a login prompt (you may want to change the boot order in your **BIOS** back to booting from hard disk).

**Congratulations, and welcome to your new Arch Linux base system!**

Your new Arch Linux base system is now a functional GNU/Linux environment ready for customization. From here, you may build this elegant set of tools into whatever you wish or require for your purposes.

Login with the root account. We will configure pacman and update the system as root, then add a normal user.

**Note:** Virtual consoles 1-6 are available. You may switch between them with ALT+F1...F6

### Step 1: Configuring the network (if necessary)

*   *This section will assist you in configuring most types of networks, if your network configuration is not working for you.*

If you properly configured your system, you should have a working network. Try to ping www.google.com to verify this.

```
# ping -c 3 www.google.com

```

*If you have successfully established a network connection, continue with **[Update, Sync, and Upgrade the system with pacman](#Step_2:_Update.2C_Sync.2C_and_Upgrade_the_system_with_pacman)**.*

If, after trying to ping www.google.com, an "unknown host" error is received, you may conclude that your network is not properly configured. You may choose to double-check the following files for integrity and proper settings:

**/etc/rc.conf** # Specifically, check your HOSTNAME= and NETWORKING section for typos and errors.

**/etc/hosts** # Double-check your format. (See above.)

**/etc/resolv.conf** # If you are using a static IP. If you are using DHCP, this file will be dynamically created and destroyed by default, but can be changed to your preference. (See [Network](/index.php/Network "Network").)

**Tip:** Advanced instructions for configuring the network can be found in the [Network](/index.php/Network "Network") article.

#### Wired LAN

Check your Ethernet with

```
# ifconfig -a

```

All interfaces will be listed. You should see an entry for eth0, or perhaps eth1\.

*   **Static IP**

If required, you can set a new static IP with:

```
# ifconfig eth0 <ip address> netmask <netmask> up 

```

and the default gateway with

```
# ip route add default via <ip address of the gateway>

```

Verify that /etc/resolv.conf contains your DNS server and add it if it is missing. Check your network again with ping www.google.com. If everything is working now, adjust /etc/rc.conf as described above for static IP.

*   **DHCP**

If you have a DHCP server/router in your network try:

```
# dhcpcd eth0

```

If this is working, adjust /etc/rc.conf as described above, for dynamic IP.

#### Wireless LAN

*   Ensure the driver has created a usable interface:

```
# iwconfig

```

*   Bring the interface up with `ifconfig <interface> up`. e.g.:

```
# ifconfig wlan0 up

```

**Note:** If you get this error message: `SIOCSIFFLAGS: No such file or directory` it most certainly means your wireless chipset requires a firmware to function, which you forgot to install during package selection. See [Does the Wireless Chipset require Firmware?](/index.php/Beginners%27_guide#Does_the_Wireless_Chipset_require_Firmware.3F "Beginners' guide") and [Select Packages](/index.php/Beginners%27_guide#D:_Select_Packages "Beginners' guide").

*   Associate your wireless device with the access point you want to use. Depending on the encryption (none, WEP, or WPA), the procedure may differ. You need to know the name of the chosen wireless network (ESSID), e.g. 'linksys' in the following examples:
*   An example using a *non-encrypted* network:

```
# iwconfig wlan0 essid "linksys"

```

*   An example using *WEP and a hexadecimal key*:

```
# iwconfig wlan0 essid "linksys" key 0241baf34c

```

*   An example using *WEP and an ASCII passphrase*:

```
# iwconfig wlan0 essid "linksys" key s:pass1

```

*   Using *WPA*, the procedure requires a bit more work. Check [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") for more information and troubleshooting:

```
# wpa_passphrase linksys "secretpassphrase" > /etc/wpa_supplicant.conf
# wpa_supplicant -B -Dwext -i wlan0 -c /etc/wpa_supplicant.conf

```

*   Check you have successfully associated to the access point before continuing:

```
# iwconfig wlan0

```

*   Request an IP address with `/sbin/dhcpcd <interface>` . e.g.:

```
# dhcpcd wlan0

```

*   Ensure you can route using `/bin/ping`:

```
# ping -c 3 www.google.com

```

You should have a working network connection. For troubleshooting, check the detailed [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup") page.

#### Analog Modem

To be able to use a Hayes-compatible, external, analog modem, you need to at least have the ppp package installed. Modify the file /etc/ppp/options to suit your needs and according to man pppd. You will need to define a chat script to supply your username and password to the ISP after the initial connection has been established. The manpages for pppd and chat have examples in them that should suffice to get a connection up and running if you're either experienced or stubborn enough. With udev, your serial ports usually are /dev/tts/0 and /dev/tts/1. Tip: Read [Dialup without a dialer HOWTO](/index.php/Dialup_without_a_dialer_HOWTO "Dialup without a dialer HOWTO").

Instead of fighting a glorious battle with the plain pppd, you may opt to install wvdial or a similar tool to ease the setup process considerably. In case you're using a so-called WinModem, which is basically a PCI plugin card working as an internal analog modem, you should indulge in the vast information found on the [LinModem](http://www.linmodems.org/) homepage.

#### ISDN

Setting up ISDN is done in three steps:

1.  Install and configure hardware
2.  Install and configure the ISDN utilities
3.  Add settings for your ISP

The current Arch stock kernels include the necessary ISDN modules, meaning that you will not need to recompile your kernel unless you're about to use rather odd ISDN hardware. After physically installing your ISDN card in your machine or plugging in your USB ISDN-Box, you can try loading the modules with modprobe. Nearly all passive ISDN PCI cards are handled by the hisax module, which needs two parameters: type and protocol. You must set protocol to '1' if your country uses the 1TR6 standard, '2' if it uses EuroISDN (EDSS1), '3' if you're hooked to a so-called leased-line without D-channel, and '4' for US NI1.

Details on all those settings and how to set them is included in the kernel documentation, more specifically in the isdn subdirectory, and available online. The type parameter depends on your card; a list of all possible types can be found in the README.HiSax kernel documentation. Choose your card and load the module with the appropriate options like this:

```
# modprobe hisax type=18 protocol=2

```

This will load the hisax module for my ELSA Quickstep 1000PCI, being used in Germany with the EDSS1 protocol. You should find helpful debugging output in your /var/log/everything.log file, in which you should see your card being prepared for action. Please note that you will probably need to load some USB modules before you can work with an external USB ISDN Adapter.

Once you have confirmed that your card works with certain settings, you can add the module options to your /etc/modprobe.d/modprobe.conf:

```
alias ippp0 hisax
options hisax type=18 protocol=2

```

Alternatively, you can add only the options line here, and add hisax to your MODULES array in the rc.conf. It's your choice, really, but this example has the advantage that the module will not be loaded until it's really needed.

That being done, you should have working, supported hardware. Now you need the basic utilities to actually use it!

Install the isdn4k-utils package, and read the manpage to isdnctrl; it'll get you started. Further down in the manpage you will find explanations on how to create a configuration file that can be parsed by isdnctrl, as well as some helpful setup examples. Please note that you have to add your SPID to your MSN setting separated by a colon if you use US NI1.

After you have configured your ISDN card with the isdnctrl utility, you should be able to dial into the machine you specified with the PHONE_OUT parameter, but fail the username and password authentication. To make this work add your username and password to /etc/ppp/pap-secrets or /etc/ppp/chap-secrets as if you were configuring a normal analogous PPP link, depending on which protocol your ISP uses for authentication. If in doubt, put your data into both files.

If you set up everything correctly, you should now be able to establish a dial-up connection with

```
# isdnctrl dial ippp0

```

as root. If you have any problems, remember to check the logfiles!

#### DSL (PPPoE)

These instructions are relevant to you only if your PC itself is supposed to manage the connection to your ISP. You do not need to do anything but define a correct default gateway if you are using a separate router of some sort to do the grunt work.

Before you can use your DSL online connection, you will have to physically install the network card that is supposed to be connected to the DSL-Modem into your computer. After adding your newly installed network card to the modules.conf/modprobe.conf or the MODULES array, you should install the rp-pppoe package and run the pppoe-setup script to configure your connection. After you have entered all the data, you can connect and disconnect your line with

```
# /etc/rc.d/adsl start

```

and

```
# /etc/rc.d/adsl stop

```

respectively. The setup usually is rather easy and straightforward, but feel free to read the manpages for hints. If you want to automatically 'dial in' at boot, add adsl to your DAEMONS array, and put a ! before the network entry, since the network is handled by adsl now.

### Step 2: Update, Sync, and Upgrade the system with [pacman](/index.php/Pacman "Pacman")

Now we will update the system using [pacman](/index.php/Pacman "Pacman").

#### What is pacman ?

[Pacman](/index.php/Pacman "Pacman") is the **pac**kage **man**ager of Arch Linux. Pacman is written in *C* and is designed from the ground up to be lightweight, to occupy a very modest memory footprint, and to be fast, simple, and versatile. It manages your entire package system and handles installation, removal, package downgrade (through cache), custom compiled package handling, automatic dependency resolution, remote and local searches and much more. Pacman's output is streamlined, very readable and provides ETA for each package download. Arch uses pkg.tar.gz tarballs and is in the process of moving to the pkg.tar.xz format.

Pacman will now be used to download software packages from remote repositories and install them onto your system.

#### Package Repositories and /etc/pacman.conf

Arch currently offers the following 4 repositories readily accessible through pacman:

**[core]**

The simple principle behind [core] is to provide only one of each necessary tool for a base Arch Linux system; The GNU toolchain, the Linux kernel, one editor, one command line browser, etc. (There are a few exceptions to this. For instance, both vi and nano are provided, allowing the user to choose one or both.) It contains all the packages that MUST be in perfect working order to ensure the system remains in a usable state. These are the absolute system-critical packages.

*   Developer maintained
*   All binary packages
*   pacman accessible
*   *The Core installation media simply contains an installer script, and a snapshot of the core repository at the time of release.*

**[extra]**

The [extra] repository contains all Arch packages that are not themselves necessary for a base Arch system, but contribute to a more full-featured environment. **X**, KDE, and Apache, for instance, can be found here.

*   Developer maintained
*   All binary packages
*   pacman accessible

**[testing]**

The [testing] repository contains packages that are candidates for the [core] or [extra] repositories. New packages go into [testing] if:

* they are expected to break something on update and need to be tested first.

* they require other packages to be rebuilt. In this case, all packages that need to be rebuilt are put into [testing] first and when all rebuilds are done, they are moved back to the other repositories.

*   Developer maintained
*   All binary packages
*   pacman accessible

**Note:** [testing] is the only repository that can have name collisions with any of the other official repositories. Therefore, if enabled, [testing] must be the first repo listed in `pacman.conf`.

**Warning:** Only experienced users should use [testing].

**[community]**

The [community] repository is maintained by the *Trusted Users (TUs)* and is simply the binary branch of the *Arch User Repository ([AUR](/index.php/AUR "AUR"))*. It contains binary packages which originated as PKGBUILDs from *AUR* [unsupported] that have acquired enough votes and were adopted by a *TU*. Like all repos listed above, [community] may be readily accessed by pacman.

*   TU maintained
*   All binary packages
*   pacman accessible

**AUR (unsupported)**

The **[AUR](/index.php/AUR "AUR")** also contains the **unsupported** branch, which cannot be accessed directly by pacman*. **AUR** [unsupported] does not contain binary packages. Rather, it provides more than sixteen thousand PKGBUILD scripts for building packages from source, that may be unavailable through the other repos. When an AUR unsupported package acquires enough popular votes, it may be moved to the AUR [community] binary repo, if a TU is willing to adopt and maintain it there.

*   TU maintained
*   All PKGBUILD bash build scripts
*   ***Not*** pacman accessible by default

* pacman wrappers (***[AUR helpers](/index.php/AUR_helpers "AUR helpers")***) can help you seamlessly access AUR.

**/etc/pacman.conf**

pacman will attempt to read /etc/pacman.conf each time it is invoked. This configuration file is divided into sections, or repositories. Each section defines a package [repository](/index.php/Official_repositories "Official repositories") that pacman can use when searching for packages. The exception to this is the options section, which defines global options.

Note that the defaults should work, so modifying at this point may be unnecessary, but verification is always recommended. Further info available in the [Mirrors](/index.php/Mirrors "Mirrors") article.

```
# nano /etc/pacman.conf

```

Example:

```
#
# /etc/pacman.conf
#
# See the pacman.conf(5) manpage for option and repository directives

#
# GENERAL OPTIONS
#
[options]
# The following paths are commented out with their default values listed.
# If you wish to use different paths, uncomment and update the paths.
#RootDir     = /
#DBPath      = /var/lib/pacman/
#CacheDir    = /var/cache/pacman/pkg/
#LogFile     = /var/log/pacman.log
HoldPkg     = pacman glibc
# If upgrades are available for these packages they will be asked for first
SyncFirst   = pacman
#XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
#XferCommand = /usr/bin/curl %u > %o

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
#IgnorePkg   =
#IgnoreGroup =

#NoUpgrade   =
#NoExtract   =

# Misc options (all disabled by default)
#NoPassiveFtp
#UseSyslog
#ShowSize
#UseDelta
#TotalDownload
#
# REPOSITORIES
#   - can be defined here or included from another file
#   - pacman will search repositories in the order defined here
#   - local/custom mirrors can be added here or in separate files
#   - repositories listed first will take precedence when packages
#     have identical names, regardless of version number
#   - URLs will have $repo replaced by the name of the current repo
#
# Repository entries are of the format:
#       [repo-name]
#       Server = ServerName
#       Include = IncludePath
#
# The header [repo-name] is crucial - it must be present and
# uncommented to enable the repo.
# 

# Testing is disabled by default.  To enable, uncomment the following
# two lines.  You can add preferred servers immediately after the header,
# and they will be used before the default mirrors.
#[testing]
#Include = /etc/pacman.d/mirrorlist

[core]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

[extra]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist 

[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#Server = file:///home/custompkgs

```

Enable all desired repositories (remove the # in front of the 'Include =' and '[repository]' lines).

*   ***When choosing repos, be sure to uncomment both the repository header lines in [brackets] as well as the 'Include =' lines. Failure to do so will result in the selected repository being omitted! This is a very common error.***

#### /etc/pacman.d/mirrorlist

Defines pacman repository mirrors and priorities.

**Build a mirrorlist using the rankmirrors script** (Optional)

`/usr/bin/rankmirrors` is a python script which will attempt to detect uncommented mirrors specified in /etc/pacman.d/mirrorlist which are closest to the installation machine based on latency. Faster mirrors will dramatically improve pacman performance, and the overall Arch Linux experience. This script may be run periodically, especially if the chosen mirrors provide inconsistent throughput and/or updates. Note that `rankmirrors` does not test for throughput. Tools such as `wget` or `rsync` may be used to effectively test for mirror throughput after a new `/etc/pacman.d/mirrorlist` has been generated.

**Initially force pacman to refresh the package lists**

Issue the following command:

```
# pacman -Syy

```

Passing two --refresh or -y flags forces pacman to refresh all package lists even if they are considered to be up to date. Issuing pacman -Syy *whenever a mirror is changed*, is good practice and will avoid possible headaches.

Use pacman to install python:

```
# pacman -S python 

```

*   ***If you get an error at this step, use the command "nano /etc/pacman.d/mirrorlist" and uncomment a server that suits you.***

**cd** to the /etc/pacman.d/ directory:

```
# cd /etc/pacman.d

```

Backup the existing /etc/pacman.d/mirrorlist:

```
# cp mirrorlist mirrorlist.backup

```

Edit mirrorlist.backup and uncomment all mirrors on the same continent or within geographical proximity to test with rankmirrors.

```
# nano mirrorlist.backup

```

Run the script against the mirrorlist.backup with the -n switch and redirect output to a new /etc/pacman.d/mirrorlist file:

```
# rankmirrors -n 6 mirrorlist.backup > mirrorlist

```

**-n 6**: rank the 6 closest mirrors

Force pacman to refresh all package lists with the new mirrorlist in place:

```
# pacman -Syy

```

#### Mirrorcheck for up-to-date packages

Some of the official mirrors may contain packages that are out-of-date. [ArchLinux Mirrorcheck](http://users.archlinux.de/~gerbra/mirrorcheck.html) reports various aspects about the mirrors such as, those experiencing network problems, data collection problems, reports the last time they have been synced, etc.

One may wish to manually inspect the mirrors in the /etc/pacman.d/mirrorlist insuring that it only contains up-to-date mirrors if having the latest package versions is a priority.

#### Ignoring packages

After executing the command "pacman -Syu", the entire system will be updated. It is possible to prevent a package from being upgraded. A typical scenario would be a package for which an upgrade may prove problematic for the system. In this case, there are two options; indicate the package(s) to skip in the pacman command line using the --ignore switch (do pacman -S --help for details) or permanently indicate the package(s) to skip in the /etc/pacman.conf file in the IgnorePkg array. List each package, with one intervening space :

```
IgnorePkg = wine  

```

The typical way to use Arch is to use pacman to install all packages unless there is no package available, in which case [ABS](/index.php/ABS "ABS") may be used. Many user-contributed package build scripts are also available in the [AUR](/index.php/AUR "AUR").

The power user is expected to keep the system up to date with pacman -Syu, rather than selectively upgrading packages. You may diverge from this typical usage as you wish; just be warned that there is a greater chance that things will not work as intended and that it could break your system. The majority of complaints happen when selective upgrading, unusual compilation or improper software installation is performed. Use of **IgnorePkg** in /etc/pacman.conf is therefore discouraged, and should only be used sparingly, if you know what you are doing.

#### Ignoring Configuration Files

In the same vein, you can also "protect" your configuration/system files from being overwritten during "pacman -Su" using the following option in your /etc/pacman.conf

```
NoUpgrade = etc/lilo.conf boot/grub/menu.lst

```

#### Get familiar with pacman

pacman is the Arch user's best friend. It is highly recommended to study and learn how to use the pacman(8) tool. Try:

```
$ man pacman

```

For more information,please look up the [pacman](/index.php/Pacman "Pacman") wiki entries at your leisure.

### Step 3: Update System

You are now ready to upgrade your entire system. Before you do, read through the [news](https://www.archlinux.org/news/) (and optionally the [announce mailing list](https://archlinux.org/pipermail/arch-announce/)). Often the developers will provide important information about required configurations and modifications for known issues. Consulting these pages before any upgrade is good practice.

Sync, refresh, and upgrade your entire new system with:

```
# pacman -Syu

```

or:

```
# pacman --sync --refresh --sysupgrade

```

pacman will now download a fresh copy of the master package list from the server(s) defined in pacman.conf(5) and perform all available upgrades. (You may be prompted to upgrade pacman itself at this point. If so, say yes, and then reissue the pacman -Syu command when finished.)

Reboot if a kernel upgrade has occurred.

**Note:** Occasionally, configuration changes may take place requiring user action during an update; read pacman's output for any pertinent information.

Pacman output is saved in /var/log/pacman.log.

See [Package Management FAQs](/index.php/Package_Management_FAQs "Package Management FAQs") for answers to frequently asked questions regarding updating and managing your packages.

##### The Arch rolling release model

Keep in mind that Arch is a **rolling release** distribution. This means there is never a reason to reinstall or perform elaborate system rebuilds to upgrade to the newest version. Simply issuing **pacman -Syu** periodically keeps your entire system up-to-date and on the bleeding edge. At the end of this upgrade, your system is completely current. **Reboot** if a kernel upgrade has occurred.

##### Network Time Protocol

You may wish to set the system time now using NTP protocol to sync the local clock to remote NTP servers. There are two options available:

*   **[NTPD](/index.php/NTPD "NTPD")** functions very well, though initial configuration may be more complex.
*   **[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")** is an alternative OpenBSD NTP project which is more simple to configure. Development may not be active for GNU/Linux at this time, as the last released version was on 14 May 2006\.

For more information see the [Network Time Protocol](/index.php/Network_Time_Protocol "Network Time Protocol") article.

### Step 4: Add a user and setup groups

<tt>UNIX</tt> is a multi-user environment. You should not do your everyday work using the root account. It is more than poor practice; it is dangerous. Root is for administrative tasks. Instead, add a normal, non-root user account using the `/usr/sbin/adduser` program, an interactive user adding program which will prompt you for the relevant data (see details below) *(recommended for beginners)*:

```
# adduser

```

**Alternative method, using `/usr/sbin/useradd`:**

Alternatively, you may use `useradd`

```
# useradd -m -G [groups] -s [login_shell] [username] 

```

*   **-m** Creates user home directory as /home/**username**. Within their home directory, a user can write files, delete them, install programs, etc. Users' home directories shall contain their data and personal configuration files, the so-called 'dot files' (their name is preceded by a dot), which are 'hidden'. (To view dotfiles, enable the appropriate option in your file manager or run ls with the -a switch.) If there is a conflict between *user* (under /home/username) and *global* configuration files, (usually under /etc/) the settings in the *user* file will prevail. Dotfiles likely to be altered by the end user include .xinitrc and .bashrc files. The configuration files for xinit and Bash respectively. They allow the user the ability to change the window manager to be started upon login and also aliases, user-specified commands and environment variables respectively. When a user is created, their dotfiles shall be taken from the /etc/skel directory where system sample files reside.
*   **-G** A list of supplementary groups which the user is also a member of. *Each group is separated from the next by a comma, with no intervening spaces*. The default is for the user to belong only to the initial group (users).
*   **-s** The path and filename of the user´s default login shell. Arch Linux init scripts use Bash. After the boot process is complete, the default login shell is user-specified. (Ensure the chosen shell package is installed if choosing something other than Bash).

Useful groups for your non-root user include:

*   **audio** - for tasks involving sound card and related software
*   **floppy** - for access to a floppy if applicable
*   **lp** - for managing printing tasks
*   **optical** - for managing tasks pertaining to the optical drive(s)
*   **storage** - for managing storage devices
*   **video** - for video tasks and hardware acceleration
*   **wheel** - for using sudo
*   **power** - used w/ power options (e.g.: shutdown with power button)

A typical desktop system example, adding a user named "archie" specifying bash as the login shell:

```
# useradd -m -G users,audio,lp,optical,storage,video,wheel,power -s /bin/bash archie

```

Next, add a password for your new user using `/usr/bin/passwd`.

An example for our user, 'archie':

```
# passwd archie

```

(You will be prompted to provide the new <tt>UNIX</tt> password.)

Your new non-root user has now been created, complete with a home directory and a login password.

**Deleting the user account:**

In the event of error, or if you wish to delete this user account in favor of a different name or for any other reason, use `/usr/sbin/userdel`:

```
# userdel -r [username]

```

*   **-r** Files in the user´s home directory will be removed along with the home directory itself and the user´s mail spool.

If you want to change the name of your user or any existing user, see the [Change username](/index.php/Change_username "Change username") page of the Arch wiki and/or the [Groups](/index.php/Groups "Groups") and [User Management](/index.php/User_Management "User Management") articles for further information. You may also check the man pages for `usermod(8)` and `gpasswd(8)`.

### Step 5: Install and setup Sudo (Optional)

Install Sudo:

```
# pacman -S sudo

```

To add a user as a sudo user (a "sudoer"), the visudo command must be run as root.

By default, the visudo command uses the editor [vi](/index.php/Vi "Vi"). If you do not know how to use vi, you may set the EDITOR environment variable to the editor of your choice, such as in this example with the editor "nano":

```
# EDITOR=nano visudo

```

**Note:** Please note that you are setting the variable and starting visudo on the same line at the same time. This will not work properly as two separated commands.

If you are comfortable using vi, issue the visudo command without the EDITOR=nano variable:

```
# visudo

```

This will open the file /etc/sudoers in a special session of vi. visudo copies the file to be edited to a temporary file, edits it with an editor, (vi by default), and subsequently runs a sanity check. If it passes, the temporary file overwrites the original with the correct permissions.

**Warning:** Do not edit /etc/sudoers directly with an editor; Errors in syntax can cause annoyances (like rendering the root account unusable). You must use the *visudo* command to edit /etc/sudoers.

To give the user full root privileges when he/she precedes a command with "sudo", add the following line:

```
USER_NAME   ALL=(ALL) ALL

```

where USER_NAME is the username of the individual.

For more information, such as sudoer <TAB> completion, see [Sudo](/index.php/Sudo "Sudo")

## Part III: Install X and configure ALSA

### Step 1: Configure sound with alsamixer

The Advanced Linux Sound Architecture (known by the acronym **ALSA**) is a Linux kernel component intended to replace the original Open Sound System (OSS) for providing device drivers for sound cards. Besides the sound device drivers, **ALSA** also bundles a user space library for application developers who want to use driver features with a higher level API than direct interaction with the kernel drivers.

**Note:** Alsa is included in the Arch mainline kernel and udev will automatically probe your hardware at boot, loading the corresponding kernel module for your audio card. Therefore, your sound should already be working, but upstream sources mute all channels by default.

**Note:** OSS4.1 has been released under a free license and is generally considered a significant improvement over older OSS versions. If you have issues with ALSA, or simply wish to explore another option, you may choose OSS4.1 instead. Instructions can be found in [OSS](/index.php/OSS "OSS")

The alsa-utils package contains the alsamixer userspace tool, which allows configuration of the sound device from the console or terminal.

By default the upstream kernel sources ship with snd_pcsp, the alsa pc speaker module. snd_pcsp is usually loaded before your "actual" sound card module. In most cases, it will be more convenient if this module is loaded last, as it will allow alsamixer to correctly control the desired sound card.

To have snd_pcsp load last, add the following to /etc/modprobe.d/modprobe.conf:

```
options snd-pcsp index=2

```

Alternatively, if you do not want snd_pcsp to load at all, blacklist it by adding the following to /etc/rc.conf:

```
MODULES=(... !snd_pcsp)

```

**Note:** You will need to unload all your sound modules and reload them for the changes to take effect. It might be easier to reboot. Your choice.

Install the alsa-utils package:

```
 # pacman -S alsa-utils

```

Also, you may want to install the alsa-oss package, which wraps applications written for [OSS](/index.php/OSS "OSS") in a compatibility library, allowing them to work with [ALSA](/index.php/ALSA "ALSA"). To install the alsa-oss package:

```
# pacman -S alsa-oss   

```

Did you add your normal user to the audio group? If not, use `/usr/bin/gpasswd`. As root do:

```
# gpasswd -a *yourusername* audio

```

As ***normal, non-root*** user, invoke `/usr/bin/alsamixer`:

```
# su - *yourusername* 
**$** alsamixer

```

Unmute the Master and PCM channels by scrolling to them with cursor left/right and pressing **M**. Increase the volume levels with the cursor-up key. (70-90 Should be a safe range.) Some machines, (like the Thinkpad T61), have a **Speaker** channel which must be unmuted and adjusted as well. Leave alsamixer by pressing ESC.

#### Sound test

Ensure your speakers are properly connected, and test your sound configuration as normal user using `/usr/bin/aplay`:

```
$ aplay /usr/share/sounds/alsa/Front_Center.wav

```

You should hear a woman's voice saying, "Front, center."

#### Saving the Sound Settings

Switch back to root user and store these settings using `/usr/sbin/alsactl` :

```
# alsactl store

```

This will create the file '/etc/asound.state', saving the alsamixer settings.

Also, add the alsa *daemon* to your DAEMONS section in /etc/rc.conf to automatically restore the mixer settings at boot.

```
# nano /etc/rc.conf
DAEMONS=(syslog-ng network crond **alsa**)

```

**Note:** The alsa daemon merely restores your volume mixer levels on boot up by reading /etc/asound.state. It is separate from the alsa audio library (and kernel level API).

Expanded information available in the [ALSA](/index.php/ALSA "ALSA") wiki entry.

### Step 2: Install X

See [Xorg](/index.php/Xorg "Xorg").

### Step 3: Configure X (Optional)

**Note:** Since X11R7.2 the X.Org X Server features autoconfiguration. Therefore, it can function without an xorg.conf file in many cases. *If* the autoconfiguration *works satisfactorily* and you do not need to specify special features such as aiglx, compositing and so forth, you may forgo creating an xorg.conf file and continue below with [Input hotplugging](#B:_Input_hotplugging).

#### B: Input hotplugging

[Input hotplugging](/index.php/Xorg_input_hotplugging "Xorg input hotplugging") is supported since the 1.4 version of the X.Org X Server and enabled by default. When enabled, X will utilize hal to allow for the hotplugging and removal of human interface devices without having to restart X.

**Warning:** Starting the **X** server using input hotplugging without the **HAL** daemon installed and running may result in the inability to use the mouse and/or keyboard, and the **X** server appearing to freeze as a result. Do not start **X** until hal is installed and running.

You must decide whether you will use input hotplugging (enabled by default), or disable it. Input hotplugging is convenient for many users, especially those with mobile machines like laptops and netbooks. Other users may wish to disable it in favor of manual or more static device configuration within /etc/xorg.conf.

**Tip:** See the article on [Xorg input hotplugging](/index.php/Xorg_input_hotplugging "Xorg input hotplugging") for full details.

##### Using input hotplugging

Install HAL, dbus and the evdev input driver:

```
# pacman -S hal dbus xf86-input-evdev

```

Set the keyboard layout (if you do not use a standard US keyboard)

```
# cp /usr/share/hal/fdi/policy/10osvendor/10-keymap.fdi /etc/hal/fdi/policy/
# nano /etc/hal/fdi/policy/10-keymap.fdi

```

Edit the "input.xkb.layout" key and possibly the "input.xkb.variant" key in this file.

**Note:** The **input.xkb.layout** key may differ from the keymap code you used with the km or loadkeys command. For instance, the uk layout corresponds to the key: **gb**.

Laptop users will also need the synaptics package to allow X to configure the touchpad:

```
# pacman -S xf86-input-synaptics

```

**Tip:** For instructions on fine tuning or troubleshooting touchpad settings, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") article.

**The HAL daemon**

The hal daemon **must** be started **before** the **X** server:

```
# /etc/rc.d/hal start

```

Add the hal daemon to the DAEMONS array in /etc/rc.conf to start it at every boot.

##### Disable input hotplugging

Disabling input hotplugging will skip devices detected by hal and will use the keyboard/mouse configuration from xorg.conf:

```
# nano /etc/X11/xorg.conf

```

add the following:

```
Section "ServerFlags"
    Option "AutoAddDevices" "False"
EndSection

```

###### Set the keyboard layout if not using a standard US keyboard

Add option lines in the "InputDevice" section of the /etc/X11/xorg.conf file specifying the keyboard layout and variant:

```
Option "XkbLayout" "be"
Option "XkbVariant" ""

```

Alternative method using the setxkbmap command:

```
# setxkbmap pl 

```

(with the proper keyboard layout instead of `pl` of course) should switch your keyboard layout in x. To make this permanent, add this command to `/home/<youruser>/.xinitrc` before starting the window manager (before command like `exec startxfce4`).

#### C: Test X

First, read the warning about input hotplugging in the previous section. At this point, you should have xorg installed, with a suitable video driver and an /etc/X11/xorg.conf configuration file, (unless you chose to attempt to use **X** without it which is perfectly acceptable). If you want to test your configuration quickly, to ensure your ability to successfully start **X** from the command line, before installing a complete desktop environment, you can do so by configuring ~/.xinitrc to invoke **Xterm**. Xterm is a simple [terminal emulator](/index.php?title=Terminal_Emulator&action=edit&redlink=1 "Terminal Emulator (page does not exist)") which runs in the **X** Server environment; it is installed as part of the base xorg packages.

##### Prepare for the test by configuring ~/.xinitrc

One of the main functions of this file is to dictate what **X** Window client is invoked with the **/usr/bin/startx** and/or **/usr/bin/xinit** program *on a per-user basis*. (The **startx** script is merely a front end to the more versatile **xinit** command.) There are vast amounts of additional configurable specifications and commands that may also be added to ~/[.xinitrc](/index.php/.xinitrc ".xinitrc") as you further customize your system.

**Note:** **[.xinitrc](/index.php/.xinitrc ".xinitrc")** is a so-called 'dot' (.) file. Files in a UNIX filesystem which are preceded with a dot (.) are 'hidden', and will not show up with a regular 'ls' command, usually for the sake of keeping directories tidy. Dot files may be seen by issuing **ls -a**. The 'rc' denotes *Run Commands* and simply indicates that it is a configuration file. Since it controls how a program runs, it is (although historically incorrect) also said to stand for "Run Control".

**startx/xinit** will start the **X** server and clients. To determine the client to run, **startx/xinit** will first look to parse a [.xinitrc](/index.php/.xinitrc ".xinitrc") file in the user's home directory. In the absence of file ~/[.xinitrc](/index.php/.xinitrc ".xinitrc"), it defaults to the global xinitrc in the xinit library directory; /etc/X11/xinit/xinitrc, which defaults to using the TWM window manager. (Hence, if you invoke startx without a ~/[.xinitrc](/index.php/.xinitrc ".xinitrc") file, a TWM session will start.) Further details in the [.xinitrc](/index.php/.xinitrc ".xinitrc") wiki entry.

Switch to your ***normal, non-root*** user:

```
# su - *yourusername*

```

*   /etc/skel/ contains files and directories to provide sane defaults for newly created user accounts. The name **skel** is derived from the word **skeleton**, because the files it contains form the basic structure for users' home directories.

**Note:** This template file **[.xinitrc](/index.php/.xinitrc ".xinitrc")** is available in the /etc/skel directory when the package **xorg-xinit** is installed.

*   Sample .xinitrc provided [here](/index.php/Xinitrc#A_standard_.xinitrc "Xinitrc")

Copy the sample xinitrc file from /etc/skel/ to your home directory:

```
$ cp /etc/skel/[.xinitrc](/index.php/.xinitrc ".xinitrc") ~/

```

Edit the file:

```
$ nano ~/.xinitrc

```

and add "`exec xterm`" so that it looks like this:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#
# exec wmaker
# exec startkde
# exec icewm
# exec blackbox
# exec fluxbox
# exec openbox-session
#
exec xterm

```

**Note:** *Be sure to have only **one** uncommented **exec** line in ~/.xinitrc* for now.

Below, we shall edit this file again to specify the appropriate desktop environment/window manager of your choice.

##### Perform the test

Test your configurations by starting **X** as **normal, non-root** user, with:

```
$ startx

```

or

```
$ xinit

```

You should have an **xterm** session open up. You can test your keyboard and its layout in it. You may have to move your mouse around until it enters the xterm area before you see the mouse cursor or xterm responds to your keyboard.

If you prove a properly configured /etc/X11/xorg.conf by successfully running the test, you can be assured that your DE/WM of choice will work smoothly.

Exit Xterm with:

```
$ exit

```

**Tip:** Advanced instructions for Xorg configuration can be found in the [Xorg](/index.php/Xorg "Xorg") article.

**Note:** With Xorg 1.6 CTRL-Alt-Backspace has been deprecated and will not work to exit out of this test. A possible workaround is to switch to a different virtual console (CTRL-Alt-F2, for example) and then switch back to the console the test is running in (probably CTRL-Alt-F1). You will then be able to use CTRL-C to kill the X test. You can enable CTRL-Alt-Backspace by editing xorg.conf, as described [here](/index.php/Xorg#Ctrl-Alt-Backspace_doesn.27t_work "Xorg").

If the screen goes black, you may still attempt to switch to a different virtual console (CTRL-Alt-F2, for example), and login blindly as root, followed by <Enter>, followed by root's password followed by <Enter>.

You can attempt to kill the X server with `/usr/bin/pkill`:

```
# pkill X

```

If pkill does not work, reboot blindly with:

```
# reboot

```

or

```
# init 6

```

##### In case of errors

If you have problems starting **X**, you can look for errors in the /var/log/Xorg.0.log file, as well as in the console output of the virtual console from which **X** was started.

Also, if using /etc/X11/xorg.conf, inspect the config file:

```
# nano /etc/X11/xorg.conf

```

for the following issues:

*   The video driver may need to be specified. e.g.:

```
Section "Device"

       ...
       Driver  "savage"
       ...

EndSection

```

*   Horizontal sync and vertical refresh specs under section "Monitor" may need to be added:

```
Section "Monitor"
       Identifier   "Monitor0"
       VendorName   "Monitor Vendor"
       ModelName    "Monitor Model"
       HorizSync     30.0 - 130.0 # Safe for LCD's
       VertRefresh   50.0 - 100.0 # Safe for LCD's and most CRT's.
EndSection

```

(If these specs are unknown, consult the documentation of the computer monitor.)

*   Color depth can be specified under section "Screen":

```
Section "Screen"
       Identifier "Screen0"
       Device     "Card0"
       Monitor    "Monitor0"
       DefaultDepth 24

```

(Typically, this will be set to 24 for true color.)

*   Also add desired Modes to the "Display" subsection, at least under the Depth 24 header, e.g.:

```
 SubSection "Display"
               Viewport   0 0
               Depth     24
               Modes "1024x768" "800x600" "640x480"

```

*   Add the following section, if eye candy which requires the composite extension is desired:

```
Section "Extensions"
 	Option "Composite" "Enable"
EndSection

```

Try the config again, after modifying, by running:

```
# startx

```

or

```
# xinit

```

***Still having trouble? Detailed instructions are in the [Xorg](/index.php/Xorg "Xorg") article.***

##### Need Help?

If you are still having trouble after consulting the [Xorg](/index.php/Xorg "Xorg") article and need assistance via the Arch forums, be sure to install and use wgetpaste:

```
# pacman -S wgetpaste

```

Use wgetpaste and provide links for the following files when asking for help in your forum post:

*   ~/.xinitrc
*   /etc/X11/xorg.conf
*   /var/log/Xorg.0.log
*   /var/log/Xorg.0.log.old

Use wgetpaste like so:

```
$ wgetpaste </path/to/file>

```

Post the corresponding links given within your forum post. Be sure to provide appropriate hardware and driver information as well.

**Warning:** ***It is very important to provide detail when troubleshooting X. Please provide all pertinent information as detailed above when asking for assistance on the Arch forums.***

## Part IV: Installing and configuring a Desktop Environment

While The **X** Window System provides the basic framework for building a *graphical user interface* (GUI), a **Desktop Environment** (DE), works atop and in conjunction with **X**, to provide a completely functional and dynamic GUI. A DE typically provides a window manager, icons, applets, windows, toolbars, folders, wallpapers, a suite of applications and abilities like drag and drop. The particular functionalities and designs of each DE will uniquely affect your overall environment and experience. Therefore, choosing a DE is a very subjective and personal decision. Choose the best environment for *your* needs.

If you desire a lighter, less demanding GUI to configure manually, you may choose to simply install a **Window Manager**, or WM. A WM controls the placement and appearance of application windows in conjunction with the X Window System but does NOT include such features as panels, applets, icons, applications, etc., by default.

*   Lightweight floating WMs include: [**Openbox**](#Openbox), [**Fluxbox**](#Fluxbox), [**FVWM2**](#FVWM2), [**pekwm**](/index.php/PekWM "PekWM"), [**evilwm**](/index.php/Evilwm "Evilwm"), **Windowmaker, and TWM**.
*   If you need something completely different, try a tiling WM like [**awesome**](/index.php/Awesome "Awesome"), [**ion3**](/index.php/Ion3 "Ion3"), [**wmii**](/index.php/Wmii "Wmii"), [**dwm**](/index.php/Dwm "Dwm"), [**xmonad**](/index.php/Xmonad "Xmonad"), or [**ratpoison**](/index.php/Ratpoison "Ratpoison").

### Step 1: Install Fonts

At this point, you may wish to save time by installing visually pleasing, true type fonts, before installing a desktop environment/window manager. Dejavu and bitstream-vera are good, general-purpose font sets. You may also want to install the Microsoft font sets, which are especially popular on websites, and may be required for the proper function of Flash animations which feature text.

Install with:

```
# pacman -S ttf-ms-fonts ttf-dejavu ttf-bitstream-vera

```

Refer to [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration") for how to configure fonts.

### Step 2: ~/.xinitrc (again)

As **non-root user**, edit your /home/username/.xinitrc to specify the DE you wish to use. This will allow you to use **startx/xinit** from the shell, in the future, to open your DE/WM of choice:

```
$ nano ~/.xinitrc

```

Uncomment or add the '**exec** ..' line of the appropriate desktop environment/window manager. Some examples are below:

For the Xfce4 desktop environment:

```
 exec startxfce4 

```

For the KDE desktop environment:

```
 exec startkde

```

A **startkde** or **startxfce4** command starts the KDE or Xfce4 desktop environment. This is exactly the same as entering:

```
$ xinit /usr/bin/startxfce4

```

or

```
$ xinit /usr/bin/startkde

```

from the shell prompt. Note that such a command does not finish until you logout of the DE. Normally the shell would wait for KDE to finish, then run the next command. The "exec" prefix to this command within the ~/.xinitrc file tells the shell that this is the last command, so the shell does not need to wait to run a subsequent command.

Remember to have only one uncommented **exec** line in your `~/.xinitrc` for now.

### Step 3: Install a Desktop Environment

Continue below, installing the DE/WM of your choice.

*   [**GNOME**](#GNOME)
*   [**KDE**](#KDE)
*   [**Xfce**](#Xfce)
*   [**LXDE**](#LXDE)
*   [**Openbox**](#Openbox)
*   [**Fluxbox**](#Fluxbox)
*   [**FVWM2**](#FVWM2)
*   [**Tiling WMs**](#Tiling_WMs)

#### GNOME

##### About GNOME

The **G**NU **N**etwork **O**bject **M**odel **E**nvironment. The GNOME project provides two things: The GNOME desktop environment, an intuitive and attractive desktop for end-users, and the GNOME development platform, an extensive framework for building applications that integrate into the rest of the desktop.

##### Installation

Install the base GNOME environment with:

```
# pacman -S gnome

```

Additionally, you can install the extras:

```
# pacman -S gnome-extra

```

It's safe to choose all packages shown in the extra package.

##### Useful DAEMONS for GNOME

Recall from above that a daemon is a program that runs in the background, waiting for events to occur and offering services.

Some users prefer to use the **hal** daemon. The **hal** daemon, among other things, will assist in automating the mounting of disks, optical drives, and USB drives/thumbdrives for use in the GUI. The hal package is installed as a dependency along with GNOME, but must be invoked to become useful.

**Warning:** The FAM (File Alteration Monitor) daemon is obsolete; use [Gamin](/index.php/Gamin "Gamin") instead, if possible. Gamin is a re-implementation of the FAM specification. It is newer, more actively maintained, and simpler to utilize:
```
# pacman -S gamin

```

You may want to install a graphical login manager. For GNOME, the **gdm** daemon is a good choice.

As root:

```
# pacman -S gdm

```

Start hal:

```
# /etc/rc.d/hal start

```

Add the desired daemons to your /etc/rc.conf DAEMONS section, so they will be invoked at boot (Note that gamin is *not* to be added to the DAEMONS array):

```
# nano /etc/rc.conf

```

```
DAEMONS=(syslog-ng network crond alsa **dbus hal gdm**)

```

**Tip:** If you prefer to log into the console and manually start X, exclude the gdm daemon.

**Note:** HAL relies on and will automatically start dbus. However, some users have reported a failure with networkmanager unless dbus is implicitly specified in the DAEMONS array. When adding dbus to the array, ensure it directly precedes HAL.

Next, edit your /etc/gdm/custom.conf and in the **[servers]** section add:

```
0=Standard vt7

```

As normal user, start X:

```
$ startx

```

or

```
$ xinit

```

If ~/.xinitrc is not configured for GNOME, you may always start it with **xinit**, followed by the path to GNOME:

```
$ xinit /usr/bin/gnome-session

```

**Tip:** Advanced instructions for installing and configuring GNOME can be found in the [GNOME](/index.php/GNOME "GNOME") article.

Congratulations! Welcome to your GNOME desktop environment on your new Arch Linux system. You may wish to continue by viewing **[General recommendations](/index.php/General_recommendations "General recommendations")**, or the rest of the information below.

##### Eye Candy

By default, GNOME does not come with many themes and icons. You may wish to install some more attractive artwork for GNOME:

A nice gtk (gui widget) theme engine (includes themes) is the murrine engine. Install with:

```
# pacman -S gtk-engine-murrine

```

Optional for more themes:

```
# pacman -S murrine-themes-collection 

```

Once it has been installed, select it with System -> Preferences -> Appearance -> Theme tab.

The Arch Linux repositories also have a few more nice themes and engines. Install the following to see for yourself:

```
# pacman -S gtk-engines gtk-aurora-engine gtk-candido-engine gtk-rezlooks-engine

```

You can find many more themes, icons, and wallpapers at [GNOME-Look](http://www.gnome-look.org).

#### KDE

##### About KDE

The **K** **D**esktop **E**nvironment. KDE is a powerful Free Software graphical desktop environment for GNU/Linux and <tt>UNIX</tt> workstations. It combines ease of use, contemporary functionality, and outstanding graphical design with the technological superiority of <tt>UNIX</tt>-like operating systems.

##### Installation

Choose one of the following, then continue below with **[Useful KDE DAEMONS](#Useful_KDE_DAEMONS)**:

1\. The package **kde** is the official and complete vanilla KDE 4.x residing under the Arch [extra] repo.

Install base kde:

```
# pacman -S kdebase-workspace

```

Install the whole Desktop Environment:

```
# pacman -S kde

```

*or*

```
# pacman -S kde-meta

```

**Note:** Learn about the difference between **kde** and **kde-meta** packages in the [KDE Packages](/index.php/KDE_Packages "KDE Packages") article.

2\. Alternatively, another KDE project exists called **KDEmod**, part of the Chakra distribution. It is an Arch Linux (and spinoff) exclusive, community-driven package set designed for modularity and offers a choice between KDE 3.5.10 or 4.x.x. KDEmod can be installed with pacman, after adding the proper repositories to /etc/pacman.conf. The project website, including complete installation instructions, can be found at [http://www.chakra-project.org/](http://www.chakra-project.org/).

[Gamin](/index.php/Gamin "Gamin"), an extension of the file alteration monitor (fam) project, is more actively developed than **fam**, and will be useful for reflecting real-time changes in the filesystem.

Install with:

```
# pacman -S gamin

```

##### Useful KDE DAEMONS

Recall from above that a daemon is a program that runs in the background, waiting for events to occur and offering services.

KDE will require the **hal** (**H**ardware **A**bstraction **L**ayer) daemon for optimal functionality. The hal daemon, among other things, will facilitate the automatic mounting of disks, optical drives, and USB drives/thumbdrives for use in the GUI. The hal package is installed when you install xorg-server, but must be invoked to become useful.

The **kdm** daemon is the **K** **D**isplay **M**anager, which provides a **graphical login**, if desired.

* * *

Start hal:

```
# /etc/rc.d/hal start

```

**Note:** HAL relies on and will automatically start dbus. However, some users have reported a failure with NetworkManager unless dbus is implicitly specified in the DAEMONS array. When adding dbus to the array, ensure it directly precedes HAL.

Edit your DAEMONS array in /etc/rc.conf:

```
# nano /etc/rc.conf

```

Add **dbus** and **hal** to your DAEMONS array, to invoke it on boot. If you prefer a graphical login, add **kdm** as well:

```
DAEMONS=(syslog-ng **dbus hal** networkmanager alsa crond **kdm**)

```

**Note:** If you installed KDEmod3 instead of normal KDE, use kdm3 instead of kdm.

*   This method will start the system at runlevel 3, (/etc/inittab default, multiuser mode), and then start KDM as a daemon.

*   Some users prefer an alternative method of starting a display manager like KDM on boot by utilizing the /etc/inittab method and starting the system at runlevel 5\. See [Display manager](/index.php/Display_manager "Display manager") for more.

*   If you prefer to log into the **console** at runlevel 3, and manually start X, leave out kdm, or comment it out with a bang, ( ! ).

Now try starting your X Server as normal user:

```
$ startx

```

or

```
$ xinit

```

**Tip:** Advanced instructions for installing and configuring KDE can be found in the [KDE](/index.php/KDE "KDE") article.

Congratulations! Welcome to your KDE desktop environment on your new Arch Linux system! You may wish to continue by viewing **[General recommendations](/index.php/General_recommendations "General recommendations")**, or the rest of the information below.

##### Eye candy

Arch KDE themes can be installed:

```
# pacman -S archlinux-themes-kde

```

#### Xfce

##### אודות Xfce

Xfce היא סביבת שולחן עבודה בממשק משתמש גרפי בקוד פתוח עבור מערכות הפעלה דמויות-יוניקס כגון לינוקס וסולאריס. Xfce נודעת בשל שימושה הנמוך במשאבי מערכת וכתוצאה מכך מהירות העבודה הגבוהה שלה, גם על מערכות מיושנות. כמו סביבות עבודה אחרות, גם Xfce מבוססות על מספר ספריות בסיסיות ואסופת תוכנות המשתמשות בהן. בין התוכנות אפשר למצוא את מנהל הקבצים Thunar, סרגל לוח, מנהל חלונות, לוח שנה עם פגישות ומנהל שולחן עבודה. Xfce מתורגמת ברובה לעברית, ותומכת באופן מלא בעברית.

##### התקנה

התקנת Xfce:

```
# pacman -S xfce4 

```

כמו כן, מומלץ להתקין ערכות נושא ותוספות:

```
# pacman -S xfce4-goodies gtk2-themes-collection

```

Note: **xfce4-xfapplet-plugin** (פלאגין המאפשר להשתמש בישומונים של GNOME בפאנל Xfce4) היא חלק מקבוצת **xfce4-goodies** והיא תלויה ב**gnome-panel**, אשר תלויה ב**gnome-desktop**. ייתכן שתרצה לקחת את זה בחשבון לפני ההתקנה, כיוון שמספר חבילות התוספת גדול.

כדי להתקין חבילת אייקונים בסיסית לתפריט:

```
# pacman -S gnome-icon-theme

```

אם ברצונך שיוצגו טיפים וטריקים בהתחברות, התקן את חבילת **fortune-mod**:

```
# pacman -S fortune-mod

```

##### Daemons שימושיים

Recall from above that a daemon is a program that runs in the background, waiting for events to occur and offering services. Some Xfce users prefer to use the **hal** daemon. The hal daemon, among other things, will automate the mounting of disks, optical drives, and USB drives/thumbdrives for use in the GUI. The hal package is installed when you install Xfce, but must be invoked to become useful.

**Note:** **fam** (מוניטור התראות אחסון) כבר מיושן. התקן את חבילת [gamin](/index.php/Gamin "Gamin") אבל אל תוסיף את gamin אל rc.conf. gamin מוגדרת אוטומטית לרוץ ברקע.

```
# pacman -S gamin

```

הרצת hal daemon:

```
# /etc/rc.d/hal start

```

**Note:** HAL relies on and will automatically start dbus. However, some users have reported a failure with NetworkManager unless dbus is implicitly specified in the DAEMONS array. When adding dbus to the array, ensure it directly precedes HAL.

Edit your DAEMONS array in /etc/rc.conf:

```
# nano /etc/rc.conf

```

Add **hal** to your DAEMONS array, to invoke at boot.

**Tip:** Advanced instructions for installing and configuring Xfce can be found in the [Xfce](/index.php/Xfce "Xfce") article.

If you wish to install one, see [Display manager](/index.php/Display_manager "Display manager"). Otherwise you can login in via the console and run:

```
 $ startxfce4

```

מזל טוב! ברוכים הבאים לסביבת שולחן העבודה Xfce על מערכת Arch Linux החדשה שלך! ייתכן שתרצה להמשיך בקריאה ב**[General recommendations](/index.php/General_recommendations "General recommendations")**, or the rest of the information below.

#### LXDE

##### About LXDE

LXDE, (for *L*ightweight *X*11 *D*esktop *E*nvironment), is a new project focused on providing a modern desktop environment which aims to be lightweight, fast, intuitive and functional while keeping system resource usage low. LXDE is quite different from other desktop environments, since each component of LXDE is a discrete and independent application, and each can be easily substituted by other programs. This modular design eliminates all unnecessary dependencies and provides more flexibility. Details and screenshots available at: [http://lxde.org/](http://lxde.org/)

LXDE provides:

1.  The OpenBox windowmanager
2.  PCManFM File manager
3.  LXpanel system panel
4.  LXSession session manager
5.  LXAppearance GTK+ theme switcher
6.  GPicView image viewer
7.  Leafpad simple text editor
8.  XArchiver: Lightweight, fast, and desktop-independent gtk+-based file archiver
9.  LXNM (still under development): Lightweight network manager for LXDE supporting wireless connections

These lightweight and versatile tools combine for quick setup, modularity and simplicity.

##### Installation

Install LXDE with:

```
# pacman -S lxde gamin openbox

```

[Gamin](/index.php/Gamin "Gamin") is a file and directory monitoring tool designed to be a subset of the [FAM](/index.php/FAM "FAM"). It runs on demand for programs that have support for it so does not require a daemon like fam does.

Add:

```
exec startlxde

```

to your ~/.xinitrc and start with *startx* or *xinit*

**Tip:** Further information available at the [LXDE](/index.php/LXDE "LXDE") wiki article.

Congratulations! Welcome to your LXDE desktop environment on your new Arch Linux system! You may wish to continue by viewing **[General recommendations](/index.php/General_recommendations "General recommendations")**, or the rest of the information below.

#### *box

##### Fluxbox

Fluxbox is yet another windowmanager for X. It's based on the Blackbox 0.61.1 code. Fluxbox looks like blackbox and handles styles, colors, window placement and similar things exactly like blackbox (100% theme/style compability).

Install Fluxbox using

```
# pacman -S fluxbox fluxconf

```

If you use gdm/kdm a new fluxbox session will be automatically added. Otherwise, you should modify your user's .xinitrc and add this to it:

```
exec startfluxbox 

```

More information is available in the [Fluxbox](/index.php/Fluxbox "Fluxbox") article.

##### Openbox

Openbox is a standards compliant, fast, light-weight, extensible window manager.

Openbox works with your applications, and makes your desktop easier to manage. This is because the approach to its development was the opposite of what seems to be the general case for window managers. Openbox was written first to comply with standards and to work properly. Only when that was in place did the team turn to the visual interface.

Openbox is fully functional as a stand-alone working environment, or can be used as a drop-in replacement for the default window manager in the GNOME or KDE desktop environments.

Install openbox using

```
# pacman -S openbox

```

Additional configuration tools are also available, if desired:

```
# pacman -S obconf obmenu

```

Once openbox is installed you will get a message to move menu.xml & rc.xml to ~/.config/openbox/ in your home directory:

```
# su - *yourusername*
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox/
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox/

```

**rc.xml** is the main configuration file for OpenBox. It may be manually edited, (or you can use OBconf). **menu.xml** configures the right-click menu.

You may log into OpenBox via graphical login using KDM/GDM, or from the shell using **startx**, in which case you will need to edit your ~/.xinitrc (as non-root user) and add the following:

```
exec openbox-session

```

You may also start OpenBox from the shell using **xinit**:

```
$ xinit /usr/bin/openbox-session

```

*   Openbox may also be used as the window manager for GNOME, KDE, and Xfce.

For KDM there is nothing left to do; openbox is listed in the sessions menu in KDM.

Some useful, lightweight programs for OpenBox are:

*   PyPanel, Tint2, or LXpanel if you want a panel
*   feh if you want to set the background
*   ROX if you want a simple file manager (also provides simple icons)
*   PcmanFM a lightweight but versatile file manager (also provides desktop icon functionality)
*   iDesk (available in [AUR](/index.php/AUR "AUR")) for providing desktop icons
*   Graveman for burning CD's or DVD's

**Tip:** More information is available in the [Openbox](/index.php/Openbox "Openbox") article.

#### FVWM2

FVWM (F Virtual Window Manager) is an extremely powerful ICCCM-compliant multiple virtual desktop window manager for the X Window system. Development is active, and support is excellent.

Install fvwm2 with

```
# pacman -S fvwm 

```

It will install the official version of the WM. However, if you want/need to use some more features than it provides, you can install the patched version from the [AUR](/index.php/AUR "AUR") (see package [fvwm-patched](https://aur.archlinux.org/packages/fvwm-patched/)) or from archlinuxfr (see [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")) using pacman:

```
# pacman -S fvwm-patched

```

fvwm will automatically be listed in kdm/gdm in the sessions menu. Otherwise, add

```
exec fvwm2 

```

to your user's .xinitrc.

When you start [FVWM2](/index.php/FVWM2 "FVWM2"), you will get into the blank configuration. However, when you left-click on the desktop, you will be able to select to configure FVWM. chose wanted modules and you are ready to go. Check out the configs in the [http://www.box-look.org](http://www.box-look.org). One should also consider checking FVWM forums at [http://fvwmforums.org](http://fvwmforums.org)

[SLiM](/index.php/SLiM "SLiM") is a very good login manager, that does not have many dependencies and acts well with FVWM. Common Applications are similar to those suggested for [Openbox](/index.php/Openbox "Openbox") or [Fluxbox](/index.php/Fluxbox "Fluxbox").

#### Tiling WMs

In addition to floating window managers, there are also several tiling window managers available. This type of window manager may be described as making more extensive usage of the keyboard, less (or no) reliance on the mouse, and window control via predefined layouts. Windows are usually resized and positioned so that they would not overlap, potentially maximizing space.

Here are some of the more popular tiling WMs, in no particular order:

*   [Awesome](/index.php/Awesome "Awesome")
*   [dwm](/index.php/Dwm "Dwm")
*   [wmii](/index.php/Wmii "Wmii")
*   [Xmonad](/index.php/Xmonad "Xmonad")

More information can be found in the [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") article.

## מולטימדיה

### קודקים, פלאגינים וג'אווה

קודקי מולטימדיה, פלאגינים וג'אווה ניתנים להתקנה ע"י:

```
pacman -S mplayer gecko-mediaplayer xine-lib xine-ui libdvdread libdvdcss alsa-oss flashplugin jre

```

לפני ההתקנה וודא את חוקיות השימוש בlibdvdcss במדינתך.

# נספח

לקבלת רשימה של [אפליקציות נפוצות](/index.php?title=%D7%90%D7%A4%D7%9C%D7%99%D7%A7%D7%A6%D7%99%D7%95%D7%AA_%D7%A0%D7%A4%D7%95%D7%A6%D7%95%D7%AA&action=edit&redlink=1 "אפליקציות נפוצות (page does not exist)") ו[אפליקציות קלות](/index.php?title=%D7%90%D7%A4%D7%9C%D7%99%D7%A7%D7%A6%D7%99%D7%95%D7%AA_%D7%A7%D7%9C%D7%95%D7%AA&action=edit&redlink=1 "אפליקציות קלות (page does not exist)"), עיינו במאמרים המיוחסים להם. ראו גם [המצלות כלליות](/index.php?title=%D7%94%D7%9E%D7%A6%D7%9C%D7%95%D7%AA_%D7%9B%D7%9C%D7%9C%D7%99%D7%95%D7%AA&action=edit&redlink=1 "המצלות כלליות (page does not exist)") עבור טיפים לאחר ההתקנה.