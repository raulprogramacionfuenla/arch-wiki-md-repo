**Состояние перевода:** На этой странице представлен перевод статьи [Xbindkeys](/index.php/Xbindkeys "Xbindkeys"). Дата последней синхронизации: 5 сентября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xbindkeys&diff=0&oldid=539929).

Ссылки по теме

*   [Xmodmap (Русский)](/index.php/Xmodmap_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xmodmap (Русский)")
*   [Sxhkd](/index.php/Sxhkd "Sxhkd")
*   [Xorg (Русский)#Автоматизация](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Автоматизация "Xorg (Русский)")

Xbindkeys - программа, позволяющая назначать команды клавишам (в том числе мультимедийным) или сочетаниям клавиш. Она не зависит от окружения рабочего стола и оконного менеджера.

## Contents

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Управление звуком](#Управление_звуком)
    *   [2.2 Управление яркостью](#Управление_яркостью)
    *   [2.3 Графический способ](#Графический_способ)
*   [3 Определение кодов клавиш](#Определение_кодов_клавиш)
*   [4 Постоянные изменения](#Постоянные_изменения)
*   [5 Имитация мультимедийных клавиш](#Имитация_мультимедийных_клавиш)
*   [6 Решение проблем](#Решение_проблем)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys).

## Настройка

Создайте пустой файл `~/.xbindkeysrc` или создайте образец файла (обратите внимание, что в нем настроены некоторые сочетания клавиш, такие как `Ctrl+f`, которые вы можете изменить или удалить):

```
$ xbindkeys -d > ~/.xbindkeysrc

```

Теперь вы можете редактировать его вручную, либо воспользоваться для настройки графической утилитой.

**Совет:** Для применения изменений выполните `xbindkeys -p` для перезагрузки настроенного файла.

### Управление звуком

Вот пример конфигурационного файла, который связывает комбинации клавиш Fn на ноутбуке с командами *pactl*, которые регулируют громкость звука. Обратите внимание, что символ решетки (#) используется для создания комментариев.

```
# Увеличить громкость звука
"pactl set-sink-volume @DEFAULT_SINK@ +1000"
   XF86AudioRaiseVolume

```

```
# Уменьшить громкость звука
"pactl set-sink-volume @DEFAULT_SINK@ -1000"
   XF86AudioLowerVolume

```

```
# Отключить звук
"pactl set-sink-mute @DEFAULT_SINK@ toggle"
   XF86AudioMute

```

Для получения информации о дополнительных командах смотрите [PulseAudio (Русский)#Регулировка звука клавиатурой](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Регулировка_звука_клавиатурой "PulseAudio (Русский)") или [ALSA#Keyboard volume control](/index.php/ALSA#Keyboard_volume_control "ALSA").

### Управление яркостью

Также можно определить сочетания клавиш, чтобы управлять яркостью экрана.

```
# Увеличить яркость
"xbacklight -inc 10"
   XF86MonBrightnessUp

```

```
# Уменьшить яркость
"xbacklight -dec 10"
   XF86MonBrightnessDown

```

### Графический способ

Для графической настройке [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xbindkeys_config-gtk2](https://aur.archlinux.org/packages/xbindkeys_config-gtk2/) и запустите:

```
$ xbindkeys_config

```

## Определение кодов клавиш

Чтобы найти код клавиши, введите следующую команду:

```
$ xbindkeys -k

```

Появится пустое окно. Нажмите кнопку, которой вы хотите назначить команду и *xbindkeys* выведет удобный фрагмент, который можно вставить в `~/.xbindkeysrc`. Например, пока окно открыто, нажмите `Alt+o` и вы получите следующий вывод (результат может отличаться):

```
"(Scheme function)"
    m:0x8 + c:32
    Alt + o

```

Первая строка представляет собой команду. Вторая содержит состояние (0x8) и код клавиши (32), о котором сообщает `xev`. Третья строка содержит значение клавиш, связанные с указанным кодом. Чтобы использовать этот вывод, скопируйте одну из двух последних строк в `~/.xbindkeysrc` и замените "(Scheme function)" на команду, которую вы хотите использовать.

**Совет:** Используйте команду `xbindkeys -mk`, чтобы держать открытым приглашение для ввода нескольких нажатий клавиш. Для выхода нажмите `q`.

Для определения клавиш мыши, вы можете использовать xev. Для получения дополнительной информации смотрите [[1]](https://blog.hanschen.org/2009/10/13/mouse-shortcuts-with-xbindkeys/).

## Постоянные изменения

После того как вы закончите настройку сочетаний клавиш, откройте файл [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)") или [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") (в зависимости от вашего оконного менеджера) и поместите

```
xbindkeys

```

перед строкой, которая запускает ваш оконный менеджер или окружение рабочего стола.

## Имитация мультимедийных клавиш

XF86Audio* и другие мультимедийные клавиши [[2]](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols) довольно хорошо реализованы в основных DE. Для клавиатур без таких клавиш вы можете имитировать их с помощью других клавиш.

```
# Уменьшить громкость звука при нажатие Super-minus
"pactl set-sink-volume 0 -1000"
   m:0x50 + c:20
   Mod2+Mod4 + minus

```

Однако для самого выполнения этих клавиш вы можете использовать такие инструменты, как [xdotool](https://www.archlinux.org/packages/?name=xdotool) (из [официальных репозиториев](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории")) и [xmacro](https://aur.archlinux.org/packages/xmacro/) (из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)")). К сожалению, поскольку вы уже удерживаете некоторую клавишу-модификатор (например, Super или Shift), X распознает ввод как `Super-XF86AudioLowerVolume`, который ничего не выполняет ничего полезного. Ниже приведен скрипт, основанный на утилитах *xmacro* и *xmodmap* из пакета [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap) [[3]](https://bbs.archlinux.org/viewtopic.php?pid=843395).

```
#!/bin/sh
echo 'KeyStrRelease Super_L KeyStrRelease minus' 
```

Это работает для одного вызова клавиши XF86AudioLowerVolume (если вы используете сочетание `Super+minus`), а не для нескольких при условие, что вы не отпускаете клавишу Super. Однако, если вы хотите, чтобы это работало, добавьте следующую строку в конец скрипта:

```
echo 'KeyStrPress Super_L' | xmacroplay :0

```

С помощью этого модифицированного скрипта, если вы нажмете комбинацию клавиш достаточно быстро, ваша клавиша Super_L останется 'включенной' до следующего раза, когда вы ее нажмете, что может привести к некоторым интересным побочным эффектам. Просто нажмите Super_L снова, чтобы переключить его состояние, или используйте оригинальный скрипт, если хотите, чтобы все 'просто работало', и смиритесь с одним нажатием на громкость вверх/вниз.

Эти инструкции совместимы с большим количеством XF86 мультимедиа клавиш (полезними из них будут XF86AudioRaiseVolume, XF86AudioLowerVolume, XF86AudioPlay, XF86AudioPrev, XF86AudioNext).

## Решение проблем

Если по какой-либо причине горячая клавиша, которую вы уже настроили в `~/.xbindkeysrc` не работает, откройте терминал и введите следующее:

```
$ xbindkeys -n

```

Нажимая на не рабочую горячую клавишу, вы можете увидеть любую ошибку *xbindkeys* (например: mistyped command/keycode,...).

Если команда для сочетания клавиш работает через xdotool в командной строке, но не при ее нажатие (это особенно заметно в gnome), добавьте "+ Release" к этой комбинации:

```
"xdotool key --clearmodifiers XF86AudioPlay"
    Mod2 + F7 + Release

```

Это заставит клавишу F7 воспроизвести/приостановить аудио. Где команда "xdotool" работает в командной строке. Если удалить "+ Release", сочетание клавиш не будет работать с xbindkeys.