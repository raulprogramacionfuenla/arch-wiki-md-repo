See [PulseAudio](/index.php/PulseAudio "PulseAudio") for the main article.

## Contents

*   [1 Volume](#Volume)
    *   [1.1 Auto-Mute Mode](#Auto-Mute_Mode)
    *   [1.2 Muted audio device](#Muted_audio_device)
    *   [1.3 Output stuck muted while Master is toggled](#Output_stuck_muted_while_Master_is_toggled)
    *   [1.4 Muted application](#Muted_application)
    *   [1.5 Volume adjustment does not work properly](#Volume_adjustment_does_not_work_properly)
    *   [1.6 Per-application volumes change when the Master volume is adjusted](#Per-application_volumes_change_when_the_Master_volume_is_adjusted)
    *   [1.7 Volume gets louder every time a new application is started](#Volume_gets_louder_every_time_a_new_application_is_started)
    *   [1.8 Sound output is only mono on M-Audio Audiophile 2496 sound card](#Sound_output_is_only_mono_on_M-Audio_Audiophile_2496_sound_card)
    *   [1.9 No sound below a volume cutoff](#No_sound_below_a_volume_cutoff)
    *   [1.10 Low volume for internal microphone](#Low_volume_for_internal_microphone)
    *   [1.11 Clients alter master output volume (a.k.a. volume jumps to 100% after running application)](#Clients_alter_master_output_volume_.28a.k.a._volume_jumps_to_100.25_after_running_application.29)
    *   [1.12 No sound after resume from suspend](#No_sound_after_resume_from_suspend)
    *   [1.13 ALSA channels mute when headphones are plugged/unplugged improperly](#ALSA_channels_mute_when_headphones_are_plugged.2Funplugged_improperly)
*   [2 Microphone](#Microphone)
    *   [2.1 Microphone not detected by PulseAudio](#Microphone_not_detected_by_PulseAudio)
    *   [2.2 PulseAudio uses wrong microphone](#PulseAudio_uses_wrong_microphone)
    *   [2.3 No microphone on ThinkPad T400/T500/T420](#No_microphone_on_ThinkPad_T400.2FT500.2FT420)
    *   [2.4 No microphone input on Acer Aspire One](#No_microphone_input_on_Acer_Aspire_One)
    *   [2.5 Static noise in microphone recording](#Static_noise_in_microphone_recording)
        *   [2.5.1 Determine sound cards in the system (1/5)](#Determine_sound_cards_in_the_system_.281.2F5.29)
        *   [2.5.2 Determine sampling rate of the sound card (2/5)](#Determine_sampling_rate_of_the_sound_card_.282.2F5.29)
        *   [2.5.3 Setting the sound card's sampling rate into PulseAudio configuration (3/5)](#Setting_the_sound_card.27s_sampling_rate_into_PulseAudio_configuration_.283.2F5.29)
        *   [2.5.4 Restart PulseAudio to apply the new settings (4/5)](#Restart_PulseAudio_to_apply_the_new_settings_.284.2F5.29)
        *   [2.5.5 Finally check by recording and playing it back (5/5)](#Finally_check_by_recording_and_playing_it_back_.285.2F5.29)
    *   [2.6 No microphone on Steam or Skype with enable-remixing = no](#No_microphone_on_Steam_or_Skype_with_enable-remixing_.3D_no)
    *   [2.7 Microphone distorted due to automatic adjustment](#Microphone_distorted_due_to_automatic_adjustment)
*   [3 Audio quality](#Audio_quality)
    *   [3.1 Enable Echo/Noise-Cancelation](#Enable_Echo.2FNoise-Cancelation)
    *   [3.2 Glitches, skips or crackling](#Glitches.2C_skips_or_crackling)
    *   [3.3 Setting the default fragment number and buffer size in PulseAudio](#Setting_the_default_fragment_number_and_buffer_size_in_PulseAudio)
        *   [3.3.1 Finding out your audio device parameters (1/4)](#Finding_out_your_audio_device_parameters_.281.2F4.29)
        *   [3.3.2 Calculate your fragment size in msecs and number of fragments (2/4)](#Calculate_your_fragment_size_in_msecs_and_number_of_fragments_.282.2F4.29)
        *   [3.3.3 Modify PulseAudio's configuration file (3/4)](#Modify_PulseAudio.27s_configuration_file_.283.2F4.29)
        *   [3.3.4 Restart the PulseAudio daemon (4/4)](#Restart_the_PulseAudio_daemon_.284.2F4.29)
    *   [3.4 Choppy sound with analog surround sound setup](#Choppy_sound_with_analog_surround_sound_setup)
    *   [3.5 Laggy sound](#Laggy_sound)
    *   [3.6 Choppy/distorted sound](#Choppy.2Fdistorted_sound)
*   [4 Hardware and Cards](#Hardware_and_Cards)
    *   [4.1 No HDMI sound output after some time with the monitor turned off](#No_HDMI_sound_output_after_some_time_with_the_monitor_turned_off)
    *   [4.2 No cards](#No_cards)
    *   [4.3 Starting an application interrupts other app's sound](#Starting_an_application_interrupts_other_app.27s_sound)
    *   [4.4 The only device shown is "dummy output" or newly connected cards are not detected](#The_only_device_shown_is_.22dummy_output.22_or_newly_connected_cards_are_not_detected)
    *   [4.5 No HDMI 5/7.1 Selection for Device](#No_HDMI_5.2F7.1_Selection_for_Device)
    *   [4.6 Failed to create sink input: sink is suspended](#Failed_to_create_sink_input:_sink_is_suspended)
    *   [4.7 Simultaneous output to multiple sound cards / devices](#Simultaneous_output_to_multiple_sound_cards_.2F_devices)
    *   [4.8 Simultaneous output to multiple sinks on the same sound card not working](#Simultaneous_output_to_multiple_sinks_on_the_same_sound_card_not_working)
    *   [4.9 Some profiles like SPDIF are not enabled by default on the card](#Some_profiles_like_SPDIF_are_not_enabled_by_default_on_the_card)
*   [5 Bluetooth](#Bluetooth)
    *   [5.1 Disable Bluetooth support](#Disable_Bluetooth_support)
    *   [5.2 Bluetooth headset replay problems](#Bluetooth_headset_replay_problems)
    *   [5.3 Automatically switch to Bluetooth or USB headset](#Automatically_switch_to_Bluetooth_or_USB_headset)
    *   [5.4 My Bluetooth device is paired but does not play any sound](#My_Bluetooth_device_is_paired_but_does_not_play_any_sound)
*   [6 Applications](#Applications)
    *   [6.1 Flash content](#Flash_content)
    *   [6.2 Permission errors bug](#Permission_errors_bug)
    *   [6.3 Audacity](#Audacity)
*   [7 Other Issues](#Other_Issues)
    *   [7.1 Bad configuration files](#Bad_configuration_files)
    *   [7.2 Cannot update configuration of sound device in pavucontrol](#Cannot_update_configuration_of_sound_device_in_pavucontrol)
    *   [7.3 Failed to create sink input: sink is suspended](#Failed_to_create_sink_input:_sink_is_suspended_2)
    *   [7.4 Pulse overwrites ALSA settings](#Pulse_overwrites_ALSA_settings)
    *   [7.5 Prevent Pulse from restarting after being killed](#Prevent_Pulse_from_restarting_after_being_killed)
    *   [7.6 Daemon startup failed](#Daemon_startup_failed)
        *   [7.6.1 Outputs by PulseAudio error status check utilities](#Outputs_by_PulseAudio_error_status_check_utilities)
    *   [7.7 Daemon already running](#Daemon_already_running)
    *   [7.8 Subwoofer stops working after end of every song](#Subwoofer_stops_working_after_end_of_every_song)
    *   [7.9 Unable to select surround configuration other than "Surround 4.0"](#Unable_to_select_surround_configuration_other_than_.22Surround_4.0.22)
    *   [7.10 Realtime scheduling](#Realtime_scheduling)
    *   [7.11 pactl "invalid option" error with negative percentage arguments](#pactl_.22invalid_option.22_error_with_negative_percentage_arguments)
    *   [7.12 Fallback device is not respected](#Fallback_device_is_not_respected)

## Volume

Here you will find some hints on volume issues and why you may not hear anything.

### Auto-Mute Mode

Auto-Mute Mode may be enabled. It can be disabled using `alsamixer`.

See [http://superuser.com/questions/431079/how-to-disable-auto-mute-mode](http://superuser.com/questions/431079/how-to-disable-auto-mute-mode) for more.

To save your current settings as the default options, run `alsactl store` as root.

### Muted audio device

If one experiences no audio output via any means while using [ALSA](/index.php/ALSA "ALSA"), attempt to unmute the sound card. To do this, launch `alsamixer` and make sure each column has a green `00` under it (this can be toggled by pressing `m`):

```
$ alsamixer -c 0

```

**Note:** alsamixer will not tell you which output device is set as the default. One possible cause of no sound after install is that PulseAudio detects the wrong output device as a default. Install [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) and check if there is any output on the pavucontrol panel when playing a *.wav* file.

### Output stuck muted while Master is toggled

In setups with multiple outputs (e.g. 'Headphone' and 'Speaker') using plain amixer to toggle Master can trigger PulseAudio to mute the active output too, but it does not necessarily unmute it when Master is toggled back to be unmuted. To resolve this, amixer must have the device flag set to 'pulse':

```
$ amixer -D pulse sset Master toggle

```

This will cause amixer to ask PulseAudio to do the toggling rather than toggling it directly. Because of this, PulseAudio will correctly unmute Master as well as any applicable output.

### Muted application

If a specific application is muted or low while all else seems to be in order, it may be due to individual `sink-input` settings. With the offending application playing audio, run:

```
$ pacmd list-sink-inputs

```

Find and make note of the `index` of the corresponding `sink input`. The `properties:` `application.name` and `application.process.binary`, among others, should help here. Ensure sane settings are present, specifically those of `muted` and `volume`. If the sink is muted, it can be unmuted by:

```
$ pacmd set-sink-input-mute <index> false

```

If the volume needs adjusting, it can be set to 100% by:

```
$ pacmd set-sink-input-volume <index> 0x10000

```

**Note:** If `pacmd` reports `0 sink input(s)`, double-check that the application is playing audio. If it is still absent, verify that other applications show up as sink inputs.

### Volume adjustment does not work properly

Check: `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common`

If the volume does not appear to increment/decrement properly using `alsamixer` or `amixer`, it may be due to PulseAudio having a larger number of increments (65537 to be exact). Try using larger values when changing volume (e.g. `amixer set Master 655+`).

### Per-application volumes change when the Master volume is adjusted

This is because PulseAudio uses flat volumes by default, instead of relative volumes, relative to an absolute master volume. If this is found to be inconvenient, asinine, or otherwise undesireable, relative volumes can be enabled by disabling flat volumes in the PulseAudio daemon's configuration file:

 `/etc/pulse/daemon.conf or ~/.config/pulse/daemon.conf` 
```
flat-volumes = no

```

and then restarting PulseAudio by executing

```
$ pulseaudio -k
$ pulseaudio --start

```

### Volume gets louder every time a new application is started

Per default, it seems as if changing the volume in an application sets the global system volume to that level instead of only affecting the respective application. Applications setting their volume on startup will therefore cause the system volume to "jump".

Fix this by disabling flat volumes, as demonstrated in the previous section. When Pulse comes back after a few seconds, applications will not alter the global system volume anymore but have their own volume level again.

**Note:** A previously installed and removed pulseaudio-equalizer may leave behind remnants of the setup in `~/.config/pulse/default.pa` or `~/.pulse/default.pa` which can also cause maximized volume trouble. Comment that out as needed.

### Sound output is only mono on M-Audio Audiophile 2496 sound card

Add the following:

 `/etc/pulseaudio/default.pa` 
```
load-module module-alsa-sink sink_name=delta_out device=hw:M2496 format=s24le channels=10 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7
load-module module-alsa-source source_name=delta_in device=hw:M2496 format=s24le channels=12 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7,aux8,aux9
set-default-sink delta_out
set-default-source delta_in

```

### No sound below a volume cutoff

Known issue (won't fix): [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133)

If sound does not play when PulseAudio's volume is set below a certain level, try setting `ignore_dB=1` in `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
load-module module-udev-detect ignore_dB=1

```

However, be aware that it may cause another bug preventing PulseAudio to unmute speakers when headphones or other audio devices are unplugged.

### Low volume for internal microphone

If you experience low volume on internal notebook microphone, try setting:

 `/etc/pulse/default.pa` 
```
set-source-volume 1 300000

```

### Clients alter master output volume (a.k.a. volume jumps to 100% after running application)

If changing the volume in specific applications or simply running an application changes the master output volume this is likely due to flat volumes mode of pulseaudio. Before disabling it, KDE users should try lowering their system notifications volume in *System Settings -> Application and System Notifications -> Manage Notifications* under the *Player Settings* tab to something reasonable. Changing the *Event Sounds* volume in KMix or another volume mixer application will not help here. This should make the flat-volumes mode work out as intended, if it does not work, some other application is likely requesting 100% volume when its playing something. If all else fails, you can try to disable flat-volumes:

 `/etc/pulse/daemon.conf` 
```
flat-volumes = no

```

Then restart PulseAudio daemon:

```
# pulseaudio -k
# pulseaudio --start

```

### No sound after resume from suspend

If audio generally works, but stops after resume from suspend, try "reloading" PulseAudio by executing:

```
$ /usr/bin/pasuspender /bin/true

```

This is better than completely killing and restarting it (`pulseaudio -k` followed by `pulseaudio --start`), because it does not break already running applications.

If the above fixes your problem, you may wish to automate it, by creating a systemd service file.

1\. Create the template service file in `/etc/systemd/system/resume-fix-pulseaudio@.service`:

```
[Unit]
Description=Fix PulseAudio after resume from suspend
After=suspend.target

[Service]
User=%I
Type=oneshot
Environment="XDG_RUNTIME_DIR=/run/user/%U"
ExecStart=/usr/bin/pasuspender /bin/true

[Install]
WantedBy=suspend.target

```

2\. Enable it for your user account

```
# systemctl enable resume-fix-pulseaudio@YOUR_USERNAME_HERE.service

```

3\. Reload systemd

```
# systemctl --system daemon-reload

```

### ALSA channels mute when headphones are plugged/unplugged improperly

If when you unplug your headphones or plug them in the audio remains muted in alsamixer on the wrong channel due to it being set to 0%, you may be able to fix it by opening `/etc/pulse/default.pa` and commenting out the line:

```
load-module module-switch-on-port-available

```

## Microphone

### Microphone not detected by PulseAudio

Determine the card and device number of your mic:

```
 $ arecord -l
 **** List of CAPTURE Hardware Devices ****
 card 0: PCH [HDA Intel PCH], device 0: ALC269VC Analog [ALC269VC Analog]
 Subdevices: 1/1
 Subdevice #0: subdevice #0

```

In hw:CARD,DEVICE notation, you would specify the above device as `hw:0,0`.

Then, edit `/etc/pulse/default.pa` and insert a `load-module` line specifying your device as follows:

```
  load-module module-alsa-source device=hw:0,0
  # the line above should be somewhere before the line below
 .ifexists module-udev-detect.so

```

Finally, restart pulseaudio to apply the new settings:

```
  $ pulseaudio -k ; pulseaudio -D

```

If everything worked correctly, you should now see your mic show up when running `pavucontrol` (under the `Input Devices` tab).

### PulseAudio uses wrong microphone

If PulseAudio uses the wrong microphone, and changing the Input Device with Pavucontrol did not help, take a look at alsamixer. It seems that Pavucontrol does not always set the input source correctly.

```
$ alsamixer

```

Press `F6` and choose your sound card, e.g. HDA Intel. Now press `F5` to display all items. Try to find the item: `Input Source`. With the up/down arrow keys you are able to change the input source.

Now try if the correct microphone is used for recording.

### No microphone on ThinkPad T400/T500/T420

Run:

```
alsamixer -c 0

```

Unmute and maximize the volume of the "Internal Mic".

Once you see the device with:

```
arecord -l

```

you might still need to adjust the settings. The microphone and the audio jack are duplexed. Set the configuration of the internal audio in pavucontrol to *Analog Stereo Duplex*.

### No microphone input on Acer Aspire One

Install pavucontrol, unlink the microphone channels and turn down the left one to 0. Reference: [http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048](http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048)

### Static noise in microphone recording

If we are getting static noise in Skype, gnome-sound-recorder, arecord, etc.'s recordings, then the sound card sample rate is incorrect. That is why there is static noise in Linux microphone recordings. To fix this, we need to set the sampling rate in `/etc/pulse/daemon.conf` for the sound hardware.

#### Determine sound cards in the system (1/5)

This requires [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) and related packages to be installed:

 `$ arecord --list-devices` 
```
**** List of CAPTURE Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC888 Analog [ALC888 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 2: ALC888 Analog [ALC888 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

Sound card is `hw:0,0`.

#### Determine sampling rate of the sound card (2/5)

 `arecord -f dat -r 60000 -D hw:0,0 -d 5 test.wav` 
```
"Recording WAVE 'test.wav' : Signed 16 bit Little Endian, Rate 60000 Hz, Stereo
Warning: rate is not accurate (requested = 60000Hz, **got = 96000Hz**)
please, try the plug plugin
```

observe, the `got = 96000Hz`. This is the maximum sampling rate of our card.

#### Setting the sound card's sampling rate into PulseAudio configuration (3/5)

The default sampling rate in PulseAudio:

 `$ grep "default-sample-rate" /etc/pulse/daemon.conf`  `; default-sample-rate = 44100` 

`44100` is disabled and needs to be changed to `96000`:

```
# sed 's/; default-sample-rate = 44100/default-sample-rate = 96000/g' -i /etc/pulse/daemon.conf

```

#### Restart PulseAudio to apply the new settings (4/5)

```
$ pulseaudio -k
$ pulseaudio --start

```

#### Finally check by recording and playing it back (5/5)

Let us record some voice using a microphone for, say, 10 seconds. Make sure the microphone is not muted and all

```
$ arecord -f cd -d 10 test-mic.wav

```

After 10 seconds, let us play the recording...

```
$ aplay test-mic.wav

```

Now hopefully, there is no static noise in microphone recording anymore.

### No microphone on Steam or Skype with enable-remixing = no

When you set `enable-remixing = no` on `/etc/pulse/daemon.conf` you may find that your microphone has stopped working on certain applications like Skype or Steam. This happens because these applications capture the microphone as mono only and because remixing is disabled, Pulseaudio will no longer remix your stereo microphone to mono.

To fix this you need to tell Pulseaudio to do this for you:

1\. Find the name of the source

```
# pacmd list-sources

```

Example output edited for brevity, the name you need is in bold:

```
   index: 2
       name: <**alsa_input.pci-0000_00_14.2.analog-stereo**>
       driver: <module-alsa-card.c>
       flags: HARDWARE HW_MUTE_CTRL HW_VOLUME_CTRL DECIBEL_VOLUME LATENCY DYNAMIC_LATENCY

```

2\. Add a remap rule to `/etc/pulse/default.pa`, use the name you found with the previous command, here we will use **alsa_input.pci-0000_00_14.2.analog-stereo** as an example:

 `/etc/pulse/default.pa` 
```
### Remap microphone to mono
load-module module-remap-source master=alsa_input.pci-0000_00_14.2.analog-stereo master_channel_map=front-left,front-right channels=2 channel_map=mono,mono

```

3\. Restart Pulseaudio

```
# pulseaudio -k

```

**Note:** Pulseaudio may fail to start if you do not exit a program that was using the microphone (e.g. if you tested on Steam before modifying the file), in which case you should exit the application and manually start Pulseaudio

```
# pulseaudio --start

```

### Microphone distorted due to automatic adjustment

If your microphone volume creeps up automatically and causes the sound to be distorted, you can fix it by disabling mic boost:

In `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-internal-mic.conf` and `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-mic.conf`,

*   Under `[Element Internal Mic Boost]` set `volume` to `zero`.
*   Under `[Element Int Mic Boost]` set `volume` to `zero`.
*   Under `[Element Mic Boost]` set `volume` to `zero`.

Then restart PulseAudio:

```
# pulseaudio -k

```

## Audio quality

### Enable Echo/Noise-Cancelation

Arch does not load the Pulseaudio Echo-Cancelation module by default, therefore, we have to add it in `/etc/pulse/default.pa`. First you can test if the module is present with `pacmd` and entering `list-modules`. If you cannot find a line showing `name: <module-echo-cancel>` you have to add

 `/etc/pulse/default.pa` 
```
### Enable Echo/Noise-Cancelation
load-module module-echo-cancel

```

then restart Pulseaudio

```
pulseaudio -k
pulseaudio --start

```

and check if the module is activated by starting `pavucontrol`. Under `Recoding` the input device should show `Echo-Cancel Source Stream from"`

### Glitches, skips or crackling

The newer implementation of the PulseAudio sound server uses timer-based audio scheduling instead of the traditional, interrupt-driven approach.

Timer-based scheduling may expose issues in some ALSA drivers. On the other hand, other drivers might be glitchy without it on, so check to see what works on your system.

To turn timer-based scheduling off add `tsched=0` in `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa`  `load-module module-udev-detect tsched=0` 

Then restart the PulseAudio server:

```
$ pulseaudio -k
$ pulseaudio --start

```

Do the reverse to enable timer-based scheduling, if not already enabled by default.

If you are using Intel's [IOMMU](https://en.wikipedia.org/wiki/IOMMU "wikipedia:IOMMU") and experience glitches and/or skips, add `intel_iommu=igfx_off` to your kernel command line.

Some Intel audio cards using the `snd-hda-intel` module need the otions `vid=8086 pid=8ca0 snoop=0`. In order to set them permanently, create/modify the following file including the line below.

 `/etc/modprobe.d/sound.conf`  `options snd-hda-intel vid=8086 pid=8ca0 snoop=0` 

Please report any such cards to [PulseAudio Broken Sound Driver page](http://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/BrokenDrivers/)

### Setting the default fragment number and buffer size in PulseAudio

#### Finding out your audio device parameters (1/4)

To find out what your sound card buffering settings are, use the following command and scroll through the output until you find the correct sink entry.

 `$ pactl list sinks` 
```
Sink #1
	State: RUNNING
	Name: alsa_output.pci-0000_00_1b.0.analog-stereo
	Description: Built-in Audio Analog Stereo
	Driver: module-alsa-card.c
	Sample Specification: s16le 2ch 44100Hz
	Channel Map: front-left,front-right
	Owner Module: 7
	Mute: no
	Volume: front-left: 42600 /  65% / -11.22 dB,   front-right: 42600 /  65% / -11.22 dB
	        balance 0.00
	Base Volume: 65536 / 100% / 0.00 dB
	Monitor Source: alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
	Latency: 70662 usec, configured 85000 usec
	Flags: HARDWARE HW_MUTE_CTRL HW_VOLUME_CTRL DECIBEL_VOLUME LATENCY 
	Properties:
		alsa.resolution_bits = "16"
		device.api = "alsa"
		device.class = "sound"
		alsa.class = "generic"
		alsa.subclass = "generic-mix"
		alsa.name = "ALC283 Analog"
		alsa.id = "ALC283 Analog"
		alsa.subdevice = "0"
		alsa.subdevice_name = "subdevice #0"
		alsa.device = "0"
		alsa.card = "1"
		alsa.card_name = "HDA Intel PCH"
		alsa.long_card_name = "HDA Intel PCH at 0xe111c000 irq 43"
		alsa.driver_name = "snd_hda_intel"
		device.bus_path = "pci-0000:00:1b.0"
		sysfs.path = "/devices/pci0000:00/0000:00:1b.0/sound/card1"
		device.bus = "pci"
		device.vendor.id = "8086"
		device.vendor.name = "Intel Corporation"
		device.product.id = "9ca0"
		device.product.name = "Wildcat Point-LP High Definition Audio Controller"
		device.form_factor = "internal"
		device.string = "front:1"
		device.buffering.buffer_size = "352800"
		device.buffering.fragment_size = "176400"
		device.access_mode = "mmap+timer"
		device.profile.name = "analog-stereo"
		device.profile.description = "Analog Stereo"
		device.description = "Built-in Audio Analog Stereo"
		alsa.mixer_name = "Realtek ALC283"
		alsa.components = "HDA:10ec0283,10ec0283,00100003"
		module-udev-detect.discovered = "1"
		device.icon_name = "audio-card-pci"
	Ports:
		analog-output-speaker: Speakers (priority: 10000, not available)
		analog-output-headphones: Headphones (priority: 9000, available)
	Active Port: analog-output-headphones
	Formats:
		pcm
...

```

Take note the `buffer_size` and `fragment_size` values for the relevant sound card.

#### Calculate your fragment size in msecs and number of fragments (2/4)

PulseAudio's default sampling rate and bit depth are set to `44100Hz` @ `16 bits`.

With this configuration, the bit rate we need is `44100`*`16` = `705600` bits per second. That is `1411200 bps` for stereo.

Let us take a look at the parameters we have found in the previous step:

```
device.buffering.buffer_size = "352800" => 352800/1411200 = 0.25 s = 250 ms
device.buffering.fragment_size = "176400" => 176400/1411200 = 0.125 s = 125 ms

```

#### Modify PulseAudio's configuration file (3/4)

 `/etc/pulse/daemon.conf` 
```
; default-fragments = X
; default-fragment-size-msec = Y

```

In the previous step, we calculated the fragment size parameter. The number of fragments is simply buffer_size/fragment_size, which in this case (`250/125`) is `2`:

 `/etc/pulse/daemon.conf` 
```
; default-fragments = **2**
; default-fragment-size-msec = **125**
```

#### Restart the PulseAudio daemon (4/4)

```
$ pulseaudio -k
$ pulseaudio --start

```

For more information, see: [Linux Mint topic](http://forums.linuxmint.com/viewtopic.php?f=42&t=44862)

### Choppy sound with analog surround sound setup

The low-frequency effects (LFE) channel is not remixed per default. To enable it the following needs to be set in `/etc/pulse/daemon.conf` :

 `/etc/pulse/daemon.conf` 
```
enable-lfe-remixing = yes

```

### Laggy sound

This issue is due to incorrect buffer sizes. First verify that the variables `default-fragments` and `default-fragment-size-msec` are not being set to non default values in the file `/etc/pulse/daemon.conf`. If the issue is still present, try setting them to the following values:

 `/etc/pulse/daemon.conf` 
```
default-fragments = 5
default-fragment-size-msec = 2
```

### Choppy/distorted sound

This can result from an incorrectly set sample rate. Try the following setting:

 `/etc/pulse/daemon.conf`  `default-sample-rate = 48000` 

and restart the PulseAudio server.

If one experiences choppy sound in applications using [OpenAL](https://en.wikipedia.org/wiki/OpenAL "wikipedia:OpenAL"), change the sample rate in `/etc/openal/alsoft.conf`:

 `/etc/openal/alsoft.conf`  `frequency = 48000` 

Setting the PCM volume above 0 dB can cause [clipping](https://en.wikipedia.org/wiki/Clipping_(audio) "wikipedia:Clipping (audio)"). Running `alsamixer` will allow you to see if this is the problem and if so fix it. Note that ALSA may not [correctly export](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/PulseAudioStoleMyVolumes) the dB information to PulseAudio. Try the following:

 `/etc/pulse/default.pa`  `load-module module-udev-detect ignore_dB=1` 

and restart the PulseAudio server. See also [#No sound below a volume cutoff](#No_sound_below_a_volume_cutoff).

## Hardware and Cards

### No HDMI sound output after some time with the monitor turned off

The monitor is connected via HDMI/DisplayPort, and the audio jack is plugged in the headphone jack of the monitor, but PulseAudio insists that it is unplugged:

 `pactl list sinks` 
```
...
hdmi-output-0: HDMI / DisplayPort (priority: 5900, not available)
...

```

This leads to no sound coming from HDMI output. A workaround for this is to switch to another VT and back again. If that does not work, try: turn off your monitor, switch to another VT, turn on your monitor, and switch back. This problem has been reported by ATI/Nvidia/Intel users.

### No cards

If PulseAudio starts, run `pacmd list`. If no cards are reported, make sure that the ALSA devices are not in use:

```
$ fuser -v /dev/snd/*
$ fuser -v /dev/dsp

```

Make sure any applications using the pcm or dsp files are shut down before restarting PulseAudio.

### Starting an application interrupts other app's sound

If you have trouble with some applications (eg. Teamspeak, Mumble) interrupting sound output of already running applications (eg. Deadbeaf), you can solve this by commenting out the line `load-module module-role-cork` in `/etc/pulse/default.pa` like shown below:

 `/etc/pulse/default.pa` 
```
### Cork music/video streams when a phone stream is active
# load-module module-role-cork

```

Then restart pulseaudo by using your normal user account with

```
pulseaudio -k
pulseaudio --start

```

### The only device shown is "dummy output" or newly connected cards are not detected

Another reason is [FluidSynth](/index.php/FluidSynth "FluidSynth") conflicting with PulseAudio as discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=154002). One solution is to remove the package [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth).

Alternatively you could modify the *fluidsynth* configuration file `/etc/conf.d/fluidsynth` and change the driver to PulseAudio, then restart *fluidsynth* and PulseAudio:

 `/etc/conf.d/fluidsynth` 
```
AUDIO_DRIVER=pulseaudio
OTHER_OPTS='-m alsa_seq-r 48000'
```

It is also possible there is an issue with logind giving permissions, see [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") for more information.

### No HDMI 5/7.1 Selection for Device

If you are unable to select 5/7.1 channel output for a working HDMI device, then turning off "stream device reading" in `/etc/pulse/default.pa` might help.

See [#Fallback device is not respected](#Fallback_device_is_not_respected).

### Failed to create sink input: sink is suspended

If you do not have any output sound and receive dozens of errors related to a suspended sink in your `journalctl -b` log, then backup first and then delete your user-specific pulse folders:

```
$ rm -r ~/.pulse ~/.pulse-cookie ~/.config/pulse

```

### Simultaneous output to multiple sound cards / devices

Simultaneous output to two different devices can be very useful. For example, being able to send audio to your A/V receiver via your graphics card's HDMI output, while also sending the same audio through the analogue output of your motherboard's built-in audio. This is much less hassle than it used to be (in this example, we are using GNOME desktop).

Using [paprefs](https://www.archlinux.org/packages/?name=paprefs), simply select "Add virtual output device for simultaneous output on all local sound cards" from under the "Simultaneous Output" tab. Then, under GNOME's "sound settings", select the simultaneous output you have just created.

If this does not work, try adding the following to `~/.asoundrc`:

```
pcm.dsp {
   type plug
   slave.pcm "dmix"
}

```

**Tip:** Simultaneous output can also be achieved manually using alsamixer. Disable "auto mute" item, then unmute other output sources you want to hear and increase their volume.

### Simultaneous output to multiple sinks on the same sound card not working

This can be useful for users who have multiple sound sources and want to play them on different sinks/outputs. An example use-case for this would be if you play music and also voice chat and want to output music to speakers (in this case Digital S/PDIF) and voice to headphones. (Analog)

This is sometimes auto detected by PulseAudio but not always. If you know that your sound card can output to both Analog and S/PDIF at the same time and PulseAudio does not have this option in its profiles in pavucontrol, or veromix then you probably need to create a configuration file for your sound card.

More in detail you need to create a profile-set for your specific sound card. This is done in two steps mostly.

*   Create udev rule to make PulseAudio choose your PulseAudio configuration file specific to the sound card.
*   Create the actual configuration.

Create a pulseadio udev rule.

**Note:** This is only an example for Asus Xonar Essence STX. Read [udev](/index.php/Udev "Udev") to find out the correct values.

**Note:** Your configuration file should have lower number than the original PulseAudio rule to take effect.
 `/usr/lib/udev/rules.d/90-pulseaudio-Xonar-STX.rules` 
```
ACTION=="change", SUBSYSTEM=="sound", KERNEL=="card*", \
ATTRS{subsystem_vendor}=="0x1043", ATTRS{subsystem_device}=="0x835c", ENV{PULSE_PROFILE_SET}="asus-xonar-essence-stx.conf" 

```

Now, create a configuration file. If you bother, you can start from scratch and make it saucy. However you can also use the default configuration file, rename it, and then add your profile there that you know works. Less pretty but also faster.

To enable multiple sinks for Asus Xonar Essence STX you need only to add this in.

**Note:** `asus-xonar-essence-stx.conf` also includes all code/mappings from `default.conf`.
 `/usr/share/pulseaudio/alsa-mixer/profile-sets/asus-xonar-essence-stx.conf` 
```
[Profile analog-stereo+iec958-stereo]
description = Analog Stereo Duplex + Digital Stereo Output
input-mappings = analog-stereo
output-mappings = analog-stereo iec958-stereo
skip-probe = yes

```

This will auto-profile your Asus Xonar Essence STX with default profiles and add your own profile so you can have multiple sinks.

You need to create another profile in the configuration file if you want to have the same functionality with AC3 Digital 5.1 output.

[See PulseAudio article about profiles](http://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/Profiles/)

### Some profiles like SPDIF are not enabled by default on the card

Some profiles like IEC-958 (i.e. S/PDIF) may not be enabled by default on the selected sink. Each time the system starts up, the card profile is disabled and the pulseaudio daemon cannot select it. You have to add the profile selection to you default.pa file. Verify the card and profile name with :

```
$ pacmd list-cards

```

Then edit the config to add the profile

 `~/.config/pulse/default.pa` 
```
## Replace with your card name and the profile you want to activate
set-card-profile alsa_card.pci-0000_00_1b.0 output:iec958-stereo+input:analog-stereo

```

Pulse audio will add this profile the pool of available profiles

## Bluetooth

### Disable Bluetooth support

If you do not use Bluetooth, you may experience the following error in your journal:

```
bluez5-util.c: GetManagedObjects() failed: org.freedesktop.DBus.Error.ServiceUnknown: The name org.bluez was not provided by any .service files

```

To disable Bluetooth support in PulseAudio, make sure that the following lines are commented out in the configuration file in use (`~/.config/pulse/default.pa` or `/etc/pulse/default.pa`):

 `~/.config/pulse/default.pa` 
```
### Automatically load driver modules for Bluetooth hardware
#.ifexists module-bluetooth-policy.so
#load-module module-bluetooth-policy
#.endif

#.ifexists module-bluetooth-discover.so
#load-module module-bluetooth-discover
#.endif

```

### Bluetooth headset replay problems

Some user [reports](https://bbs.archlinux.org/viewtopic.php?id=117420) huge delays or even no sound when the Bluetooth connection does not send any data. This is due to the `module-suspend-on-idle` module, which automatically suspends sinks/sources on idle. As this can cause problems with headset, the responsible module can be deactivated.

To disable loading of the `module-suspend-on-idle` module, comment out the following line in the configuration file in use (`~/.config/pulse/default.pa` or `/etc/pulse/default.pa`):

 `~/.config/pulse/default.pa` 
```
### Automatically suspend sinks/sources that become idle for too long
#load-module module-suspend-on-idle

```

Finally restart PulseAudio to apply the changes.

### Automatically switch to Bluetooth or USB headset

Add the following:

 `/etc/pulse/default.pa` 
```
# automatically switch to newly-connected devices
load-module module-switch-on-connect

```

### My Bluetooth device is paired but does not play any sound

[See the article in Bluetooth section](/index.php/Bluetooth#My_device_is_paired_but_no_sound_is_played_from_it "Bluetooth")

Starting from PulseAudio 2.99 and bluez 4.101 you should **avoid** using Socket interface. Do NOT use:

 `/etc/bluetooth/audio.conf` 
```
[General]
Enable=Socket

```

If you face problems with A2DP and PA 2.99 make sure you have [sbc](https://www.archlinux.org/packages/?name=sbc) library.

## Applications

### Flash content

Since Adobe Flash does not directly support PulseAudio, the recommended way is to [configure ALSA to use the virtual PulseAudio sound card](/index.php/PulseAudio#ALSA "PulseAudio").

If Flash audio is lagging, you may try to have Flash access ALSA directly. See [PulseAudio#ALSA/dmix without grabbing hardware device](/index.php/PulseAudio#ALSA.2Fdmix_without_grabbing_hardware_device "PulseAudio") for details.

### Permission errors bug

 `pulseaudio --start` 
```
E: [autospawn] core-util.c: Failed to create secure directory (/run/user/1000/pulse): Operation not permitted
W: [autospawn] lock-autospawn.c: Cannot access autospawn lock.
E: [pulseaudio] main.c: Failed to acquire autospawn lock
```

Known programs that changes permissions for `/run/user/*user id*/pulse` when using [Polkit](/index.php/Polkit "Polkit") for root elevation:

*   [sakis3g](https://aur.archlinux.org/packages/sakis3g/)

As a workaround, include [gksu](https://www.archlinux.org/packages/?name=gksu) or [kdesu](https://www.archlinux.org/packages/?name=kdesu) in a [desktop entry](/index.php/Desktop_entry "Desktop entry"), or add `*username* ALL=NOPASSWD: /usr/bin/*program_name*` to [sudoers](/index.php/Sudoers "Sudoers") to run it with [sudo](https://www.archlinux.org/packages/?name=sudo) or `gksudo` without a password.

The other workaround is to uncomment and set `daemonize = yes` in the `/etc/pulse/daemon.conf`.

See also [[1]](https://bbs.archlinux.org/viewtopic.php?id=135955).

### Audacity

When starting Audacity you may find that your headphones no longer work. This can be because Audacity is trying to use them as a recording device. To fix this, open Audacity, then set its recording device to `pulse:Internal Mic:0`.

Under some circumstances, playback may be distorted, very fast, or freeze, as discussed in the [Audacity Wiki's Linux Issues page](http://wiki.audacityteam.org/wiki/Linux_Issues#ALSA_and_other_sound_systems).

The solution proposed in this page may work: start Audacity with:

```
$ env PULSE_LATENCY_MSEC=30 audacity

```

If the solution above does not fix this issue, one may wish to temporarily disable pulseaudio while running Audacity by using the `pasuspender` command:

```
$ pasuspender -- audacity

```

Then, be sure to select the appropriate ALSA input and output devices in Audacity.

See also [#Setting the default fragment number and buffer size in PulseAudio](#Setting_the_default_fragment_number_and_buffer_size_in_PulseAudio).

## Other Issues

### Bad configuration files

After starting PulseAudio, if the system outputs no sound, it may be necessary to delete the contents of `~/.config/pulse` and/or `~/.pulse`. PulseAudio will automatically create new configuration files on its next start.

### Cannot update configuration of sound device in pavucontrol

[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) is a handy GUI utility for configuring PulseAudio. Under its 'Configuration' tab, you can select different profiles for each of your sound devices e.g. analogue stereo, digital output (IEC958), HDMI 5.1 Surround etc.

However, you may run into an instance where selecting a different profile for a card results in the pulse daemon crashing and auto restarting without the new selection "sticking". If this occurs, use the other useful GUI tool, [paprefs](https://www.archlinux.org/packages/?name=paprefs), to check under the "Simultaneous Output" tab for a virtual simultaneous device. If this setting is active (checked), it will prevent you changing any card's profile in pavucontrol. Uncheck this setting, then adjust your profile in pavucontrol prior to re-enabling simultaneous output in paprefs.

### Failed to create sink input: sink is suspended

If you do not have any output sound and receive dozens of errors related to a suspended sink in your `journalctl -b` log, then backup first and then delete your user-specific pulse folders:

```
$ rm -r ~/.pulse ~/.pulse-cookie ~/.config/pulse

```

### Pulse overwrites ALSA settings

PulseAudio usually overwrites the ALSA settings — for example set with alsamixer — at start-up, even when the ALSA daemon is loaded. Since there seems to be no other way to restrict this behaviour, a workaround is to restore the ALSA settings again after PulseAudio has started. Add the following command to `.xinitrc` or `.bash_profile` or any other [autostart](/index.php/Autostart "Autostart") file:

```
restore_alsa() {
 while [ -z "$(pidof pulseaudio)" ]; do
  sleep 0.5
 done
 alsactl -f /var/lib/alsa/asound.state restore 
}
restore_alsa &

```

### Prevent Pulse from restarting after being killed

Sometimes you may wish to temporarily disable Pulse. In order to do so you will have to prevent Pulse from restarting after being killed.

 `~/.config/pulse/client.conf` 
```
# Disable autospawning the PulseAudio daemon
autospawn = no
```

### Daemon startup failed

Try resetting PulseAudio:

```
$ rm -rf /tmp/pulse* ~/.pulse* ~/.config/pulse
$ pulseaudio -k
$ pulseaudio --start

```

*   Check that options for sinks are set up correctly.

*   If you configured in default.pa to load and use the OSS modules then check with [lsof](https://www.archlinux.org/packages/?name=lsof) that `/dev/dsp` device is not used by another application.

*   Set a preferred working resample method. Use `pulseaudio --dump-resample-methods` to see a list with all available resample methods you can use.

*   To get details about currently appeared unfixed errors or just get status of daemon use commands like `pax11publish -d` and `pulseaudio -v` where `v` option can be used multiple time to set verbosity of log output equal to the `--log-level[=LEVEL]` option where LEVEL is from 0 to 4\. See the [Outputs by PulseAudio error status check utilities](/index.php/PulseAudio#Outputs_by_PulseAudio_error_status_check_utilities "PulseAudio") section.

See also man pages for [pax11publish](http://linux.die.net/man/1/pax11publish) and [pulseaudio](http://linux.die.net/man/1/pulseaudio) for more details.

#### Outputs by PulseAudio error status check utilities

If the `pax11publish -d` shows error like:

```
N: [pulseaudio] main.c: User-configured server at "user", refusing to start/autospawn.

```

then run `pax11publish -r` command then could be also good to logout and login again. This manual cleanup is always required when using LXDM because it does not restart the X server on logout; see [LXDM#PulseAudio](/index.php/LXDM#PulseAudio "LXDM").

If the `pulseaudio -vvvv` command shows error like:

```
E: [pulseaudio] module-udev-detect.c: You apparently ran out of inotify watches, probably because Tracker/Beagle took them all away. I wished people would do their homework first and fix inotify before using it for watching whole directory trees which is something the current inotify is certainly not useful for. Please make sure to drop the Tracker/Beagle guys a line complaining about their broken use of inotify.

```

This can be resolved temporary by:

```
$ echo 100000 > /proc/sys/fs/inotify/max_user_watches

```

For permanent use save settings in the *99-sysctl.conf* file:

 `/etc/sysctl.d/99-sysctl.conf` 
```
# Increase inotify max watchs per user
fs.inotify.max_user_watches = 100000
```

**Warning:** It may cause much bigger consumption of memory by kernel.

**See also**

*   [proc_sys_fs_inotify](http://www.linuxinsight.com/proc_sys_fs_inotify.html) and [dnotify, inotify](http://lwn.net/Articles/604686/)- more details about *inotify/max_user_watches*
*   [reasonable amount of inotify watches with Linux](http://stackoverflow.com/questions/535768/what-is-a-reasonable-amount-of-inotify-watches-with-linux?answertab=votes#tab-top)
*   [inotify](http://linux.die.net/man/7/inotify) - man page

### Daemon already running

On some systems, PulseAudio may be started multiple times. journalctl will report:

```
[pulseaudio] pid.c: Daemon already running.

```

Make sure to use only one method of autostarting applications. [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) includes these files:

*   `/etc/X11/xinit/xinitrc.d/pulseaudio`
*   `/etc/xdg/autostart/pulseaudio.desktop`
*   `/etc/xdg/autostart/pulseaudio-kde.desktop`

Also check user autostart files and directories, such as [xinitrc](/index.php/Xinitrc "Xinitrc"), `~/.config/autostart/` etc.

### Subwoofer stops working after end of every song

Known issue: [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099)

To fix this, must edit: `/etc/pulse/daemon.conf` and enable `enable-lfe-remixing` :

 `/etc/pulse/daemon.conf` 
```
enable-lfe-remixing = yes

```

### Unable to select surround configuration other than "Surround 4.0"

If you are unable to set 5.1 surround output in pavucontrol because it only shows "Analog Surround 4.0 Output", open the ALSA mixer and change the output configuration there to 6 channels. Then restart pulseaudio, and pavucontrol will list many more options.

### Realtime scheduling

If rtkit does not work, you can manually set up your system to run PulseAudio with real-time scheduling, which can help performance. To do this, add the following lines to `/etc/security/limits.conf`:

```
@pulse-rt - rtprio 9
@pulse-rt - nice -11

```

Afterwards, you need to add your user to the `pulse-rt` group:

```
# gpasswd -a <user> pulse-rt

```

### pactl "invalid option" error with negative percentage arguments

`pactl` commands that take negative percentage arguments will fail with an 'invalid option' error. Use the standard shell '--' pseudo argument to disable argument parsing before the negative argument. *e.g.* `pactl set-sink-volume 1 -- -5%`.

### Fallback device is not respected

PulseAudio does not have a true default device. Instead it uses a ["fallback"](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/DefaultDevice/), which only applies to new sound streams. This means previously run applications are not affected by the newly set fallback device.

[gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center), [mate-media](https://www.archlinux.org/packages/?name=mate-media) and [paswitch](https://aur.archlinux.org/packages/paswitch/) handle this gracefully. Alternatively:

1\. Move the old streams in [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) manually to the new sound card.

2\. Stop Pulse, erase the "stream-volumes" in `~/.config/pulse` and/or `~/.pulse` and restart Pulse. This also resets application volumes.

3\. Disable stream device reading. This may be not wanted when using different soundcards with different applications.

 `/etc/pulse/default.pa` 
```
load-module module-stream-restore restore_device=false

```