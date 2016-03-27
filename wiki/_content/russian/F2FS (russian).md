[F2FS](https://en.wikipedia.org/wiki/ru:F2FS "wikipedia:ru:F2FS") (Flash-Friendly File System) — файловая система, ориентированная на использование с накопителями на основе NAND флэш-памяти. Поддержка файловой системы F2FS включена в ядро Linux начиная с 3.8.

## Создание раздела F2FS

Для того, чтобы создать раздел F2FS, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Создание раздела:

```
# mkfs.f2fs -l mylabel */dev/sdxY*

```

где `*/dev/sdxY*` — раздел для форматирования в F2FS.

## Монтирование раздела F2FS

Пользователю, скорее всего, понадобится вручную загрузить модуль ядра F2FS перед монтированием раздела. Выполните с правами суперпользователя:

```
# modprobe f2fs

```

После этого можно смонтировать раздел:

```
# mount -t f2fs */dev/sdxY* /mnt

```

## Установка Arch Linux на раздел F2FS

В [последних релизах](https://www.archlinux.org/download/) стало возможным установить корневой каталог Arch Linux в раздел с файловой системой F2FS:

1.  Создайте корневой раздел с F2FS, как описано в разделе [#Создание раздела F2FS](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0_F2FS).
2.  Создайте отдельный раздел для `/boot` с ext2 или любой другой файловой системой, поддерживаемой загрузчиком.
3.  Продолжите процесс установки согласно [Руководство для новичков#Монтирование разделов](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%B4%D0%BB%D1%8F_%D0%BD%D0%BE%D0%B2%D0%B8%D1%87%D0%BA%D0%BE%D0%B2#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2 "Руководство для новичков") в сеансе [chroot](/index.php/Change_root "Change root").
4.  Также установите пакет [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) в только что установленную систему
5.  Не выходя из сеанса chroot пересоздайте образ initramfs.

Обратите внимание, что теперь не требуется изменять `/etc/mkinitpcio.conf`, так как хук `filesystems` сам добавляет модуль f2fs в образ initramfs.