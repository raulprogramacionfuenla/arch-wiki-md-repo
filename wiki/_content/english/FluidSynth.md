[FluidSynth](http://www.fluidsynth.org/) is a real-time software synthesizer based on the SoundFont 2 specifications. It is required by [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad), and thus is installed as a dependency of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group.

## Contents

*   [1 Installing FluidSynth](#Installing_FluidSynth)
*   [2 How to use FluidSynth](#How_to_use_FluidSynth)
    *   [2.1 Standalone mode](#Standalone_mode)
    *   [2.2 ALSA daemon mode](#ALSA_daemon_mode)
*   [3 How to convert MIDI to OGG](#How_to_convert_MIDI_to_OGG)

## Installing FluidSynth

The first step is to [install](/index.php/Install "Install") the [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth) package.

**However, FluidSynth will not produce any sound yet**. This is because FluidSynth does not include any instrument samples. To produce sound, instrument patches and/or soundfonts need to be installed and fluidsynth configured so it knows where to find them. You can install [SoundFont sample](/index.php/Timidity#SoundFonts "Timidity").

## How to use FluidSynth

There are two ways to use FluidSynth. Either as MIDI player or as daemon adding MIDI support to ALSA.

### Standalone mode

You can simply use fluidsynth to play MIDI files:

```
$ fluidsynth -a alsa -m alsa_seq -l -i /usr/share/soundfonts/FluidR3_GM2-2.sf2 example.midi

```

assuming than you installed [soundfont-fluid](https://www.archlinux.org/packages/?name=soundfont-fluid).

There are many other options to fluidsynth; see manpage or use -h to get help.

One may wish to use pulseaudio instead of alsa as the argument to the -a option.

### ALSA daemon mode

If you want fluidsynth to run as ALSA daemon, edit `/etc/conf.d/fluidsynth` and add your soundfont along with any other changes you would like to make. For e.g., fluidr3:

```
SOUND_FONT=/usr/share/soundfonts/FluidR3_GM2-2.sf2
AUDIO_DRIVER=alsa
OTHER_OPTS='-is -m alsa_seq -r 48000'

```

After that, you can [start/enable](/index.php/Start/enable "Start/enable") the fluidsynth service.

The following will give you an output software MIDI port (in addition of hardware MIDI ports on your system, if any):

 `$ aconnect -o` 
```
client 128: 'FLUID Synth (5117)' [type=user]
   0 'Synth input port (5117:0)'
```

An example of usage for this is aplaymidi:

```
$ aplaymidi -p128:0 example.midi

```

## How to convert MIDI to OGG

Simple command lines to convert midi to ogg:

```
$ fluidsynth -nli -r 48000 -o synth.cpu-cores=2 -T oga -F example.ogg /usr/share/soundfonts/fluidr3/FluidR3GM.SF2 example.MID

```

Here's a little script to convert multiple midi files to ogg in parallel:

```
#!/bin/bash
maxjobs=$(grep processor /proc/cpuinfo | wc -l)
midi2ogg() {
	name=$(echo $@ | sed -r s/[.][mM][iI][dD][iI]?$//g | sed s/^[.][/]//g)
	for arg; do 
	fluidsynth -nli -r 48000 -o synth.cpu-cores=$maxjobs -F "/dev/shm/$name.raw" /usr/share/soundfonts/fluidr3/FluidR3GM.SF2 "$@"
	oggenc -r -B 16 -C 2 -R 48000 "/dev/shm/$name.raw" -o "$name.ogg"
	rm "/dev/shm/$name.raw"
	## Uncomment for replaygain tagging
	#vorbisgain -f "$name.ogg" 
	done
}
export -f midi2ogg
find . -regex '.*[.][mM][iI][dD][iI]?$' -print0 | xargs -0 -n 1 -P $maxjobs bash -c 'midi2ogg "$@"' --

```