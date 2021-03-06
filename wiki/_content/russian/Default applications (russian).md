**Состояние перевода:** На этой странице представлен перевод статьи [Default applications](/index.php/Default_applications "Default applications"). Дата последней синхронизации: 13 декабря 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Default_applications&diff=0&oldid=502566).

Ссылки по теме

*   [Ярлыки приложений](/index.php/%D0%AF%D1%80%D0%BB%D1%8B%D0%BA%D0%B8_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Ярлыки приложений")
*   [Окружение рабочего стола](/index.php/%D0%9E%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Окружение рабочего стола")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")

**Зачем нужны типы MIME**: Благодаря им программа "узнает", как поступить с некоторым файлом, например есть файл с расширением *.pdf* ОС должна "знать", чем открыть и как поступить с данным файлом. Как раз типы MIME сообщают ОС об этом.

Существует множество приложений,способных обрабатывать данные одного определенного типа, поэтому пользователи и даже некоторые пакеты собирают списки приложений по умолчанию для каждого [#типа MIME](#.D0.A2.D0.B8.D0.BF.D1.8B_MIME). Хотя изначально Arch Linux не определяет приложения по умолчанию, [окружение рабочего стола](/index.php/%D0%9E%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Окружение рабочего стола") может это сделать. Также некоторые окружения рабочего стола предоставляют графический интерфейс или файловый менеджер, которые могут интерактивно настраивать приложения по умолчанию. Если вы не используете окружение рабочего стола, вам может потребоваться установить дополнительное программное обеспечение для удобного управления приложениями по умолчанию.

## Contents

*   [1 Типы MIME](#.D0.A2.D0.B8.D0.BF.D1.8B_MIME)
    *   [1.1 База данных MIME](#.D0.91.D0.B0.D0.B7.D0.B0_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_MIME)
        *   [1.1.1 Новый тип MIME](#.D0.9D.D0.BE.D0.B2.D1.8B.D0.B9_.D1.82.D0.B8.D0.BF_MIME)
    *   [1.2 Ярлыки приложений](#.D0.AF.D1.80.D0.BB.D1.8B.D0.BA.D0.B8_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
*   [2 Установка приложений по умолчанию](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [2.1 Переменные окружения](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.2 Стандарт XDG](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG)
        *   [2.2.1 Формат](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82)
    *   [2.3 mailcap](#mailcap)
*   [3 Утилиты](#.D0.A3.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B)
    *   [3.1 xdg-utils](#xdg-utils)
    *   [3.2 Альтернативы xdg-open](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D1.8B_xdg-open)
        *   [3.2.1 perl-file-mimeinfo](#perl-file-mimeinfo)
        *   [3.2.2 mimeo](#mimeo)
        *   [3.2.3 whippet](#whippet)
        *   [3.2.4 Собственные замены](#.D0.A1.D0.BE.D0.B1.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B7.D0.B0.D0.BC.D0.B5.D0.BD.D1.8B)
    *   [3.3 lsdesktopf](#lsdesktopf)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Отсутствует файл .desktop](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D1.84.D0.B0.D0.B9.D0.BB_.desktop)
    *   [4.2 Отсутствует ассоциация](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D0.B0.D1.81.D1.81.D0.BE.D1.86.D0.B8.D0.B0.D1.86.D0.B8.D1.8F)
    *   [4.3 Нет приложения по умолчанию](#.D0.9D.D0.B5.D1.82_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [4.4 Нестандартная ассоциация](#.D0.9D.D0.B5.D1.81.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D0.B0.D1.8F_.D0.B0.D1.81.D1.81.D0.BE.D1.86.D0.B8.D0.B0.D1.86.D0.B8.D1.8F)
    *   [4.5 Переменные в файлах .desktop, которые влияют на запуск приложения](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0.D1.85_.desktop.2C_.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.B2.D0.BB.D0.B8.D1.8F.D1.8E.D1.82_.D0.BD.D0.B0_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)

## Типы MIME

Перед установкой приложения по умолчанию для каждого типа файла, тип файла должен быть обнаружен. Существует два распространенных способа проверить это:

*   используя расширение имени файла, например .html или .jpeg
*   используя [магическое число](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D1%81%D0%B8%D0%B3%D0%BD%D0%B0%D1%82%D1%83%D1%80_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2 "w:ru:Список сигнатур файлов") в первых байтах файла

Однако возможно, что один тип файла идентифицируется несколькими различными магическими числами и расширениями имен файлов, поэтому [типы MIME](https://en.wikipedia.org/wiki/ru:MIME-%D1%82%D0%B8%D0%BF%D1%8B "w:ru:MIME-типы") используются для представления различных типов файлов. Типы MIME определяются двумя частями, разделенными косой чертой: `*тип*/*подтип*`. Тип описывает общую категорию содержимого, тогда как подтип идентифицирует конкретный тип данных. Например, `image/jpeg` является типом MIME для [JPEG](https://en.wikipedia.org/wiki/ru:JPEG "w:ru:JPEG") изображений, тогда как `video/H264` является типом MIME для [H.264](https://en.wikipedia.org/wiki/ru:H.264 "w:ru:H.264") видео.

Технически каждый тип MIME должен быть зарегистрирован в [IANA](https://en.wikipedia.org/wiki/ru:IANA "w:ru:IANA")[[1]](http://www.iana.org/assignments/media-types/media-types.xhtml), однако многие приложения используют неофициальные типы MIME; они часто имеют тип, начинающийся с `x-`, например `x-scheme-handler/https` для HTTPS URL. Для локального использования, [#База данных MIME](#.D0.91.D0.B0.D0.B7.D0.B0_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_MIME) может использоваться другими пакетами для регистрации новых типов MIME.

### База данных MIME

Система поддерживает базу данных распознанных типов MIME: [Общая база данных MIME](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176). База данных построена из файлов XML, установленных пакетами в `/usr/share/mime/packages`, используя инструменты из [shared-mime-info](https://www.archlinux.org/packages/?name=shared-mime-info).

Файлы в `/usr/share/mime/` не должны редактироваться напрямую, однако их можно сохранить в отдельную базу данных для каждого пользователя в `~/.local/share/mime/`.

#### Новый тип MIME

В этом примере определяется новый тип MIME `application/x-foobar` и присваивается любому файлу с расширением *.foo*. Просто создайте следующий файл:

 `~/.local/share/mime/packages/application-x-foobar.xml` 
```
<?xml version="1.0" encoding="UTF-8"?>
<mime-info xmlns="http://www.freedesktop.org/standards/shared-mime-info">
    **<mime-type type="application/x-foobar">**
        <comment>foo file</comment>
        <icon name="application-x-foobar"/>
        <glob-deleteall/>
        **<glob pattern="*.foo"/>**
    </mime-type>
</mime-info>
```

А затем обновите базу данных MIME

```
$ update-mime-database ~/.local/share/mime

```

Конечно, это никак не повлияет, если ярлыки приложения не связаны с типом MIME. Вам может потребоваться создать новые [#Ярлыки приложений](#.D0.AF.D1.80.D0.BB.D1.8B.D0.BA.D0.B8_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9) или отредактировать [#mimeapps.list](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG).

### Ярлыки приложений

Каждый пакет может использовать [ярлыки приложений](/index.php/%D0%AF%D1%80%D0%BB%D1%8B%D0%BA%D0%B8_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Ярлыки приложений") для предоставления информации о типах MIME, которые могут быть обработаны с помощью программного обеспечения. Чтобы обеспечить быстрый поиск в обратном направлении, система использует инструменты из пакета [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) для анализа файлов рабочего стола и создания обратного сопоставления, хранящегося в `/usr/share/applications/mimeinfo.cache`. Это единственный файл, который программы должны прочитать, чтобы найти все файлы рабочего стола, которые могут использоваться для обработки данного типа MIME. Использование базы данных проще и быстрее, чем непосредственно считывать сотни файлов *.desktop.*

Файлы в `/usr/share/applications/` не должны редактироваться напрямую, можно поддерживать отдельную базу данных для каждого пользователя в `~/.local/share/applications/`. Для получения дополнительной информации смотрите статью [Ярлыки приложений](/index.php/%D0%AF%D1%80%D0%BB%D1%8B%D0%BA%D0%B8_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Ярлыки приложений").

## Установка приложений по умолчанию

Настройка приложений по умолчанию зависит от используемого лаунчера. К сожалению, существует несколько несовместимых стандартов, и многие программы даже имеют свои собственные форматы.

Наиболее распространенные стандарты описаны ниже для ручного редактирования. Также существует несколько [#Утилит](#.D0.A3.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B), которые могут сделать работу, которая может или не может реализовать следующие стандарты.

### Переменные окружения

Консольные программы, в частности, настраиваются путем установки соответствующей [переменной окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)"), например, `BROWSER` или `EDITOR`. Смотрите раздел [Переменные окружения#Примеры](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B "Переменные окружения").

### Стандарт XDG

[Стандарт XDG](https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html) является наиболее распространенным при настройке окружения рабочего стола. Приложения по умолчанию для каждого типа MIME хранятся в файлах `mimeapps.list`, которые могут храниться в нескольких местах. Их проверяют в следующем порядке, причем более ранние ассоциации имеют приоритет над более поздними:

| Путь | Применение |
| `~/.config/mimeapps.list` | пользовательские переопределения |
| `/etc/xdg/mimeapps.list` | общесистемные переопределения |
| `~/.local/share/applications/mimeapps.list` | (**Устаревшее**) пользовательские переопределения |
| `/usr/local/share/applications/mimeapps.list`
`/usr/share/applications/mimeapps.list` | переопределения предоставляемые дистрибутивом по умолчанию |

Кроме того, можно определить [окружение рабочего стола](/index.php/%D0%9E%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Окружение рабочего стола") по умолчанию для конкретных приложений в файле с именем `*desktop*-mimeapps.list` где `*desktop*` это имя окружения рабочего стола (Из переменной окружения `XDG_CURRENT_DESKTOP`). Например, `/etc/xdg/xfce-mimeapps.list` определяет общесистемные переопределения приложений по умолчанию для [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)"). Эти переопределения для рабочего стола имеют приоритет над соответствующим файлом, не относящимся к окружению рабочему столу. Например, `/etc/xdg/xfce-mimeapps.list` имеет приоритет над `/etc/xdg/mimeapps.list`, но по-прежнему переопределяется `~/.config/mimeapps.list`.

**Совет:** Несмотря на то, что несколько устаревших приложений все еще читают/записывают в `~/.local/share/applications/mimeapps.list`. Чтобы облегчить обслуживание, просто соедините его ссылкой `$ ln -s ~/.config/mimeapps.list ~/.local/share/applications/mimeapps.list` . Обратите внимание, что символическая ссылка должна быть по этому пути, потому что [#xdg-utils](#xdg-utils) удаляет и воссоздает `~/.config/mimeapps.list` при записи в него, что приведет к поломке любых символических/жестких ссылок.

**Примечание:** Вы также можете найти файлы в этих местах с именем `defaults.list`. Этот файл похож на `mimeapps.list`, за исключением того, что он отображает только приложения по умолчанию (не добавленные/удаленные ассоциации). Сейчас он устарел и должен быть вручную объединен с `mimeapps.list`.

#### Формат

Рассмотрим следующий пример:

 `mimeapps.list` 
```
[Added Associations]
image/jpeg=bar.desktop;baz.desktop
video/H264=bar.desktop
[Removed Associations]
video/H264=baz.desktop
[Default Applications]
image/jpeg=foo.desktop
```

Каждый раздел назначает один или несколько ярлыков приложений типам MIME.

*   **Added Associations** (Добавленные ассоциации) указывают, что приложения поддерживают открытие этого типа MIME. Например, `bar.desktop` и `baz.desktop` могут открывать изображения JPEG. Это может повлиять на список приложений, который вы видите при щелчке правой кнопкой мыши по файлу в файловом менеджере.
*   **Removed Associations** (Удаленные ассоциации) указывают, что приложения *не* поддерживают этот тип MIME. Например, `baz.desktop` не может открыть видео H.264.
*   **Default Applications** (Приложения по умолчанию) указывают, что приложения должны выбираться по умолчанию для открытия этого типа MIME. Например, изображения JPEG должны быть открыты с помощью `foo.desktop`. Это неявно добавляет связь между приложением и типом MIME. Если есть несколько приложений, они проверяются по порядку.

Каждый раздел является необязательным и может быть опущен, если он не нужен.

### mailcap

Формат [mailcap(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mailcap.4) используется почтовыми программами, такими как [mutt](https://www.archlinux.org/packages/?name=mutt) и [sylpheed](https://www.archlinux.org/packages/?name=sylpheed) для открытия нетекстовых файлов. Чтобы эти программы использовали [xdg-open](#xdg-utils), отредактируйте `~/.mailcap`:

 `~/.mailcap` 
```
*/*; xdg-open "%s"

```

**Важно:** Если вы используете [run-mailcap](https://aur.archlinux.org/packages/run-mailcap/), для него может быть делегирован `xdg-open`. Это вызовет бесконечный цикл, если вы настроили свой `.mailcap`, как описано выше.

## Утилиты

Хотя можно настроить приложения по умолчанию и типы MIME путем прямого редактирования [#mimeapps.list](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG) и [#База данных MIME](#.D0.91.D0.B0.D0.B7.D0.B0_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_MIME), существует множество инструментов, которые могут упростить процесс. Эти инструменты также важны, поскольку приложения могут делегировать открытие файлов этими инструментами, а не пытаться реализовать стандарт типа MIME.

Если вы используете [окружение рабочего стола](/index.php/%D0%9E%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Окружение рабочего стола"), вы должны сначала проверить, предоставляет ли он свою собственную утилиту. Она должна быть предпочтительнее этих альтернатив.

### xdg-utils

[xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) предоставляет официальные утилиты для управления типами MIME и приложениями по умолчанию в соответствии со [стандартом XDG](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG). Самое главное, что он предоставляет `/usr/bin/xdg-open`, который используют многие приложения, чтобы открыть файл с помощью приложения по умолчанию. Он не зависит от окружения рабочего стола, в том смысле, что он пытается использовать собственный инструмент приложения по умолчанию для каждой среды и предоставляет свой собственный механизм, если неизвестная среда не обнаружена. Примеры:

```
# определение типа MIME файла
$ xdg-mime query filetype photo.jpeg
image/jpeg

# определение приложения по умолчанию для типа MIME
$ xdg-mime query default image/jpeg
gimp.desktop

# изменение приложения по умолчанию для типа MIME
$ xdg-mime default feh.desktop image/jpeg

# открытие файла со своим стандартным приложением
$ xdg-open photo.jpeg

# ярлык для открытия всех веб типов MIME с помощью одного приложения
$ xdg-settings set default-web-browser firefox.desktop

# ярлык для установки приложения по умолчанию для схемы URL
$ xdg-settings set default-url-scheme-handler irc xchat.desktop

```

**Совет:** Если окружение рабочего стола не обнаружено, обнаружение типа MIME возвращается к использованию [file](https://www.archlinux.org/packages/?name=file) который—по иронии судьбы—не реализует стандарт XDG. Если вы хотите, чтобы [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) работал нормально без окружения рабочего стола, вам необходимо установить [#perl-file-mimeinfo](#perl-file-mimeinfo) или одну из [альтернатив xdg-open](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D1.8B_xdg-open).

### Альтернативы xdg-open

Из-за сложности [#xdg-utils](#xdg-utils) версии `xdg-open` может быть сложно отлаживать, когда открывается неправильное приложение по умолчанию. Из-за этого существует множество альтернатив, которые пытаются улучшить его. Некоторые из этих альтернатив заменяют двоичный файл `/usr/bin/xdg-open`, тем самым изменяя поведение приложений по умолчанию для большинства приложений. Другие просто предоставляют альтернативный метод выбора приложений по умолчанию.

#### perl-file-mimeinfo

[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) предоставляет инструменты `mimeopen` и `mimetype`. Они имеют немного более приятный интерфейс, чем их эквиваленты [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils):

```
# определение типа MIME файла
$ mimetype photo.jpeg
photo.jpeg: image/jpeg

# выбор приложения по умолчанию для этого файла
$ mimeopen -d photo.jpeg
Please choose an application

    1) Feh (feh)
    2) GNU Image Manipulation Program (gimp)
    3) Pinta (pinta)

use application #

# открытие файла со своим стандартным приложением
$ mimeopen -n photo.jpeg

```

Самое главное, что приложения [#xdg-utils](#xdg-utils) на самом деле вызывают `mimetype` вместо `file` для обнаружения типа MIME, если он не обнаруживает ваше [окружение рабочего стола](/index.php/%D0%9E%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Окружение рабочего стола"). Это важно, потому что `file` не следует за [стандартом XDG](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG).

**Примечание:** [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) до версии 0.28-1 не *полностью* соответствует [стандарту XDG](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG). Например, он не считывает [переопределения предоставляемые дистрибутивом по умолчанию](https://github.com/mbeijen/File-MimeInfo/issues/20) и сохраняет конфигурацию в [устаревших местах](https://github.com/mbeijen/File-MimeInfo/issues/8).

#### mimeo

[mimeo](https://aur.archlinux.org/packages/mimeo/) предоставляет инструмент `mimeo` который объединяет функции `xdg-open` и `xdg-mime`.

```
# определение типа MIME файла
$ mimeo -m photo.jpeg
photo.jpeg
  image/jpeg

# выбор приложения по умолчанию для этого типа MIME
$ mimeo --add image/jpeg feh.desktop

# открытие файла со своим стандартным приложением
$ mimeo photo.jpeg

```

Однако большая разница с *xdg-utils* заключается в том, что mimeo также поддерживает пользовательские "файлы ассоциаций", которые допускают более сложные ассоциации. Например, передача определенных аргументов командной строки на основе регулярного выражения соответствует:

```
# открытие ссылки на YouTube в VLC, не открывая новый экземпляр
vlc --one-instance --playlist-enqueue %U
  ^https?://(www.)?youtube.com/watch\?.*v=

```

[xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/) исправляет *xdg-utils* так что `xdg-open` возвращается в mimeo, если окружение рабочего стола не обнаружено.

#### whippet

[whippet](https://aur.archlinux.org/packages/whippet/) предоставляет инструмент `whippet`, который похож на `xdg-open`. Он имеет интеграцию с X11, используя [libnotify](https://www.archlinux.org/packages/?name=libnotify) для отображения ошибок и [dmenu](https://www.archlinux.org/packages/?name=dmenu) для отображения вариантов между открываемыми приложениями.

```
# открытие файла со своим стандартным приложением
$ whippet -M photo.jpeg

# выбор из всех возможных приложений для открытия файла (без установки значения по умолчанию)
$ whippet -m photo.jpeg

```

В дополнение к стандарту [#mimeapps.list](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG), *whippet* также может использовать базу данных SQlite ассоциаций весового приложения/типа MIME/регулярных выражений для определения, какое приложение использовать.

#### Собственные замены

Следующие пакеты заменяют [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), однако они предоставляют только сценарий `xdg-open`. Эти версии `xdg-open` не выполняют каких-либо делегирования для инструментов, ориентированных на окружение рабочего стола и не читают/не записывают стандартный файл [#mimeapps.list](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG) (каждый из них имеет свой собственный пользовательский конфиг), поэтому они не могут хорошо интегрироваться с другими программами, которые управляют приложениями по умолчанию. Однако вы можете найти их более простыми в использовании, если вы не используете окружение рабочего стола.

**Важно:** Если вам нужны какие-либо `xdg-*` двоичные файлы из [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), отличные от `xdg-open`, тогда вы не должны использовать эти приложения, так как они не предоставляют их.

| Пакет | Особенности |
| [linopen](https://aur.archlinux.org/packages/linopen/) | Разрешает правила регулярного выражения, может указывать запасное приложение для открывания файлов |
| [mimi-git](https://aur.archlinux.org/packages/mimi-git/) | Может изменять аргументы команды для каждого типа MIME |
| [busking-git](https://aur.archlinux.org/packages/busking-git/) | Аналогично *mimi*, но при этом поддерживает правила регулярных выражений |
| [sx-open](https://aur.archlinux.org/packages/sx-open/) | Использует простой конфигурационный файл на основе оболочки пользователя (shell) |

### lsdesktopf

[lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/) предоставляет несколько способов поиска в базе данных MIME и ярлыков MIME на рабочем столе.

Например, чтобы увидеть все расширения MIME в файлах *.desktop* в системе, которые имеют тип MIME `video`, вы можете использовать `lsdesktopf --gm -gx video` или для поиска в файлах базы данных XML, используйте `lsdesktopf --gdx -gx video`. Чтобы получить краткий обзор того, сколько и какие файлы *.desktop* могут быть связаны с определенным типом MIME, используйте `lsdesktopf --gen-mimeapps`. Чтобы просмотреть все расширения имен файлов в файлах базы данных XML, используйте `lsdesktopf --gdx -gfx`.

## Решение проблем

Если файл не открывается вашим желаемым приложением по умолчанию, существует несколько возможных причин. Вам может потребоваться проверить каждый случай.

### Отсутствует файл .desktop

Для связывания приложений с типами MIME требуются [ярлыки приложений](/index.php/%D0%AF%D1%80%D0%BB%D1%8B%D0%BA%D0%B8_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Ярлыки приложений"). Убедитесь, что такая запись существует и может использоваться для открытия (вручную) файлов в приложении.

### Отсутствует ассоциация

Если в ярлыке приложения не указан тип MIME под его ключом `MimeType`, он не будет учитываться, когда приложение необходимо для открытия этого типа. Измените [#mimeapps.list](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG), чтобы добавить связь между файлом .desktop и типом MIME.

### Нет приложения по умолчанию

Если ярлык приложения связан с типом MIME, его просто нельзя установить как значение по умолчанию. Измените [#mimeapps.list](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG), чтобы установить связь по умолчанию.

### Нестандартная ассоциация

Приложения могут игнорировать или частично реализовывать [стандарт XDG](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_XDG). Проверьте использование устаревших файлов, таких как `~/.local/share/applications/mimeapps.list` и `~/.local/share/applications/defaults.list`. Если вы пытаетесь открыть файл из другого приложения (например, веб-браузера или файлового менеджера), проверьте, имеет ли это приложение собственный способ выбора приложений по умолчанию.

### Переменные в файлах .desktop, которые влияют на запуск приложения

Окружения рабочего стола и файловые менеджеры, поддерживающие программы запуска спецификаций в соответствии с определением в файлах *.desktop*. Смотрите раздел [Ярлыки приложений#Ярлык приложения](/index.php/%D0%AF%D1%80%D0%BB%D1%8B%D0%BA%D0%B8_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.AF.D1.80.D0.BB.D1.8B.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F "Ярлыки приложений").

Как правило, настройка упакованных файлов *.desktop* не требуется, но она может быть с ошибками. Даже если приложение содержит необходимое описание типа MIME в файле *.desktop*, то иногда переменная `MimeType`, которая используется для ассоциации, может неправильно запускаться или вообще не запускаться, или запускаться без открытия файла.

Это может произойти, например, если в переменной `Exec` отсутствуют внутренние параметры, необходимые для открытия файла или того, как приложение отображается в меню. Переменная `Exec` обычно начинается с `%`; чтобы узнать поддерживаемые параметры в настоящее время смотрите [exec-переменные](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#exec-variables).

В следующей таблице перечислены основные записи переменных файлов *.desktop* которые влияют на запуск приложения, если у него есть тип MIME, связанный с ним.

| Имена переменных | Пример 1 | Пример 2 | Описание |
| DBusActivatable | DBusActivatable=true | DBusActivatable=false | Приложение взаимодействует с [D-Bus](https://www.freedesktop.org/wiki/Software/dbus/).
Смотрите также настройки: [D-Bus](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#dbus). |
| MimeType | MimeType=application/vnd.oasis.opendocument.text | MimeType=application/vnd.sun.xml.math | Список типов MIME, поддерживаемых приложением |
| StartupWMClass | StartupWMClass=google-chrome | StartupWMClass=xpad | Связывает окна с владельцем приложения |
| Terminal | Terminal=true | Terminal=false | Запуск в терминале по умолчанию |