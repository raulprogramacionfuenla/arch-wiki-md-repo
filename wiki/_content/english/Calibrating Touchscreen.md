To use multiple displays (some of which are touchscreens), you need to tell Xorg the mapping between the touch surface and the screen. This can be done using `xinput` to set the touchscreen's coordinate transformation matrix, as described [in the X.Org Wiki](http://www.x.org/wiki/XInputCoordinateTransformationMatrixUsage).

This is a guide to do that, the old-fashioned way, in cases when xrandr does not know about your separate screens because they have been merged into one (e.g., when using TwinView). Everyone else, please go to [Touchscreen](/index.php/Touchscreen "Touchscreen") to do it the easy way.

You will need to run the `xinput` command every time you attach the monitor or log in. Or course, you can add the command to your session-autostart. You can also use [Udev](/index.php/Udev "Udev") to automate this.

## Contents

*   [1 Using nVidia's TwinView](#Using_nVidia.27s_TwinView)
    *   [1.1 Get to know your system](#Get_to_know_your_system)
        *   [1.1.1 Your screen](#Your_screen)
        *   [1.1.2 Your touch device](#Your_touch_device)
        *   [1.1.3 Touch area](#Touch_area)
    *   [1.2 Calculate the Coordinate Transformation Matrix](#Calculate_the_Coordinate_Transformation_Matrix)
    *   [1.3 Apply the Matrix](#Apply_the_Matrix)
    *   [1.4 Do it automatically via a udev rule](#Do_it_automatically_via_a_udev_rule)
*   [2 Troubleshooting](#Troubleshooting)
*   [3 See also](#See_also)

## Using nVidia's TwinView

### Get to know your system

#### Your screen

Using TwinView, X will see all your Screens as one big screen. You can get your total height and width by executing

```
$ xrandr

```

. You should see a line like this:

```
 3600x1230      50.0* 

```

what means, your total width is 3600 and your total height is 1230.

#### Your touch device

Your next job is to get your device's name. Execute

```
$ xinput list

```

and find it by it's name. E.g. if the line can look like this

```
⎜   ↳ Acer T230H                              	id=24	[slave  pointer  (2)]

```

your device name is

```
Acer T230H

```

Execute

```
xinput list-props "Device Name"

```

and make sure there is a property called

```
Coordinate Transformation Matrix

```

(If not, you may probably selected the wrong device)

#### Touch area

You need to shrink your touch area into a rectangle which is smaller than the total screen. This means, you have to know four values:

*   Height of touch area
*   Width of touch area
*   horizontal offset (x offset) (amount of pixels between the left edge of your total screen and the left edge of your touch area)
*   vertical offset (y offset) (amount of pixels between the top edge of your total screen and the top edge of your touch area)

### Calculate the Coordinate Transformation Matrix

Now, calculate these as accurate as possible:

*   c0 = touch_area_width / total_width
*   c2 = touch_area_height / total_height
*   c1 = touch_area_x_offset / total_width
*   c3 = touch_area_y_offset / total_height

The matrix is

```
[ c0 0  c1 ]
[ 0  c2 c3 ]
[ 0  0  1  ]

```

which is represented as a row-by-row array:

```
c0 0 c1 0 c2 c3 0 0 1

```

### Apply the Matrix

Execute

```
xinput set-prop "Device Name" --type=float "Coordinate Transformation Matrix" c0 0 c1 0 c2 c3 0 0 1

```

e.g.

```
xinput set-prop "Acer T230H" --type=float "Coordinate Transformation Matrix" 0.533333333 0 0 0 0.87804878 0.12195122 0 0 1

```

to calibrate your touchscreen device. Now, it should work properly.

### Do it automatically via a udev rule

Create a file something like /etc/udev/rules.d/99-acer-touch.rules with contents like this:

```
ENV{ID_VENDOR_ID}=="2149",ENV{ID_MODEL_ID}=="2703",ENV{WL_OUTPUT}="DVI1",ENV{LIBINPUT_CALIBRATION_MATRIX}="1 0 0  0 1 0"

```

Substitute your own touchscreen's vendor ID, model ID, the xrandr output name, and the calibration matrix that you calculated above. This is based on the assumption that you are using the libinput driver for your touchscreen.

## Troubleshooting

If, after following these instructions, multiple clicks occur in different places when you touch the screen, you will need to build the [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) package using the [ABS](/index.php/ABS "ABS"), applying [this patch](http://patchwork.freedesktop.org/patch/5024/) before you build the package. (This patch fails on the current xorg source, but the bug is present on at least 1 system.)

## See also

[Calibrate Translation Matrix Documentation in the X.Org Wiki](http://www.x.org/wiki/XInputCoordinateTransformationMatrixUsage)