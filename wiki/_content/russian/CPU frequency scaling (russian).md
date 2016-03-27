`Cpufrequtils` — это набор утилит разработанных для поддержки функции масштабирования частоты процессора, технологии, преимущественно применяемой в ноутбуках, которая позволяет операционной системе увеличивать или уменьшать тактовую частоту процессора в зависимости от нагрузки на систему и/или схемы энергопотребления. Например, масштабирование частоты процессора может сократить частоту 2 ГГц процессора до 1 ГГц когда ноутбук работает от батарей, увеличивая таким образом время работы, снижая нагрев и уменьшая шум вентилятора.

При использовании совместно с [Pm-utils](/index.php/Pm-utils "Pm-utils") и [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools"), владельцы обеспечены полным набором утилит для управления энергопотреблением.

## Contents

*   [1 Установка cpufrequtils](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_cpufrequtils)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Драйвер управления частотой процессора](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D0.BE.D0.B9_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.BE.D1.80.D0.B0)
        *   [2.1.1 Intel](#Intel)
        *   [2.1.2 AMD](#AMD)
    *   [2.2 Загрузка при старте системы](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8_.D1.81.D1.82.D0.B0.D1.80.D1.82.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [2.3 Преимущества использования в GNOME](#.D0.9F.D1.80.D0.B5.D0.B8.D0.BC.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.B0_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B2_GNOME)
    *   [2.4 Laptop Mode Tools](#Laptop_Mode_Tools)
    *   [2.5 Регуляторы масштабирования (схемы энергопотребления)](#.D0.A0.D0.B5.D0.B3.D1.83.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D1.8B_.D0.BC.D0.B0.D1.81.D1.88.D1.82.D0.B0.D0.B1.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.28.D1.81.D1.85.D0.B5.D0.BC.D1.8B_.D1.8D.D0.BD.D0.B5.D1.80.D0.B3.D0.BE.D0.BF.D0.BE.D1.82.D1.80.D0.B5.D0.B1.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F.29)
        *   [2.5.1 Изменение параметров работы регулятора ondemand](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D1.80.D0.B5.D0.B3.D1.83.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_ondemand)
        *   [2.5.2 Взаимодействие с событиями ACPI](#.D0.92.D0.B7.D0.B0.D0.B8.D0.BC.D0.BE.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.B8.D0.B5_.D1.81_.D1.81.D0.BE.D0.B1.D1.8B.D1.82.D0.B8.D1.8F.D0.BC.D0.B8_ACPI)
    *   [2.6 Демон](#.D0.94.D0.B5.D0.BC.D0.BE.D0.BD)
*   [3 Устранение неисправностей](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.B8.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BD.D0.BE.D1.81.D1.82.D0.B5.D0.B9)

## Установка cpufrequtils

[cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils) - это набор утилит для *масштабирования частоты процессора*. Установка этого пакета необязательна, но крайне рекомендуется, так как предоставляет полезные наборы команд для консоли и демона для запуска масштабирования при старте системы.

[powertop](https://www.archlinux.org/packages/?name=powertop) предоставляет ту же информацию, что и команда cpufreq-info, однако уступает ей в детальности.

Пакет [cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils) доступен в репозитории [extra]:

```
# pacman -S cpufrequtils

```

## Настройка

Настройка масштабирования частоты производится в три этапа:

1.  загрузка соответствующего драйвера управления частотой процессора.
2.  загрузка желаемого регулятора масштабирования.
3.  настройка метода управления регуляторами: ручной (через /sys или cpufreq-set), через cpufrequtils [daemon](/index.php/Cpufrequtils_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.94.D0.B5.D0.BC.D0.BE.D0.BD "Cpufrequtils (Русский)"), laptop-mode-tools, acpid или пи помощи апплета окружения рабочего стола.
4.  (опционально) настройка масштабирования частоты.

### Драйвер управления частотой процессора

Для корректного управления масштабированием частотой, ОС прежде всего должна знать параметры вашего процессора(ов). Для этого нужно загрузить модуль ядра, который может считывать и управлять параметрами вашего процессора(ов).

Для большинства современных ноутбуков и настольных компьютеров можно использовать драйвер **`acpi-cpufreq`**, однако есть ещё такие варианты как *p4-clockmod, powernow-k6, powernow-k7, powernow-k8,* и *speedstep-centrino*. Чтобы увидеть полный список, запустите:

```
$ ls /lib/modules/$(uname -r)/kernel/arch/x86/kernel/cpu/cpufreq/

```

**Tip:** Для AMD "K10" используйте драйвер `powernow-k8`.

Для загрузки драйвера вручную:

#### Intel

```
# modprobe acpi-cpufreq

```

Для более старых процессоров Intel, система может выдать:

```
FATAL: Error inserting acpi_cpufreq ([...]/acpi-cpufreq.ko): No such device

```

В этой ситуации, замените модуль ядра `acpi_cpufreq` на `speedstep-centrino`, `p4-clockmod` или `speedstep-ich`.

**Tip:** Учтите, что модуль speedstep-centrino устарел, а модуль p4-clockmod поддерживает только performance и powersave регуляторов.)

#### AMD

```
# modprobe powernow-k8

```

### Загрузка при старте системы

Для автоматической загрузки драйвера во время старта системы, добавьте соответствующий драйвер в массив MODULES в файле `/etc/rc.conf`. Например:

```
MODULES=( **acpi-cpufreq** vboxdrv fuse fglrx iwl3945 ... )

```

Как только загружен правильный драйвер cpufreq, вы можете посмотреть детальную информацию о вашем процессоре(ах), выполнив:

```
$ cpufreq-info

```

Вот пример вывода `cpufreq-info`:

```
$ cpufreq-info

```

```
 analyzing CPU 0:
  driver: acpi-cpufreq
  CPUs which need to switch frequency at the same time: 0 1
  hardware limits: 1000 MHz - 2.00 GHz
  available frequency steps: 2.00 GHz, 1.67 GHz, 1.33 GHz, 1000 MHz
  available cpufreq governors: ondemand, performance
  current policy: frequency should be within 1000 MHz and 2.00 GHz.
                  The governor "performance" may decide which speed to use
                  within this range.
  current CPU frequency is 2.00 GHz.
 analyzing CPU 1:
  driver: acpi-cpufreq
  CPUs which need to switch frequency at the same time: 0 1
  hardware limits: 1000 MHz - 2.00 GHz
  available frequency steps: 2.00 GHz, 1.67 GHz, 1.33 GHz, 1000 MHz
  available cpufreq governors: ondemand, performance
  current policy: frequency should be within 1000 MHz and 2.00 GHz.
                  The governor "performance" may decide which speed to use
                  within this range.
  current CPU frequency is 2.00 GHz.

```

Для просмотра списка доступных регуляторов:

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors

```

Наблюдать за частотой процессора в режиме реального времени можно, выполнив команду:

```
watch grep \"cpu MHz\" /proc/cpuinfo

```

### Преимущества использования в GNOME

У среды рабочего стола GNOME есть апплет для управления регуляторами "на лету". Чтобы каждый раз не вводить пароль при переключении, просто создайте `/var/lib/polkit-1/localauthority/50-local.d/org.gnome.cpufreqselector.pkla` и отредактируйте файл:

```
[org.gnome.cpufreqselector]
Identity=unix-user:USER
Action=org.gnome.cpufreqselector
ResultAny=no
ResultInactive=no
ResultActive=yes
```

Слово USER замените на ваше имя пользователя.

Пакет [desktop-privileges](https://aur.archlinux.org/packages/desktop-privileges/) в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") содержит файл .pkla для авторизованного использования апплета всей группой пользователей power.

### Laptop Mode Tools

Если Вы используете или планируете использовать [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") для других возможностей энергосбережения, Вы можете также дать этой программе возможность управлять частотой Вашего процессора. Просто добавьте модуль `acpi-cpufreq` в массив MODULES в файле `/etc/rc.conf`:

```
MODULES=(**acpi-cpufreq**)

```

Затем просмотрите файл `/etc/laptop-mode/conf.d/cpufreq.conf` для определения регуляторов, частот и политик использования.

### Регуляторы масштабирования (схемы энергопотребления)

Регуляторы можно рассматривать как заранее сконфигурированые схемы энергопотребления процессора. Регуляторы должны быть загружены как модули ядра, чтобы их могли видеть такие программы как kpowersave и gnome-power-manager. Вы можете загрузить столько гувернёров, сколько вам угодно, однако в любой момент времени активным будет только один.

Доступные регуляторы:

	`cpufreq_performance` *(по-умолчанию)*

	регулятор *performance(производительность)* встроен в ядро и поддерживает процессор(ы) на максимальной тактовой частоте

	`cpufreq_ondemand` *(рекомендуется)*

	динамически увеличивает/уменьшает тактовую частоту процессора в зависимости от загруженности системы

	`cpufreq_conservative`

	похож на ondemand, но более экономный (предпочтение отдаётся меньшим тактовым частотам)

	`cpufreq_powersave`

	процессор работает на минимально возможной тактовой частоте

	`cpufreq_userspace`

	тактовая частота задаётся пользователем вручную

Добавьте необходимый регулятор в массив MODULES в `/etc/rc.conf` (обязательно после модуля acpi-cpufreq) :

```
MODULES=(acpi-cpufreq ***cpufreq_ondemand cpufreq_powersave*** vboxdrv fuse fglrx iwl3945 ... )

```

Вы можете вручную установить регулятора при помощи команды `cpufreq-set` (как root), однако, эта настройка не сохранится после перезагрузки/выключения. Например:

```
# cpufreq-set -g ondemand

```

Заметьте, что предыдущие команды задавали регулятора только для первого процессора. Если у Вас многоядерный процессор или многопроцессорная система, используйте флаг -c, чтобы задать регулятор для определенного процессора. Например, чтобы задать регулятор для четвертого процессора (нумерация начинается с нуля):

```
# cpufreq-set -c 3 -g ondemand

```

Чтобы задать регулятор для всех ядер многоядерного процессора, введите (пример для 6-ядерного процессора):

```
# for i in 0 1 2 3 4 5; do cpufreq-set -c $i -g ondemand; done

```

Чтобы задать максимальный и минимальный пределы частоты для регулятора используйте опции -u и -d. Например, зададим максимальный предел 2.20GHz и минимальный предел 1.50GHz для регулятора ondemand и всех ядер 6-ядерного процессора:

```
# for i in 0 1 2 3 4 5; do cpufreq-set -c $i -g ondemand -u 2.20Ghz -d 1.50Ghz; done

```

Для дополнительной информации запустите `cpufreq-set --help` или `man cpufreq-set`.

Если Вам нужен графический интерфейс для настройки регуляторов или частоты, есть пакет [trayfreq](/index.php/Trayfreq "Trayfreq"), который при запуске появляется в трее.

#### Изменение параметров работы регулятора ondemand

Чтобы изменить значение загрузки процессора, при котором регулятор повышает частоту, нужно изменять значение в файле `/sys/devices/system/cpu/cpufreq/ondemand/up_threshold`. Текущее значение можно посмотреть, выполнив:

```
# cat /sys/devices/system/cpu/cpufreq/ondemand/up_threshold

```

Значение по-умолчанию равно `95`, в версии ядра 2.6.37\. Это значит, что частота повысится, как только загрузка процессора достигнет 95%. Можете изменить это значение, запустив:

```
echo "15" > /sys/devices/system/cpu/cpufreq/ondemand/up_threshold

```

**Note:** Минимальное допустимое значение, которое Вы вводите, должно быть не ниже значение в файле down_threshold; если Вы попробуете внести меньшее значение, bash вернет ошибку: "bash: echo: write error: Invalid argument"

**Note:** Добавление строки с помощью команды echo в файл `/etc/rc.local` позволит настройке "пережить" перезагрузку. Однако, должен быть выставлен гувернер `ondemand`.

Если Вы не хотите дожидаться загрузки демона cpufreq при старте системы (например, чтобы уменьшить время загрузки), добавьте это в файл `/etc/rc.local`:

```
(sleep 30 && sh -c "echo -n 75 > /sys/devices/system/cpu/cpu0/cpufreq/ondemand/up_threshold")& 

```

#### Взаимодействие с событиями ACPI

Пользователи могут сконфигурировать автоматическое масштабирование при различных событиях ACPI, таких как подключение устройства питания или закрытия крышки ноутбука. Эти события определяются в `/etc/acpi/handler.sh`. Если пакет [acpid](https://www.archlinux.org/packages/?name=acpid) установлен, этот файл уже должен существовать по указанному пути. Например, чтобы изменить регулятор с `performance` на `conservative` при отключении устройства питания и вернуть его на место при подключении:

```
/etc/acpi/handler.sh

```

```
[...]

 ac_adapter)
     case "$2" in
         AC*)
             case "$4" in
                 00000000)
                     echo "conservative" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor    
                     echo -n $minspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode start
                 ;;
                 00000001)
                     echo "performance" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
                     echo -n $maxspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode stop
                 ;;
             esac
         ;;
         *) logger "ACPI action undefined: $2" ;;
     esac
 ;;

[...]

```

### Демон

`cpufrequtils` также включает в себя демона, который позволяет установить регулятор масштабирования и частоту процессора при старте системы, без использования дополнительных пакетов, таких как *kpowersave*.

Перед тем, как запустить демона, отредактируйте `/etc/conf.d/cpufreq`. Выберите нужный Вам регулятор, выставите минимальную/максимальную частоту процессора, к примеру:

```
/etc/conf.d/cpufreq

```

```
#configuration for cpufreq control

# valid governors:
#  ondemand, performance, powersave,
#  conservative, userspace
governor="ondemand"

# valid suffixes: Hz, kHz (default), MHz, GHz, THz
min_freq="1GHz"
max_freq="2GHz"

```

**Note:** Точные значения минимальной и максимальной частоты процессора можно узнать, запустив `cpufreq-info` после загрузки драйвера ЦП (`modprobe acpi-cpufreq`). Эти значения задавать необязательно. Вы можете закомментировать строки min/max_freq. Масштабирование будет работать автоматически.

После настройки можете запустить демона:

```
# /etc/rc.d/cpufreq start

```

Для автоматического запуска демона при старте системы, добавьте `cpufreq` в массив DAEMONS в файле `/etc/rc.conf`. К примеру:

```
DAEMONS=(syslog-ng networkmanager @alsa @crond @cupsd **@cpufreq**)

```

## Устранение неисправностей

*   Некоторые приложения, например, [ntop](/index.php/Ntop "Ntop"), могут некорректно работать при масштабировании частоты. В случае с ntop может произойти сегментация или Вы можете потерять информацию, так как регулятор `ondemand` не может достаточно быстро среагировать на повышение нагрузки на процессор и повысить частоту, а текущей частоты не хватит для обработки всех пакетов, пришедших на сетевой интерфейс.

*   Некоторые модели процессоров могут не очень хорошо работать на стандартных настройках регулятора `ondemand` (например, видео воспроизводится с рывками или тормозит анимация окон). Это можно решить, не только отключив полностью масштабирование частоты. Также можно увеличить "агрессивность" переключения частоты. Просто снизьте значение переменной *up_threshold* для каждого процессора. См. [изменение параметров работы регулятора ondemand](/index.php/Cpufrequtils_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D1.80.D0.B5.D0.B3.D1.83.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_ondemand "Cpufrequtils (Русский)").

*   Иногда демон задает не максимальную частоту процессора, а частоту немного меньше (2.99МГц вместо 3МГц). В этой ситуации задайте значение максимальной частоты немного больше максимальной. Например, если максимальная частота процесстора 3МГц, задайте переменной max_freq значение 3.01МГц.

*   Некоторые модели BIOS испытывают трудности с масштабированием частот, да и с переключением на повышенные частоты. Правда, это можно обойти. Добавьте строку "processor.ignore_ppc=1" в загрузку ядра или установите значение /sys/module/processor/parameters/ignore_ppc равное 1.

*   Некоторые комбинации драйверов ALSA и звуковых карт могут вызвать заикание звука во время переключения частот регулятором. Пока это можно решить только отключением регулятора масшабирования.