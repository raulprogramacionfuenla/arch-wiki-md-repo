Related articles

*   [LIRC](/index.php/LIRC "LIRC")

Step-by-step setup guide for USB (MCE [Media Center Edition]) IR receiver with universal remote control

## LIRC quick start guide

**This is a quick-start guide only.** Please refer to man pages of the commands and files used and online documentation for in-depth help.

### Prerequisites

*   Get a USB IR receiver, preferably an MCE model which is almost always supported out-of-the-box
*   Re-purpose an old universal remote control you have lying around the house

### Installation and verification

*   [Install](/index.php/Install "Install") the [lirc](https://www.archlinux.org/packages/extra/x86_64/lirc/) package
*   Plug in the USB IR receiver
*   Make sure there are fully charged batteries in your remote control
*   Get some kind of output/response from the remote using `mode2`:

```
   $ sudo mode2

```

Point the remote control at the IR receiver and press some buttons. This will attempt to autodetect the correct input device using the default "devinput" driver. However, this might not work without manual configuration of protocols.

*   If no button presses are detected for most keys, change IR protocols

If you get no response to the remote control buttons you want to use, you likely need to enable different protocols:

```
   $ sudo ir-keytable -p <protocol> -p <protocol> ...

```

Look at the output of `ir-keytable` (as well as `cat /sys/class/rc/rc0/protocols`). NOTE: When you have problems, `sudo ir-keytable -p all` is your friend!

*   If no button presses are detected for most keys, try different universal remote control device modes

You may also need to try different universal remote control device modes (TV, DVD, Audio, etc., buttons) in order to detect button presses when you're getting started. (You could possibly reprogram the universal remote's modes, but that would likely be a long trial-and-error process to find a setting that works.)

*   After reconfiguring IR protocols and remote control device mode, retest:

```
   $ sudo mode2

```

Point the remote control at the IR receiver and press some buttons. If button presses for most keys are not detected repeat the prior two steps until they are (or just use `sudo ir-keytable -p all`).

### Setup and testing

*   If you have narrowed down what protocols you need to support for your remote control, set them:

```
   $ sudo ir-keytable -p sony -p rc-5

```

Otherwise, you can just use all protocols:

```
   $ sudo ir-keytable -p all

```

*   Determine the correct device for your IR receiver. Use either the default "devinput" driver or the older "default" driver:

```
   $ mode2 --driver devinput --list-devices
   $ mode2 --driver default --list-devices
   $ ir-keytable

```

*   Use the device found for your USB IR receiver, e.g., /dev/input/event11:

```
   $ sudo mode2 --driver devinput --device /dev/input/event11

```

or just try:

```
   $ sudo mode2 --driver devinput --device auto

```

See if button presses are detected.

*   If required, edit lirc_options.conf, e.g., if you're using the driver "default" instead of "devinput":

```
   $ sudo vi /etc/lirc/lirc_options.conf

```

*   Test your remote to see if scancodes are printed:

```
   $ sudo ir-keytable -t

```

See if button presses are detected.

*   Create a modified systemd lircd.service file which loads the correct protocols:

```
   $ sudo cp /usr/lib/systemd/system/lircd.service /etc/systemd/system/
   $ sudo vi /etc/systemd/system/lircd.service

```

At the end of the `[Service]` section add the following line:

 `/etc/systemd/system/lircd.service` 
```
[Service]
...
ExecStartPost=/usr/bin/ir-keytable -p <protocol> -p <protocol>
```

where each "<protocol>" string is replaced by the protocol(s) you need (or just use `/usr/bin/ir-keytable -p all`).

*   Start the lirc daemon so you can record keypresses in order to write an lircd configuration file for your remote control:

```
   $ sudo systemctl start lircd

```

*   Use irrecord to record keypress scancodes

Run:

```
   $ sudo irrecord

```

to save/record the keystrokes to be used for your application. Follow `irrecord`'s instructions.

*   Install the recorded lircd configuration file:

```
   $ sudo mv device_name.lircd.conf /etc/lirc/lircd.conf.d/
   $ sudo chown root:root /etc/lirc/lircd.conf.d/device_name.lircd.conf

```

*   Move devinput.lircd.conf to devinput.lircd.dist to disable it, because you're not using an IR keyboard and/or mouse, just the IR receiver:

```
   $ sudo mv /etc/lirc/lircd.conf.d/devinput.lircd.conf /etc/lirc/lircd.conf.d/devinput.lircd.dist

```

*   Restart the lirc daemon so you use the newly created lircd.conf file:

```
   $ sudo systemctl restart lircd

```

*   Test to make sure the keys you recorded are correctly detected, that is, the correct key symbol is output for each button you press:

```
   $ irw

```

See if the correct key symbols are reported, and if repeated signals are properly rejected.

### Troubleshooting

*   Keypresses aren't detected

Repeat sections [#Installation and verification](#Installation_and_verification) then [#Setup and testing](#Setup_and_testing) above.

*   Repeated keypress events

If you're having keypress repeating problems (each button press is echoed multiple times), examine the output of `irw`. The second column value is the repeat count. This will increment when repeated signals are detected. Each decoded button press with its count reset to "00" is reported as a separate button press event by lircd.

To fix this problem, generally the "gap" parameter sampled by `irrecord` in the device_name.lircd.conf file should be adjusted, often to a much larger value (e.g., from 44968 up to 113975).

After editing/adjusting any lircd configuration file, be sure to restart lircd (as shown above).

### Final configuration

*   Write an lircrc file for your end user application

This file is used by all client programs built with lirc support that attach to lircd to read IR control events. Edit ~/.lircrc to issue commands to the program to be controlled. Test this configuration by running:

```
   $ ircat prog

```

to see if the correct "config" strings for program "prog" are being output when you press all the buttons you wish to use. If ~/.lircrc isn't read by your application or just doesn't work, an alternate default location is ~/.config/lircrc.

### Final testing

*   Test!

Finally, run your end user application and test remote control button presses to control it. If it works, you're done! If not, review and repeat the above sections as necessary to get each configuration step working before proceeding to the next step or section.