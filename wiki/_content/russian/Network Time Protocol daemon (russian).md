Эта статья описывает, как установить и настроить NTPd (Network Time Protocol daemon), наиболее распространенный способ синхронизации [часов](/index.php/System_time "System time") в системе GNU/Linux с серверами в сети Интернет при помощи [NTP](https://en.wikipedia.org/wiki/NTP "wikipedia:NTP"). Если все настроено правильно, Ваш компьютер тоже может выступать в роли сервера синхронизации времени.

## Contents

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
*   [3 Запуск демона](#Запуск_демона)
    *   [3.1 Запуск ntpd](#Запуск_ntpd)
    *   [3.2 NetworkManager](#NetworkManager)
    *   [3.3 Использование не root-пользователем](#Использование_не_root-пользователем)
*   [4 Синхронизация часов без запуска демона](#Синхронизация_часов_без_запуска_демона)
*   [5 Альтернативы](#Альтернативы)
*   [6 См. также](#См._также)
*   [7 Внешние источники](#Внешние_источники)

## Установка

Пакет [ntp](https://www.archlinux.org/packages/?name=ntp) доступен в репозитории [extra]:

 `# pacman -S ntp` 

## Настройка

Самая первая строка в вашем файле `/etc/ntp.conf` определяет серверы, с которыми планируется синхронизироваться. NTP использует иерархическую систему «часовых уровней». Уровень 1 синхронизован с высокоточными часами, например, с системой GPS, ГЛОНАСС (Единая Государственная шкала времени РФ) или атомным эталоном времени. Уровень 2 синхронизируется с одной из машин уровня 1, и так далее.

Однако следует учитывать, что уровни не всегда являются показателями точности. Обычно для синхронизации пользовательских машин используются серверы третьего уровня. Если Вы не знаете серверов NTP в Вашем регионе, используйте [pool.ntp.org](http://www.pool.ntp.org/) и выберите сервер в Вашем регионе. Например,

```
server 0.it.pool.ntp.org iburst
server 1.it.pool.ntp.org iburst
server 2.it.pool.ntp.org iburst
server 3.it.pool.ntp.org iburst

```

Опция 'iburst' рекомендуется, с ее помощью посылается шквал пакетов, если не удается установить соединение с сервером с первого раза. Напротив, опцию 'burst' не используйте никогда без особого разрешения, так как Вы можете попасть в "черный список".

При настройке своего NTP сервера, нужно добавить *localhost* в список серверов, так как в случае потери соединения с сетью Интернет, сервер продолжит синхрозировать время в сети. Для этого добавьте *localhost* как сервер десятого уровня при помощи команды `fudge`, чтобы синхронизация не происходила, пока соединение с Интернет доступно:

```
server 127.127.1.0
fudge  127.127.1.0 stratum 10

```

Затем, определите правила, по которым к Вашему серверу смогут подключаться клиенты (*localhost* - это тоже клиент) при помощи команды *restrict*. Также добавьте в файл конфигурации:

```
restrict default nomodify nopeer

```

Эти настройки не позволят пользователям изменять что-либо. Можете также добавить следующие опции:

```
restrict default kod nomodify notrap nopeer noquery

```

Теперь нужно указать ntpd, какие подключения к Вашему серверу разрешены; если Вы не конфигурируете сервер NTP, следующей строки будет достаточно:

```
restrict 127.0.0.1

```

В противном случае, можно добавить больше клиентов:

```
restrict 1.2.3.4 nomodify
restrict 192.168.0.0 mask 255.255.255.0 nomodify notrap

```

Эти строки укажут *ntpd*, что адресам 1.2.3.4, а также всем адресам подсети 192.168.0.0/24 позволено синхронизировать время с Вашим сервером, но не позволено ничего изменять.

Если Вы желаете принудительно определить адреса по протоколу IPv6, напишите *-6* перед IP-адресом или именем хоста (*-4* принудительно устанавливает протокол IPv4), например:

```
restrict -6 default nomodify nopeer
restrict -6 ::1    # ::1 - это 127.0.0.1 в шестой версии протокола IP

```

Наконец, установите файл-буфер (в котором будет находиться погрешность часов системы) и журнал (лог):

```
driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

Примерная конфигурация выглядит так:

 `/etc/ntp.conf` 
```
server 0.it.pool.ntp.org iburst
server 1.it.pool.ntp.org iburst
server 2.it.pool.ntp.org iburst
server 3.it.pool.ntp.org iburst

restrict default nomodify nopeer
restrict 127.0.0.1

driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

Вообще, журнал (лог) устанавливать необязательно, но рекомендуется для того, чтобы знать, какие изменения проводит *ntpd*.

В заключении, никогда не забывайте читать man: [ntp.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntp.conf.5). Это ответит на многие Ваши вопросы. Также можно посмотреть `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`).

## Запуск демона

### Запуск ntpd

Если Вы используете sysvinit:

 `# /etc/rc.d/ntpd start` 

Поместите *ntpd* в массив DAEMONS в файле `/etc/rc.conf`, чтобы он загружался при старте системы:

 `/etc/rc.conf` 
```
...

DAEMONS=(... ntpd ...)
```

Если Вы используете systemd:

`systemctl start ntpd`

Для загрузки при старте системы

`systemctl enable ntpd`

### NetworkManager

*ntpd* можно включать/выключать вместе со стартом сетевого соединения с помощью networkmanager-dispatcher-ntpd:

 `# pacman -S networkmanager-dispatcher-ntpd` 

### Использование не root-пользователем

Если программа скомпилирована с флагом *--enable-linux-caps*, ntpd может запустить не root-пользователь (стандартный пакет в Arch Linux имеет эту опцию).

**Примечание:** Перед тем, как выполнять следующие действия, убедитесь, что файл `/var/lib/ntp/ntp.drift` существует.

Создайте группу *ntp* и пользователя *ntp*:

```
# groupadd ntp

# useradd -r -d /var/lib/ntp -g ntp -s /bin/false ntp
```

Смените владельца директории ntp на пользователя ntp:

 `# chown -R ntp:ntp /var/lib/ntp` 

Отредактируйте `/etc/conf.d/ntp-client.conf` и измените

```
NTPD_ARGS="-g"

```

на

```
NTPD_ARGS="-g -u ntp:ntp"

```

Наконец, перезапустите демона:

 `# /etc/rc.d/ntpd restart` 

## Синхронизация часов без запуска демона

Если Вы просто хотите синхронизировать часы без запуска демона *ntpd*, добавьте в файл `/etc/rc.local` следующее:

```
ntpd -qg &

```

**Примечание:**

*   Если Вы хотите использовать этот метод, убедитесь, что на момент обработки файла `rc.local` сетевое соединение уже установлено (например, Вам не следует запускать демон для подключения к сети Интернет в фоновом режиме (знак "@" перед демоном) в файле `/etc/rc.conf`)
*   Аппаратные часы автоматически подстраиваются по часам системы каждый раз, когда Вы выключаете компьютер, через команду в файле `/etc/rc.shutdown`

**Важно:**

*   Использование этого метода весьма не рекомендуется для серверов, да и для обычных компьютеров, которым приходится работать по 2-3 дня, так как время синхронизируется только один раз при старте системы.
*   Запуск "`ntpd -qg`" через событие планировщика задач *cron* вообще нужно избегать, если Вы не знаете, к чему приведет мгновенное изменение времени во время работы Ваших программ.

## Альтернативы

Доступная альтернатива *ntpd* - это [OpenNTPD](/index.php/OpenNTPD "OpenNTPD"), часть проекта OpenBSD (не поддерживается сообществом Linux).

## См. также

*   [Время](/index.php/Time_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Time (Русский)") - дополнительная информация об аппаратных и системных часах в Linux.
*   [ВНИИФТРИ](http://www.vniiftri.ru/rus/news/91.html) - список серверов NTP Государственного эталона времени и частоты (ГЭВЧ) Российской Федерации.

## Внешние источники

*   [http://www.ntp.org/](http://www.ntp.org/)
*   [http://support.ntp.org/](http://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [http://www.eecis.udel.edu/~mills/ntp/html/index.html](http://www.eecis.udel.edu/~mills/ntp/html/index.html)