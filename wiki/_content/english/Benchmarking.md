Benchmarking is the act of measuring performance and comparing the results to another system's results or a widely accepted standard through a unified procedure. This unified method of evaluating system performance can help answer questions such as:

*   Is the system performing as it should?
*   What driver version should be used to get optimal performance?
*   Is the system capable of doing task x?

Many tools can be used to determine system performance, the following provides a list of tools available.

## Contents

*   [1 Standalone tools](#Standalone_tools)
    *   [1.1 glxgears](#glxgears)
    *   [1.2 UnixBench](#UnixBench)
    *   [1.3 interbench](#interbench)
    *   [1.4 ttcp](#ttcp)
    *   [1.5 iperf](#iperf)
    *   [1.6 time](#time)
    *   [1.7 hdparm](#hdparm)
    *   [1.8 Unigine Engine](#Unigine_Engine)
*   [2 Software suites](#Software_suites)
    *   [2.1 Bonnie++](#Bonnie.2B.2B)
    *   [2.2 IOzone](#IOzone)
    *   [2.3 HardInfo](#HardInfo)
    *   [2.4 Phoronix Test Suite](#Phoronix_Test_Suite)
    *   [2.5 PTS Desktop Live](#PTS_Desktop_Live)
*   [3 Flash media](#Flash_media)

## Standalone tools

### glxgears

glxgears is a popular OpenGL test that renders a very simple OpenGL performance and outputs the frame rate. Though glxgears can be useful as a test of direct rendering capabilities of the graphics driver, it is an outdated tool that is not representative of the current state of GNU/Linux graphics and overall OpenGL possibilities. glxgears only tests a small segment of the OpenGL capabilities that might be used in a game. Performance increases noted in glxgears will not necessarily be realized in any given game. See [here](http://wiki.cchtml.com/index.php/Glxgears_is_not_a_Benchmark) for more information.

glxgears can be installed via the [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) and [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos) (for [Multilib](/index.php/Multilib "Multilib")) packages.

### UnixBench

A unixbench package is available in the [AUR](/index.php/AUR "AUR"): [unixbench](https://aur.archlinux.org/packages/unixbench/). To run benchmark run *ubench* in terminal.

See also:

*   [https://github.com/kdlucas/byte-unixbench](https://github.com/kdlucas/byte-unixbench)
*   [https://github.com/kdlucas/byte-unixbench/blob/master/UnixBench/USAGE](https://github.com/kdlucas/byte-unixbench/blob/master/UnixBench/USAGE)

### interbench

interbench is an application designed to benchmark interactivity in Linux. It is designed to measure the effect of changes in Linux kernel design or system configuration changes such as CPU, I/O scheduler and filesystem changes and options.
**Tip:** With careful benchmarking, different hardware can be compared.

interbench is available in the [AUR](/index.php/AUR "AUR"): [interbench](https://aur.archlinux.org/packages/interbench/).

See also:

*   [Realtime process management](/index.php/Realtime_process_management "Realtime process management")
*   [Advanced traffic control](/index.php/Advanced_traffic_control "Advanced traffic control")
*   [Linux-ck](/index.php/Linux-ck "Linux-ck")
*   [Linux-pf](/index.php/Linux-pf "Linux-pf")

### ttcp

(n)(nu)ttcp measures point-to-point bandwidth over any network connection. The program must be provided on both nodes between which bandwidth is to be determined.

Various flavors of ttcp can be found in the [AUR](/index.php/AUR "AUR") (see links below).

See also:

*   [ttcp](https://aur.archlinux.org/packages/ttcp/)
*   [nttcp](https://aur.archlinux.org/packages/nttcp/)
*   [nuttcp](https://aur.archlinux.org/packages/nuttcp/)

### iperf

iperf is an easy to use point-to-point bandwidth testing tool that can use either TCP or UDP. It has nicely formatted output and a parallel test mode.

[iperf](https://www.archlinux.org/packages/?name=iperf) can be installed, or a different version of iperf is available with [iperf3](https://www.archlinux.org/packages/?name=iperf3).

### time

The time command provides timing statistics about the command run by displaying the time that passed between invocation and termination. Time is available on most basic linux systems.

```
$ time tar -zxvf archive.tar.gz

```

### hdparm

Storage media can be benchmarked with [Hdparm](/index.php/Hdparm "Hdparm") ([hdparm](https://www.archlinux.org/packages/?name=hdparm)).

See also [Benchmarking/Data storage devices#Using hdparm](/index.php/Benchmarking/Data_storage_devices#Using_hdparm "Benchmarking/Data storage devices").

### Unigine Engine

[Unigine corp.](http://www.unigine.com/) has produced several modern OpenGL benchmarks based on their graphics engine with features such as:

*   Per-pixel dynamic lighting
*   Normal & parallax occlusion mapping
*   64-bit HDR rendering
*   Volumetric fog and light
*   Powerful particle systems: fire, smoke, explosions
*   Extensible set of shaders (GLSL / HLSL)
*   Post-processing: depth of field, refraction, glow, blurring, color correction and much more.

Unigine benchmarks have found recent usage by those looking to overclock their systems. Heaven especially has been used for initial stability testing of overclocks.

These benchmarks can be found in the [AUR](/index.php/AUR "AUR") (see links below).

See also:

*   [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/)
*   [unigine-tropics](https://aur.archlinux.org/packages/unigine-tropics/)
*   [unigine-sanctuary](https://aur.archlinux.org/packages/unigine-sanctuary/)
*   [unigine-valley](https://aur.archlinux.org/packages/unigine-valley/)

## Software suites

### Bonnie++

[bonnie++](https://www.archlinux.org/packages/?name=bonnie%2B%2B) is a C++ rewrite of the [original Bonnie](http://www.textuality.com/bonnie/) benchmarking suite is aimed at performing several tests of hard drive and filesystem performance.

**Note:** The original Bonnie suite does not appear to have been released under the GPL or other compatible license.

See also:

*   [Author's site](http://www.coker.com.au/bonnie++/)
*   [Wikipedia:Bonnie++](https://en.wikipedia.org/wiki/Bonnie%2B%2B "wikipedia:Bonnie++")

### IOzone

IOzone is useful for performing a broad filesystem analysis of a vendor’s computer platform.

This program is available in the [AUR](/index.php/AUR "AUR"): [iozone](https://aur.archlinux.org/packages/iozone/).

See also BBS Article: [iozone to evaluate I/O schedulers... results NOT what you'd expect!](https://bbs.archlinux.org/viewtopic.php?pid=969463).

### HardInfo

[hardinfo](https://www.archlinux.org/packages/?name=hardinfo) can gather information about your system's hardware and operating system, perform benchmarks, and generate printable reports either in HTML or in plain text formats. HardInfo performs CPU and FPU benchmarks and has a very clean GTK-based interface.

See also [Author's site](http://wiki.hardinfo.org/HomePage).

### Phoronix Test Suite

*The [Phoronix Test Suite](http://www.phoronix-test-suite.com/) is the most comprehensive testing and benchmarking platform available that provides an extensible framework for which new tests can be easily added. The software is designed to effectively carry out both qualitative and quantitative benchmarks in a clean, reproducible, and easy-to-use manner.*

*The Phoronix Test Suite is based upon the extensive testing and internal tools developed by Phoronix.com since 2004 along with support from leading tier-one computer hardware and software vendors. This software is open-source and licensed under the GNU GPLv3.*

*Originally developed for automated Linux testing, support to the Phoronix Test Suite has since been added for OpenSolaris, Apple Mac OS X, Microsoft Windows, and BSD operating systems. The Phoronix Test Suite consists of a lightweight processing core (pts-core) with each benchmark consisting of an XML-based profile and related resource scripts. The process from the benchmark installation, to the actual benchmarking, to the parsing of important hardware and software components is heavily automated and completely repeatable, asking users only for confirmation of actions.*

*The Phoronix Test Suite interfaces with OpenBenchmarking.org as a collaborative web platform for the centralized storage of test results, sharing of test profiles and results, advanced analytical features, and other functionality. Phoromatic is an enterprise component to orchestrate test execution across multiple systems with remote management capabilities.*

This suite can be [installed](/index.php/Pacman "Pacman") with the package [phoronix-test-suite](https://www.archlinux.org/packages/?name=phoronix-test-suite). There is also a developmental version available with [phoronix-test-suite-git](https://aur.archlinux.org/packages/phoronix-test-suite-git/).

### PTS Desktop Live

**Warning:** The live image does not look like it has been maintained since 2010.

As an alternative to the installation of the Phoronix Test Suite to the system, Phoronix also provides a Live-CD. This Live-CD offers all the features of the Phoronix Test Suite and includes the latest [ATI](/index.php/ATI "ATI") and [NVIDIA](/index.php/NVIDIA "NVIDIA") binary drivers. It will allow you to run 40+ benchmarks from a live environment without the need to store anything on your hard drive and includes a working GUI interface.

See also:

*   [Official link](http://www.phoronix-test-suite.com/?k=pts_desktop_live)
*   [Documentation](http://www.phoronix-test-suite.com/documentation/2.4/pts_desktop_live.html)

## Flash media

Performance characteristics can be measured quantitatively using [iozone](https://aur.archlinux.org/packages/iozone/). *Sustained* read and write values can, but often do not, correlate to real-world use cases of I/O heavy operations, such as unpacking and writing a number of files on a system update. A relevant metric to consider in these cases is the **random write** speed for small files.

The example invocation tests a 10M file using a 4k record size:

```
$ iozone -e -I -a -s 10M -r 4k -i 0 -i 1 -i 2
...

                                                                random   random
              kB  reclen    write  rewrite    read    reread    read     write
           10240       4      661      649     5802     5822     3892      624

```

**Note:**

*   Test values are reported in KB/s.
*   For performance charts on SD cards and other flash media, see for example [Tom's Hardware](http://www.tomshardware.com/charts/memory-cards,39.html).

See also:

*   [Linux Benchmarking Homepage](http://lbs.sourceforge.net/)
*   [Phoronix.com](http://www.phoronix.com/)
*   [Interbench Homepage](http://users.on.net/~ckolivas/interbench/)
*   [Unigine.com](http://unigine.com/download/)