**MPlayer** - популярный мультимедийный проигрыватель для Linux. Он поддерживает великое множество аудио и видео форматов, однако большинство людей используют его лишь как видеопроигрыватель.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Дополнительная информация по установке](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B5)
    *   [2.1 Графический интерфейс (GUI)](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81_.28GUI.29)
    *   [2.2 Интеграция в браузеры](#.D0.98.D0.BD.D1.82.D0.B5.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D0.B2_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D1.8B)
        *   [2.2.1 Firefox](#Firefox)
        *   [2.2.2 Konqueror](#Konqueror)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Редактирование файла конфигурации](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.2 Использование vdpau (только для новых видеокарт nVidia)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_vdpau_.28.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B4.D0.BB.D1.8F_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82_nVidia.29)
        *   [3.2.1 Используя файл конфигурации](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
        *   [3.2.2 Используя скрипт-обертку](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82-.D0.BE.D0.B1.D0.B5.D1.80.D1.82.D0.BA.D1.83)
    *   [3.3 Полупрозрачный вывод видео в видеокартах Radeon и активация Composite](#.D0.9F.D0.BE.D0.BB.D1.83.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE_.D0.B2_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE.D0.BA.D0.B0.D1.80.D1.82.D0.B0.D1.85_Radeon_.D0.B8_.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.B0.D1.86.D0.B8.D1.8F_Composite)
    *   [3.4 Потоковый вывод аудио через jack](#.D0.9F.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.B2.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_jack)
*   [4 Использование MPlayer](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_MPlayer)
    *   [4.1 Горячие клавиши](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
    *   [4.2 Просмотр потокового видео](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.BF.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BE)
    *   [4.3 Воспроизведение DVD с поддержкой меню навигации](#.D0.92.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_DVD_.D1.81_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.BE.D0.B9_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BD.D0.B0.D0.B2.D0.B8.D0.B3.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.4 Перемотка во время загрузки](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.BE.D1.82.D0.BA.D0.B0_.D0.B2.D0.BE_.D0.B2.D1.80.D0.B5.D0.BC.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [4.5 Увеличиваем максимальную громкость](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC_.D0.BC.D0.B0.D0.BA.D1.81.D0.B8.D0.BC.D0.B0.D0.BB.D1.8C.D0.BD.D1.83.D1.8E_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Нет картинки в Smplayer](#.D0.9D.D0.B5.D1.82_.D0.BA.D0.B0.D1.80.D1.82.D0.B8.D0.BD.D0.BA.D0.B8_.D0.B2_Smplayer)
    *   [5.2 (S)mplayer не продолжает воспроизведение после паузы](#.28S.29mplayer_.D0.BD.D0.B5_.D0.BF.D1.80.D0.BE.D0.B4.D0.BE.D0.BB.D0.B6.D0.B0.D0.B5.D1.82_.D0.B2.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BF.D0.B0.D1.83.D0.B7.D1.8B)
    *   [5.3 Прозрачный SMPlayer в окружении рабочего стола Gnome с включенным Composite](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D1.8B.D0.B9_SMPlayer_.D0.B2_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0_Gnome_.D1.81_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_Composite)
    *   [5.4 Mplayer не может открыть файлы с пробелами](#Mplayer_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D1.82.D1.8C_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_.D1.81_.D0.BF.D1.80.D0.BE.D0.B1.D0.B5.D0.BB.D0.B0.D0.BC.D0.B8)
*   [6 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [mplayer](https://www.archlinux.org/packages/?name=mplayer).

Последнюю версию всегда можно найти в AUR: [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/).

Также можете попробовать [mplayer2](http://www.mplayer2.org/), ответвление от проекта MPlayer: [mplayer2-git](https://aur.archlinux.org/packages/mplayer2-git/).

## Дополнительная информация по установке

### Графический интерфейс (GUI)

Для MPlayer существует немало графических интерфейсов:

*   Qt: [smplayer](https://www.archlinux.org/packages/?name=smplayer). Пакет [smplayer-themes](https://www.archlinux.org/packages/?name=smplayer-themes) содержит различные темы для него
*   Gtk+: [pymp](https://aur.archlinux.org/packages/pymp/) и [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)
*   gmplayer: больше не входит в состав пакета [mplayer](https://www.archlinux.org/packages/?name=mplayer). Существует альтернативный пакет [mplayer-x](https://aur.archlinux.org/packages/mplayer-x/), включающий в себя *gmplayer*

### Интеграция в браузеры

Если вы желаете выводить видео в вашем любимом браузере с помощью MPlayer, следуйте приведенным в этом разделе инструкциям.

#### Firefox

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer).

**Примечание:** Для установки потребуется [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer), полноценный графический интерфейс к MPlayer

#### Konqueror

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [kmplayer](https://aur.archlinux.org/packages/kmplayer/).

**Примечание:** Также является полноценным графическим интерфейсом к MPlayer

## Настройка

### Редактирование файла конфигурации

Общесистемный конфигурационный файл - `/etc/mplayer/mplayer.conf`, файл конфигурации пользователя - `~/.mplayer/config`. Пример конфигурации можно посмотреть в файле `/etc/mplayer/example.conf`.

Пример файла с настройками:

 `/etc/mplayer/example.conf` 
```
# Это конфигурация по-умолчанию, применяется ко всем файлам
[default]
# использовать X11 для вывода видео
vo=xv
# использовать alsa для вывода звука
ao=alsa
# ao=oss # использовать OSS4
# использовать 6-канальный звук, если возможно
channels = 6
# установить масштаб субтитров равным 3% от размера экрана
subfont-text-scale = 3
# не использовать конфигурацию для шрифтов
nofontconfig = 1
# добавить черные полосы 
# для широкоэкранных мониторов
vf-add=expand=::::1:16/9:16
# для обычных мониторов
#vf-add=expand=::::1:4/3:16

#преобразование 2-х канального звука в 6-канальный - профиль
# используйте -profile 2chto6ch для активации
[2chto6ch]
af-add=pan=6:1:0:.4:0:.6:2:0:1:0:.4:.6:2

#преобразование 6-канального звука в 2-хканальный - профиль
# используйте -profile 6chto2ch для активации
[6chto2ch]
af-add=pan=2:0.7:0:0:0.7:0.5:0:0:0.5:0.6:0.6:0:0

# Отключает заставку экрана
heartbeat-cmd="xscreensaver-command -deactivate &" # останавливает xscreensaver
stop-xscreensaver="yes" # останавливает gnome-screensaver
```

### Использование vdpau (только для новых видеокарт nVidia)

VDPAU - это библиотека, позволяющяя использовать технологию PureVideo HD в Linux. Таким образом, возможно производить аппаратное декодирование видео, сжатого кодеками H.264 и VC-1 (а также xvid, divx и т.п., если это позволяет видеокарта).

Перед тем, как устанавливать, убедитесь, что:

*   Видеокарта поддерживает вывод vdpau ([таблица совместимости](https://en.wikipedia.org/wiki/ru:PureVideo#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0_PureVideo_HD_GPU "wikipedia:ru:PureVideo"))
*   Драйвер *nvidia* установлен

Теперь выберите способ автоматического включения vdpau.

#### Используя файл конфигурации

Включите следующие строки в общесистемный файл конфигурации или файл конфигурации пользователя:

```
vo=vdpau,
vc=ffmpeg12vdpau,ffwmv3vdpau,ffvc1vdpau,ffh264vdpau,ffodivxvdpau,

```

**Примечание:** На концах строк должны стоять запятые!

**Важно:** Библиотека *ffodivxvdpau* поддерживается лишь новыми сериями карт nVidia. Указывать этот кодек или нет - зависит от видеокарты

#### Используя скрипт-обертку

В [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") есть bash-скрипт [mplayer-vdpau-auto](https://aur.archlinux.org/packages/mplayer-vdpau-auto/), который автоматически распознает, какой кодек использовать и когда использовать `vo=vdpau`.

### Полупрозрачный вывод видео в видеокартах Radeon и активация Composite

Для того, чтобы получить полупрозрачный вывод видео в X, Вам нужно активировать вывод текстур в MPlayer:

```
$ mplayer -vo xv:adaptor=1 <File>

```

Или добавить следующую строку в ~/.mplayer/config:

```
vo=xv:adaptor=1

```

Вы можете использовать `xvinfo` , чтобы проверить, какие режимы поддерживает ваша видеокарта.

### Потоковый вывод аудио через jack

Отредактируйте `~/.mplayer/config`, добавив:

```
ao=jack

```

## Использование MPlayer

### Горячие клавиши

	*Это список основных горячих клавиш для MPlayer.*

| Клавиша | Описание |
| p | Пауза/воспроизведение. |
| Пробел | Пауза/воспроизведение. |
| Стрелка влево | Переход на 10 секунд назад. |
| Стрелка вправо | Переход на 10 секунд вперед. |
| Стрелка вниз | Переход на одну минуту назад. |
| Стрелка вверх | Переход на одну минуту вперед. |
| < | Перейти назад по списку воспроизведения. |
| > | Перейти вперед по списку воспроизведения. |
| m | Выключить звук. |
| 0 | Сделать погромче. |
| 9 | Сделать потише. |
| f | Переход в полноэкранный режим или обратно. |
| o | Показать статистику OSD. |
| j | Переключение между возможными вариантами субтитров. |
| # (Shift+3) | Переключение между возможными вариантами звуковой дорожки. |
| `I` (Shift+i) | Показать название файла. |
| 1, 2 | Настройка контрастности. |
| 3, 4 | Настройка цветовой гаммы. |

Обратите внимание, что буквенные клавиши по умолчанию будут работать только, что если включена латинская раскладка (кириллические буквы, соответсвующие латинским можно самостоятельно добавить в конфигурационный файл).

### Просмотр потокового видео

Если вы желаете просматривать потоковое видео (т.е. ссылки *.asx), используйте для воспроизведения:

```
$ mplayer -playlist nekotoraya_ssylka_na_potok.asx

```

потому что без опции -playlist такого рода файлы не воспроизводятся.

### Воспроизведение DVD с поддержкой меню навигации

Если вы желаете воспроизводить DVD-диски с поддержкой меню навигации, используйте следующюю команду:

```
$ mplayer -nocache dvdnav://

```

### Перемотка во время загрузки

Если вы хотите перематывать видео во время загрузки, добавьте в конфигурацию

```
 idx=yes

```

### Увеличиваем максимальную громкость

Если громкость при воспроизведении недостаточна, можно увеличить ее программно через сам mplayer. Включите softvol и установите максимальный уровень громкости значением от 10 до 10000.

```
softvol=1
softvol-max=600

```

## Решение проблем

### Нет картинки в Smplayer

У Smplayer бывают проблемы с открытием файлов *.mp4* (и иногда *.flv*). Если при воспроизведении нет картинки, добавьте следующие строки в файл конфигурации `~/.mplayer/config`:

```
 [extension.mp4]
 demuxer=mov

```

Если проблема осталась, то это, вероятно, потому, что smplayer сохраняет свои настройки в отдельный файл. Решение — удалить его.

```
 $ rm -rf ~/.config/smplayer/file_settings

```

### (S)mplayer не продолжает воспроизведение после паузы

Smplayer иногда не продолжает воспроизведение после паузы в случае, когда выбрано неверное устройство для вывода звука. Если используется PulseAudio, запускайте mplayer с аргументом "-ao pulse" или отредактируйте конфигурацию `~/.mplayer/config`, добавив

```
 ao=pulse

```

В Smplayer выберите "Output-driver" в разделе "General" - "Audio" опций (options).

### Прозрачный SMPlayer в окружении рабочего стола Gnome с включенным Composite

Вы сталкивались с проблемой прозрачного экрана SMPlayer при использовании Compiz или cairo-dock? То есть Вы слышите звук, но видео не отображается. Вот как устранить эту проблему (запустите в терминале):

```
   sudo bash -c "cat > /usr/bin/smplayer.helper" <<EOF
   export XLIB_SKIP_ARGB_VISUALS=1
   exec smplayer.real "$@"
   EOF
   sudo chmod 755 /usr/bin/smplayer.helper
   sudo mv /usr/bin/smplayer{,.real}
   sudo ln -sf smplayer.helper /usr/bin/smplayer

```

Если вы не используете sudo, тогда просто наберите `su`, чтобы войти в систему как root, и выполните скрипт, приведенный выше.

### Mplayer не может открыть файлы с пробелами

Если вы пытаетесь открыть файл с пробелами (Самый лучший фильм) и mplayer выдает ошибку о том, что не может открыть файл (file:///Самый%20лучший%20фильм), где все пробелы преобразованы в %20, то откройте `/usr/share/applications/mplayer.desktop` и измените строку

```
Exec=gmplayer %U

```

на

```
Exec=gmplayer %F

```

## Ссылки

*   [Официальный сайт MPlayer](http://www.mplayerhq.hu/)
*   [MPlayer на википедии](http://ru.wikipedia.org/wiki/Mplayer)
*   [Список горячих клавиш MPlayer](http://www.keyxl.com/aaa2fa5/302/MPlayer-keyboard-shortcuts.htm)