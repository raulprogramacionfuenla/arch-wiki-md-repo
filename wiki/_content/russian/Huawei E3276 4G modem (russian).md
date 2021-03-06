В этой статье описывается, как подключить и произвести первичную настройку 4G модема Huawei E3276 в Arch Linux. Инструкция написана для модема от оператора МегаФон. С этой инструкцией вы сможете настроить подключение к сети для дальнейшей установки Arch Linux.

## Contents

*   [1 Подготовка](#Подготовка)
    *   [1.1 Информация о режимах модема](#Информация_о_режимах_модема)
    *   [1.2 Установка и настройка необходимого ПО](#Установка_и_настройка_необходимого_ПО)
        *   [1.2.1 Linux](#Linux)
        *   [1.2.2 Windows](#Windows)
*   [2 Переключение режима модема](#Переключение_режима_модема)
    *   [2.1 Завершение работы программы](#Завершение_работы_программы)
*   [3 Настройка сети](#Настройка_сети)
    *   [3.1 Автоподключение](#Автоподключение)

## Подготовка

### Информация о режимах модема

Для того, чтобы система корректно распознавала модем, необходимо переключить режим модема, оставив включенными только два порта: PCUI и

модемный. В этом случае вы больше не сможете пользоваться другими встроенными функциями модема, например карт-ридером. До того как

производить нижеследующие операции, рекомендуется скопировать на компьютер ПО модема, оно может вам пригодится при работе с модемом на

операционной системе Windows.

**Примечание:** Необходимо отключить проверку PIN кода на сим-карте.

### Установка и настройка необходимого ПО

#### Linux

*   Установите [minicom](https://www.archlinux.org/packages/?name=minicom). Посмотрите все подключенные устройства следующей командой:

```
$ ls /dev/tty*

```

Если к другим USB-портам вашей машины ничего не подключено, помимо всего остального, в конце списка у вас должны определиться два

устройства: **ttyUSB0** и **ttyUSB1**.

*   Запустите minicom следующей командой:

```
$ minicom --device=/dev/ttyUSB0

```

**Примечание:** **/dev/ttyUSB0** в данном случае — это имя девайса, к которому будет обращаться демон ppp. Имя может отличаться.

#### Windows

*   Отключите модем от сети, закройте ПО, использующее модем.
*   Скачайте и запустите бесплатную программу [DC-unlocker](https://www.dc-unlocker.com).
*   Нажмите **Определить модем** (иконка в виде лупы).

## Переключение режима модема

*   После того, как вы подключились к модему, попробуйте ввести следующую команду, не обращая внимания на входящие сообщения:

```
ATE

```

*   Если все хорошо, отключите входящие сообщения следующей командой:

```
AT^CURC=0

```

*   Переключите, наконец, режим модема:

```
AT^SETPORT="FF;10,12"

```

### Завершение работы программы

**Linux:** Завершите работу minicom последовательным нажатием «Ctrl+A» и «Q».
**Windows:** Просто закройте окно программы.
**Извлеките модем и вставьте обратно.**

## Настройка сети

*   Создайте файл **/etc/ppp/options-mobile** со следующим содержимым:

```
/dev/ttyUSB0
921600
defaultroute
usepeerdns
crtscts
lock
noauth
local
persist
modem
nopcomp
novjccomp
nobsdcomp
nodeflate
noaccomp
ipcp-accept-local
ipcp-accept-remote
noipdefault

```

*   Создайте файл **/etc/ppp/peers/megafon** и пропишите в нем следующее:

```
file /etc/ppp/options-mobile
connect "/usr/sbin/chat -v -t15 -f /etc/ppp/chatscripts/megafon.chat"

```

*   Создайте папку **/etc/ppp/chatscripts**, а в нем файл **megafon.chat**. Пропишите в него:

```
ABORT 'NO CARRIER'
REPORT CONNECT
TIMEOUT 6
'' 'AT'
'OK' 'AT+CGDCONT=1,"IP","internet"'
'OK' 'ATD*99*1#'
TIMEOUT 30
CONNECT

```

Готово, теперь вы можете подключиться к интернету, используя следующую команду:

```
sudo pon megafon

```

И отключиться, введя:

```
sudo poff megafon

```

### Автоподключение

Чтобы сеть поднималась автоматически при старте системы, необходимо включить соответствующий юнит:

```
systemctl enable ppp@megafon.service

```