Ссылки по теме

*   [Microcode (Русский)](/index.php/Microcode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Microcode (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Boot loader](/index.php/Boot_loader "Boot loader"). Дата последней синхронизации: 2015-04-01\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Boot_loader&diff=0&oldid=363255).

Загрузчик (boot loader) - это первичная программа, которую запускает [BIOS](https://en.wikipedia.org/wiki/ru:BIOS перед тем как начать [процесс загрузки](/index.php/Arch_boot_process_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch boot process (Русский)"). В Arch вы можете использовать [различные виды](/index.php/Category:Boot_loaders_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Boot loaders (Русский)") загрузчиков, такие как [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)") и [Syslinux](/index.php/Syslinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Syslinux (Русский)"). Некоторые загрузчики поддерживают только BIOS или только UEFI, а некоторые поддерживают и то и то.

Эта страница содержит краткие инструкции для загрузчиков, доступных в Arch. Для подробной информации смотрите соответствующую страницу для нужного вам загрузчика.

## Contents

*   [1 Загрузчики поддерживающие BIOS и UEFI](#Загрузчики_поддерживающие_BIOS_и_UEFI)
    *   [1.1 GRUB](#GRUB)
    *   [1.2 Syslinux](#Syslinux)
    *   [1.3 BURG](#BURG)
*   [2 Загрузчики поддерживающие только UEFI](#Загрузчики_поддерживающие_только_UEFI)
    *   [2.1 Linux Kernel EFISTUB](#Linux_Kernel_EFISTUB)
        *   [2.1.1 systemd-boot](#systemd-boot)
        *   [2.1.2 rEFInd](#rEFInd)
        *   [2.1.3 Clover](#Clover)
    *   [2.2 ELILO](#ELILO)
*   [3 Загрузчики поддерживающие только BIOS](#Загрузчики_поддерживающие_только_BIOS)
    *   [3.1 GRUB Legacy](#GRUB_Legacy)
    *   [3.2 LILO](#LILO)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 UEFI boot loader не отображается в UEFI меню](#UEFI_boot_loader_не_отображается_в_UEFI_меню)
*   [5 Смотритие также](#Смотритие_также)

## Загрузчики поддерживающие BIOS и UEFI

### GRUB

[GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)") самый популярный загрузчик, конфигурационные файлы можно сгенерировать автоматически.

### Syslinux

[Syslinux](/index.php/Syslinux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Syslinux (Русский)") в настоящее время ограничивается загрузкой файлов только из того раздела, куда он установлен.

### BURG

**Примечание:** BURG не поддерживается официально разработчиками Arch.

Смотрете [BURG](/index.php/BURG "BURG").

## Загрузчики поддерживающие только UEFI

### Linux Kernel EFISTUB

Ядро Linux можно загружать непосредственно используя встроенный EFI stub загрузчик. Смотрите [EFISTUB](/index.php/EFISTUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "EFISTUB (Русский)").

#### systemd-boot

systemd включает в себя EFI загрузчик (ранее назывался gummiboot), который предоставляет текстовое меню для загрузки EFISTUB ядер. Смотрите [systemd-boot](/index.php/Systemd-boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-boot (Русский)").

#### rEFInd

rEFInd - это UEFI Boot Manager, который предоставляет графическое меню для загрузки EFISTUB ядер. Смотрите [rEFInd (Русский)](/index.php/REFInd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "REFInd (Русский)").

#### Clover

Clover - это UEFI Boot Manager, который предоставляет графический интерфейс в родном разрешении для загрузки EFISTUB ядер. Смотрите [Clover](/index.php/Clover "Clover").

### ELILO

**Важно:** Разработчики ELILO дали понять, что он больше не находится в активной разработке. Это означает, что не будут добавляться новые функции, а будут только появляться исправления ошибок. Смотрите [https://sourceforge.net/mailarchive/message.php?msg_id=31524008](https://sourceforge.net/mailarchive/message.php?msg_id=31524008) для дополнительной информации. ELILO официально не поддерживается разработчиками Arch.

ELILO - это UEFI версия загрузчика [LILO](/index.php/Graphical_Lilo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Graphical Lilo (Русский)"), поддерживающего только BIOS. Его конфигурационнный файл `elilo.conf` похож на конфигурационный файл для [LILO](/index.php/Graphical_Lilo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Graphical Lilo (Русский)"). Его разработчики предоставляют скомпилированные бинарники, которые доступны на [http://sourceforge.net/projects/elilo/](http://sourceforge.net/projects/elilo/) и AUR пакет в [elilo-efi](https://aur.archlinux.org/packages/elilo-efi/).

## Загрузчики поддерживающие только BIOS

**Примечание:** Данные загрузчики официально не поддерживаются разработчиками Arch.

### GRUB Legacy

GRUB Legacy (также известный как grub-0.97) - это древняя ветка [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"), поддерживающая только BIOS. Смотрите [GRUB Legacy (Русский)](/index.php/GRUB_Legacy_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB Legacy (Русский)").

### LILO

Смотрите [Graphical Lilo (Русский)](/index.php/Graphical_Lilo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Graphical Lilo (Русский)").

## Решение проблем

### UEFI boot loader не отображается в UEFI меню

На некоторых материнских платах с UEFI, таких как платы с чипсетом Intel Z77, добавление записей с помощью `efibootmgr` или `bcfg` из EFI Shell не сработает, поскольку они не будут отображаться в списке меню загрузки после их добавления в NVRAM.

Это происходит потому что данные материнские платы умеют загружать только Microsoft Windows. Чтобы решить эту проблему, вы должны поместить `.efi` файл в том месте, куда его помещает Windows.

Скопируйте файл `bootx64.efi` с установочного носителя Arch Linux (`FSO:`) в директорию Microsoft вашего ESP раздела на вашем жёстком диске (`FS1:`). Сделайте это, загрузив в EFI shell и наберите:

```
FS1:
cd EFI
mkdir Microsoft
cd Microsoft
mkdir Boot
cp FS0:\EFI\BOOT\bootx64.efi FS1:\EFI\Microsoft\Boot\bootmgfw.efi

```

После перезагрузки, все записи, добавленнные в NVRAM должны отображаться в меню загрузки.

## Смотритие также

*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)
*   [Rod Smith - rEFInd, a fork or rEFIt](http://www.rodsbooks.com/refind/)
*   [Linux Kernel Documentation on EFISTUB](https://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob_plain;f=Documentation/x86/efi-stub.txt;hb=HEAD)
*   [Linux Kernel EFISTUB Git Commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=291f36325f9f252bd76ef5f603995f37e453fc60;hp=55839d515495e766605d7aaabd9c2758370a8d27)
*   [Rod Smith's page on EFISTUB](http://www.rodsbooks.com/efi-bootloaders/efistub.html)
*   [rEFInd Documentation for booting EFISTUB Kernels](http://www.rodsbooks.com/refind/linux.html)