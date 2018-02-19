## Contents

*   [1 Booting and startup](#Booting_and_startup)
    *   [1.1 Booting from Arch Linux ISO](#Booting_from_Arch_Linux_ISO)
    *   [1.2 Add entries to UEFI menu](#Add_entries_to_UEFI_menu)
    *   [1.3 Use Secure Boot with trusted EFI executables](#Use_Secure_Boot_with_trusted_EFI_executables)
*   [2 Configuration](#Configuration)
    *   [2.1 Function keys](#Function_keys)
*   [3 Trusted Platform Module](#Trusted_Platform_Module)
*   [4 Hardware identification](#Hardware_identification)

## Booting and startup

### Booting from Arch Linux ISO

In order to boot from the Arch Linux ISO, hit `F2` to enter UEFI settings (InsydeH20 settings v5.0). Then set the supervisor password. From there you can disable Secure Boot and boot from any media.

### Add entries to UEFI menu

[UEFI](/index.php/UEFI "UEFI") will not boot from menu entries created by *efibootmgr*. Use [bcfg](/index.php/Bcfg "Bcfg") in the UEFI Shell (v.2) to add an entry. Boot from the Arch Linux ISO to get a UEFI Shell.

### Use Secure Boot with trusted EFI executables

You can use Secure Boot and mark EFI executables as trusted through the UEFI settings. The executables must end with `.efi`. For example, if you use [EFISTUB](/index.php/EFISTUB "EFISTUB") to boot the Linux kernel directly, you must copy `vmlinuz-linux` to `vmlinuz-linux.efi` and then mark that file as trusted in the UEFI settings. Whenever the executable is updated, it must be removed from the trusted list and then re-added as trusted in the UEFI settings. It is only possible to remove all trusted entries at once, not individually.

See [Secure Boot](/index.php/Secure_Boot "Secure Boot") for other options.

## Configuration

### Function keys

Many function keys work without any need for changing settings. Suspend (`Fn+F4`), blanking the screen (`Fn+F6`), touchpad disable/enable (`Fn-F7`), and keyboard backlight disable/enable (`Fn+F9`) all work. Additionally `Fn+Del` is mapped to `Ins` correctly, as well as `Fn+12` to `Scroll Lock`.

To add functionality for brightness keys (`Fn+Left` and `Fn+Right`) append the following parameters to your kernel boot line:

```
acpi_osi=Linux acpi_backlight=vendor

```

Other function keys are exposed as media keys and can be added as [keyboard shortcuts](/index.php/Keyboard_shortcuts "Keyboard shortcuts") for the desired operation.

| Function Key (`Fn+`) | Media Key |
| `F3` | `XF86WLAN` |
| `F8` | `XF86AudioMute` |
| `Up` | `XF86AudioRaiseVolume` |
| `Down` | `XF86AudioLowerVolume` |
| `Home` | `XF86AudioPlay` |
| `Page Up` | `XF86AudioStop` |
| `Page Down` | `XF86AudioPrev` |
| `End` | `XF86AudioNext` |

## Trusted Platform Module

You may have the following entries in your systemd journal.

```
Feb 17 09:58:29 kernel: platform MSFT0101:00: failed to claim resource 1: [mem 0xfed40000-0xfed40fff]
Feb 17 09:58:29 kernel: acpi MSFT0101:00: platform device creation failed: -16

```

These are related to the Trusted Platform Module (TPM), which can be safely disabled in the UEFI settings if you do not use TPM.

## Hardware identification

 `lsusb` 
```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 0408:a030 Quanta Computer, Inc.
Bus 001 Device 002: ID 04ca:3015 Lite-On Technology Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
 `lspci` 
```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 02)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 620 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1d.3 PCI bridge: Intel Corporation Device 9d1b (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
02:00.0 Network controller: Qualcomm Atheros QCA9377 802.11ac Wireless Network Adapter (rev 31)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTL8411B PCI Express Card Reader (rev 01)
03:00.1 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 12)
```
 `lscpu` 
```
Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              4
On-line CPU(s) list: 0-3
Thread(s) per core:  2
Core(s) per socket:  2
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
CPU family:          6
Model:               142
Model name:          Intel(R) Core(TM) i3-7100U CPU @ 2.40GHz
Stepping:            9
CPU MHz:             700.122
CPU max MHz:         2400.0000
CPU min MHz:         400.0000
BogoMIPS:            4800.00
Virtualization:      VT-x
L1d cache:           32K
L1i cache:           32K
L2 cache:            256K
L3 cache:            3072K
NUMA node0 CPU(s):   0-3
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm arat pln pts hwp hwp_notify hwp_act_window hwp_epp
```