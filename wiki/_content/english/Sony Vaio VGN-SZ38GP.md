## Contents

*   [1 Switch Mode](#Switch_Mode)
*   [2 Screen Brightness](#Screen_Brightness)
*   [3 Wifi](#Wifi)
*   [4 Fan Speed](#Fan_Speed)
*   [5 Power Saving](#Power_Saving)

## Switch Mode

*   When you finished your installation, download the [latest nvidia driver](http://www.nvidia.com/object/linux-display-ia32-256.44-driver.html)
*   Backup the files : libGL.so.1.2 and libglx.so that you can find respectively under the folder /usr/lib/ and /usr/lib/xorg/modules/extensions/

*   **You need to copy them in a different location because when you will install the nvidia driver it will automatically remove them.**
*   Backup your xorg.conf file that you can find under /etc/X11/

*I choose to put the lib file under the folder /opt/gpu/intel/lib and the xorg.conf as /etc/X11/xorg.intel*

*   Reboot the computer in Speed Mode.

If you are running X you need to kill it. First go to a command prompt using Ctrl+Alt+F1-6 and after you have login run the command: killall X. You also need to kill kdm (killall kdm) or other login manager that you may have since it will make X respawn.

Then you have to change the runlevel by using the command: init 3.

*   Run the script provided by nvidia to install the driver, it will automatically generate a new xorg.conf file with the correct setting for you graphic card.
*   Backup the files libGL.so.<Nvidia Version> and libglx.so.<Nvidia Version> that you can respectively find in /usr/lib and /usr/lib/xorg/modules/extensions
*   Backup xorg.conf file generated by the nvidia driver

*I choose to put the lib file under the folder /opt/gpu/nv/lib and the xorg.conf as /etc/X11/xorg.nv*

*   Now use the following script :

```
#!/bin/bash
VIDEO=`lspci | grep -c nVidia`
NVIDIA_VERSION="256.35"
if [ "$VIDEO" = 1 ]; then
cp -f /etc/X11/xorg.conf.nv /etc/X11/xorg.conf
ln -sf /opt/gpu/nv/libGL.so.$NVIDIA_VERSION /usr/lib/libGL.so.1
ln -sf /opt/gpu/nv/libglx.so.$NVIDIA_VERSION /usr/lib/xorg/modules/extensions/libglx.so
echo "Speed Mode"
else
cp -f /etc/X11/xorg.conf.intel /etc/X11/xorg.conf
ln -sf /opt/gpu/intel/libGL.so.1.2 /usr/lib/libGL.so.1
ln -sf /opt/gpu/intel/libglx.xorg /usr/lib/xorg/modules/extensions/libglx.so
echo "Stamina Mode"
fi

```

*   Make you script executable using the following command : chmod +x <your_script_name>
*   Add your script path to the /etc/rc.local file.

## Screen Brightness

For each graphic card there is a specific program that handle it, for the Intel card it is xbacklight and for Nvidia card it is smartdimmer.

xbacklight is installed by default with the Intel driver so you have nothing to do, but for Nvidia you will have to install [smartdimmer](https://aur.archlinux.org/packages/smartdimmer/) from the [AUR](/index.php/AUR "AUR"). Know we will have to configure acpi to configure the fn keys.

*   Go to /etc/acpi/events and create two files sonybright-down sonybright-up.
*   in the first one add the following line :

```
# /etc/acpi/events/sony-brightness-down
event=sony/hotkey SPIC 00000001 00000010
action=/etc/acpi/actions/sonybright.sh down

```

*   in the second one add the following line :

```
# /etc/acpi/events/sony-brightness-up
event=sony/hotkey SPIC 00000001 00000011
action=/etc/acpi/actions/sonybright.sh up

```

*   Now you will have to create two script file for handling the brightness for each graphic card.
*   Create a file named intelbright.sh and put the following line inside :

```
#!/bin/bash
if [ "x$1" = "xdown" ]; then
xbacklight -dec 10;
elif [ "x$1" = "xup" ]; then
xbacklight -inc 20;
fi

```

**If the previous script does not work, you can use the alternative one below :**

```
#!/bin/bash
val=$(cat /sys/class/backlight/sony/actual_brightness)
if [ "x$1" = "xdown" ]; then
((val--));
elif [ "x$1" = "xup" ]; then
((val++));
fi
echo $val > /sys/class/backlight/sony/brightness

```

*   Create a file named nvlbright.sh and put the following line inside :

```
#!/bin/bash
if [ "x$1" = "xdown" ]; then
smartdimmer -d;
elif [ "x$1" = "xup" ]; then
smartdimmer -i;
fi

```

*   You can now add the following line to the script that we used to switch graphic card :

```
#!/bin/bash
VIDEO=`lspci | grep -c nVidia`
NVIDIA_VERSION="256.35"
if [ "$VIDEO" = 1 ]; then
cp -f /etc/X11/xorg.conf.nv /etc/X11/xorg.conf
**cp -f /opt/gpu/bright/nvbright.sh /etc/acpi/actions/sonybright.sh**
ln -sf /opt/gpu/nv/libGL.so.$NVIDIA_VERSION /usr/lib/libGL.so.1
ln -sf /opt/gpu/nv/libglx.so.$NVIDIA_VERSION /usr/lib/xorg/modules/extensions/libglx.so
echo "Speed Mode"
else
cp -f /etc/X11/xorg.conf.intel /etc/X11/xorg.conf
**cp -f /opt/gpu/bright/intelbright.sh /etc/acpi/actions/sonybright.sh**
ln -sf /opt/gpu/intel/libGL.so.1.2 /usr/lib/libGL.so.1
ln -sf /opt/gpu/intel/libglx.xorg /usr/lib/xorg/modules/extensions/libglx.so
echo "Stamina Mode"
fi

```

## Wifi

If you have your wireless switch that is not automatically activating your wireless if you do not turn it on before turn on your computer. You can fix the problem by adding the following line to /etc/modprobe.d/modprobe.conf

```
options sony-laptop mask=0xffffdfff

```

## Fan Speed

You can control the fan speed by using the **vaiofand** daemon that you can find on this address : [http://vaio-utils.org/fan/](http://vaio-utils.org/fan/) There is also a PKGBUILD available in [AUR](https://aur.archlinux.org/packages.php?ID=38826).

## Power Saving

You can automatically turn of some device like the bluetooth, the firewire port, the cd/dvd drive or the audio card by using the **vaiopower** daemon that you can find on this address : [http://vaio-utils.org/power/](http://vaio-utils.org/power/) There is also a PKGBUILD available in [AUR](https://aur.archlinux.org/packages/vaiopower/).