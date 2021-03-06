Ссылки по теме

*   [Mount (Русский)](/index.php/Mount_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mount (Русский)")

В этом документе описываются способы использования различных USB накопителей в Linux. Это также касается и других устройств, таких как цифровые камеры или телефоны, которые распознаются как обычные USB накопители.

## Contents

*   [1 Монтирование USB устройств](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_USB_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [1.1 Автоматическое монтирование с помощью udev](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_udev)
        *   [1.1.1 Автомонтирование с использованием systemd](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_systemd)
    *   [1.2 Монтирование вручную](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B2.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
        *   [1.2.1 Где взять ядро, поддерживающее usb_storage](#.D0.93.D0.B4.D0.B5_.D0.B2.D0.B7.D1.8F.D1.82.D1.8C_.D1.8F.D0.B4.D1.80.D0.BE.2C_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D1.8E.D1.89.D0.B5.D0.B5_usb_storage)
        *   [1.2.2 Опознавание устройств](#.D0.9E.D0.BF.D0.BE.D0.B7.D0.BD.D0.B0.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
            *   [1.2.2.1 Использование системных имен (node names) ( /sd* )](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D1.85_.D0.B8.D0.BC.D0.B5.D0.BD_.28node_names.29_.28_.2Fsd.2A_.29)
            *   [1.2.2.2 Использование UUID](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_UUID)
        *   [1.2.3 Монтирование USB флэш-памяти](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_USB_.D1.84.D0.BB.D1.8D.D1.88-.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8)
            *   [1.2.3.1 От имени суперпользователя (root)](#.D0.9E.D1.82_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D1.81.D1.83.D0.BF.D0.B5.D1.80.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.28root.29)
            *   [1.2.3.2 От имени обычного пользователя при помощи mount](#.D0.9E.D1.82_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D0.BE.D0.B1.D1.8B.D1.87.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_mount)
            *   [1.2.3.3 От имени обычного пользователя посредством fstab](#.D0.9E.D1.82_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B8_.D0.BE.D0.B1.D1.8B.D1.87.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.D0.BF.D0.BE.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.BE.D0.BC_fstab)

## Монтирование USB устройств

Если у вас свежая система со стандартным ядром Arch и современная [среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола"), USB устройство должно автоматически появляться на рабочем столе при подключении, и лезть в консоль не потребуется.

Если этого не произошло см. далее.

### Автоматическое монтирование с помощью udev

См. [Udev:Автомонтирование USB-устройств](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_USB-.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2 "Udev (Русский)"). Простой способ настройки автомонтирования жестких дисков для однопользовательских систем с использованием udev заключается в следующем: создается файл `/etc/udev/rules.d/automount.rules` со следующим содержимым:

 `ACTION=="add", ENV{DEVTYPE}=="partition", RUN+="domount %N"` 

и исполняемый от root файл `/usr/lib/udev/domount` со следующим содержимым (необходимо вставить корректные для Вашей системы значения):

```
#!/bin/sh

#edit the following variables to suit your needs
MYUID=1000              # your user uid
MYGID=100               # your user gid
MYLOGIN=al              # your login
TERM=lxterminal         # your terminal emulator
MYSHELL=zsh             # your shell
export DISPLAY=:0       # your X display

TMPFILE=/run/automount.$RANDOM
DIR=`cat /etc/fstab | grep -v '#' | grep $* | awk '{print $2;}'`
if [ "x$DIR" = "x" ]; then
        MYUUID=`blkid -o value -s UUID $*`
        if [ "x$MYUUID" = "x" ]; then
                MYUUID="unknown"
        fi
        DIR=/run/media/$MYUUID
fi
mkdir -p /run/media
mkdir -p $DIR
cat > $TMPFILE << EOF
#!/bin/sh
echo "$* will be mounted on $DIR. "
sudo /bin/mount -o uid=$MYUID,gid=$MYGID $* $DIR
cd $DIR
$MYSHELL
cd
sudo /bin/umount $DIR
EOF
chmod a+x $TMPFILE
su $MYLOGIN -c "$TERM -t 'Terminal - $* mounted on $DIR' -e $TMPFILE"
sleep 1; rm -f $TMPFILE

```

При подключении USB-диска происходит автомонтирование и открывается окно терминала. Чтобы размонтировать устройства, просто нажмите Ctrl + D в окне терминала. Место монтирования определяется в `/etc/fstab` или, при его отсутствии, создается на основе UUID раздела.

Чтобы ваш пароль не запрашивался при команде размонтирования, добавьте (заменить на ваше имя пользователя) `имя_пользователя` в `/etc/sudoers` с помощью команды visudo. См. [Sudo (Русский)](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Sudo (Русский)")

 `имя_пользователя	ALL=(ALL) NOPASSWD: /bin/umount` 

Если терминал не появляется проверьте команду его запуска. Например, в xfce4, используется команда "Terminal -T <title> -e <script-file> .

#### Автомонтирование с использованием systemd

Предыдущий способ плох тем что выключает скрипт через 3 минуты, и окно с консолью завершится в любом случае. Поэтому создаем новый файл **/etc/systemd/flash-mount@.service** и пишем туда:

```
[Unit]
Description=Автомонтирование съемных устройств

[Service]
Type=oneshot
ExecStart=/usr/lib/udev/domount %I

[Install]
WantedBy=multi-user.target

```

Теперь отредактируем файл **/etc/udev/rules.d/automount.rules**:

```
ACTION=="add", ENV{DEVTYPE}=="partition", DRIVERS=="usb-storage", ENV{SYSTEMD_WANTS}="flash-mount@%N.service"

```

Теперь скрипт **/usr/lib/udev/domount**, вот улучшенная версия скрипта которая поддерживает русские символы:

```
#!/bin/sh

MYUID=1000              # Ваш uid
MYGID=100               # группа users
MYLOGIN=user            # ваш логин
TERM=xterm         	# ваш эмулятор терминала
MYSHELL=bash            # ваш шелл
export DISPLAY=:0       # Ваш X дисплей

TMPFILE=/run/automount.$RANDOM
DIR=`cat /etc/fstab | grep -v '#' | grep $* | awk '{print $2;}'`
if [ "x$DIR" = "x" ]; then
        MYUUID=`blkid -o value -s UUID $*`
        if [ "x$MYUUID" = "x" ]; then
                MYUUID="unknown"
        fi
        DIR=/run/media/$MYUUID
fi
mkdir -p /run/media
mkdir -p $DIR
cat > $TMPFILE << EOF
#!/bin/sh
echo "$* был примонтирован в $DIR. "
sudo /bin/mount -o iocharset=utf8,uid=$MYUID,gid=$MYGID $* $DIR
cd $DIR
$MYSHELL
sudo /bin/umount -l $DIR
EOF

export LANG=ru_RU.UTF-8
export LC_CTYPE=ru_RU.UTF-8
export LC_NUMERIC=ru_RU.UTF-8
export LC_TIME=ru_RU.UTF-8
export LC_COLLATE=ru_RU.UTF-8
export LC_MONETARY=ru_RU.UTF-8
export LC_MESSAGES=ru_RU.UTF-8
export LC_PAPER=ru_RU.UTF-8
export LC_NAME=ru_RU.UTF-8
export LC_ADDRESS=ru_RU.UTF-8
export LC_TELEPHONE=ru_RU.UTF-8
export LC_MEASUREMENT=ru_RU.UTF-8
export LC_IDENTIFICATION=ru_RU.UTF-8
export LC_ALL=
chmod a+x $TMPFILE

su $MYLOGIN -c "$TERM -e $TMPFILE"
sleep 1
rm -f $TMPFILE
rmdir "$DIR"

```

Теперь применяем правила:

```
udevadm control --reload-rules && udevadm trigger

```

Монтируем флешку и проверяем!

### Монтирование вручную

**Примечание:** Перед тем, как обвинить Arch Linux в том, что он не монтирует USB устройства, стоит проверить все доступные порты. Часть разъёмов могут не обслуживаться контроллером (или не подключены к контроллеру вообще, в случае портов на передней панели), и устройства физически не смогут монтироваться. Теоретически контроллер портов может оказаться выключенным; для того, чтобы это проверить, нужно зайти в BIOS и отыскать параметр с названием вроде "Onboard USB Controller" — должен быть "Enabled".

#### Где взять ядро, поддерживающее usb_storage

Если не используется самодельное (самосборное) ядро, то можно скачать одно из готовых, все имеющиеся ядра Arch Linux настроены должным образом. В случае самосборного ядра, следует убедиться, что при компиляции была включена поддержка SCSI, SCSI-Disk и usb_storage. Если установлена последняя версия [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"), то можно просто подключить носитель, и система автоматически подгрузит все необходимые модули ядра. Более ранним версиям udev дополнительно потребуется наличие HotPlug. Либо то же самое можно сделать вручную:

```
# modprobe usb-storage
# modprobe sd_mod      (только для ядер без SCSI)

```

#### Опознавание устройств

Самое первое, что нужно знать об устройстве, так это его идентификатор, присвоенный ядром.

##### Использование системных имен (node names) ( /sd* )

Это наиболее простой способ, но присвоение имен зависит от порядка, в котором устройства были подключены. способы получения системных имён (именований по шине):

*   поиск среди результатов вывода команды `dmesg` системного имени устройства, для удобства можно использовать в сочетании с `grep`:

```
$ dmesg | egrep "sd[a-z]"

```

*   выполнением команды:

```
# fdisk -l

```

которая отобразит все доступные таблицы разделов.

**Примечание:** Если среди результатов нет устройства, то можно использовать команду `lsusb`, чтобы убедиться, что оно действительно было опознано системой.

##### Использование UUID

Для каждого устройства существует [UUID](https://en.wikipedia.org/wiki/UUID "wikipedia:UUID") (Universally Unique Identifier — уникальный идентификатор как один из методов постоянных именований устройств), эти идентификаторы предназначены для отслеживания устройств в независимости от их системных имен, а значит расположения на шине и порядка обнаружения (например `/dev/sda`).

Чтобы узнать все UUIDы, известные системе, нужно выполнить:

 `# blkid -o list -c /dev/null` 
```
device         fs_type  label     mount point        UUID
------------------------------------------------------------------------------------------
/dev/sda1      ext2               /boot              7f4cef7e-7ee2-489a-b759-d52ba23b692c
/dev/sda2      swap               (not mounted)      a807fff3-e89f-46d0-ab17-9b7ad3efa7b5
/dev/sda3      ext4               /                  81917291-fd1a-4ffe-b95f-61c05cfba76f
/dev/sda4      ext4               /home              c4c23598-19fb-4562-892b-6fb18a09c7d3
/dev/sdb1      ext4     X2        /mnt/X1            4bf265f7-da17-4575-8758-acd40885617b
/dev/sdc1      ext4     X1        /mnt/X2            4bf265f7-da17-4575-8758-acd40885617b
/dev/sdd1      ext4     Y2        /mnt/Y2            8a976a06-3e56-476f-b73a-ea3cad41d915
/dev/sde1      ext4     Z2        /mnt/Z2            9d35eaae-983f-4eba-abc9-434ecd4da09c
/dev/sdf1      ext4     Y1        /mnt/Y1            e2ec37a9-0689-46a8-a07b-0609ce2b7ea2
/dev/sdg1      ext4     Z1        /mnt/Z1            9fa239c1-720f-42e0-8aed-39cf53a743ed
/dev/sdj1      ext4     RAPT      (not mounted)      a9ed7ecb-96ce-40fe-92fa-e07a532ed157
/dev/sdj2      swap               <swap>             20826c74-eb6d-46f8-84d8-69b933a4bf3f

```

*Здесь можно видеть целый список дисков, видимых системой, и длинные строчки с символами. Так вот эти строчки и есть те самые uuidы.*

*   Теперь нужно подключить USB устройство и подождать несколько секунд . . .

*   Заново выполнить `blkid -o list -c /dev/null`

*Появилось новое устройство и UUID? Это и есть USB накопитель*

**Tip:** Если `blkid` не работает так, как ожидалось (или не работает вообще), то можно заглянуть в поисках UUIDов в `/dev/disk/by-uuid/`:
```
$ ls -lF /dev/disk/by-uuid/

```

#### Монтирование USB флэш-памяти

Для этого нужно создать папку, в которую в дальнейшем будет монтироваться флэшка:

```
# mkdir /mnt/usbstick

```

##### От имени суперпользователя (root)

Монтировать устройство рутом при помощи команды (только нужно заменить **device_node** найденным устройством, как было показано выше):

```
# mount **device_node** /mnt/usbstick

```

или

```
# mount -U **UUID** /mnt/usbstick

```

Если `mount` не распознаёт формат устройства (файловой системы), то можно попробовать с ключом `-t <тип файловой системы>`, а также глянуть в [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) для просвещения.

**Примечание:** Если же вообще ничего не помогло, то, возможно, нужно чинить флэшку, см. [Format a device](/index.php/Format_a_device "Format a device"). Но перед этим имеет смысл попробовать на другом компьютере или операционной системе.

##### От имени обычного пользователя при помощи mount

Чтобы непривилегированные пользователи могли записывать данные на USB носитель, нужно прописать следующую команду:

```
$ sudo mount -o gid=users,fmask=113,dmask=002 /dev/sda1 /mnt/usbstick

```

##### От имени обычного пользователя посредством fstab

Для того, чтобы простой поьзователь мог спокойно монтировать USB-накопитель через [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)"), нужно добавить следующую строку в файл `/etc/fstab`:

```
/dev/sda1 /mnt/usbstick vfat **user**,noauto,noatime,flush 0 0

```

или, что ещё лучше:

```
UUID=E8F1-5438 /mnt/usbstick vfat **user**,noauto,noatime,flush 0 0

```

(см. описание для **user** и других параметров в статье [main article](/index.php/Fstab "Fstab"))

**Примечание:** Здесь `/dev/sda1` должно быть заменено на имя флэшки (если оно не /dev/sda1, конечно). Если непонятно, см. [Монтирование USB флэш-памяти](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_USB_.D1.84.D0.BB.D1.8D.D1.88-.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8).

Все, теперь любой пользователь может монтировать флэшку при помощи:

```
$ mount /mnt/usbstick

```

И отмонтировать, используя:

```
$ umount /mnt/usbstick

```

**Примечание:** Извлекать флэшку, не выполнив размонтирование, опасно.