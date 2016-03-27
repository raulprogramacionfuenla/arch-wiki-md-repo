[Xcompmgr](http://cgit.freedesktop.org/xorg/app/xcompmgr/) - это простой [композитный менеджер окон](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BE%D0%BC%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80_%D0%BE%D0%BA%D0%BE%D0%BD "wikipedia:ru:Композитный менеджер окон"), умеющий прорисовывать тени и создавать примитивную прозрачность с помощью **transset**. Разработан как доказательство возможности существования легковесных альтернатив Compiz Fusion.

Так как xcompmgr не заменяет оконный менеджер, он является идеальным для придания элегантности легковестным [оконным менеджерам](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)")

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Форки и обновленные версии](#.D0.A4.D0.BE.D1.80.D0.BA.D0.B8_.D0.B8_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Прозрачность окон](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BE.D0.BA.D0.BE.D0.BD)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Запуск/остановка xcompmgr по требованию](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA.2F.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_xcompmgr_.D0.BF.D0.BE_.D1.82.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [3.2 Переключатель Xcompmgr](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B0.D1.82.D0.B5.D0.BB.D1.8C_Xcompmgr)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Падает Mozilla Firefox при работающем флеше](#.D0.9F.D0.B0.D0.B4.D0.B0.D0.B5.D1.82_Mozilla_Firefox_.D0.BF.D1.80.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.89.D0.B5.D0.BC_.D1.84.D0.BB.D0.B5.D1.88.D0.B5)
    *   [4.2 Картинка оказывается светло-серой после входа в систему (например в Openbox)](#.D0.9A.D0.B0.D1.80.D1.82.D0.B8.D0.BD.D0.BA.D0.B0_.D0.BE.D0.BA.D0.B0.D0.B7.D1.8B.D0.B2.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D1.81.D0.B2.D0.B5.D1.82.D0.BB.D0.BE-.D1.81.D0.B5.D1.80.D0.BE.D0.B9_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83_.28.D0.BD.D0.B0.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80_.D0.B2_Openbox.29)
    *   [4.3 BadPicture request в awesome](#BadPicture_request_.D0.B2_awesome)
    *   [4.4 Экран не обновляется в awesome после изменения разрешения](#.D0.AD.D0.BA.D1.80.D0.B0.D0.BD_.D0.BD.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D0.B2_awesome_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F)

## Установка

Перед установкой Xcompmgr, убедитесь в правильности установки и настройки [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"). Чтобы убедиться, что расширение [Composite](/index.php/Composite "Composite") включено для X Server, выполните:

 `$ xdpyinfo | grep Composite`  `Composite` 

Если вывод отсутствует, добавьте опцию `Composite` в раздел `Extensions` в xorg.conf:

 `/etc/X11/xorg.conf` 
```
Section "Extensions"
        Option  "Composite" "true"
EndSection
```

Xcompmgr может быть [установлен](/index.php/Pacman "Pacman") из пакета [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr), доступного в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Для обеспечения прозрачности также необходимо установить [transset-df](https://www.archlinux.org/packages/?name=transset-df) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Для примера см. [Xterm#Automatic transparency](/index.php/Xterm#Automatic_transparency "Xterm").

### Форки и обновленные версии

Существуют форки, в которые внесены различные исправления:

*   **xcompmgr-dana** — Один из первых форков Xcompmgr.

	[http://oliwer.net/xcompmgr-dana/](http://oliwer.net/xcompmgr-dana/) || [xcompmgr-dana](https://aur.archlinux.org/packages/xcompmgr-dana/)

*   **[Compton](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)")** — Форк Xcompmgr, содержащий большинство предыдущих исправлений и многие другие.

	[https://github.com/chjj/compton](https://github.com/chjj/compton) || [compton-git](https://aur.archlinux.org/packages/compton-git/)

## Настройка

Для запуска `xcompmgr`, выполните:

```
$ xcompmgr -c

```

Для автозагрузки с сеансом X, добавьте следущее в [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)"):

```
xcompmgr -c &

```

Вместо `-c` Вы можете экспериментировать с другими настройками  изменив отбрасывание теней или даже включить затухание. Пример:

```
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &

```

Для получения полного списка опций, выполните:

```
$ xcompmgr --help

```

### Прозрачность окон

Хотя практическое применение ограничено из-за его низкой производительности, `transset-df` может быть использована для установки прозрачности отдельных окон.

Чтобы установить прозрачность окна программы, убедитесь, что она запущена, затем выполните:

```
$ transset-df *прозрачность*

```

где *прозрачность* это число от 0 до 1, где 0 - абсолютная прозрачность, а 1 - непрозрачный.

Курсор превратится в крест. Наведите его на желаемую программу. Например, `transset-df 0.25` установит прозрачность до 75%.

## Советы и рекомендации

### Запуск/остановка xcompmgr по требованию

Этот скрипт (например в ~/bin) позволяет легко остановить/перезапустить композитный менеджер.

 `~/.bin/comp` 
```
#!/bin/bash
#
# Start a composition manager.
# (xcompmgr in this case)

comphelp() {
    echo "Composition Manager:"
    echo "   (re)start: COMP"
    echo "   stop:      COMP -s"
    echo "   query:     COMP -q"
    echo "              returns 0 if composition manager is running, else 1"
    exit
}

checkcomp() {
    pgrep xcompmgr &>/dev/null
}

stopcomp() {
    checkcomp && killall xcompmgr
}

startcomp() {
    stopcomp
    # Example settings only. Replace with your own.
    xcompmgr -CcfF -I-.015 -O-.03 -D6 -t-1 -l-3 -r4.2 -o.5 &
    exit
}

case "$1" in
    "")   startcomp ;;
    "-q") checkcomp ;;
    "-s") stopcomp; exit ;;
    *)    comphelp ;;
esac

```

Для удобства использования скрипта можно определить горячие клавиши, используя, например, [Xbindkeys](/index.php/Xbindkeys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xbindkeys (Русский)"). Это позволит перезапускать или временно приостанавливать xcompmgr в случае необходимости, не прерывая работу.

### Переключатель Xcompmgr

Следующий скрипт для привязки любой горячей клавиши:

```
#!/bin/bash

if pgrep xcompmgr &>/dev/null; then
    echo "Turning xcompmgr ON"
    xcompmgr -c -C -t-5 -l-5 -r4.2 -o.55 &
else
    echo "Turning xcompmgr OFF"
    pkill xcompmgr &
fi

exit 0

```

## Решение проблем

### Падает Mozilla Firefox при работающем флеше

Вы можете исправить это, создав файл `/etc/profile.d/flash.sh`, содержащий строку:

```
export XLIB_SKIP_ARGB_VISUALS=1

```

**Важно:** Это отключит эффекты композитинга.

### Картинка оказывается светло-серой после входа в систему (например в Openbox)

Эта ошибка исправляется путем установки [hsetroot](https://aur.archlinux.org/packages/hsetroot/) и настройкой цвета фона, выполнив `hsetroot -solid "#000000"` (введите код нужного цвета, вместо *#000000*) до `xcompmgr`.

### BadPicture request в awesome

Если вы получаете следующую ошибку в [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)"):

```
 error 163: BadPicture request 149 minor 8 serial 34943
 error 163: BadPicture request 149 minor 8 serial 34988
 error 163: BadPicture request 149 minor 8 serial 35033

```

просто установите [feh](/index.php/Feh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Feh (Русский)") и перезапустите [awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)").

### Экран не обновляется в awesome после изменения разрешения

При использовании внешнего монитора могут возникнуть проблемы при автоматическом изменении разрешения экрана: часть экрана становится "застывшей" и больше не обновляется. Эта проблема возникает из-за первоначального изменения разрешения (происходит перед пуском Xcompmgr), а также при установки фона в [awesome](/index.php/Awesome "Awesome") с помощью [feh](/index.php/Feh "Feh").

Чтобы исправить это, необходимо установить [hsetroot](https://aur.archlinux.org/packages/hsetroot/) из [[official repositories (Русский)|официальных репозиториев] и добавить следующую строку в `.xinitrc` перед `xcompmgr`:

```
hsetroot -solid "#000066"

```

(можно заменить *#000066* на любой другой цвет).