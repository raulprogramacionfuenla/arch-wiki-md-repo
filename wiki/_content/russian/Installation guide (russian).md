Этот документ является кратким руководством по установке [Arch Linux](/index.php/Arch_Linux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Linux (Русский)") с официального установочного образа. Перед установкой рекомендуется посмотреть [часто задаваемые вопросы](/index.php/FAQ_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "FAQ (Русский)"). Более подробное описание процесса установки вы можете найти на странице [Руководство для новичков](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%B4%D0%BB%D1%8F_%D0%BD%D0%BE%D0%B2%D0%B8%D1%87%D0%BA%D0%BE%D0%B2 "Руководство для новичков"). Полезную информацию о различных этапах установки также смотрите на страницах в категории [Получение и установка Arch](/index.php/Category:Getting_and_installing_Arch_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Getting and installing Arch (Русский)").

Бóльшую часть ответов на свои вопросы вы сможете найти на этих вики-страницах, а также на [man-страницах](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") конкретных программ; общий обзор процесса настройки смотрите на странице [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt). Получить помощь вы также сможете в [IRC-канале поддержки пользователей](/index.php/IRC_channel "IRC channel"), а также на [англоязычном](https://bbs.archlinux.org/) и [русскоязычном](http://archlinux.org.ru/forum/) форумах Arch Linux.

## Contents

*   [1 Загрузка](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
*   [2 Перед установкой](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.BE.D0.B9)
    *   [2.1 Установка раскладки клавиатуры](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [2.2 Соединение с Интернетом](#.D0.A1.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82.D0.BE.D0.BC)
    *   [2.3 Синхронизация системных часов](#.D0.A1.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D1.85_.D1.87.D0.B0.D1.81.D0.BE.D0.B2)
    *   [2.4 Разбиение дисков на разделы](#.D0.A0.D0.B0.D0.B7.D0.B1.D0.B8.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2_.D0.BD.D0.B0_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8B)
    *   [2.5 Форматирование разделов](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
    *   [2.6 Монтирование разделов](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
*   [3 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [3.1 Выбор зеркал для загрузки](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [3.2 Установка основных пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.3 Настройка системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [3.4 Установка загрузчика](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D0.B0)
    *   [3.5 Перезагрузка](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0)
*   [4 После установки](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)

## Загрузка

Загрузите наиболее свежий установочный ISO-образ Arch Linux со [страницы загрузки Arch Linux](https://www.archlinux.org/download/). Там представлен гибридный образ Arch Linux, позволяющий загружать версии x86_64 и i686 в зависимости от системной архитектуры и выбора пользователя.

Обратите внимание, что никакие пакеты не включены в установочный образ: в процессе установки они будут загружены из удаленного репозитория. Таким образом, для установки потребуется активное подключение к интернету.

После загрузки установочного образа, проверьте его целостность с помощью подписи PGP (выполните `pacman-key -v *inst-image.iso*.sig`) или контрольных сумм (`md5sum *inst-image.iso*`), которые указаны на странице загрузки.

Теперь образ может быть записан на компакт-диск, [на флеш-накопитель](/index.php/USB_flash_installation_media_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "USB flash installation media (Русский)") или просто смонтирован.

## Перед установкой

После загрузки с установочного образа потребуется выполнить некоторые шаги для предварительной подготовки к процессу установки.

### Установка раскладки клавиатуры

По умолчанию используется американская раскладка. Другие раскладки можно загрузить командой `loadkeys *файл_keymap*`: файлы keymap вы найдете в каталоге `/usr/share/kbd/keymaps/` (путь и расширение можно опустить).

### Соединение с Интернетом

Служба DHCP уже запущена при загрузке для найденных Ethernet-адаптеров (смотрите также [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети")). Для беспроводных сетевых адаптеров запустите `wifi-menu` чтобы соединиться с беспроводной сетью (смотрите также [Настройка беспроводной сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B1%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D0%B5%D1%82%D0%B8 "Настройка беспроводной сети")). Если необходимо настроить статический IP или использовать другие средства настройки сети, остановите службу DHCP командой `systemctl stop dhcpcd.service` и используйте [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)").

### Синхронизация системных часов

Смотрите страницу [Systemd-timesyncd (Русский)](/index.php/Systemd-timesyncd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-timesyncd (Русский)").

### Разбиение дисков на разделы

Смотрите страницу [Разметка дисков](/index.php/%D0%A0%D0%B0%D0%B7%D0%BC%D0%B5%D1%82%D0%BA%D0%B0_%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2 "Разметка дисков"); возможно, потребуется создать некоторые служебные разделы: смотрите [UEFI#EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI") и [GRUB#GUID Partition Table (GPT) specific instructions](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). Если вы хотите создать блочное устройство для [LVM](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"), [disk encryption](/index.php/Disk_encryption "Disk encryption") или [RAID](/index.php/RAID "RAID"), сделайте это сейчас.

### Форматирование разделов

Смотрите раздел [File systems#Create a filesystem](/index.php/File_systems#Create_a_filesystem "File systems") и статью [Swap](/index.php/Swap "Swap").

### Монтирование разделов

Смонтируйте корневой раздел в `/mnt`. После этого вы можете создать каталоги для отдельных разделов (`/mnt/boot`, `/mnt/home` и т. д.) и смонтировать их, а также активировать ваш раздел подкачки если вы хотите, чтобы эти разделы впоследствии были определены *genfstab*.

## Установка

### Выбор зеркал для загрузки

Отредактируйте `/etc/pacman.d/mirrorlist` для выбора зеркал для загрузки среди доступных. Местные серверы зеркал обычно работают быстрее; однако, вы можете выбирать и по другим критериям; смотрите также страницу [Зеркала](/index.php/%D0%97%D0%B5%D1%80%D0%BA%D0%B0%D0%BB%D0%B0 "Зеркала"). Эта копия файла `mirrorlist` будет впоследствии перенесена на установленную систему, поэтому полезно сразу выбрать наиболее подходящие зеркала.

### Установка основных пакетов

Используйте скрипт [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) для установки группы пакетов [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base

```

Другие пакеты или группы могут быть установлены здесь же (для этого просто укажите их имена через пробел).

### Настройка системы

Сгенерируйте файл [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") (используйте ключ `-U` или `-L`, чтобы для идентификации разделов использовались UUID или метки, соответственно):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

[Перейдите к корневому каталогу](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Change root (Русский)") новой системы:

```
# arch-chroot /mnt

```

Установите [имя хоста](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D1.83.D0.B7.D0.BB.D0.B0 "Network configuration (Русский)"):

```
# echo *имя_хоста* > /etc/hostname

```

Задайте [часовой пояс](/index.php/Time_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A7.D0.B0.D1.81.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BF.D0.BE.D1.8F.D1.81 "Time (Русский)"):

```
# ln -sf /usr/share/zoneinfo/*зона*/*субзона* /etc/localtime

```

Включите [локали](/index.php/Locale_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Locale (Русский)"), раскомментировав их в `/etc/locale.gen`, после чего сгенерируйте их:

```
# locale-gen

```

Укажите настройки локалей в `/etc/locale.conf`, и, если нужно, в `$HOME/.config/locale.conf`:

```
# echo LANG=*ваша_локаль* > /etc/locale.conf

```

Добавьте [набор клавиш](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") консоли и [шрифты](/index.php/Fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A8.D1.80.D0.B8.D1.84.D1.82_.D0.B2_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8 "Fonts (Русский)") в `/etc/vconsole.conf`.

Снова настройте сеть для нового окружения: смотрите страницы [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети") и [Настройка беспроводной сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B1%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D0%B5%D1%82%D0%B8 "Настройка беспроводной сети").

Настройте `[/etc/mkinitcpio.conf](/index.php/Mkinitcpio "Mkinitcpio")` если нужны дополнительные возможности *mkinitcpio*. Создайте новый ramdisk:

```
# mkinitcpio -p linux

```

Установите пароль суперпользователя:

```
# passwd

```

### Установка загрузчика

Смотрите статью [Загрузчики](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA%D0%B8 "Загрузчики").

### Перезагрузка

Выйдите из окружения chroot, набрав `exit` или нажав `Ctrl+D`.

Также вы можете размонтировать все разделы с помощью команды `umount -R /mnt{boot,home,}` , чтобы убедиться в том, что ни один из разделов не остался занят какой-либо программой. Если нужно, используйте [fuser](https://en.wikipedia.org/wiki/fuser_(Unix) для поиска таких программ.

Теперь перезагрузите компьютер, набрав `reboot`: если какие-нибудь разделы остались смонтированными, они будут автоматически размонтированы [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"). Не забудьте извлечь установочный диск. После загрузки войдите в систему в качестве суперпользователя.

## После установки

Дополнительные шаги по настройке системы после установки вы можете найти на странице [Основные рекомендации](/index.php/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BA%D0%BE%D0%BC%D0%B5%D0%BD%D0%B4%D0%B0%D1%86%D0%B8%D0%B8 "Основные рекомендации").

Множество интересных и полезных программ вы найдете на странице [Список приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Список приложений").