Related articles

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Функциональность файлового менеджера](/index.php/%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0 "Функциональность файлового менеджера")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Сравнение тайловых оконных менеджеров](/index.php/%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%82%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D1%85_%D0%BE%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D1%85_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%BE%D0%B2 "Сравнение тайловых оконных менеджеров")
*   [Clipboard](/index.php/Clipboard "Clipboard")
*   [Автозапуск#Графический](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA#Графический "Автозапуск")

**Состояние перевода:** На этой странице представлен перевод статьи [i3](/index.php/I3 "I3"). Дата последней синхронизации: 4 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=I3&diff=0&oldid=403050).

[i3](http://i3wm.org/) это динамический [тайловый оконный менеджер](https://en.wikipedia.org/wiki/Tiling_window_manager "wikipedia:Tiling window manager") вдохновленный [wmii](/index.php/Wmii "Wmii") и нацеленный на разработчиков и опытных пользователей.

Клиенты (окна) располагаются внутри контейнеров и организованы в древовидную структуру. Ветки дерева могут быть разделены горизонтально или вертикально, сами контейнеры могут быть сгруппированы в режиме вкладок и в стековом режиме. Окно также может быть плавающим, однако будет располагаться на отдельном слое поверх остальных окон.

Заявленные цели для i3 содержат четкую документацию, надлежащую поддержку нескольких мониторов, древовидную структуру для окон, а также различные режимы, как в [vim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vim (Русский)").

## Contents

*   [1 Установка](#Установка)
    *   [1.1 Экранный менеджер](#Экранный_менеджер)
    *   [1.2 xinitrc](#xinitrc)
*   [2 Использование](#Использование)
    *   [2.1 Запуск приложений](#Запуск_приложений)
    *   [2.2 Назначение клавиш](#Назначение_клавиш)
    *   [2.3 Контейнеры](#Контейнеры)
*   [3 Настройка](#Настройка)
    *   [3.1 Цветовые схемы](#Цветовые_схемы)
    *   [3.2 i3bar](#i3bar)
        *   [3.2.1 Альтернативы i3bar](#Альтернативы_i3bar)
    *   [3.3 i3status](#i3status)
        *   [3.3.1 Замены i3status](#Замены_i3status)
        *   [3.3.2 Оболочки для i3status](#Оболочки_для_i3status)
        *   [3.3.3 Шрифты-иконки в строке состояния](#Шрифты-иконки_в_строке_состояния)
    *   [3.4 Эмулятор терминала](#Эмулятор_терминала)
*   [4 Советы и хитрости](#Советы_и_хитрости)
    *   [4.1 Расширенная навигация по окнам](#Расширенная_навигация_по_окнам)
    *   [4.2 Быстрый переход к открытому окну](#Быстрый_переход_к_открытому_окну)
    *   [4.3 Быстро перейти к необходимому окну](#Быстро_перейти_к_необходимому_окну)
    *   [4.4 Сохранить и восстановить расположение окон](#Сохранить_и_восстановить_расположение_окон)
        *   [4.4.1 Сохранить текущее расположение окон одного рабочего пространства](#Сохранить_текущее_расположение_окон_одного_рабочего_пространства)
        *   [4.4.2 Восстановить расположение окон на рабочем пространстве](#Восстановить_расположение_окон_на_рабочем_пространстве)
    *   [4.5 Контейнер для электронного блокнота](#Контейнер_для_электронного_блокнота)
    *   [4.6 Хранитель экрана и управление питанием](#Хранитель_экрана_и_управление_питанием)
    *   [4.7 Выключение, перезагрузка, блокировка экрана](#Выключение,_перезагрузка,_блокировка_экрана)
    *   [4.8 Вкладки или стековый просмотр веб-страниц](#Вкладки_или_стековый_просмотр_веб-страниц)
    *   [4.9 Переменные рабочих областей](#Переменные_рабочих_областей)
    *   [4.10 Правильное обращение с плавающими диалогами](#Правильное_обращение_с_плавающими_диалогами)
    *   [4.11 Скорость Загрузки/Отдачи сети в statusbar](#Скорость_Загрузки/Отдачи_сети_в_statusbar)
*   [5 Патчи](#Патчи)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 Общее](#Общее)
    *   [6.2 Кнопки в строке сообщений i3 не работают](#Кнопки_в_строке_сообщений_i3_не_работают)
    *   [6.3 Неисправная строка оболочки в тайловом терминале](#Неисправная_строка_оболочки_в_тайловом_терминале)
    *   [6.4 Курсор мыши остается в режиме ожидания](#Курсор_мыши_остается_в_режиме_ожидания)
    *   [6.5 Не реагируют сочетания клавиш](#Не_реагируют_сочетания_клавиш)
    *   [6.6 Тиринг (разрыв картинки по горизонтали)](#Тиринг_(разрыв_картинки_по_горизонтали))
*   [7 Смотри также](#Смотри_также)

## Установка

Установите из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") [группу пакетов](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_группы_пакетов "Pacman (Русский)") `i3`, которая включает пакеты:

*   [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) - непосредственно менеджер окон
*   [i3status](https://www.archlinux.org/packages/?name=i3status), предназначенный для вывода строки статуса в i3bar через [stdout](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_.28stdout.29 "wikipedia:Standard streams")
*   [i3lock](https://www.archlinux.org/packages/?name=i3lock) - блокировщик экрана

Дополнительные пакеты доступны в [пользовательском репозитории Arch](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Установите [i3-git](https://aur.archlinux.org/packages/i3-git/), чтобы получить версию для разработчиков.

Также смотрите раздел [#Патчи](#Патчи).

### Экранный менеджер

[i3-wm](https://www.archlinux.org/packages/?name=i3-wm) включает в себя `i3.desktop` как [Xsession](/index.php/Xsession "Xsession") который запускает оконный менеджер. `i3-with-shmlog.desktop` включает логи (полезно для отладки). Установите [i3-gnome](https://aur.archlinux.org/packages/i3-gnome/), чтобы добавить сессию [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)").

### xinitrc

Отредактируйте ваш `~/.xinitrc`, добавив в него:

```
exec i3

```

Если вы хотите, чтобы i3 вел лог (полезно для отладки), добавьте эту строку в `~/.xinitrc`:

```
exec i3 -V >> ~/.i3/i3log 2>&1

```

Если вы используете бинарный драйвер Nvidia **<302.17**, то вам следует добавить флаг --force-xinerama в `~/.xinitrc`. Подробное описание можно найти на [i3wm.org](http://i3wm.org/docs/multi-monitor.html).

```
exec i3 --force-xinerama

```

Если у вас есть проблемы с преобразованием клавиш (например `;` точки с запятой), используйте [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) или смотрите [Extra keyboard keys (Русский)](/index.php/Extra_keyboard_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Extra keyboard keys (Русский)").

```
$ xev | grep -A2 --line-buffered '^KeyRelease' | sed -n '/keycode /s/^.*keycode \([0-9]*\).* (.*, \(.*\)).*$/\1 \2/p'

```

## Использование

Для большей информации смотрите [официальную документацию](http://i3wm.org/docs), а именно [i3 Пользовательское Руководство](http://i3wm.org/docs/userguide.html).

### Запуск приложений

i3 использует [dmenu](/index.php/Dmenu "Dmenu") в качестве запуска приложений, которое вызывается по умолчанию `$mod+d`. В качестве альтернативы, можно использовать [dmenu2](https://aur.archlinux.org/packages/dmenu2/) из AUR которое имеет намного больше возможностей, включая прозрачность и поддержку шрифтов Xft.

[i3-wm](https://www.archlinux.org/packages/?name=i3-wm) содержит *i3-dmenu-desktop*, [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") оболочку для *dmenu* который использует [desktop entries](/index.php/Desktop_entries "Desktop entries") для создания списка всех установленных приложений. Кроме того, пакет [j4-dmenu-desktop-git](https://aur.archlinux.org/packages/j4-dmenu-desktop-git/) может быть использован; это небольшая замена *i3-dmenu-desktop*, но более быстрая [1](https://github.com/enkore/j4-dmenu-desktop/blob/master/README.md).

### Назначение клавиш

В i3, команды вызываются с помощью клавиши модификатора, называющейся `$mod`. По умолчанию (Mod1) это `Alt`, с популярной альтернативой (Mod4), которая известна как `Super`.

Смотрите [справочную карту i3](http://i3wm.org/docs/refcard.html) и [Использование i3](http://i3wm.org/docs/userguide.html#_using_i3) по умолчанию. Смотрите [назначение клавиш](http://i3wm.org/docs/userguide.html#keybindings) чтобы добавить новые сочетания/горячие клавиши.

### Контейнеры

i3 управляет окнами в виде древовидной структуры, с контейнерами, как со строительными блоками. Эта структура филиалов с горизонтальным или вертикальным разделением. Контейнеры по умолчанию тайловые (tiled), но могут быть установлены как стэковые лэйауты (stacked layouts), таки в плавающем режиме (floating) (например для диалоговых окон). Плавающие окна всегда поверх.

Для подробностей смотрите [Дерево i3](http://i3wm.org/docs/userguide.html#_tree) и [Данные древовидной структуры и контейнеров](http://www.youtube.com/watch?v=AWA8Pl57UBY).

## Настройка

Для подробностей смотрите [Настройку i3](http://i3wm.org/docs/userguide.html#configuring). Данная статья предполагает, что файл настроек *i3* расположен в папке `~/.config`.

### Цветовые схемы

Файл настроек позволяет настраивать цвет оформления окон, но синтаксис непрактичен для создавания или использования. Есть несколько проектов, которые делают это проще и включают в себя различные вложенные пользователями темы.

*   **i3-style** — Изменяет ваш файл настроек в месте темы, на использование объекта JSON, предназначенного для частой доводки или изменения цветовой схемы

	[https://github.com/acrisci/i3-style](https://github.com/acrisci/i3-style) || [nodejs-i3-style](https://aur.archlinux.org/packages/nodejs-i3-style/)

*   **j4-make-config** — Объединяет ваш файл настроек с коллекцией тем или персональных частей настроек, например настройка host-specific, позволяет быстро и гибко измененять темы, динамически кастомизировать настройки.

	[https://github.com/okraits/j4-make-config](https://github.com/okraits/j4-make-config) || [j4-make-config-git](https://aur.archlinux.org/packages/j4-make-config-git/)

### i3bar

В дополнение к показу информации рабочих областей, i3 bar может выступать в качестве входных данных для i3status или альтернативы, такие как те, которые упомянуты в следующем разделе. Например:

 `~/.config/i3/config` 
```
bar {
    output            LVDS1
    status_command    i3status
    position          top
    mode              hide
    workspace_buttons yes
    tray_output       none

    font -misc-fixed-medium-r-normal--13-120-75-75-C-70-iso10646-1

    colors {
        background #000000
        statusline #ffffff

        focused_workspace  #ffffff #285577
        active_workspace   #ffffff #333333
        inactive_workspace #888888 #222222
        urgent_workspace   #ffffff #900000
    }
}
```

За дополнительной информацией обращайтесь в раздел [Configuring i3bar](http://i3wm.org/docs/userguide.html#_configuring_i3bar) официального руководства пользователя.

#### Альтернативы i3bar

Некоторые пользователи предпочитают панели, такие как те, которые предусмотрены обычными [Средами рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"). Это может быть реализовано в i3, путём запуска приложения панели во время загрузки.

Для [панели XFCE](/index.php/Xfce#Panel "Xfce"), добавьте следующую строку в любом месте `~/.config/i3/config`:

```
exec --no-startup-id xfce4-panel --disable-wm-check

```

Можно отключить i3bar закомментировав секцию `bar{ }` в `~/.config/i3/config` или используя:

 `~/.config/i3/config` 
```
# bar toggle, hide or show 
bindsym $mod+m bar mode toggle

```

Таким образом, вы можете показать или скрыть бар когда пожелаете.

### i3status

Скопируйте файлы настроек по умолчанию в домашний каталог:

```
$ cp /etc/i3status.conf ~/.config/i3status/config

```

Не все плагины определяются в настройках по умолчанию, и некоторые значения настроек могут быть недействительными для вашей системы, поэтому должны быть внесены соответствующие изменения. Для подробностей смотрите [i3status(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/i3status.1).

#### Замены i3status

*   **[conky](/index.php/Conky "Conky")** — Высоко расширяемая система мониторинга. Для использования с i3bar см [этот учебник](http://i3wm.org/docs/user-contributed/conky-i3bar.html)

	[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **i3blocks** — Расширяется с помощью shell-скриптов. Может обрабатывать события мыши, прерывания, и определение интервалов регенерации на основе каждого блока.

	[https://github.com/vivien/i3blocks](https://github.com/vivien/i3blocks) || [i3blocks](https://www.archlinux.org/packages/?name=i3blocks)

*   **i3phtatus** — Легко расширяемая замена i3status предназначена для i3bar, написан на PHP.

	[https://github.com/mwgg/i3phtatus](https://github.com/mwgg/i3phtatus) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **i3pystatus** — Расширяемый Python 3 статус бар со множеством плагинов и опций настроек по умолчанию.

	[https://github.com/enkore/i3pystatus](https://github.com/enkore/i3pystatus) i3pystatus || [i3pystatus-git](https://aur.archlinux.org/packages/i3pystatus-git/)

*   **i3situation** — Другой Python 3 генератор статус бара.

	[https://github.com/HarveyHunt/i3situation](https://github.com/HarveyHunt/i3situation) || [i3situation-git](https://aur.archlinux.org/packages/i3situation-git/)

*   **j4status** — Обеспечивает строку статуса, настраиваемую с помощью плагинов, написан на C.

	[http://j4status.j4tools.org/](http://j4status.j4tools.org/) || [j4status-git](https://aur.archlinux.org/packages/j4status-git/)

#### Оболочки для i3status

*   **[h2status](/index.php/H2status "H2status")** — Баш оболочка для i3status, позволяет в качестве входных данных использовать записи в формате JSON, и может обрабатывать события мыши, а также асинхронные обновления в строке состояния.

	[H2status](/index.php/H2status "H2status") || [h2status](https://aur.archlinux.org/packages/h2status/)

*   **i3cat** — на основе оболочки [go](/index.php/Go "Go"), которая может объединить ввод данных из нескольких внешних источников. Может обрабатывать события мыши и перенаправление указаных пользователем сигналов для своих подпроцессов.

	[http://vincent-petithory.github.io/i3cat/](http://vincent-petithory.github.io/i3cat/) || [i3cat-git](https://aur.archlinux.org/packages/i3cat-git/)

*   **py3status** — Расширяемая оболочка i3status написанная на Python.

	[https://github.com/ultrabug/py3status](https://github.com/ultrabug/py3status) || [py3status](https://www.archlinux.org/packages/?name=py3status)

*   **YaGoStatus** — Еще одна оболочка для i3status (и не только) написанная на Go.

	[https://github.com/burik666/yagostatus](https://github.com/burik666/yagostatus) || [yagostatus-git](https://aur.archlinux.org/packages/yagostatus-git/)

#### Шрифты-иконки в строке состояния

*i3bar* может быть [пропатчен](#Патчи) для поддержки XBM icon, но вместо этого, вы можете использовать шрифты-иконки.

*   **ttf-font-awesome** — Масштабируемые векторные иконки, которые могут быть настроены с помощью CSS. [http://fortawesome.github.io/Font-Awesome/cheatsheet/](http://fortawesome.github.io/Font-Awesome/cheatsheet/) Шпаргалка] показывающая пункт Unicode для каждого символа.

	[http://fortawesome.github.io/Font-Awesome/](http://fortawesome.github.io/Font-Awesome/) || [ttf-font-awesome](https://www.archlinux.org/packages/?name=ttf-font-awesome)

*   **ttf-font-icons** — Непересекающаяся и последовательная смесь Awesome и Ionicons. Она также позволяет избежать дублирования между DejaVu Sans и Awesome.

	[https://www.dropbox.com/s/9iysh2i0gadi4ic/icons.pdf](https://www.dropbox.com/s/9iysh2i0gadi4ic/icons.pdf) || [ttf-font-icons](https://aur.archlinux.org/packages/ttf-font-icons/).

Чтобы объединить шрифты, определите последовательность переходящего в резерв шрифта в вашем файле настроек, отделяя шрифты `,` вот так:

 `~/.config/i3/config` 
```
bar {
  ...
  font pango:DejaVu Sans Mono, Icons 8
  ...
}
```

В соответствии с [синтаксисом pango](https://developer.gnome.org/pango/stable/pango-Fonts.html#pango-font-description-from-string), размер шрифта задается только один раз, список семейств шрифтов разделяется запятой. Установка размера для каждого шрифта применится ко всем, кроме последнего, который будет игнорироваться.

Добавьте иконки в формат строки в `~/.config/i3status/config` используя числа Unicode, приведенные в шпаргалке, указанной выше. Метод ввода будет варьироваться между текстовыми редакторами. Например, чтобы вставить значок "heart" (номер unicode f004):

*   в различных текстовых редакторах графического интерфейса (например [gedit](/index.php/Gedit "Gedit"), Leafpad) и терминалов (например GNOME Terminal, xfce4-terminal): `ctrl+shift+u`, `f004`, `Enter`
*   в [Emacs](/index.php/Emacs "Emacs"): `ctrl+x`, `8`, `Enter`, `f004`, `Enter`
*   в [Vim (Русский)](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vim (Русский)") (в режиме вставки): `Ctrl+v`, `uf004`
*   в [urxvt (Русский)](/index.php/Urxvt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Urxvt (Русский)"): удерживая `Ctrl+Shift`, наберите `f004`

### Эмулятор терминала

По умолчанию при нажатии `$mod+Return` запускается `i3-sensible-terminal` представляющий собой скрипт, вызывающий терминал. Для порядка вызова терминала, смотрите [i3-sensible-terminal(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/i3-sensible-terminal.1).

Вместо запуска выбора терминала, измените эту строку в `~/.config/i3/config`:

```
bindsym $mod+Return exec i3-sensible-terminal

```

Кроме того, [установите](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#На_системном_уровне "Environment variables (Русский)") переменную `$TERMINAL`:

```
$ export TERMINAL=*Ваш Терминал*

```

## Советы и хитрости

### Расширенная навигация по окнам

Смотрите [i3, советы по навигациям в окнах (Англ.)](http://www.slackword.net/?p=657).

### Быстрый переход к открытому окну

*   [quickswitch-for-i3](https://github.com/proxypoke/quickswitch-for-i3) – утилита, написанная на python, позволяющая быстро пеходить к окнам и менять их расположение.
*   **i3-wm-scripts** — search for and jump to windows with particular names matching regexp

	[https://github.com/yiuin/i3-wm-scripts](https://github.com/yiuin/i3-wm-scripts) ||

*   **winmenupy** — Launches dmenu with a list of clients, sorted after workspaces. Selecting a client jumps to that window.

	[https://github.com/ziberna/i3-py/blob/master/examples/winmenu.py](https://github.com/ziberna/i3-py/blob/master/examples/winmenu.py) ||

*   **rofi** — Search and jump to open and scratchpad window

	[https://davedavenport.github.io/rofi/](https://davedavenport.github.io/rofi/) || [rofi](https://www.archlinux.org/packages/?name=rofi)

### Быстро перейти к необходимому окну

Добавьте в`.i3/config`: [[3]](https://faq.i3wm.org/question/853/how-to-jump-to-urgent-workspace/)

```
bindsym $mod+x [urgent=latest] focus

```

### Сохранить и восстановить расположение окон

Начиная с версии 4.8, и дальше *i3* может сохранить и восстановить рабочее пространство слоёв (лэйаутов). Чтобы это сделать, необходимы следующие пакеты: [perl-anyevent-i3](https://www.archlinux.org/packages/?name=perl-anyevent-i3) и [perl-json-xs](https://www.archlinux.org/packages/?name=perl-json-xs) из [оффициальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

**Примечание:** В этом разделе предоставлен быстрый урок о том как сохранить текущую раскладку окон из одного рабочего пространства, и как восстановить его для дальнейшего использования. Обратитесь к [официальной документации](http://i3wm.org/docs/layout-saving.html) для подробностей.

#### Сохранить текущее расположение окон одного рабочего пространства

Чтобы сохранить текущее расположение окон, выполните следующие действия:

1.  Во-первых, выполните различные команды, чтобы открыть окна в предпочтительной рабочей области и измените их размер, если это необходимо. Совершите запись каждой выполненной команды для каждого окна.
2.  Теперь, в новой рабочей области откройте терминал и запустите следующее: `i3-save-tree --workspace N > ~/.i3/workspace_N.json` где N есть число предпочтительной рабочей области. Это позволит сохранить текущую структуру рабочей области N в файл `~/.i3/workspace_N.json`.
3.  Вновь созданный файл должен быть отредактирован, однако это может быть сделано с помощью следующих команд: `tail -n +2 ~/.i3/workspace_N.json | fgrep -v '// splitv' | sed 's|//||g' > ~/.i3/workspace_N.json` 

#### Восстановить расположение окон на рабочем пространстве

Есть два способа восстановить расположение окон на рабочем пространстве: написав сценарий, или отредактировать `~/.i3/config` для автоматической загрузки макета. В этом разделе только первый случай будет рассматриваться, обратитесь к [официальной документации](http://i3wm.org/docs/layout-saving.html#_restoring_the_layout) для второго случая.

Для восстановления сохраненного макета в предыдущем разделе, создайте файл с именем`load_layout.sh` со следующим содержанием:

*   Исходные строки:

 `~/load_layout.sh` 
```
#!/bin/bash
i3-msg "workspace M; append_layout ~/.i3/workspace_N.json"
```

где М - номер рабочей области, в которую вы хотели бы загрузить ранее сохраненный макет, и N это номер рабочей области сохранённой в предыдущем разделе.

*   И команды исполльзуемые в предыдущей секции чтобы получить нужные окна, но заключённые в круглые скобки и амперсандом (&) перед последней скобкой.

Например, если сохранённый макет содержит три `uxterm` окна:

 `~/load_layout.sh` 
```
#!/bin/bash

# Во-первых, мы добавим сохраненный макет рабочей области N в рабочую область M
i3-msg "workspace M; append_layout ~/.i3/workspace_N.json"

# И, наконец, мы заполним контейнеры программами
(uxterm &)
(uxterm &)
(uxterm &)
```

Затем установим файл как исполняемый:

```
chmod u+x ~/load_layout.sh

```

И, наконец, расположение рабочих областей N может быть загружено в рабочие области М, запустив:

```
~/load_layout.sh

```

**Совет:** Добавьте`bindsym $mod+g exec ~/load_layout.sh` в `~/.i3/config` и перезапустите i3, сочетание Mod+g запустит этот скрипт.

**Примечание:** Если сценарий, описанный выше, не работает как следует, обратитесь к [официальной документации](http://i3wm.org/docs/layout-saving.html#_editing_layout_files). Секции *swallows* в `~/.i3/workspace_N.json` нужно редактировать вручную.

### Контейнер для электронного блокнота

По умолчанию, [scratchpads (блокноты)](http://i3wm.org/docs/userguide.html#_scratchpad) содержат только одно окно. Однако контейнеры также могут быть сделаны блокнотом.

Создайте новый контейнер (например, `Mod+Enter`), разделите их (`Mod+v`) и создайте другой контейнер. Сфокусируйтесь на родительском (`Mod+a`), разделите в противоположном направлении (`Mod+h`), и создайте снова.

Фокус на первом контейнере (с акцентом родительского по мере необходимости), сделайте окно плавающим (floating) (`Mod+Shift+Space`), и переместите его в блокнот (`Mod+Shift+-`). Теперь вы можете разделить контейнеры по предпочтению.

**Примечание:** Контейнеры не могут быть изменены индивидуально в плавающих окнах. Измените размер контейнеров до создания плавающих окон.

**Совет:** При использовании только терминальных приложений, рассмотрим мультиплексор, такой как [tmux](/index.php/Tmux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Tmux (Русский)").

Смотрите также [[4]](https://faq.i3wm.org/question/138/multiple-scratchpad/i3).

### Хранитель экрана и управление питанием

Вы можете использовать [DPMS](/index.php/DPMS "DPMS") на пустом экране или отправлять в режим ожидания/отключать ваш монитор. Добавьте следующие строки в ваш `~/.config/i3/config` чтобы отправить ваш монитор в режим ожидания после 10 минут простоя.

```
exec --no-startup-id xset dpms 600

```

С [xss-lock-git](https://aur.archlinux.org/packages/xss-lock-git/) вы можете зарегистрировать скринлокер (экранный блокировщик) для вашей сессии i3\. xss-lock подписывается на systemd-events `suspend`, `hibernate`, `lock-session`, и `unlock-session` с соответствующими действиями (запускает блокировщик и ждёт пока пользователь не разблокирует или не убъёт процесс блокировщика). Он также реагирует на [X screensaver](/index.php/Display_Power_Management_Signaling#xset_screen-saver_control "Display Power Management Signaling") и работает или убивает блокировщик в ответ на сигналы x-сервера. Запустите xss-lock в вашем [автозапуске](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Autostarting (Русский)") добавив следующее:

```
xss-lock -- i3lock -n -i *background_image.png* &

```

Кроме того, вы можете использовать [xautolock](https://www.archlinux.org/packages/?name=xautolock) для блокировки экрана после заданного периода времени:

```
xautolock -time 10 -locker "i3lock -i *background_image.png*" &

```

Смотрите также [#Выключение, перезагрузка, блокировка экрана](#Выключение,_перезагрузка,_блокировка_экрана) и [Pm-utils#Creating your own hooks](/index.php/Pm-utils#Creating_your_own_hooks "Pm-utils").

### Выключение, перезагрузка, блокировка экрана

Так как нет иконок на экране для Выключения, Перезагрузки и Блокировки Экрана, для удобства, мы можем задать комбинацию горячих клавиш. Ниже предпологается, что установлен [polkit](https://www.archlinux.org/packages/?name=polkit), чтобы позволять обычным (не привелигелированным) пользователям запускать команды [управления питанием](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Управление_питанием "Systemd (Русский)").

Добавьте следующие строки в ваш `~/.config/i3/config`, по завершению вам будет предложен запрос, когда вы нажимаете `$mod+pause`.

```
set $Locker i3lock && sleep 1

set $mode_system System (l) lock, (e) logout, (s) suspend, (h) hibernate, (r) reboot, (Shift+s) shutdown
mode "$mode_system" {
    bindsym l exec --no-startup-id $Locker, mode "default"
    bindsym e exec --no-startup-id i3-msg exit, mode "default"
    bindsym s exec --no-startup-id $Locker && systemctl suspend, mode "default"
    bindsym h exec --no-startup-id $Locker && systemctl hibernate, mode "default"
    bindsym r exec --no-startup-id systemctl reboot, mode "default"
    bindsym Shift+s exec --no-startup-id systemctl poweroff -i, mode "default"  

    # back to normal: Enter or Escape
    bindsym Return mode "default"
    bindsym Escape mode "default"
}

bindsym $mod+Pause mode "$mode_system"

```

**Примечание:**

*   `sleep 1` adds a small delay to prevent possible race conditions with suspend [[5]](https://bugs.launchpad.net/ubuntu/+source/unity-2d/+bug/830348)
*   The `-i` argument for `systemctl poweroff` causes a shutdown even if other users are logged-in (this requires [polkit](https://www.archlinux.org/packages/?name=polkit)), or when *logind* (wrongly) assumes so. [[6]](https://bugs.freedesktop.org/show_bug.cgi?id=62676)
*   If you use [xss-lock-git](https://aur.archlinux.org/packages/xss-lock-git/), call `xset s activate` to start the locker. With [xautolock](https://www.archlinux.org/packages/?name=xautolock) the command is `xautolock -locknow`
*   Вы можете использовать отдельный скрипт для более сложного поведения, и ссылаться на него в режиме. Смотрите [[7]](https://gist.github.com/anonymous/c8cd0a59bf4acb273068) для примера.

Для получения альтернативных блокировщиков экрана, смотрите [этот список](/index.php/List_of_applications/Security_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Блокировка_экрана "List of applications/Security (Русский)").

### Вкладки или стековый просмотр веб-страниц

Некоторые веб-браузеры намеренно не внедряют вкладки, управление вкладками считается задачей менеджера окон, не задачей браузера.

Для того чтобы i3 управлял вкладками веб-браузера (в этом примере для [uzbl](/index.php/Uzbl "Uzbl")), добавьте следующую строку в ваш `~/.config/i3/config`

```
for_window [class="Uzbl-core"] focus child, layout stacking, focus

```

Это для стекового просмотра веб-страниц, это означает, что окна будут показаны вертикально. Преимущество над вкладками является то, что названия окон полностью видны, даже если открыто много окон браузера.

Если вы предпочитаете вкладки, с окнами в горизонтальном направлении ('tabs'), используйте:

```
for_window [class="Uzbl-core"] focus child, layout tabbed, focus

```

### Переменные рабочих областей

Так как рабочих областей в i3 определено много, будет полезно присвоить переменные рабочим областям. Например [[8]](https://github.com/dkeg/bloat2.0/blob/master/i3config#L55):

```
set $WS1 term
set $WS2 web
set $WS3 misc
set $WS4 media
set $WS5 code

```

Затем замените имена рабочих области в соответствии с их переменной:

```
bindsym $mod+1          workspace $WS1
...
bindsym $mod+Shift+1    move container to workspace $WS1

```

Для болшей информации смотрите [изменение названий рабочих областей](http://i3wm.org/docs/userguide.html#_changing_named_workspaces_moving_to_workspaces).

### Правильное обращение с плавающими диалогами

Многие диалоги должны открываться, по умолчанию, в плавающем режиме (floating), но многие до сих пор открываются в тайловом режиме (tiling). Чтобы изменить это поведение, проверьте WM_WINDOW_ROLE с [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) и добавьте правильные правила в `~/.i3/config` используя [pcre](http://www.pcre.org/) синтаксис):

```
for_window [window_role="pop-up"] floating enable
for_window [window_role="task_dialog"] floating enable

```

Вы также можете использовать как правило титл и названия регулярных выражений:

```
for_window [title="Preferences$"] floating enable

```

или `WM_CLASS`:

```
for_window [class="(?i)mplayer"] floating enable

```

### Скорость Загрузки/Отдачи сети в statusbar

Вы можете адаптировать этот [скрипт](http://code.stapelberg.de/git/i3status/tree/contrib/measure-net-speed.bash). Для этого,

*   переименуйте обе ваши сетевые карты в соответствии с вашей системой (используйте `ip addr`)
*   найдите их `/sys/devices` затем замените соответствующими:

```
$ find /sys/devices -name *network_interface*

```

**Совет:** Использование `/sys/class/net/*interface*/statistics/` не зависит от расположения PCI.

Теперь просто сохраните сценарий в подходящем месте (например `~/.config/i3`) и укажите вашу программу статуса.

## Патчи

Пакеты с патчами, не вошедшими в апстрим, доступны в [AUR](/index.php/AUR "AUR"):

*   **i3bar-icons-git** — Отоброжает иконки XBM в i3bar

	[https://github.com/ashinkarov/i3-extras](https://github.com/ashinkarov/i3-extras) || [i3bar-icons-git](https://aur.archlinux.org/packages/i3bar-icons-git/)

*   **i3-smart-border** — Умные границы (borders)

	[https://github.com/ashinkarov/i3-extras](https://github.com/ashinkarov/i3-extras) || [i3-smart-border](https://aur.archlinux.org/packages/i3-smart-border/)

*   **i3-wm-iconpatch** — Поддержка значков в Titlebar

	[https://github.com/ashinkarov/i3-extras](https://github.com/ashinkarov/i3-extras) || [i3-wm-iconpatch](https://aur.archlinux.org/packages/i3-wm-iconpatch/)

## Решение проблем

### Общее

Во многих случаях, ошибки фиксируются в разрабатываемой версии [i3-git](https://aur.archlinux.org/packages/i3-git/) (из [AUR](/index.php/AUR "AUR")) и в апстриме попросят воспроизвести какие-либо ошибки в этой версии. [[9]](http://i3wm.org/docs/debugging.html) Смотрите также [Debug - Getting Traces#General](/index.php/Debug_-_Getting_Traces#General "Debug - Getting Traces").

### Кнопки в строке сообщений i3 не работают

Кнопки, такие как "Edit config" в `i3-msg` вызывают `i3-sensible-terminal`, поэтому убедитесь, что ваш [#Эмулятор терминала](#Эмулятор_терминала) признаётся i3.

### Неисправная строка оболочки в тайловом терминале

i3 v4.3 и выше игнорирует размер инкремента подсказки для тайловых окон [[10]](https://www.mail-archive.com/i3-discuss@i3.zekjur.net/msg00709.html). This may cause terminals to wrap lines prematurely, amongst other issues. As a workaround, make the offending window floating, before tiling it again.

### Курсор мыши остается в режиме ожидания

При запуске приложения или сценария, которое не поддерживает загружаемые уведомления, курсор мыши будет оставаться в режиме занят/часы/и т.п. в течение 60 секунд.

Чтобы решить эту проблему для конкретного приложения, используйте параметр `--no-startup-id`, например:

```
exec --no-startup-id ~/script
bindsym $mod+d exec --no-startup-id dmenu_run

```

Чтобы отключить эту анимацию в глобальном масштабе, смотрите [Темы курсора#Создание ссылок на недостающие курсоры](/index.php/%D0%A2%D0%B5%D0%BC%D1%8B_%D0%BA%D1%83%D1%80%D1%81%D0%BE%D1%80%D0%B0#Создание_ссылок_на_недостающие_курсоры "Темы курсора").

### Не реагируют сочетания клавиш

Некоторые утилиты, такие как [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot") могут не работать при использовании регулярных горячих клавиш (выполнятся после нажатия клавиш). В таких случаях, выполняйте команду после ключа "освобождения" с параметром `--release` [[11]](http://i3wm.org/docs/userguide.html#keybindings):

```
bindsym --release Print exec --no-startup-id scrot
bindsym --release Shift+Print exec --no-startup-id scrot -s

```

### Тиринг (разрыв картинки по горизонтали)

i3 [не должным образом осуществляет двойную буферизацию](https://github.com/i3/i3/issues/661) следовательно, может появится тиринг или мерцание. Чтобы предотвратить это, установите и настройте [compton](/index.php/Compton_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Compton (Русский)"). [[12]](https://faq.i3wm.org/question/3279/do-i-need-a-composite-manager-compton/?answer=3282#post-id-3282)

## Смотри также

*   [Comparison of tiling window managers (Русский)](/index.php/Comparison_of_tiling_window_managers_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Comparison of tiling window managers (Русский)") - Сравнение тайловых оконных менеджеров.
*   [Официальный сайт](http://i3wm.org)
*   [funtoo Wiki](http://www.funtoo.org/I3_Tiling_Window_Manager)
*   [i3 Исходный код](http://code.stapelberg.de/git/i3)
*   [i3-extras](https://github.com/ashinkarov/i3-extras) - Коллекция скриптов и патчей
*   [i3ipc-glib](https://github.com/acrisci/i3ipc-glib) - Библиотека расширений i3
*   [i3ipc-ruby](https://github.com/veelenga/i3ipc-ruby) - Усовершенствованная библиотека расширений i3 на Ruby
*   [j4tools](http://www.j4tools.org/) - неофициальные утилиты предназначенные для работы с i3

**Arch Linux Forums**

*   [The i3 thread](https://bbs.archlinux.org/viewtopic.php?id=99064) - A general discussion about i3
*   [i3 desktop screenshots and config sharing](https://bbs.archlinux.org/viewtopic.php?id=103369)

**Screencasts**

*   [i3 window manager v4.1 screencast](http://www.youtube.com/watch?v=Wx0eNaGzAZU)