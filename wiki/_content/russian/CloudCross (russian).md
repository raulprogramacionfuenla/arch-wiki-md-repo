[CloudCross](http://cloudcross.mastersoft24.ru) - клиент [Google Drive](/index.php/Google_Drive "Google Drive"), написанный на чистом [Qt](/index.php/Qt "Qt") без использования других сторонних библиотек. CloudCross опубликован под лицензией [GPL](/index.php?title=GPL&action=edit&redlink=1 "GPL (page does not exist)"). Основные особенности программы:

*   Поддержка двусторонней конвертации документов из форматов Microsoft Office и Open/Libre Office в формат Google Doc, при выгрузке и обратное преобразование, при загрузке.
*   Поддержка, так называемых, черных и белых списков файлов, которые участвуют в синхронизации.
*   Настройка предпочтения локальных или удаленных файлов с изменениями, состояние которых будет синхронизировано.
*   Управление созданием новых версий файлов на Google Drive.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Варианты использования](#.D0.92.D0.B0.D1.80.D0.B8.D0.B0.D0.BD.D1.82.D1.8B_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [4 Возможные проблемы](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [4.1 Удаление файлов, вместо скачивания](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.2C_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_.D1.81.D0.BA.D0.B0.D1.87.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [4.2 Постоянная загрузка/выгрузка офисных файлов](#.D0.9F.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.BD.D0.B0.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0.2F.D0.B2.D1.8B.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BE.D1.84.D0.B8.D1.81.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2)
*   [5 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

Установите пакет [cloudcross](https://aur.archlinux.org/packages/cloudcross/).

## Использование

После установки определите папку, содержимое которой будет синхронизироваться с Google Drive. Перейдите в нее и пройдите аутентификацию:

```
$ ccross -a

```

Вам будет предложено скопировать ссылку и вставить ее в браузер. Перейдя по предложенной ссылке, вы авторизуетесь на своем аккаунте Google и примете запрошенные разрешения для приложения CloudCross. После этого вам выдадут код подтверждения, который надо встпвить в программу. После прохождения аутентификации прграмма готова к работе.

## Варианты использования

CloudCross может использоваться в различных ситуациях, когда необходима синхронизация локальных файлов с файлами в облаке. Это может быть, например, дублирование ценных файлов в Google Drive, совместная работа с Google Docs или резервное копирование.

## Возможные проблемы

При использовании CloudCross могут возникнуть некоторые проблемы.

### Удаление файлов, вместо скачивания

При запуске синхронизации в пустой папке, вместо скачивания файлов из Google Drive, файлы в облаке удаляются. Это происходит потому, что по умолчанию программа считает приоритетными локальные файлы. Чтобы этого избежать, используйте при запуске опцию --prefer=remote

```
$ ccross --prefer=remote

```

Но, в любом случае, вы должны помнить, что ни локальные ни удаленные файлы не удаляются безвозвратно. Вы всегда можете восстановить их из корзины на Google Drive или из папки .trash в синхронизируемой директории.

### Постоянная загрузка/выгрузка офисных файлов

Если используется опция --convert-doc, которая производит конвертацию офисных документов в формат Google Doc и обратно, то вы можете наблюдать ситуацию, что офисные файлы выгруженные на сервер и неизмененные с тех пор, при следующей синхронизации начинают загружаться обратно. А при следующей синхронизации опять выгружаться на сервер. Это не является ошибкой. Так происходит потому, что конвертация изменяет контрольную сумму файла, не изменяя содержимого и программа видя изменения пытается их синхронизировать. Если же файл был изменен, с момента последней синхронизации, то синхронизируется более новая версия файла.

## Ссылки

*   [Рускоязычный сайт](http://cloudcross.mastersoft24.ru/ru)
*   [Группа в Facebook](https://www.facebook.com/groups/cloudcross)