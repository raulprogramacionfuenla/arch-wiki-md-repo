CD rippers are designed to extract ("rip") the raw digital audio (in a format commonly called CDDA) from a compact disc to a file or other output. Most CD rippers also support burning audio to a CD and transcoding it on-the-fly.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Ripping](#Ripping)
    *   [2.1 Using a CD ripper](#Using_a_CD_ripper)
    *   [2.2 Using a shell script](#Using_a_shell_script)
*   [3 Post-processing](#Post-processing)
    *   [3.1 Tag editors](#Tag_editors)
    *   [3.2 Converting to other formats](#Converting_to_other_formats)
*   [4 See also](#See_also)

## Introduction

Music is usually stored on audio CDs in an uncompressed format (requires a lot of space, e.g. 700MB for only 80 minutes of audio). Extracting the audio from the CD usually involves compressing it so that it requires less space using:

	Lossless compression

	same quality, less space.

	Lossy compression

	lower quality, much less space.

Most common formats to convert to are: APE and FLAC for lossless and MP3 and OGG for lossy.

## Ripping

### Using a CD ripper

For some examples of CD rippers see: [Optical disc drive#Ripping](/index.php/Optical_disc_drive#Ripping "Optical disc drive").

### Using a shell script

If you want to rip an audio CD gapless and using CD-Text you can use the shell script at [[1]](https://gist.github.com/anonymous/df51d12829bb1dac40e0). You need to [install](/index.php/Install "Install") the [mp3splt](https://www.archlinux.org/packages/?name=mp3splt), [cdrtools](https://www.archlinux.org/packages/?name=cdrtools) and [vorbis-tools](https://www.archlinux.org/packages/?name=vorbis-tools) packages, all available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Post-processing

### Tag editors

For some examples of audio tag editors see: [List of applications#Audio tag editors](/index.php/List_of_applications#Audio_tag_editors "List of applications").

### Converting to other formats

If the CD ripper you used does not support the format you wanted to convert to you can use other encoders/decoders such as [FFmpeg](/index.php/FFmpeg "FFmpeg") or [MEncoder](/index.php/MEncoder "MEncoder"). Some simple scripts to convert from [flac](/index.php/Convert_Flac_to_Mp3 "Convert Flac to Mp3") to MP3 can also be found on the wiki.

## See also

*   RIAA and actual laws allow backup of physically obtained media under these conditions [RIAA - The Law](https://www.riaa.com/physicalpiracy.php?content_selector=piracy_online_the_law).