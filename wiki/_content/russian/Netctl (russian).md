*netctl* — это инструмент командной строки, используемый для настройки и управления сетевыми подключениями через профили. Это нативный проект Arch Linux для настройки сети.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Автоматизация](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
        *   [3.1.1 Основной метод](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4)
        *   [3.1.2 Автоматическое переключение профилей](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B5.D0.B9)
    *   [3.2 Переход с netcfg](#.D0.9F.D0.B5.D1.80.D0.B5.D1.85.D0.BE.D0.B4_.D1.81_netcfg)
    *   [3.3 Хеширование пароля (256-битный Pre-Shared Key)](#.D0.A5.D0.B5.D1.88.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8F_.28256-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.B9_Pre-Shared_Key.29)
*   [4 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.1 Экспериментальный графический интерфейс](#.D0.AD.D0.BA.D1.81.D0.BF.D0.B5.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D1.82.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81)
    *   [4.2 Установка DHCP-клиента для всех профилей](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_DHCP-.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0_.D0.B4.D0.BB.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B5.D0.B9)
    *   [4.3 Замена 'netcfg current'](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_.27netcfg_current.27)
    *   [4.4 Eduroam](#Eduroam)
    *   [4.5 Объединение сетевых интерфейсов (бондинг)](#.D0.9E.D0.B1.D1.8A.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D1.8B.D1.85_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.BE.D0.B2_.28.D0.B1.D0.BE.D0.BD.D0.B4.D0.B8.D0.BD.D0.B3.29)
        *   [4.5.1 Балансировка нагрузки](#.D0.91.D0.B0.D0.BB.D0.B0.D0.BD.D1.81.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
        *   [4.5.2 Подключение к беспроводной сети при отказе проводной](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_.D0.B1.D0.B5.D1.81.D0.BF.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D0.B5.D1.82.D0.B8_.D0.BF.D1.80.D0.B8_.D0.BE.D1.82.D0.BA.D0.B0.D0.B7.D0.B5_.D0.BF.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9)
    *   [4.6 Использование любого сетевого интерфейса](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BB.D1.8E.D0.B1.D0.BE.D0.B3.D0.BE_.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.B0)
    *   [4.7 Использование хуков](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.85.D1.83.D0.BA.D0.BE.D0.B2)
    *   [4.8 Проблемы с соединением после пробуждения](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D1.83.D0.B6.D0.B4.D0.B5.D0.BD.D0.B8.D1.8F)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Job for netctl@XXX.service failed](#Job_for_netctl.40XXX.service_failed)
    *   [5.2 dhcpcd: ipv4_addroute: File exists](#dhcpcd:_ipv4_addroute:_File_exists)
    *   [5.3 Таймаут при DHCP-подключении](#.D0.A2.D0.B0.D0.B9.D0.BC.D0.B0.D1.83.D1.82_.D0.BF.D1.80.D0.B8_DHCP-.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B8)
    *   [5.4 Тайм-аут соединения](#.D0.A2.D0.B0.D0.B9.D0.BC-.D0.B0.D1.83.D1.82_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Установите пакет [netctl](https://www.archlinux.org/packages/?name=netctl), доступный в [официальных репозиториях](/index.php/Official_Repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official Repositories (Русский)").

Опциональные зависимости перечислены в таблице ниже.

| Функция | Пакет | Программа netctl
(если есть) |
| Автоматическое соединение с беспроводными сетями | [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond) | `netctl-auto` |
| Автоматическое проводное содинение | [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) | `netctl-ifplugd` |
| WPA | [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) |
| DHCP | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) или [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| Wifi-меню | [dialog](https://www.archlinux.org/packages/?name=dialog) |
| PPPoE | [ppp](https://www.archlinux.org/packages/?name=ppp) |

**Важно:** Вы можете потерять соединение после установки *netctl*, если у вас запущена какая-нибудь другая служба, которая может конфликтовать с *netctl*. Используйте команду `systemctl --type=service` чтобы убедиться, что не запущены другие службы настройки сети.

## Использование

Перед началом использования netctl желательно прочитать следующие страницы:

*   [netctl](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.1.txt)
*   [netctl.profile](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt)
*   [netctl.special](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.special.7.txt)

## Настройка

Для управления сетевыми соединениями *netctl* использует профили, файлы которых расположены в `/etc/netctl`. В `/etc/netctl/examples` можно найти примеры типовых настроек:

*   ethernet-dhcp
*   ethernet-static
*   wireless-wpa
*   wireless-wpa-static

Вы можете использовать любой файл из предоставленных примеров как основу для своей конфигурации, для этого просто скопируйте файл в `/etc/netctl` и отредактируйте необходимым образом:

```
# cp /etc/netctl/examples/wireless-wpa /etc/netctl/*имя_профиля*

```

**Важно:** Начиная с версии 197, [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") больше не присваивает интерфейсам имена стандартного вида `wlan*X*` и `eth*X*`, несмотря на то, что такие имена используются в примерах на этой странице. Смотрите [Network configuration (Русский)#Имена устройств](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.BC.D0.B5.D0.BD.D0.B0_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2 "Network configuration (Русский)") для получения подробной информации.

**Совет:** Для автоматического создания профиля беспроводного соединения в `/etc/netctl` воспользуйтесь командой `wifi-menu -o` (запускать с правами суперпользователя).

Как только вы создали профиль, попробуйте установить соединение:

```
# netctl start *имя_профиля*

```

**Примечание:** Здесь *имя_профиля* — это имя файла профиля. Указание полного пути к файлу является ошибкой.

Если было выведено сообщение об ошибке, выполните `journalctl -xn` и `netctl status *имя_профиля*` для выяснения ее причины. Исправьте настройки профиля и повторите попытку.

### Автоматизация

Если используется только один профиль на один интерфейс или вы хотите переключать профили вручную, то подойдет [основной метод](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4) — пользователям серверов, рабочих станций, роутеров и т. п.

Если требуется часто переключаться между несколькими профилями, используйте [автоматическое переключение профилей](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B5.D0.B9) — будет полезно пользователям ноутбуков.

#### Основной метод

При использовании этого метода создается служба [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), которая будет запускаться при загрузке системы. Изменения в файле профиля не будут отражаться в файле конфигурации службы автоматически, поэтому, после внесения изменений в файл, необходимо вновь включить профиль командой:

```
# netctl enable *имя_профиля*

```

**Примечание:** Соединение будет установлено только в том случае, если профиль может быть успешно запущен во время загрузки системы (во время запуска службы). Это значит, что во время загрузки сетевой кабель должен быть подключен, а беспроводная сеть доступна.

**Совет:** Вы можете запускать профиль Ethetnet со статическим IP независимо от того, подключен кабель или нет. Для этого добавьте `SkipNoCarrier=yes` в файл конфигурации профиля.

#### Автоматическое переключение профилей

Для автоматического переключения профилей netctl предоставляет две специальных службы [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"):

*   Для проводных соединений: `netctl-ifplugd@*interface*.service`. Сервис автоматически изменяет профиль при подключении и отключении кабеля.
*   Для беспроводных соединений: `netctl-auto@*interface*.service`. Сервис автоматически изменяет профиль при переходе из диапазона одной сети в диапазон другой.

Сначала [установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") необходимые пакеты:

*   Пакет [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond) требуется для использования `netctl-auto@*interface*.service`
*   Пакет [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) требуется для использования `netctl-ifplugd@*interface*.service`

Теперь создайте в каталоге `/etc/netctl` все профили, которые должны будут запускаться с помощью `netctl-auto@*interface*.service` и `netctl-ifplugd@*interface*.service`.

Если вы хотите, чтобы какой-то из беспроводных профилей **не** запускался автоматически службой `netctl-auto@*interface*.service`, то вам следует явно указать это в файле профиля, добавив в него `ExcludeAuto=yes`.

В случае нескольких беспроводных профилей, вы также можете установить приоритет запуска каждого, указав его в параметре `Priority=[0-9]` секции `WPAConfigSection` (см. пример в `/etc/netctl/examples/wireless-wpa-configsection`. По умолчанию, `netctl-ifplugd@*interface*.service` первым предпочтет профиль, который использует [DHCP](https://en.wikipedia.org/wiki/ru:DHCP "wikipedia:ru:DHCP"). Для того, чтобы сначала был запущен профиль, использующий статический IP, можно использовать опцию `AutoWired=yes`. Подробную информацию смотрите в `netctl.profile(5)`.

**Важно:** С опцией `Security=wpa-config` невозможно автоматическое подключение к WPA профилю средствами netctl-auto. Вместо этого используйте `Security=wpa-configsection`.

После того, как все профили настроены, включите нужные вам службы:

```
# systemctl enable netctl-auto@*interface*.service
# systemctl enable netctl-ifplugd@*interface*.service

```

**Важно:**

*   Если один из профилей содержит ошибки, например пустую переменную `Key=`, юнит systemd не сможет запуститься, отобразив при загрузке сообщение `"Failed to read or parse configuration '/run/network/wpa_supplicant_wlan0.conf'`, даже если профиль с ошибкой не был включен.
*   Этот метод несовместим с [основным методом](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4). Если вы ранее включали профиль через netctl запустите `netctl disable *имя_профиля*`, чтобы предотвратить запуск профиля дважды при загрузке.

Начиная с версии netctl 1.3, стало возможным вручную управлять сетевым интерфейсом, контролируемым службой netctl-auto без необходимости остановки службы. Это реализовано с помощью одноименной утилиты netctl-auto. Чтобы просмотреть список доступных команд, наберите:

```
# netctl-auto --help

```

### Переход с netcfg

netctl хранит профили в `/etc/netctl/`, а не в `/etc/network.d/`, как это делал netcfg.

Чтобы перейти с netcfg, необходимо выполнить, как минимум, следующие шаги:

*   Отключите службы netcfg: `systemctl disable netcfg.service`.
*   Удалите netcfg и [установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") netctl.
*   Переместите файлы сетевых профилей в новую директорию.
*   Переименуйте переменные в соответствии с `netctl.profile(5)` (в основном, необходимо привести переменные к регистру [UpperCamelCase](https://en.wikipedia.org/wiki/ru:CamelCase "wikipedia:ru:CamelCase"). Например `CONNECTION` нужно переименовать в `Connection`).
*   Убедитесь, что в переменной `Address` профиля со статическим IP прописана маска подсети после IP адреса (например: `Address=('192.168.1.23**/24'** '192.168.1.87**/24'**)`)
*   Если вы настраивали беспроводное соединение по образцу `wireless-wpa-configsection`, обратите внимание, что это перезапишет опции `wpa_supplicant`, определенные выше скобок. Для подключения к скрытой беспроводной сети добавьте `scan_ssid=1` к опциям в `wireless-wpa-configsection`; `Hidden=yes` больше не действует.
*   На ваше усмотрение можно убрать кавычки вокруг переменных, для которых кавычки не обязательны.
*   Выполните `netctl enable *имя_профиля*` для каждого профиля в старом массиве `NETWORKS`. Специальная опция `last` больше не нужна, смотрите описание netctl.service в [netctl.special(7)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.special.7.txt).
*   Вместо *netcfg-menu* используйте `netctl list` и `netctl start *имя_профиля*`. *wifi-menu* остался доступным.
*   В отличие от netcfg, по умолчанию netctl не устанавливает логическое соединение на интерфейсе, если [сетевая плата](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%B5%D1%82%D0%B5%D0%B2%D0%B0%D1%8F_%D0%BF%D0%BB%D0%B0%D1%82%D0%B0 "wikipedia:ru:Сетевая плата"), не подключена к другой работающей плате. Чтобы это исправить, добавьте `SkipNoCarrier=yes` в конец вашего файла `/etc/netctl/*имя_профиля*`.

### Хеширование пароля (256-битный Pre-Shared Key)

**Примечание:** Этот метод позволяет зашифровать пароль в файле конфигурации беспроводной сети так, чтобы скрыть его от прочтения посторонними. Однако, это не защищает от использования вашего файла с зашифрованной версией пароля посторонним пользователем с правами на его чтение для подключения к сети.

У пользователей, не желающих, чтобы их пароль хранился в открытом виде, есть возможность использовать 256-битный хеш, вычисляемый на основе пароля и SSID сети стандартными алгоритмами. Реализовать хеширование пароля можно двумя способами:

*   Для генерации нужных настроек в `/etc/netctl/` использовать `wifi-menu -o`.
*   Ручная настройка, описанная ниже.

Какой бы метод вы не выбрали, для ограничения доступа к паролю следует установить нужные права на файл профиля:

```
# chmod 600 /etc/netctl/*имя_профиля*

```

Вычислите хеш с помощью [wpa_passphrase](/index.php/WPA_Supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81 "WPA Supplicant (Русский)"):

 `$ wpa_passphrase *your_essid* *passphrase*` 
```
network={
  ssid="*your_essid*"
  #psk="*passphrase*"
  psk=64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
}
```

**Примечание:** Не закрывайте терминал, эта информация будет нужна далее.

Во втором окне терминала скопируйте файл-образец wireless-wpa из каталога `/etc/netctl/examples` в `/etc/netctl`:

```
# cp /etc/netctl/examples/wireless-wpa /etc/netctl/wireless-wpa

```

Теперь следует отредактировать `/etc/netctl/wireless-wpa`, добавив в переменную `Key` ключ, сгенерированный ранее с помощью *wpa_passphrase*.

В итоге профиль wireless-wpa будет выглядеть следующим образом:

 `/etc/netctl/wireless-wpa` 
```
Description='A simple WPA encrypted wireless connection using 256-bit PSK'
Interface=wlp2s2
Connection=wireless
Security=wpa
IP=dhcp
ESSID=*your_essid*
Key=\"64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
```

**Примечание:**

*   Убедитесь, что корректно использованы специальные правила расстановки кавычек (special quoting rules) для переменной `Key`, которые описаны в конце [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt).
*   Если пароль не проходит проверку, попробуйте удалить `\"` из переменной `Key`.

## Советы и рекомендации

### Экспериментальный графический интерфейс

Вы можете попробовать работать с *netctl*, используя экспериментальный графический интерфейс, доступный в пакете [netgui](https://aur.archlinux.org/packages/netgui/). Учтите, что *netgui* все еще находится в разработке, и вам следует также быть знакомым со структурой и содержимым конфигурационных файлов *netctl*, чтобы иметь возможность самостоятельно устранять возможные неполадки. Другая графическая оболочка, [netctl-gui](https://aur.archlinux.org/packages/netctl-gui/), предоставляет основанный на [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)") графический интерфейс, демон DBus и виджет для [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)").

### Установка DHCP-клиента для всех профилей

Если вы хотите установить DHCP-клиент, используемый по умолчанию для всех профилей сетевого интерфейса, создайте исполняемый файл `/etc/netctl/interfaces/*interface_name*` с такой строкой:

```
DHCPClient='*your_dhcp_client*'

```

Где *your_dhcp_client* – название вашей программы-клиента, например *dhclient* или *dhcpcd*.

### Замена 'netcfg current'

Если в недавнем прошлом вы использовали `netcfg current`, то теперь можете использовать `# netctl-auto current` в качестве замены для профилей, начинающихся с `netctl-auto` (доступно с версии netctl 1.3).

Чтобы получить имена всех доступных профилей, используйте команду

```
# netctl list | awk '/*/ {print $2}'

```

### Eduroam

Смотрите [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise").

### Объединение сетевых интерфейсов (бондинг)

Из [документации ядра Linux](https://www.kernel.org/doc/Documentation/networking/bonding.txt):

	*The Linux bonding driver provides a method for aggregating multiple network interfaces into a single logical "bonded" interface. The behavior of the bonded interfaces depends on the mode. Generally speaking, modes provide either hot standby or load balancing services. Additionally, link integrity monitoring may be performed.*

перевод:

	*Объединение сетевых интерфейсов в Linux можно осуществить с помощью драйвера бондинга, он предоставляет методы для сопряжения нескольких сетевых интерфейсов в один логический. Поведение связанных интерфейсов зависит от режима. В общем случае, объединенные интерфейсы могут работать в режиме горячего резерва (для отказоустойчивости) или в режиме балансировки нагрузки.*

#### Балансировка нагрузки

Для использования бондинга с netctl потребуется пакет [ifenslave](https://www.archlinux.org/packages/?name=ifenslave).

Скопируйте `/etc/netctl/examples/bonding` в `/etc/netctl/bonding` и отредактируйте его. Например:

 `/etc/netctl/bonding` 
```
Description='Bond Interface'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'eth1')
IP=dhcp
IP6=stateless
```

Теперь можно отменить старые настройки и установить запуск бондинга по умолчанию. Переключитесь на новый профиль:

```
# netctl switch-to bonding

```

**Примечание:** По умолчанию для двайвера бондинга используется политика цикличности (*the round-robin policy*). Что это значит, можно узнать в [документации](https://www.kernel.org/doc/Documentation/networking/bonding.txt).

**Совет:** Чтобы проверить статус режима бондинга, выполните: `$ cat /proc/net/bonding/bond0` 

#### Подключение к беспроводной сети при отказе проводной

В этом разделе представлен способ использования *бондинга* для автоматического переключения на запасную беспроводную сеть в случае потери основного проводного соединения. Это полезно, если беспроводной и проводной сетевой интерфейс подключаются к одной и той же сети. Для этого ваша беспроводная точка доступа (маршрутизатор) должна быть настроена в режиме моста.

Вам понадобятся дополнительные пакеты из официальных репозиториев: [ifenslave](https://www.archlinux.org/packages/?name=ifenslave) и [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant).

Первым делом включите модуль бондинга для загрузки при старте системы, как показано на странице [Kernel modules (Русский)#Loading](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Loading "Kernel modules (Русский)"):

 `/etc/modules-load.d/bonding.conf`  `bonding` 

Затем настройте драйвер `bonding` для работы в режиме `active-backup`, а в опции `primary` укажите имя сетевого интерфейса, который должен быть нормально активен (как правило, для этого используется проводной интерфейс; узнать имя ваших сетевых интерфейсов вы можете с помощью команды `ip link`).

 `/etc/modprobe.d/bonding.conf`  `options bonding mode=active-backup miimon=100 primary=eth0 max_bonds=0` 

Опция `miimon` нужна для определения потери соединения. Опция `max_bonds` позволяет избежать появления ошибки `Interface bond0 already exists`. Более подробую информацию вы можете найти в [документации ядра Linux](https://www.kernel.org/doc/Documentation/networking/bonding.txt).

Теперь создайте профиль netctl, который будет объединять оба ваших интерфейса в один мастер-интерфейс (`bond0`). Вы можете объединить таким образом любое количество имеющихся сетевых интерфейсов.

 `/etc/netctl/failover` 
```
Description='A wired connection with failover to wireless'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'wlan0')
IP='dhcp'
```

Если вы настраивали профили для интерфейсов `eth0` и `wlan0`, отключите их перед тем, как включать профиль `failover`:

```
# netctl enable failover

```

Теперь вам необходимо настроить *wpa_supplicant* для соединения с беспроводной сетью:

 `/etc/wpa_supplicant/wpa_supplicant-wlan0.conf` 
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Также добавьте в файл блок(и) `network` для указания настроек отдельных беспроводных сетей, к которым будет подключаться *wpa_supplicant*:

```
network={
    ssid="SSID"
    psk=PSK
}

```

Для генерирования зашифрованного закрытого ключа используйте *wpa_passphrase*, как показано на странице [WPA supplicant (Русский)#Сопряжение при помощи wpa_passphrase](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BE.D0.BF.D1.80.D1.8F.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_wpa_passphrase "WPA supplicant (Русский)").

Теперь включите службу `wpa_supplicant` на сетевом интерфейсе, для которого вы произвели настройку:

```
# systemctl enable wpa_supplicant@wlan0

```

После перезагрузки соединение будет установлено.

**Примечание:** Если при загрузке системы вы получили ошибку
```
bonding: wlan0 is up - this may be due to an out of date ifenslave

```

это значит, что *wpa_supplicant* запустился перед профилем *netctl*. Это происходит потому, что [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") выполняет запуск программ параллельно. *ifenslave* требует, чтобы все интерфейсы были выключены перед тем, как выполнять их сопряжение с мастер-интерфейсом.

Для решения проблемы необходимо установить зависимость службы `wpa_supplicant@wlan0` от `netctl@failover profile`, так, чтобы они запускались последовательно. Создайте файл зависимости, как показано на странице [systemd (Русский)#Обработка зависимостей](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9E.D0.B1.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B0_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B8.D0.BC.D0.BE.D1.81.D1.82.D0.B5.D0.B9 "Systemd (Русский)"):

 `/etc/systemd/system/wpa_supplicant@wlan0.service.d/customdependency.conf` 
```
[Unit]
After=netctl@failover.service
```

После чего перезагрузите систему. Вы можете проверить, работает ли бондинг, используя команду

```
# journalctl -u netctl@failover.service

```

Для проверки состояния отдельных интерфейсов, наберите:

```
# ip link

```

Вы должны увидеть что-то наподобие:

```
1: eth0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master bond0 state UP mode DEFAULT group default qlen 1000
    link/ether xx:xx:xx:xx:xx:xx brd ff:ff:ff:ff:ff:ff
2: wlan0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master bond0 state UP mode DORMANT group default qlen 1000
    link/ether xx:xx:xx:xx:xx:xx brd ff:ff:ff:ff:ff:ff
3: bond0: <BROADCAST,MULTICAST,MASTER,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default 
    link/ether xx:xx:xx:xx:xx:xx brd ff:ff:ff:ff:ff:ff

```

Теперь вы можете проверить, работает ли переключение на резервный интерфейс, запустив загрузку большого файла по сети (или, например, начав просмотр потокового видео) и отсоединив разъем проводного интерфейса. Передача данных должна непрерывно продолжаться. После подключения разъема проводного интерфейса должен произойти обратный переход. При возникновении проблем, используйте команды

```
# journalctl -u netctl@failover.service

```

и

```
# journalctl -u wpa_supplicant@wlan0.service

```

для отладки.

### Использование любого сетевого интерфейса

В некоторых случаях может быть желательно, чтобы профиль мог использовать любой доступный сетевой интерфейс. Например, вы администрируете несколько компьютеров различной конфигурации, и для каждого используете одинаковый образ системного диска, чтобы избежать переустановки системы на каждом конкретном компьютере (особенно это удобно, если компьютеры не имеют своих устройств ввода/вывода). Если вы используете стандартную схему именования сетевых интерфейсов, и у компьютера только единственный сетевой адаптер, вы можете смело предположить, что eth0 — правильное имя интерфейса. Однако, если вы используете новую [схему именования](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) udev, устройствам будут присвоены имена, зависящие от их физического подключения на плате (например, enp1s0). Это значит, что профиль netctl содержащий точное название интерфейса, может работать на одном комьютере, и не работать на другом, в котором сетевое устройство названо иначе.

Быстрое и «грязное» решение заключается в использовании каталога `/etc/netctl/interfaces/`. Выберите псевдоним (alias) для сетевого интерфейса (`en-any` в этом примере), и создайте следующий файл:

 `/etc/netctl/interfaces/en-any` 
```
#!/bin/bash
for interface in /sys/class/net/en*; do
        break;
done
Interface=$(basename $interface)
echo "en-any: using interface $Interface";

```

Не забудьте дать файлу права на выполнение.

Теперь создайте профиль, который будет использовать этот интерфейс. Укажите псевдоним интерфейса в параметре `Interface`. Пример:

 `/etc/netctl/wired` 
```
Description='Wired'
Interface=en-any
Connection=ethernet
IP=static
Address=('192.168.1.15/24')
Gateway='192.168.1.1'
DNS=('192.168.1.1')

```

Теперь, когда профиль `wired` будет запущен, любой компьютер использующий эти файлы конфигурации автоматически установит соединение, используя сетевой интерфейс, найденный первым при загрузке системы, в не зависимости от того, какое ему имя даст udev. Учтите, что это не самый надежный способ: если в компьютере несколько интерфейсов, netctl может попытаться присвоить им одинаковое имя, что приведет к неработоспособности соединения. Использование *netctl-auto* может стать несколько более надежным решением.

### Использование хуков

netctl поддерживает общие хук-скрипты в `/etc/netctl/hooks/`, и хуки для каждого сетевого интерфейса в `/etc/netctl/interfaces/`. Вы можете указывать все опции netctl аналогично с обычными файлами профиля в эти скрипты, включая `ExecUpPost` и `ExecDownPre`. Когда состояние соединения изменяется, netctl загружает (через *source*) все исполняемые скрипты в `hooks`, затем прочитывает файл профиля и наконец загружает (*source*) исполняемый скрипт в каталога `interfaces`, имя которого совпадает с именем сетевого интерфейса, который используется в профиле. Таким образом, опции в скрипте интерфейса могут переопределять значения опций в файле профиля, а он, в свою очередь, может переопределять значения скриптов в `hooks`. Переменные `$INTERFACE`, `$SSID`, `$ACTION` и `$Profile` доступны для использования в хук-скриптах. Для получения более подробной информации смотрите [man-страницу](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") `netctl.profile(5)`.

Пример скрипта, который запускает команду после того, как соединение установлено (для всех профилей):

 `/etc/netctl/hooks/postconnect` 
```
#!/bin/sh

ExecUpPost="systemctl start crashplan.service; systemctl start dropbox@<username>.service"

```

### Проблемы с соединением после пробуждения

В некоторых случаях соединение может не восстанавливаться самостоятельно после того, как компьютер некоторое время находился в режиме сна. Если для переподключения требуется перезапуск сетевого интерфейса, вы можете создать файл службы [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), который будет выполнять необходимые действия для перезапуска сетевого интерфейса после пробуждения. Ниже приведен пример такого файла, который использует службу `netctl-auto` для перезапуска интерфейса `wlan0`:

 `/etc/systemd/system/netctl-wlan0-resume.service` 
```
[Unit]
Description=Restart netctl-auto on resume.
After=suspend.target

[Service]
Type=oneshot
RemainAfterExit=no
ExecStart=/usr/bin/systemctl restart netctl-auto@wlan0
ExecStart=/usr/bin/echo netctl-wlan0-resume: Successfully restarted netctl-auto@wlan0

[Install]
WantedBy=suspend.target

```

Измените команду в опции `ExecStart` в соответствии с вашими нуждами.

После создания файла [включите](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") службу (в данном примере, `netctl-wlan0-resume`).

## Решение проблем

### Job for netctl@XXX.service failed

Иногда возникают проблемы с подключением к беспроводной сети с использованием *netctl*, сопровождаемые следующим сообщением:

 `# netctl start wlan0-ssid` 
```
Job for netctl@wlan0\x2ssid.service failed. See 'systemctl status netctl@wlan0\x2ssid.service' and 'journalctl -xn' for details.

```

При этом, в выводе `journalctl -xn` наблюдается следующее:

1\. Если сетевой интерфейс (в нашем примере `wlan0`) уже был запущен

```
network[2322]: The interface of network profile 'wlan0-ssid' is already up

```

Остановка интерфейса должна помочь:

```
# ip link set wlan0 down

```

Теперь попробуйте снова:

```
# netctl start wlan0-ssid

```

2\. Если сетевой интерфейс был остановлен, то:

```
dhcpcd[261]: wlan0: ipv4_sendrawpacket: Network is down

```

Один из способов это исправить — использовать другой DHCP-клиент, например [dhclient](https://www.archlinux.org/packages/?name=dhclient). После установки пакета настройте клиент:

 `/etc/netctl/wlan0-ssid` 
```
...
DHCPClient='dhclient'

```

Добавление опции `ForceConnect` также может помочь:

 `/etc/netctl/wlan0-ssid` 
```
...
ForceConnect=yes

```

Сохраните файл и попробуйте соединиться используя профиль:

```
# netctl start wlan0-ssid

```

### dhcpcd: ipv4_addroute: File exists

Иногда использование *dhcpcd* с netctl вызывает проблемы с переподключением: netctl сообщает об успешном подключении, но вы все еще получаете ошибки тайм-аута при соединении. В этом случае, прежний маршрут по умолчанию (default route) все еще остается в системе и не обновляется. Решение состоит в том, чтобы использовать [dhclient](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_DHCP-.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0_.D0.B4.D0.BB.D1.8F_.D0.B2.D1.81.D0.B5.D1.85_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B5.D0.B9) в качестве DHCP-клиента. Больше информации о проблеме вы сможете найти [здесь (англ.)](https://bbs.archlinux.org/viewtopic.php?pid=1399842#p1399842).

### Таймаут при DHCP-подключении

Если вы получаете сообщения о тайм-ауте при попытке подключения через DHCP, вы можете увеличить время таймаута, используя значение выше 30 секунд, установленных в netctl по умолчанию. Создайте файл в каталоге `/etc/netctl/hooks/` или `/etc/netctl/interfaces/`, добавьте в него строку `TimeoutDHCP=40`, где 40 — время тайм-аута. Не забудьте выдать файлу права на запуск.

### Тайм-аут соединения

При проблемах с тайм-аутом, не связанных с DHCP (например, если у вас статический IP), если наблюдаемые ошибки похожи на следующие при запуске профиля:

 `# journalctl _SYSTEMD_UNIT=netctl@*имя_профиля*.service` 
```
Starting network profile '*profile*'...
No connection found on interface 'wlan0' (timeout)
Failed to bring the network up for profile '*profile*'

```

Попробуйте увеличить значения тайм-аутов соединения в вашем файле профиля:

 `/etc/netctl/*имя_профиля*` 
```
...
TimeoutUp=300
TimeoutCarrier=300

```

Не забудьте заново активировать ваш профиль:

```
# netctl reenable *имя_профиля*

```

## Смотрите также

*   [Анонс и официальная страница обсуждения](https://bbs.archlinux.org/viewtopic.php?id=157670)
*   [cinnamon-applet-netctl-systray-menu](https://aur.archlinux.org/packages/cinnamon-applet-netctl-systray-menu/) - aпплет для Cinnamon