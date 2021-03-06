*IceWM — менеджер окон для X Window System в Unix-подобных операционных системах. Разработка IceWM началась с нуля в 1997-ом году, проект написан целиком на C++ и выпущен на условиях лицензии GNU LGPL. Цель проекта — создание рабочей среды с удобным и быстрым интуитивным интерфейсом с широкими возможностями для настройки пользователем. В частности, все функции графического интерфейса доступны при использовании только клавиатуры. В то же время в число задач входила максимальная «лёгкость» IceWM в плане потребляемых ресурсов компьютера — памяти и процессора.*

IceWM полностью соответствует i18n и поддерживает работу с русским языком.(Источник: [[1]](https://ru.wikipedia.org/wiki/IceWM))

## Contents

*   [1 Установка](#Установка)
*   [2 Запуск IceWM](#Запуск_IceWM)
*   [3 Настройка](#Настройка)
    *   [3.1 Меню](#Меню)
    *   [3.2 Темы](#Темы)
*   [4 Файловые менеджеры](#Файловые_менеджеры)
*   [5 См. также](#См._также)

## Установка

IceWM находится в [официальном репозитории](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"), пакет называется [icewm](https://www.archlinux.org/packages/?name=icewm).

Кроме того, в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") находятся последняя тестовая версия ([icewm-testing](https://aur.archlinux.org/packages/icewm-testing/)) и весрия CVS ([icewm-cvs](https://aur.archlinux.org/packages/icewm-cvs/)). В этих версиях были добавлены новые возможности и устранены некоторые ошибки (в связи с медленным развитием эти версии часто соответствуют версии в extra/icewm).

## Запуск IceWM

**Графический вход**

Просто выберите *IceWM* из меню сеанса вашего любимого [display manager (Русский)](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

**Вручную**

Для базового сеанса, добавьте следующее в файл `~/.xinitrc`

```
exec icewm

```

Для запуска icewm, icewmbg и icewmtray с вашим сеансом IceWM, добавьте следующее в файл `~/.xinitrc`

```
exec icewm-session

```

Смотри [xinitrc (Русский)](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") для деталей, таких как сохранение сеанса logind.

## Настройка

Хотя настройка IceWM и основана на ручной правке текстовых конфигов, применяются также и различные GUI-программы, в частности [icewm-utils](https://aur.archlinux.org/packages/icewm-utils/) из [community](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#community "Official repositories (Русский)"). Однако эти инструменты являются относительно устаревшими и большинство пользователей предпочитают вручную редактировать текстовые файлы конфигурации. Изменения можно вносить как общесистемно (в `/etc/icewm/`), так и для конкретного пользователя (в `~/.icewm/`).

Для изменения стандартной конфигурации icewm, нужно скопировать конфигурационные файлы из `/usr/share/icewm/` в `~/.icewm/`, например:

**Примечание:** Выполняйте все действия от простого пользователя, а не от root.

```
$ mkdir ~/.icewm/
$ cp -R /usr/share/icewm/* ~/.icewm/

```

Доступны следующие файлы конфигурации

*   `preferences` содержит параметры управления поведением IceWM.
*   `menu` содержит пункты и структуру главного меню.
*   `keys` содержит дополнительные комбинации клавиш пользователя.
*   `toolbar` содержит кнопки запуска приложений на панели задач.
*   `winoptions` содержит параметры отвечающие за поведение отдельных приложений, описанных пользователем.
*   `theme` содержит название текущей темы оформления.
*   `startup` исполняемый файл, запускающийся во время первоначальной загрузки оконного менеджера.
*   `shutdown` исполняемый файл, запускающийся во время завершения работы оконного менеджера.

### Меню

*   [menumaker](https://www.archlinux.org/packages/?name=menumaker) (доступен в [community](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#community "Official repositories (Русский)")) - это скрипт на Python, автоматически создающий меню установленных в системе приложений. Хотя в меню и будет добавлено множество нежелательных пунктов, может оказаться, что использование MenuMaker предпочтительнее ручного редактирования файла `menu`. Запускайте MenuMaker с флагом -f, чтоб он смог перезаписать существующий файл меню:

```
$ mmaker -f icewm

```

*   Еще одним инструментом является, написанный на perl, [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu):

```
$ xdg_menu --format icewm --fullmenu --root-menu /etc/xdg/menus/arch-applications.menu > ~/.icewm/menu

```

### Темы

По умолчанию включено несколько тем оформления, в репозитории можно дополнительно найти пакет с ножеством тем - [icewm-themes](https://aur.archlinux.org/packages/icewm-themes/). Хотя большинство тем имеют спартанский вид, в стиле'old Windows', существуют и более современные. Примеры хороших тем оформления: [Carbonit+Ice](http://box-look.org/content/show.php/Carbonit+Ice?content=146421), [IceBuntu](http://box-look.org/content/show.php/IceBuntu?content=62935) или [IceClearlooks](http://box-look.org/content/show.php/IceClearlooks?content=96346). Еще больше тем оформления можно найти на [box-look.org](http://www.box-look.org/index.php?xcontentmode=7311).

## Файловые менеджеры

Следует отметить, что IceWM только оконный менеджер и, следовательно, не включает в себя файловый менеджер. Для поддержки значков рабочего стола можно использовать [PCManFM](/index.php/PCManFM "PCManFM") и Rox Filer, так же для достижения этой функциональности также может быть использован [iDesk](/index.php/Idesk "Idesk").

**Примечание:** Для получения большего списка файловых менеджеров, рекомендуется изучить список в категории [File managers](/index.php/Category:File_managers "Category:File managers").

## См. также

*   [Xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Official IceWM website](https://ice-wm.org/)
*   [IceWM - The Cool Window Manager](http://www.osnews.com/story.php/7774/IceWM--The-Cool-Window-Manager/) - Подробное вступление на OSNews
*   [IceWM - A desktop for Windows emigrants](http://polishlinux.org/apps/window-managers/icewm-a-desktop-for-windows-emmigrants/) - Обзор и руководство от polishlinux.org