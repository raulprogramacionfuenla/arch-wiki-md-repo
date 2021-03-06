Ссылки по теме

*   [lm sensors (Русский)](/index.php/Lm_sensors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Lm sensors (Русский)")

[hddtemp](https://savannah.nongnu.org/projects/hddtemp/) это небольшая утилита (включающая в состав службу), позволяющая узнать температуру жесткого диска посредством S.M.A.R.T. (для устройств, поддерживающих эту технологию).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
*   [3 Служба](#Служба)
*   [4 Мониторинг](#Мониторинг)
*   [5 Solid State Drives](#Solid_State_Drives)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [hddtemp](https://www.archlinux.org/packages/?name=hddtemp), доступный в [официальных репозиториях](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D1%85 "Официальных репозиториях").

## Использование

Hddtemp требует привилегий суперпользователя. Команда `hddtemp` должна сопровождаться указанием как минимум одного физического устройства или нескольких, разделяемых пробелами. Например:

```
# hddtemp /dev/sd*a* /dev/sd*b* ... /dev/sd*z*

```

## Служба

Запуск службы позволит получить информацию о температуре по TCP/IP, использовать, например, со скриптами.

Эта служба [контролируется](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_юнитов "Systemd (Русский)") `hddtemp.service`.

**Примечание:** аргументы `hddtemp` указаны в файле юнита `/usr/lib/systemd/system/hddtemp.service`. Это особенно важно при использовании нескольких дисков,так как по умолчанию включено отслеживание только для `/dev/sda`. Измените `ExecStart`, [отредактировав](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Редактирование_предоставленных_пакетами_файлов_юнитов "Systemd (Русский)") `hddtemp.service`:

*   Создайте каталог в `/etc/systemd/system`:

```
# mkdir /etc/systemd/system/hddtemp.service.d

```

*   Создайте файл `customexec.conf`, в котором понадобится указать физические диски для отслеживания, например:

 `/etc/systemd/system/hddtemp.service.d/customexec.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/hddtemp -dF /dev/sda /dev/sdb /dev/sdc
```

Вы также можете использовать [скрипт автоматического создания](https://github.com/AndyCrowd/auto-generate-configuration-files/blob/master/gen-customexec.conf-hddtemp.sh), который при помощи [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) обнаруживает все жесткие диски, поддерживаемые [hddtemp](https://www.archlinux.org/packages/?name=hddtemp); в результате чего сгенерированный шаблон файла `customexec.conf` будет отображаться в стандартном выводе.

*   [Перезагрузите systemd](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%B8%D1%82%D0%B5_systemd "Перезагрузите systemd").
*   [Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `hddtemp`.

Чтобы получить информацию о температуре, подключитесь к серверу со включеной службой, которая прослушивает порт 7634.

Посредством [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
$ telnet localhost 7634

```

Посредством [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat):

```
$ nc localhost 7634

```

Вывод будет примерно следующий:

```
|/dev/sda|ST3500413AS|32|C||/dev/sdb|ST2000DM001-1CH164|36|C|

```

Более читаемый вариант:

 `$ nc localhost 7634 |sed 's/|//m' | sed 's/||/ 
/g' | awk -F'|' '{print $1 " " $3 " " $4}'` 
```
/dev/sda 32 C 
/dev/sdb 36 C
```

Для получения дополнительной информации смотрите man-страницу:

```
$ man hddtemp

```

## Мониторинг

Hddtemp может быть встроен в [различные системы мониторинга](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Состояние_системы "List of applications (Русский)").

## Solid State Drives

Для получения значения температуры Hddtemp обычно считывает поле `194` данных S.M.A.R.T. жесткого диска. В SSD накопителях информация о температуре обычно хранится в поле `190`. Можно посмотреть этот параметр, выполнив следующие команды:

```
$ smartctl -a /dev/sdX

```

или

```
$ hddtemp --debug /dev/sdX

```

Другой способ - вручную обновить базу данных hddtemp, указав требуемый накопитель с параметрами поля и единицы измерения в `/usr/share/hddtemp/hddtemp.db`. Например:

```
$ echo '"Samsung SSD 840 EVO 250GB" 190 C "Samsung SSD 840 EVO 250GB"' >> /usr/share/hddtemp/hddtemp.db

```