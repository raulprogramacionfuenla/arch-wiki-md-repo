*dhcpd* – свободная реализация [DHCP](https://en.wikipedia.org/wiki/ru:DHCP "wikipedia:ru:DHCP")-сервера от [Internet Systems Consortium](http://www.isc.org/downloads/dhcp/). Он может использоваться, к примеру, на машине, выполняющей роль маршрутизатора для автоматической настройки подключаемых устройств локальной сети.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Запуск на одном сетевом интерфейсе](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BD.D0.B0_.D0.BE.D0.B4.D0.BD.D0.BE.D0.BC_.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.BC_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.B5)
        *   [3.1.1 При помощи настройки dhcpd](#.D0.9F.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_dhcpd)
        *   [3.1.2 При помощи файла службы](#.D0.9F.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [dhcp](https://www.archlinux.org/packages/?name=dhcp), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Настройка

Присвойте статический адрес IPv4 тому сетевому интерфейсу, для которого вы хотите запустить DHCP-сервер (в наших примерах будет использоваться `eth0`). Обратите внимание, что у двух различных сетевых интерфейсов на одной машине не должны полностью совпадать первые три октета адреса.

```
# ip link set up dev eth0
# ip addr add 139.96.30.100/24 dev eth0 # произвольный адрес для примера

```

**Совет:** Обычно для частных сетей используется одна из трех следующих подсетей, которые специально зарезервированы и гарантированно не будут конфликтовать ни с каким хостом в сети Интернет:

*   `192.168/16` (подсеть `192.168.0.0`, маска подсети `255.255.0.0`)
*   `172.16/12` (подсеть `172.16.0.0`, маска подсети `255.240.0.0`)
*   `10/8` (для больших сетей; подсеть `10.0.0.0`, маска подсети `255.0.0.0`)

Смотрите также [RFC 1918](http://www.ietf.org/rfc/rfc1918.txt).

Чтобы настроить автоматическое присвоение статического IP при загрузке системы, смотрите [Network configuration (Русский)#Статический IP-адрес](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_IP-.D0.B0.D0.B4.D1.80.D0.B5.D1.81 "Network configuration (Русский)").

Стандартный файл настроек `dhcpd.conf` содержит много незакомментированных примеров, поэтому следует переместить его в другое место, например

```
# mv /etc/dhcpd.conf /etc/dhcpd.conf.example

```

и создать на его месте новый.

Минимальный файл настроек `dhcpd.conf` может выглядеть следующим образом:

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.8.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;
}

```

Опция `domain-name-servers` содержит адреса DNS-серверов, которые передаются клиентам. В данном примере используются публичные DNS-сервера Google. Если в вашей подсети уже есть DNS-серверы (например, предоставленные провайдером), следует указать их адреса. Если на компьютере уже настроен собственный DNS-сервер, то укажите его адрес (т.е., `139.96.30.100` в нашем примере).

Опции `subnet-mask` и `routers` содержат маску подсети и список маршрутизаторов в этой подсети, соответственно. В большинстве случаев для небольших сетей подойдет маска `255.255.255.0`, а в качестве маршрутизатора используется та же машина, на которой настроен DHCP-сервер.

Блоки `subnet` содержат настройки для отдельных подсетей, которые сопоставляются сетевым интерфейсам, на которых запущен *dhcpd*. В примере определена одна подсеть `139.96.30.0/24`, для которой задан диапазон IP-адресов. Подключаемым клиентам будут присваиваться адреса из этого диапазона.

После завершения настройки запустите демон *dhcpd* с помощью службы `dhcpd4.service`; чтобы служба запускалась автоматически при загрузке системы, включите ее. Как это сделать вы можете найти на странице [Systemd (Русский)#Использование юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)").

Теперь для каждого компьютера, который подключается к интерфейсу `eth0`, будет присвоен IPv4-адрес из диапазона `139.96.30.150` – `139.96.30.250`.

## Советы и рекомендации

### Запуск на одном сетевом интерфейсе

Если ваш компьютер уже является частью нескольких сетей, может возникнуть ситуация, когда адреса будут выдаваться в том числе и компьютерам из другой сети. Это можно исправить настройкой *dhcpd* или создав специальный файл службы, который будет указывать, на каком конкретно интерфейсе будет работать *dhcpd*.

#### При помощи настройки dhcpd

Чтобы исключить конкретный интерфейс, в файле настроек создайте пустой блок `subnet` для этого интерфейса:

 `/etc/dhcpd.conf` 
```
# Исключить DHCP из демилитаризованной зоны (192.168.2.0/24)
subnet 192.168.2.0 netmask 255.255.255.0 {
}

```

#### При помощи файла службы

Стандартный файл службы `dhcpd4.service` запускает *dhcpd* на всех доступных интерфейсах. Если вам нужно запустить *dhcpd* лишь на одном интерфейсе, создайте следующий файл:

 ` /etc/systemd/system/dhcpd4@.service` 
```
[Unit]
Description=IPv4 DHCP server on %I
Wants=network.target
After=network.target

[Service]
Type=forking
PIDFile=/run/dhcpd4.pid
ExecStart=/usr/bin/dhcpd -4 -q -pf /run/dhcpd4.pid %I
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target

```

Теперь вы можете запустить *dhcpd* на одном конкретном интерфейсе, например `eth0`:

```
# systemctl start dhcpd4@eth0.service

```

## Смотрите также

*   [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)")