# Метод

Для начала скачайте базы данных пакетов и перенесите их на ваш компьютер, находящийся без доступа к Сети.

**Для i686**:

*   [ftp://ftp.archlinux.org/core/os/i686/core.db.tar.gz](ftp://ftp.archlinux.org/core/os/i686/core.db.tar.gz)
*   [ftp://ftp.archlinux.org/extra/os/i686/extra.db.tar.gz](ftp://ftp.archlinux.org/extra/os/i686/extra.db.tar.gz)
*   [ftp://ftp.archlinux.org/community/os/i686/community.db.tar.gz](ftp://ftp.archlinux.org/community/os/i686/community.db.tar.gz)
*   [ftp://ftp.archlinux.org/multilib/os/i686/multilib.db.tar.gz](ftp://ftp.archlinux.org/multilib/os/i686/multilib.db.tar.gz)

**Для x86_64:**

*   [ftp://ftp.archlinux.org/core/os/x86_64/core.db.tar.gz](ftp://ftp.archlinux.org/core/os/x86_64/core.db.tar.gz)
*   [ftp://ftp.archlinux.org/extra/os/x86_64/extra.db.tar.gz](ftp://ftp.archlinux.org/extra/os/x86_64/extra.db.tar.gz)
*   [ftp://ftp.archlinux.org/community/os/x86_64/community.db.tar.gz](ftp://ftp.archlinux.org/community/os/x86_64/community.db.tar.gz)
*   [ftp://ftp.archlinux.org/multilib/os/x86_64/multilib.db.tar.gz](ftp://ftp.archlinux.org/multilib/os/x86_64/multilib.db.tar.gz)

Следующие шаги обновят базы данных, как если-бы вы ввели `pacman -Sy`

Сделайте следующее на вашем оффлайн-компьютере (как root):

В фигурных скобках три папки, повторите команды для каждой из них. Команду tar выполняйте, как описано, при условии, что вы находитесь в директории с этими папками, иначе вам потребуется написать путь к ним после "-xzf". Например,

```
 tar -xzf /media/usb/core -C /var/lib/pacman/sync/core

```

Итак, команды.

```
mkdir -p /var/lib/pacman/sync/{core,extra,community, multilib}
rm -r /var/lib/pacman/sync/{core,extra,community, multilib}/*
tar -xzf {core,extra,community, multilib}.db.tar.gz -C /var/lib/pacman/sync/{core,extra,community, multilib}

```

Данные команды создадут в **/var/lib/pacman/sync** четыре папки, очистят их и распакуют соответствующие tar-архивы в каждую из них.

**Tip:** Убедитесь в том, что вы активировали как минимум один из серверов, указанных в файле /etc/pacman.d/mirrorlist. В противном случае единственное, что вы получите, это сообщение об ошибке.

Итак, у вас есть базы данных. Для начала, обновим уже существующее.

```
pacman -Sup --noconfirm > pkglist

```

Данная команда создаст в текущей директории файл pkglist (имя файла можете указать своё), где будут написаны ссылки для скачивания всех нужных для обновления системы пакетов. По возможности откройте файл и удалите всё, что не является ссылками. Это понадобится для скачивания wget'ом (хотя и не обязательно, не являющиеся ссылками строки wget пропустит). Перенесите файл с ссылками на компьютер с доступом к Сети. Теперь вы можете скачать пакеты вручную, либо воспользоваться удобным wget'ом.

```
  wget -P <путь_куда_скачивать> -i <путь_к_файлу_с_ссылками>

```

(Лично я скачиваю в папку "pkg", для удобства копирования.)

Перенесите папку со скачанными пакетами на оффлайн-компьютер и копируйте их в **var/cache/pacman/pkg**.

Вы можете копировать не пакеты, а саму папку, уже названную pkg, в таком случае путь будет **/var/cache/pacman**. После копирования вводим

```
 pacman -Su

```

Команда обновит пакеты, свежие версии которых уже скачаны и перенесены.

Для установки других пакетов поступаем по аналогии, разнится лишь команда:

```
 pacman -Sp <имя_пакета> > <файл_для_сохранения_ссылок>

```

И установка:

```
 pacman -S <имя_пакета>

```

## Немного о базах данных

Так как Arch является дистрибутивом "rolling-release", обновление пакетов происходит постоянно. Уже через пару дней вы рискуете увидеть, что базы данных пакетов устарели и скачать по составленному списку ссылок уже нельзя. В таком случае вы можете либо скачивать базы снова, либо использовать сервера, где хранятся старые версии пакетов. Прочитать, как это сделать, можно [здесь](/index.php/Downgrade#Other_Information "Downgrade").

## Пример использования команд

У нас есть обновлённая система, и мы решаем, что хорошо-бы установить файловый менеджер. Я остановился на **Midnight Commander'**e.

(Все значения, как то путь для скачки, название файла с ссылками и сам пакет- могут быть любыми, какими захотите вы. Например, в случае с xorg указываем xorg вместо mc, в случае с GNOME - gnome, etc. )

```
 pacman -Sp mc > mid_com_pkg

```

Создали список для скачки пакета mc. У меня файл создаётся прямо на флешку, поэтому копировать его нужды нет. Если у вас не так:

```
 cp mid_com_pkg <место_монтирования_переносного_носителя>

```

Перенесли, скачали по ссылкам удобным для себя образом. Следом скачанные пакеты копируем в **/var/cache/pacman**. (С учётом, что скачивали вы в папку pkg и находитесь на месте её расположения)

```
 cp -r pkg /var/cache/pacman

```

Если у вас пакеты в какой-то другой папке:

```
 cp <папка_с_пакетами>/* /var/cache/pacman/pkg

```

Если папка находится не в текущей директории - дополняем перед "pkg" или "<папка_с_пакетами>/*" также путь к папке. Подойдёт как абсолютный, т.е. от корня "/", так и относительный. Теперь, когда пакет перенесён

```
 pacman -S mc

```

После установки вводим в консоли `mc` и получаем окно Midnight Commander'a.

**Внимание**

Статья не является дословным переводом оригинала, поэтому вы найдёте в ней несколько отличий.