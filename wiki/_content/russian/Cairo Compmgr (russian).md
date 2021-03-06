Cairo Composite Manager - универсальный и расширяемый [композитный менеджер](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager"), который для своей работы использует библиотеку [cairo](https://ru.wikipedia.org/wiki/Cairo). Присутствует возможность добавлять разные дополнительные эффекты рабочего стола, с помощью подключаемых плагинов. Имеет возможности прорисовки теней, анимации окон и меню, управления прозрачностью окон и управления оконными декорациями.

Как и [Xcompmgr](/index.php/Xcompmgr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xcompmgr (Русский)"), не заменяет собой и не инициирует выход из окружения, что делает его одним из самых интересных решений для пользователей легковесных окружений (таких как [Openbox](/index.php/Openbox "Openbox"), [Fluxbox](/index.php/Fluxbox "Fluxbox"), и др.) которые хотят украсить свой рабочий стол.

## Contents

*   [1 Предварительные требования](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B2.D0.B0.D1.80.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.82.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
*   [4 Дополнительная информация](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F)

## Предварительные требования

Для использования Cairo Composite Manager, необходимо в обязательном порядке иметь выполненные условия:

*   [Xorg](/index.php/Xorg "Xorg") должен быть сконфигурирован и запущен
*   Посредством графических драйверов должна быть активирована поддержка Composite

## Установка

На выбор у вас есть несколько путей установки, вам только необходимо выбрать более подходящий для Вас. Первый - установка пакета [cairo-compmgr](https://aur.archlinux.org/packages/cairo-compmgr/) доступного в репозитории [community]. Второй - установка самой свежей версии пакета из пользовательского [AUR](/index.php/AUR "AUR").

При компиляции пакета из [AUR](/index.php/AUR "AUR") можно игнорировать недостающий `gconf`, проблем при этом не наблюдается. Но удачной компиляции не достигнуть без обязательного удовлетворения зависимости `vala`. Без неё сборка программы невозможна. В случае отсутствия `gconf` удалите последние 3 строки из PKGBUILD, где упоминается последний.

## Конфигурация

Для начала работы с Cairo Composite Manager, воспользуйтесь командой:

```
$ cairo-compmgr 

```

Для автоматического запуска, при старте вашего окружения,воспользуйтесь возможностями автозапуска Вашего окружения или просто добавьте в Ваш `~/.xinitrc`:

```
cairo-compmgr &

```

При начале работы Cairo Composite Manager интегрирует себя в системный трей, откуда можно вызвать окно его конфигурации, совершив правый клик мышки по иконке программы.

Если для вас нет необходимости использовать некоторые плагины (например Вам необходима только возможность управления прозрачностью xcompmgr), вы можете выключить их в окне настройки. При выгрузке модулей Вы можете наблюдать задержки и полную перерисовку Вашего рабочего стола.

## Дополнительная информация

*   [Composite](/index.php/Composite "Composite")
*   [Xcompmgr](/index.php/Xcompmgr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xcompmgr (Русский)") -- Легковесный композитный менеджер, в задачи которого входит возможность создания теней и прорисовки простой прозрачности.
*   [Compiz Fusion](/index.php/Compiz_Fusion "Compiz Fusion") -- Композитный менеджер с большими возможностями, использующий для работы возможности 3D графики и анимации.
*   [Wikipedia:Compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")