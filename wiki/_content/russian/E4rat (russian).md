Уменьшение времени загрузки системы и входа в X-ы для файловой системы ext4 с использованием [утиллит e4rat](http://e4rat.sourceforge.net/).

e4rat - проект Andreas Rid и Gundolf Kiefer, расшифровывается как e4 'reduced access time' (сокращение времени доступа), применяется только в файловой системе [ext4](/index.php/Ext4 "Ext4"). В [набор утилит e4rat](http://e4rat.sourceforge.net/) входит: e4rat-collect, e4rat-realloc и e4rat-preload.

## Contents

*   [1 Описание](#.D0.9E.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [1.1 Кому это нужно, а кому нет](#.D0.9A.D0.BE.D0.BC.D1.83_.D1.8D.D1.82.D0.BE_.D0.BD.D1.83.D0.B6.D0.BD.D0.BE.2C_.D0.B0_.D0.BA.D0.BE.D0.BC.D1.83_.D0.BD.D0.B5.D1.82)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.1 e4rat-collect](#e4rat-collect)
    *   [3.2 e4rat-realloc](#e4rat-realloc)
    *   [3.3 e4rat-preload](#e4rat-preload)
    *   [3.4 Альтернатива: e4rat-preload-lite](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.B0:_e4rat-preload-lite)
*   [4 e4rat и различные системы инициализации](#e4rat_.D0.B8_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D0.B8.D0.BD.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8)
*   [5 Bootchart](#Bootchart)
    *   [5.1 bootchart 0.9-9](#bootchart_0.9-9)
    *   [5.2 bootchart2](#bootchart2)
*   [6 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
    *   [6.1 startup.log не создается](#startup.log_.D0.BD.D0.B5_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.B5.D1.82.D1.81.D1.8F)
    *   [6.2 e4rat - отчеты об ошибках в файловой системе ext2](#e4rat_-_.D0.BE.D1.82.D1.87.D0.B5.D1.82.D1.8B_.D0.BE.D0.B1_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B0.D1.85_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B5_ext2)
    *   [6.3 /var/lib/e4rat/startup.log не доступен](#.2Fvar.2Flib.2Fe4rat.2Fstartup.log_.D0.BD.D0.B5_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B5.D0.BD)

## Описание

Если взглянуть на статистику [bootchart](/index.php/Bootchart "Bootchart"), то можно заметить, что при загрузке системы ни жесткий диск, ни CPU не используются полностью. e4rat позволяет максимально задействовать жесткий диск и CPU, ускоряя таким образом процесс загрузки. Все проводится в три этапа:

*   **e4rat-collect** - собирает статистику по используемым файлам в течении определенного времени (по умолчанию 120 секунд, но может быть скорректировано)
*   **e4rat-realloc** - перераспределяет файлы из списка (помещает их в одну область диска)
*   **e4rat-preload** - заранее загружает нужные файлы в память

### Кому это нужно, а кому нет

e4rat может быть полезной в системах с одним пользователем, использующим автозапуск Х-в, при этом также можно ускорить запуск нужных программ. На серверах или при загрузке в CLI - время загрузки системы может снизиться не на много. Для SSD-дисков вообще нет смысла использовать, поскольку у них отсутствуют движущиеся части и, как следствие, отсутствуют (почти) задержки, однако, пользователям таких дисков, может быть полезно ознакомиться с [Ureadahead](/index.php/Ureadahead "Ureadahead").

**Примечание:** **Пользователи ureadahead**, в [официальном руководстве e4rat](http://e4rat.sourceforge.net/wiki/index.php/Main_Page#Ubuntu_and_ureadahead) говориться о том, что ureadahead конфликтует с e4rat. Это может быть верным для Ubuntu, но в Arch Linux эти пакеты возможно будут работать нормально, хотя процесс загрузки, скорее всего, и не ускорится.

Перед использованием e4rat рекомендуется сделать резервные копии изменяемых во избежание потери важных данных.

## Установка

Пакет [e4rat](https://aur.archlinux.org/packages/e4rat/) можно найти в репозитории [community] и установить так:

```
# pacman -S e4rat

```

## Использование

Далее более подробно:

### e4rat-collect

Чтоб e4rat смог создать список файлов, необходимо отредактировать файл `/boot/grub/menu.lst` ([grub](/index.php/Grub "Grub") legacy) или `/boot/grub/grub.cfg` ([grub2](/index.php/Grub2 "Grub2")), добавив в строку загрузки ядра linux следующее:

 `init=/sbin/e4rat-collect` 

Данное действие нужно будет выполнить один раз, поэтому также можно просто отредактировать нужную строку в меню grub на этапе загрузки из командной строки.

После загрузки, в течении 120 секунд, e4rat-collect будет собирать нужную информацию. Поэтому, в течении 2-х минут после загрузки, запустите X-ы, откройте любимый браузер или почтовую программу и т.д., при этом утилита зарегистрирует все запущенные программы и используемые файлы. При необходимости можно изменить стандартное время сбора статистики, для этого отредактируйте файл `/etc/e4rat.conf`. Чтобы вручную завершить работу e4rat-collect, выполните:

 `e4rat-collect -k` 

или

 `pkill e4rat-collect` 

После загрузки и успешного завершения работы e4rat-collect должен появиться файл: `/var/lib/e4rat/startup.log`

Теперь не забудьте удалить команду запуска e4rat-collect из своего файла `menu.lst` или `grub.cfg` (не обязательно, если вы ее добавляли из командной строки [GRUB](/index.php/GRUB "GRUB") в процессе загрузки системы).

### e4rat-realloc

Для запуска процесса перемещения файлов, согласно созданному в предыдущем шаге списку, необходимо перейти в init 1:

 `sudo init 1` 

Авторизоваться в качестве root и выполнить:

 `e4rat-realloc  /var/lib/e4rat/startup.log` 

В зависимости от того, сколько файлов перечислено в `startup.log`, процесс может затянуться на продолжительное время.

**Важно:** Ни в коем случае не прерывайте процесс перемещения файлов, так как это может привести к порче данных и дальнейшей невозможности загрузки системы!

### e4rat-preload

Отредактируйте файл `/boot/grub/menu.lst` ([grub](/index.php/Grub "Grub") legacy) или `/boot/grub/grub.cfg` ([grub2](/index.php/Grub2 "Grub2")), добавив в параметры загрузки ядра:

 `init=/sbin/e4rat-preload` 
**Примечание:** В случае использования grub2, параметры загрузки ядра добавляйте в строку `GRUB_CMDLINE_LINUX="..."` файла `/etc/default/grub`.

Перезагружайтесь и наслаждайтесь.

**Примечание:** После обновления системы может понадобиться выполнить заново все описанные для [#e4rat-collect](#e4rat-collect), [#e4rat-realloc](#e4rat-realloc) и [#e4rat-preload](#e4rat-preload) действия

### Альтернатива: e4rat-preload-lite

[jlindgren](https://bbs.archlinux.org/viewtopic.php?id=117776&p=1) в качестве альтернативы разработал бинарный preload, позволяющий сэкономить несколько секунд при загрузке.

Экономия достигается за счет:

*   использования чистого C без каких-либо зависимостей от внешних библиотек, что позволяет уменьшить количество связанных файлов *.so* с 22 до 3
*   предварительной загрузки первых 100 файлов (таких как дескрипторы и файлы содержимого) перед запуском `/sbin/init`, и дальнейшей загрузки остальных файлов как параллельно, так и в определенной последовательности

[e4rat-preload-lite](https://aur.archlinux.org/packages/e4rat-preload-lite/) можно установить из [AUR](/index.php/AUR "AUR").

Отредактируйте файл `/boot/grub/menu.lst` ([GRUB legacy](/index.php/GRUB_Legacy_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB Legacy (Русский)")) или `/boot/grub/grub.cfg` ([GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)")), добавив в параметры загрузки ядра:

 `init=/usr/sbin/e4rat-preload-lite` 

Перезагружайтесь и наслаждайтесь.

## e4rat и различные системы инициализации

По умолчанию e4rat-collect после завершения будет заменена на /sbin/init. Если вам нужно указать другой PID 1, например /bin/[systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), отредактируйте файл `/etc/e4rat.conf`, раскомментировав в нем строку с нужным параметром **init**

## Bootchart

**Примечание:** Еще находится в разработке и толком не работает - любые предложения приветствуются

Запустите [Bootchart](/index.php/Bootchart "Bootchart") до и после использования e4rat, а затем сравните полученные результаты. Должны появиться видимые изменения.

### bootchart 0.9-9

В этой версии журнал ведется только до запуска [экранного менеджера](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"). Для обхода данного ограничения можно попробовать выполнить следующее (работает не у всех):

В файле `/etc/bootchartd.conf` установите:

 `AUTO_STOP_LOGGER="no"` 

Когда будет нужно остановить работу сервиса - выполните:

 `~# bootchartd stop` 

Для запуска e4rat-preload и bootchart добавив в параметры загрузки ядра:

 `init=/sbin/bootchartd bootchart_init=/sbin/e4rat-preload` 

### bootchart2

Для совместного использования bootchart2 с e4rat отредактируйте `/sbin/bootchartd` и заменить строку `init="/sbin/init"` на `init="/sbin/e4rat-preload"`.

`/etc/bootchartd.conf` от bootchart2 устроен иначе, а строка

```
EXIT_PROC="kdm_greet xterm konsole gnome-terminal metacity mutter compiz ldm icewm-session enlightenment"

```

может быть скорректирована таким образом, что можно будет либо завершать программу вручную (если оставить строку пустой), либо, при запуске указанной в строке программы, bootchart2 будет остановлен автоматически.

## Устранение неполадок

Если что-то не работает - можно попробовать следующее.

### startup.log не создается

*   отключите все проверки в `rc.conf`
*   изучите все сообщения из

```
# dmesg | grep e4rat

```

*   в `e4rat.conf` увеличите значения verbose и loglevel до 31.

### e4rat - отчеты об ошибках в файловой системе ext2

*   в файле `grub.cfg` или `menu.lst` добавьте в параметры загрузки ядра:

```
rootfstype=ext4

```

### /var/lib/e4rat/startup.log не доступен

*   это говорит о том, что /var расположен на отдельном разделе и при загрузке еще не был смонтирован. Вам нужно переместить `startup.log` на раздел который доступен (лучше всего в /etc/e4rat/) и, для сохранения изменений, перенастроить `/etc/e4rat.conf`:

 `startup_log_file /etc/e4rat/startup.log`