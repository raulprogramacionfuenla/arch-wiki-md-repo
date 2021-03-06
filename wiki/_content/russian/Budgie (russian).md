**Состояние перевода:** На этой странице представлен перевод статьи [Budgie](/index.php/Budgie "Budgie"). Дата последней синхронизации: 14 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Budgie&diff=0&oldid=425749).

Related articles

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [GTK+ (Русский)](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)")

Budgie написанный с нуля рабочий стол, который используется по умолчанию в Операционной Системе Solus. К тому же, более современный дизайн Budgie может имитировать внешний вид рабочего стола GNOME 2.

Сейчас Budgie находится в стадии разработки, так что могут появляться ошибки и добавляться новые возможности.

## Contents

*   [1 Установка](#Установка)
    *   [1.1 Запуск](#Запуск)
*   [2 Использование](#Использование)
*   [3 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/Help:%D0%A7%D1%82%D0%B5%D0%BD%D0%B8%D0%B5#Установка_пакетов "Help:Чтение") последний стабильный пакет [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) или текущую разрабатываемую версию [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/). Также рекомендуется установить необязательные зависимости, чтобы получить более полную рабочую среду. Также рекомендуется установить группу [gnome](https://www.archlinux.org/groups/x86_64/gnome/), которая содержит приложения для стандартной работы GNOME.

### Запуск

Выберите сессию *Budgie Desktop* [Экранного менеджера](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер"), или измените [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") добавив Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Использование

Вы можете видеть уведомления сообщений, устанавливать громкость, и изменять внешний вид рабочего стола при помощи боковой панели, под названием "Raven". Доступ к ней осуществляется нажатием `Super+N` или щелчком по Апплету Индикатора Состояния.

## Смотрите также

*   [Официальный сайт проекта Solus (Англ.)](https://solus-project.com/)
*   [Официальный git-репозиторий для разработки Solus (Англ.)](https://git.solus-project.com/)
*   [Build status for Solus projects](https://build.solus-project.com/)