Ссылки по теме

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [grub-gfx (Русский)](/index.php/Grub-gfx_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Grub-gfx (Русский)")
*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")

[GNU GRUB](http://www.gnu.org/software/grub/) это [Многосистемный](http://www.gnu.org/software/grub/manual/multiboot/) загрузчик. Он является ответвлением от GRUB,(GRand Unified Bootloader), который был разработан Эриком Стефаном Болейном (Erich Stefan Boleyn).

Вкратце, *загрузчик* - это первая программа, которая загружается при старте компьютера. Она отвечает за загрузку и передачу управления ядру Linux. Ядро, в свою очередь, запускает остальную часть операционной системы.

В данный момент, GRUB де-факто является стандартным загрузчиком LINUX, и в скором времени будет заменён на [GRUB2](/index.php/GRUB2 "GRUB2"). Когда это случится, "GRUB" сменит свое текущее название на "GRUB Legacy".

## Contents

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Определение корневой директории для GRUB](#Определение_корневой_директории_для_GRUB)
    *   [2.2 Двойная загрузка с Windows](#Двойная_загрузка_с_Windows)
    *   [2.3 Двойная загрузка с GNU/Linux](#Двойная_загрузка_с_GNU/Linux)
    *   [2.4 chainloader and configfile](#chainloader_and_configfile)
*   [3 Установка загрузчика](#Установка_загрузчика)
    *   [3.1 Установка в MBR](#Установка_в_MBR)
    *   [3.2 Установка в раздел](#Установка_в_раздел)
    *   [3.3 Альтернативный метод (grub-install)](#Альтернативный_метод_(grub-install))
*   [4 Советы и трюки](#Советы_и_трюки)
    *   [4.1 Загрузка в графическом режиме](#Загрузка_в_графическом_режиме)
    *   [4.2 Видеорежим](#Видеорежим)
        *   [4.2.1 vbetest](#vbetest)
        *   [4.2.2 hwinfo](#hwinfo)
        *   [4.2.3 Видеорежимы, детектируемые GRUB](#Видеорежимы,_детектируемые_GRUB)
    *   [4.3 Метки разделов](#Метки_разделов)
    *   [4.4 Парольная защита](#Парольная_защита)
    *   [4.5 Перезагрузка в ОС по выбору](#Перезагрузка_в_ОС_по_выбору)
    *   [4.6 Взаимодействие LILO и GRUB](#Взаимодействие_LILO_и_GRUB)
    *   [4.7 Загрузочная дискета GRUB](#Загрузочная_дискета_GRUB)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 GRUB Error 17](#GRUB_Error_17)
    *   [5.2 Случайная установка GRUB в раздел Windows](#Случайная_установка_GRUB_в_раздел_Windows)
    *   [5.3 Редактирование параметров GRUB из меню загрузки](#Редактирование_параметров_GRUB_из_меню_загрузки)
    *   [5.4 Ошибка device.map](#Ошибка_device.map)
    *   [5.5 Выбор ОС при перезагрузке KDE не работает](#Выбор_ОС_при_перезагрузке_KDE_не_работает)
*   [6 Внешние ресурсы](#Внешние_ресурсы)

## Установка

Пакет GRUB устанавливается по умолчанию в процессе установки Arch Linux. Если Вы первоначально не отметили для установки данный пакет, его можно установить с помощью:

```
# pacman -S grub

```

После установки пакета дополнительно необходимо установить загрузчик GRUB в загрузочный сектор или на раздел диска, чтобы он смог выполнять загрузку операционной системы(систем). Этот процесс описан в главе [Установка загрузчика](#Установка_загрузчика).

## Настройка

Файл настроек расположен в `/boot/grub/menu.lst`. Отредактируйте этот файл в соответствии с Вашими требованиями.

*   `timeout #` -- время ожидания (в секундах) перед загрузкой операционной системы по умолчанию (`default`).
*   `default #` -- номер записи, соответствующий операционной системе, загружаемой по умолчанию по истечении времени `timeout`.

Пример файла настроек (директория `/boot` расположена на отдельном разделе):

```
/boot/grub/menu.lst

```

```
# Конфигурационный файл для GRUB - The GNU GRand Unified Bootloader
# /boot/grub/menu.lst

# ПРЕОБРАЗОВАНИЕ ИМЕН УСТРОЙСТВ
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,1)
#  /dev/sda3       (hd0,2)
#

#  ВИДЕОРЕЖИМ - РАЗРЕШЕНИЕ ФРЕЙМБУФЕРА (FRAMEBUFFER RESOLUTION)
#     +-------------------------------------------------+
#          | 640x480    800x600    1024x768   1280x1024
#      ----+--------------------------------------------
#      256 | 0x301=769  0x303=771  0x305=773   0x307=775
#      32K | 0x310=784  0x313=787  0x316=790   0x319=793
#      64K | 0x311=785  0x314=788  0x317=791   0x31A=794
#      16M | 0x312=786  0x315=789  0x318=792   0x31B=795
#     +-------------------------------------------------+
#  для более детальной информации о настройках видеорежима:
#  http://wiki.archlinux.org/index.php/GRUB#Framebuffer_Resolution
#
# Совет: Если Вам необходимо разрешение 1024x768, добавьте "vga=773" к строке kernel.
#

# Общие настройки:
timeout   5
default   0
color light-blue/black light-cyan/blue

# Неявная нумерация загрузочных секций начинается с 0

# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda3 ro
initrd /initramfs-linux.img

# (1) Windows
#title Windows
#rootnoverify (hd0,0)
#makeactive
#chainloader +1

```

### Определение корневой директории для GRUB

GRUB должен обладать информацией о том, где в системе находятся его файлы. Это важно, поскольку таких мест может быть несколько (в случае с несколькими операционными системами). Файлы GRUB всегда располагаются в директории `/boot`, которая может находиться на отдельном разделе.

**Примечание:** GRUB присваивает имена устройствам хранения данных иначе, чем это делает ядро.

*   Жесткие диски именуются как **(hdX)**; также именуются и любые USB устройства хранения данных.
*   Нумерация устройств и разделов начинается с нуля. Например, первый обнаруженный BIOS-ом жесткий диск будет иметь имя **(hd0)**. Второе устройство будет иметь имя **(hd1)**. Тот же принцип верен и для разделов. Например, второй раздел на первом жестком диске будет именоваться **(hd0,1)**.

Если Вы не уверены где в Вашем случае находится `/boot`, используйте команду `find` во встроенной командной оболочке GRUB. Для того чтобы открыть командную оболочку, наберите:

```
# grub

```

Ниже приведен пример для систем *без отдельного* раздела под `/boot`, т.е. когда `/boot` является обычной директорией внутри корневой директории `/`:

```
grub> find /boot/grub/stage1

```

Следующий пример для систем *с отдельным* разделом `/boot`:

```
grub> find /grub/stage1

```

GRUB найдет нужный файл и выведет местоположение файла stage1, нарпимер:

```
(hd1,0)

```

Полученное значение должно быть указано в строке `root` в Вашем файле настроек. Для выхода из командной оболочки наберите `quit`.

### Двойная загрузка с Windows

Добавьте следующие строки в конец Вашего `/boot/grub/menu.lst` (подразумевается, что Windows установлена на первый раздел первого диска):

```
title Windows
rootnoverify (hd0,0)
makeactive #если Вы используете Windows 7, закомментируйте эту строку
chainloader +1

```

**Примечание:** Windows, начиная с версии 2000, НЕ требует для нормальной загрузки, чтобы система располагалась на первом разделе диска (вопреки распространенному заблуждению). Если по какой-либо причине изменился номер раздела с уже установленной Windows (например, если Вы добавили раздел перед существующим разделом с Windows), Вам необходимо внести соответствующие изменения в файл `boot.ini` (см. [эту статью](http://vlaurie.com/computers2/Articles/bootini.htm) для более детальной информации).

Если Windows расположена на другом жестком диске, необходимо использовать команду map. Тогда Windows будет считать, что она установлена на первый жесткий диск. Предположим, что Windows установлена на первый раздел второго диска:

```
title Windows
map (hd0) (hd1)
map (hd1) (hd0)
rootnoverify (hd1,0)
makeactive #если Вы используете Windows 7, закомментируйте эту строку
chainloader +1

```

### Двойная загрузка с GNU/Linux

Вы можете указать настройки, подобные тем, которые определяет сам Arch Linux во время установки, например:

```
title Other Linux
root (hd0,2)
kernel /path/to/kernel root=/dev/sda3 ro
initrd /path/to/initrd

```

Однако могут потребоваться дополнительные параметры, или может не использоваться начальный RAM диск. Проверьте содержимое файла `/boot/grub/menu.lst` в других установленных дистрибутивах, чтобы выяснить корректные значения параметров загрузки, но лучшим решением будет использование команд [chainloader and configfile](#chainloader_and_configfile)

### `chainloader` and `configfile`

Для облегчения процесса дальнейшего сопровождения системы, рекомендуется использовать команды `chainloader` и `configfile` для загрузки дистрибутивов, имеющих механизмы "автоматической" настройки параметров GRUB (например, Debian, Ubuntu, OpenSUSE). Таким образом, дистрибутивы будут самостоятельно управлять параметрами своей загрузки, в т.ч. и `menu.lst`.

*   Команда загрузки `chainloader` выполнит вызов другого загрузчика, вместо того, чтобы загружать образ ядра. Эта функция удобна в случае, если в загрузочной записи раздела есть установленный загрузчик (например, GRUB). Таким образом, мы можем установить "главный" GRUB в главную загрузочную запись (MBR), и, дополнительно для каждого дистрибутива, установить GRUB в загрузочные записи разделов(PBR), на которых они установлены.

*   Команда `configfile` сообщает GRUB, что он должен загрузить определенный конфигурационный файл. Эта возможность используется для подгрузки файла `menu.lst`, который принадлежит другому дистрибутиву. При этом не требуется обязательное наличие отдельно установленного GRUB для этого дистрибутива. Однако главным недостатком такого подхода является возможная несовместимость установленного GRUB с "чужим"`menu.lst`, поскольку некоторые дистрибутивы вносят существенные модификации в свои версии GRUB.

Например, GRUB устанавливается в [MBR](/index.php/MBR "MBR"), а другой загрузчик (это может быть GRUB или [LILO](/index.php/LILO_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LILO (Русский)")) уже установлен в загрузочный сектор `(hd0,2)`.

```
---------------------------------------------
|   |           |           |   %           |
| M |           |           | B %           |
| B |  (hd0,0)  |  (hd0,1)  | L %  (hd0,2)  |
| R |           |           |   %           |
|   |           |           |   %           |
---------------------------------------------
  |                           ^
  |       chainloading        |
  -----------------------------

```

В данном случае достаточно прописать в `menu.lst`:

```
title Other Linux
root (hd0,2)
chainloader +1

```

Если загрузчиком в `(hd0,2)` является GRUB, можно использовать команду `configfile`:

```
title Other Linux
root (hd0,2)
configfile /boot/grub/menu.lst

```

Команда `chainloader` также может быть использована для запуска загрузчика расположенного в MBR на другом диске.

```
title Other drive
rootnoverify (hd1)
chainloader +1

```

## Установка загрузчика

GRUB может быть установлен с отдельного носителя (например, с LiveCD), или путем установки из-под запущенного Arch Linux. Переустановка загрузчика GRUB требуется довольно редко, в ней нет необходимости, когда:

*   Изменился конфигурационный файл.
*   Обновлен пакет GRUB.

Установка/переустановка загрузчика *необходима* когда:

*   Загрузчик ещё не установлен.
*   Другая операционная система при установке затерла существующий загрузчик.
*   Загрузчик не стартует по неизвестным причинам.

Несколько замечаний, прежде чем мы продолжим:

*   Убедитесь, что Ваш файл настройки `/boot/grub/menu.lst` не содержит ошибок. Обратитесь к [Определение корневой директории для GRUB](#Определение_корневой_директории_для_GRUB) для того, чтобы убедиться, что имена устройств заданы корректно.
*   Для того чтобы большинство версий BIOS корректно распознало наличие загрузчика, GRUB должен быть установлен в [MBR](/index.php/MBR "MBR") (первый сектор жесткого диска), или в первом разделе первого устройства хранения данных. Для того чтобы позволить различным дистрибутивам управлять настройкой своих опций загрузки, можно использовать несколько экземпляров GRUB, см. [chainloader and configfile](#chainloader_and_configfile) .
*   Для некоторых случаев потребуется установка загрузчика GRUB из-под `chroot` окружения, например для установки загрузчика на RAID-тома, или в случае, когда загрузчик вышел из строя, и Вы не можете загрузить Вашу операционную систему. Для этого вам необходимо выполнить [Change root](/index.php/Change_root "Change root") из-под LiveCD, или другой инсталляции Linux.
*   Файлы `*stage*` должны находиться в `/boot/grub`, что может не соответствовать действительности, если загрузчик не был установлен в процессе установки системы. Данное затруднение может быть разрешено путем копирования необходимых файлов: `cp -a /usr/lib/grub/i386-pc/* /boot/grub`.

Сначала откройте командную оболочку GRUB:

```
# grub

```

Используйте команду `root` с параметром, полученным в результате команды `find` (см.[Определение корневой директории для GRUB](#Определение_корневой_директории_для_GRUB) ), чтобы указать GRUB, какой из разделов содержит stage1 (и, соответственно, там же находится и `/boot`):

```
grub> root (hd1,0)

```

**Tip:** Командная оболочка GRUB поддерживает автодополнение по клавише **Tab**. Если Вы наберете 'root (hd' и нажмете **Tab** дважды, Вы увидите список доступных устройств, аналогично можно получить список доступных разделов. Автодополнение также работает и в загрузочном меню GRUB. Например, если Вы допустили ошибку в конфигурационном файле, вы можете позже в загрузочном меню отредактировать запись, используя автодополнение по клавише **Tab**, чтобы получить подсказку, какое имя устройства/раздела нужно указать вместо ошибочного. См. [Редактирование параметров GRUB из меню загрузки](#Редактирование_параметров_GRUB_из_меню_загрузки).

### Установка в MBR

Следующий пример устанавливает загрузчик GRUB в [MBR](/index.php/MBR "MBR") первого жесткого диска:

```
grub> setup (hd0)

```

### Установка в раздел

Следущий пример устанавливает загрзчик GRUB в первый раздел первого жесткого диска:

```
grub> setup (hd0,0)

```

После выполнения команды `setup`, введите команду `quit`, для того, чтобы выйти из командной оболочки. Если Вы используете chroot, выйдите из chroot окружения и отмонтируйте разделы (см. [exit your chroot and unmount partitions](/index.php/Change_root "Change root")). Теперь выполните перезагрузку системы.

### Альтернативный метод (grub-install)

**Tip:** Этот метод менее надежный, более предпочтительной является установка загрузчика из командной оболочки GRUB.

Используйте команду `grub-install` с именем целевого устройства для установки загрузчика. Например, для установки загрузчика в MBR первого диска:

```
# grub-install /dev/sda

```

grub-install сообщит, удачно ли прошел процесс установки. Если вонзникли проблемы, воспользуйтесь методом установки из командной оболочки GRUB.

## Советы и трюки

Замечания по дополнительным параметрам.

### Загрузка в графическом режиме

Для разного рода "украшений" можно использовать [grub-gfx](/index.php/Grub-gfx "Grub-gfx"). [GRUB2](/index.php/GRUB2 "GRUB2") также предлагает расширенные графические возможности, такие как фоновые изображения и растровые шрифты.

### Видеорежим

Вы можете использовать один из видеорежимов, описанных в примере `menu.lst`, однако, если Вы решили задействовать широкоэкранный LCD монитор с использованием его родного разрешения, то нижеперечисленные советы помогут Вам достичь желаемого.

В статье [Wikipedia](https://en.wikipedia.org/wiki/VESA_BIOS_Extensions#Linux_video_mode_numbers "wikipedia:VESA BIOS Extensions"), представлен расширенный список разрешений фреймбуфера (тех, которые не входят в стандарт VBE). Но при использовании разрешения 1440x900 (`vga=867`) возникают проблемы. Это связано с тем, что производители видеокарт не ограничены стандартом VBE 3, и они могут выбирать номера кодов для видеорежимов, как им заблагорассудится. Именно поэтому эти коды различаются для разных видеокарт (иногда даже и у одного и того же производителя).

Таким образом, вместо использования готовой таблицы, будет лучше воспользоваться методами, описанными ниже, для получения корректного кода видеорежима.

#### vbetest

1.  Установите пакет [lrmi](https://aur.archlinux.org/packages/lrmi/), который содержит утилиту *vbetest* (пользователи системы x86_64 должны использовать [#hwinfo](#hwinfo) вместо *vbetest*)
2.  Запустите *vbetest* от имени суперпользователя
3.  Запомните значение в [ ], соответствующее выбранному Вами видеорежиму
4.  Нажмите `q` для выхода из *vbetest*
    1.  Вы можете проверить выбранный вами видеорежим, достаточно запустить от имени суперпользователя команду `vbetest -m <ваш_код>`. Вы должны увидеть таблицу [такого плана](http://www.phoronix.net/image.php?id=803&image=x_vbespy_5)
5.  Прибавьте **512** к значению, которое Вы получили на предыдущем шаге, и пропишите его в параметр `vga` для соответствующей записи `menu.lst`
6.  Перезагрузите машину и любуйтесь полученным результатом

Например, *vbetest* выдает на компьютере:

```
[356] 1440x900 (256 color palette)
[357] 1440x900 (8:8:8)

```

Значит искомое значение - это 357\. Затем, 357 + 512 = 869, значит необходимо указать **vga=869**. Добавляем полученное значение к строке kernel в файле `menu.lst`, как показано ниже:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=869**

```

**Примечание:**

*   (8:8:8) Глубина цвета 24-bit (то же и для 32bit)
*   (5:6:5) Глубина цвета 16-bit
*   (5:5:5) Глубина цвета 15-bit

#### hwinfo

1.  Установите пакет [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) из [AUR].
2.  Запустите команду `hwinfo --framebuffer` с правами пользователя root.
3.  Выберите код, соответствующий желаемому разрешению.
4.  Используйте полученный 6-ти значный код с префиксом 0x для параметра `vga=` в соотв. записи kernel в `menu.lst`. Если Вы предпочитаете не использовать префикс 0x, тогда необходимо перевести значения кода из шестнадцатеричной системы в десятичную.

Пример вывода команды **hwinfo**:

```
Mode 0x0364: 1440x900 (+1440), 8 bits
Mode 0x0365: 1440x900 (+5760), 24 bits

```

Соответственно срока в `menu.lst` должна иметь вид:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=0x0365**

```

**Примечание:** *vbetest* выдает значения кодов в формате VESA, чтобы преобразовать их в соответствующие коды видеорежимов ядра - необходимо прибавить значение 512\. Команда *hwinfo*, напротив, выдает коды видеорежимов ядра, и не требует дополнительных манипуляций с полученным значением (не считая необязательного перевода в десятичную систему).

#### Видеорежимы, детектируемые GRUB

Существует достаточно простой метод определения кода видеорежима с использованием соотв. возможностей самого GRUB.

В строке kernel укажите, что ядро должно предложить пользователю самостоятельно выбрать код видеорежима во время загрузки.

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=ask**

```

Теперь перезапустите систему. GRUB предложит на выбор список доступных основных видеорежимов, также доступна опция сканирования, для детектирования дополнительных видеорежимов.

Вы можете выбрать любое значение (нужно запомнить это значение, оно понадобится на следующем шаге) и продолжить процесс загрузки.

Выбранное Вами значение кода видеорежима является **шестнадцатеричным**, чтобы использовать его как опцию в строке kernel, переведите данное значение в **десятичную** систему.

Теперь замените значение параметра vga **ask** на десятичное значение кода видеорежима. Например, строка kernel для режима **[369] 1680x1050x32** будет выглядеть:

```
kernel /vmlinuz-linux root=/dev/sda1 ro **vga=873**

```

### Метки разделов

Если Вы периодически меняете (или планируете менять) расположение разделов на диске, или меняете местами сами устройства жестких дисков (вообще, любые действия, которые приводят к тому, что у одного и того же устройства может меняться имя в системе), тогда для Вас имеет смысл адресовать загрузочные устройства не по именам вида **(hdX,Y)** а по меткам. Для установки метки раздела формата ext2, ext3, ext4 используется команда:

```
e2label </dev/drive|partition> label

```

Задайте для устройства метку длиной не более 16 символов, и не содержащую пробелов, в противном случае GRUB не сможет корректно распознать подобную метку. Затем пропишите в `menu.lst` строку вида:

```
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/Arch_Linux ro

```

### Парольная защита

Вы можете установить пароль в конфигурационном файле GRUB для тех операционных систем, которые необходимо защитить от несанкционированной загрузки. Пароль загрузчика GRUB удобно использовать, когда аналогичная возможность BIOS либо не доступна, либо не предоставляет необходимой функциональности.

Сначала выберите пароль (постарайтесь его не забыть в дальнейшем), затем зашифруйте его:

```
# grub-md5-crypt
Password:
Retype password:
$1$ZOGor$GABXUQ/hnzns/d5JYqqjw

```

Затем добавьте строку с зашифрованным паролем в конфигурационный файл GRUB (строка с паролем должна находиться в начальной части файла, чтобы GRUB корректно её обработал):

```
# general configuration
timeout   5
default   0
color light-blue/black light-cyan/blue

password --md5 $1$ZOGor$GABXUQ/hnzns/d5JYqqjw

```

Затем, для каждой операционной системы, которую Вы желаете защитить, добавьте команду `lock`:

```
# (0) Arch Linux
title  Arch Linux
lock
root   (hd0,1)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/Arch_Linux ro
initrd /boot/initramfs-linux.img
```

**Важно:** Если в BIOS отсутствует возможность загрузки с других устройств (таких как CD-привод), и паролем защищены все операционные системы, то будет достаточно проблематично возобновить загрузку в случае, если Вы забыли свой пароль.

### Перезагрузка в ОС по выбору

Если Вам часто приходится перегружаться в другую ОС (например, Windows), иногда бывает утомительным следить за процессом перезагрузки, чтобы не пропустить момент выбора нужной ОС, и случайно, не загрузиться опять в систему по умолчанию. Для решения данной проблемы существует возможность назначения временной "ОС по умолчанию".

Предположим у нас есть файл `menu.lst` с подобными настройками:

```
/boot/grub/menu.lst

```

```
# general configuration:
timeout 10
default 0
color light-blue/black light-cyan/blue

# (0) Arch
title  Arch Linux
root (hd0,1)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/ARCH ro
initrd /boot/initramfs-linux.img

# (1) Windows
title Windows XP
rootnoverify (hd0,0)
makeactive
chainloader +1

```

Текущей ОС по умолчанию является Arch (0). Измените значение `default 0` на `default saved` - теперь при загрузке, номер ОС по умолчанию будет взят из файла `default` в папке GRUB. Запись в файл `default` выполняет команда **savedefault**, поэтому добавьте `savedefault 0` в конец объявления параметров Windows. Таким образом, мы добьемся того, что когда загружается Windows - системой по умолчанию снова становится Arch (даже если до этого системой по умолчанию была Windows).

Теперь, всё, что нам нужно - это найти простой способ установки значения **ОС по умолчанию**. Такую возможность предоставляет команда `grub-set-default`. Например, чтобы из Arch перегрузиться сразу в Windows, наберите команду:

```
 sudo grub-set-default 1 && sudo shutdown -r now

```

Возможно Вы захотите [разрешить пользователям выключение системы](/index.php/%D0%A0%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B8%D1%82%D1%8C_%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8F%D0%BC_%D0%B2%D1%8B%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Разрешить пользователям выключение системы") без необходимости ввода пароля root. Такую же процедуру необходимо выполнить и для команды `grub-set-default`.

### Взаимодействие LILO и GRUB

Если в ваше системе установлен пакет [LILO](/index.php/LILO "LILO"), удалите его.

```
pacman -R lilo

```

При выполнении некоторых задач (например при компилировании ядра с командой `make all`) пакет LILO может значиться в зависимостях, и может быть автоматически установлен в систему, при этом загрузчик GRUB будет затерт.

**Примечание:** Команда `pacman -R lilo` удалит пакет из системы, но не удалит загрузчик LILO из MBR. Загрузчик LILO, находящийся в MBR может быть перезаписан только в процессе установки другого загрузчика (например, GRUB).

### Загрузочная дискета GRUB

Для начала отформатируйте дискету:

```
 fdformat /dev/fd0
 mke2fs /dev/fd0

```

Затем подмонтируйте её:

```
 mount -t ext2 /dev/fd0 /mnt/fl

```

Установите GRUB на дискету:

```
 grub-install --root-directory=/mnt/fl '(fd0)'

```

Скопируйте Ваш `menu.lst` на дискету:

```
 cp /boot/grub/menu.lst /mnt/fl/boot/grub/menu.lst

```

И, в завершение, отмонтируйте дискету:

```
 umount /mnt/fl

```

Теперь, в случае возникновения проблем с загрузкой, Вы можете загрузить Вашу систему используя загрузочную дискету GRUB.

Дополнительная информация: [Super GRUB Disk](http://www.supergrubdisk.org/)

## Решение проблем

### GRUB Error 17

В случае неразберихи с таблицей разделов, всё что Вы можете наблюдать при попытке загрузки системы - это лаконичное сообщение "GRUB error 17". Существует несколько причин, которые могут привести к искажению таблицы разделов. Чаще всего подобные проблемы связаны с изменением порядка разделов, в результате работы пользователя с программой [GParted](/index.php/GParted "GParted"). Например, Вы удалили раздел `/dev/sda6`, затем изменили размер раздела `/dev/sda7`, и, наконец, создали заново раздел, который, как ожидалось, снова должен стать `/dev/sda6`. Однако этот новый раздел получит, например, имя `/dev/sda9`.

Исправить таблицу разделов достаточно легко. Для этого загрузитесь с Live-CD, войдите в систему как root и запустите команду:

```
# fdisk /dev/sda

```

Затем войдите в режим *e[x]tra/expert*. Далее *[f]ix the partition order*, и сохраните таблицу *[w]rite*. Затем выйдите из программы fdisk. Проверить состояние таблицы разделов после исправления можно с помощью команды `fdisk -l`. Теперь осталось исправить параметры GRUB, см. предыдущую секцию [Установка загрузчика](#Установка_загрузчика).

Обычно, всё что Вам нужно - это указать корректное расположение директории `/boot` и перезаписать загрузчик, находящийся в [MBR](/index.php/MBR "MBR"). Например:

```
# grub

```

```
grub> root (hd0,6)
grub> setup (hd0)
grub> quit

```

Более детальная информация о "GRUB Error 17" доступна [по ссылке](http://stringofthoughts.wordpress.com/2009/05/24/grub-error-17-debianubuntu)

### Случайная установка GRUB в раздел Windows

Если Вы случайно установили GRUB на раздел с Windows, GRUB запишет определенные данные в загрузочный сектор раздела, затерев при этом ссылку на загрузчик Windows.

Для восстановления загрузочной записи Вам понадобится загрузочный диск с консолью восстановления (Windows Recovery Console) для вашей версии Windows. Поскольку многие поставщики не предоставляют загрузочные диски для восстановления (а создают скрытые разделы для восстановления системы), Microsoft предоставляет возможность скачать эти инструменты. Если Вы использете XP, перейдите [по этой ссылке](http://tips.vlaurie.com/2006/05/recovery-console-for-those-without-an-xp-disk/), чтобы получить возможность использовать дискету в качестве диска восстановления (Recovery CD). Загрузитесь с диска Recovery CD (или войдите в режим Recovery c установочного диска), и запустите команду `fixboot`, чтобы восстановить загрузочный сектор. После этого вам снова придется устанавливать GRUB, ---только теперь установите его в MBR, а не в раздел с Windows---.

Более детальная информация: [ссылка](/index.php/MBR#Restoring_a_Windows_boot_record "MBR").

### Редактирование параметров GRUB из меню загрузки

Выбрав один из пунктов в меню загрузки, Вы можете отредактировать его нажав клавишу **e**. Использйте автодополнение по клавише **Tab**, чтобы получить подсказку по доступным именам устройств/разделов, используте клавишу **Esc** для выхода. После того, как Вы отредактировали запись, можете попытаться загрузить её, нажав клавишу **b**. Внесенные Вами изменения **не будут сохранены**.

### Ошибка device.map

Если во время устаноки, или во время загрузки появляются ошибки с упоминанием файла `/boot/grub/device.map`, необходимо выполнить команду:

```
# grub-install --recheck /dev/sda

```

для того, чтобы GRUB пересоздал таблицу устройств, даже если она уже существует. Это может потребоваться после изменения разделов, или добавления/удаления жесткик дисков.

### Выбор ОС при перезагрузке KDE не работает

Если в окне перезагрузки KDE Вы открыли подменю со списком операционных систем, выбрали нужную ОС, перегрузили компьютер, и по прежнему загрузились в ОС по умолчанию, вместо выбранной, тогда проверьте наличие строки

```
default saved

```

В Вашем `/boot/grub/menu.lst`.

## Внешние ресурсы

*   [GNU GRUB](http://www.gnu.org/software/grub/)
*   [GRUB Grotto](http://www.troubleshooters.com/linux/grub/index.htm)
*   [Linux Kernel Documentation :: kernel-perameters.txt](http://www.mjmwired.net/kernel/Documentation/kernel-parameters.txt)
*   [List of kernel parameters with further explanation and grouped by similar options](http://www.kernel.org/pub/linux/kernel/people/gregkh/lkn/lkn_pdf/ch09.pdf)

*   Изучите также [примеры конфигурации GRUB](/index.php?title=%D0%9F%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B_%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D0%B8_GRUB&action=edit&redlink=1 "Примеры конфигурации GRUB (page does not exist)")