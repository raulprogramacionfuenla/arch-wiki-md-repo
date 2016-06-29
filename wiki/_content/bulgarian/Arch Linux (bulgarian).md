Arch Linux е самостоятелно разработвана обществена дистрибуция за i686/x86-64, базирана на модела rolling-release и насочена за опитни потребители на GNU/Linux, която предлага големи binary repositories и прекрасна систем за управление на пакети, както и пакетна система подобна на ports. Разработването се стреми между баланс от минимализъм, елегантност, чист код и модерност. Версия 0.1 (Homer) бе пусната на 11 март, 2002г.

## Contents

*   [1 Преимущества](#.D0.9F.D1.80.D0.B5.D0.B8.D0.BC.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.B0)
*   [2 Уникално управление на пакети](#.D0.A3.D0.BD.D0.B8.D0.BA.D0.B0.D0.BB.D0.BD.D0.BE_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B8)
*   [3 Модерност](#.D0.9C.D0.BE.D0.B4.D0.B5.D1.80.D0.BD.D0.BE.D1.81.D1.82)
*   [4 Семплост](#.D0.A1.D0.B5.D0.BC.D0.BF.D0.BB.D0.BE.D1.81.D1.82)
*   [5 Допълнително четене](#.D0.94.D0.BE.D0.BF.D1.8A.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D0.BD.D0.BE_.D1.87.D0.B5.D1.82.D0.B5.D0.BD.D0.B5)

## Преимущества

Arch предлага минимална среда по време на инсталацията, (без GUI), компилирана за архитектури i686 и x86-64\. Arch е лек, гъвкав, семпъл и се стреми да бъде много близък до UNIX. Философията и внедряването на дизайна му го правят лесен за разширяване и дават възможност да интегриране във всякакви системи - от конзолна машина на минималис до най-грандиозните и пълни със свойства десктоп среди. Вместо да съкращава и маха ненужни и стари пакети, Arch дава възможноста на потребителя да инсталира основа без никакви настройки по подразбиране. *Потребителят* е този, който решава какъв ще е Arch Linux.

## Уникално управление на пакети

Arch е подържана от лесна за ползване binary пакетна система ([pacman](/index.php/Pacman "Pacman")), която дава възможност да се обновява цялата система с една команда. Pacman е написан на **C** и е проектиран от нищото да бъде лек, семпъл и много бърз. Arch също предлага система за създаване на пакети подобна на ports, ([Arch Build System](/index.php/Arch_Build_System "Arch Build System")) да улеснява създаването на инсталационни пакети от програмен код, които също така могат да бъдат синхронизирани с една команда. Можете даже да пресъздадете цялата ви система с една команда. Всичко се върши просто и прозрачно. Моделът rolling release дава възможност за само една пълна инсталация, както и продължителни и непрекъснати обновления,без никога да трябва да преинсталирате или да правите сложни системни обновления за всяка отделна версия.

## Модерност

Arch Linux се стреми да подържа последните версии на софтуеъра който предлага, със системата rolling-release. В момента подържаме пакет за модерни ядра нагалсени за минималните i686 и x86-64 системи, хиляди допълнителни, висококачесвени binary пакети сред които repositories подържани от разработчици и потребители, и хиляди скриптове за PKGBUILD, за създаване и пакетиране от програмен код. Arch предлага непроменен, vanilla софтуеър; пакетите се предлагат от чист програмен код, както авторът го е писал по предназначение. Промени по кода се правят в много редки случаи, за да се предотвратят катастрофи в случай на несъвпадения във версиите, които могат да се появят по време на rolling обновления. Arch обединява много от новите свойства достъпни за потребителите на GNU/Linux, като модерни файлови системи (Ext2/3/4, Reiser, XFS, JFS), LVM2/EVMS, софтуерен RAID, поддръжка на udev и initcpio, както и най-новите ядра на Linux.

## Семплост

[The Arch Way](/index.php/The_Arch_Way "The Arch Way") е философия нещата да са прости. Базовата система на Arch е минимална, но напълно функционираща GNU/Linux среда; Linux ядро, верига приспособления на GNU, и допълнително, помагателни програми за command line средата, като **links** и **Vi**. Тази изчистена основа може да бъде разширена както потребителят поиска.

Простата система init на Arch е дълбоко вдъхновена от начина на *BSD да инкорпорира заявки чрез *един файл* ([rc.conf](/index.php/Rc.conf "Rc.conf")) вместо от сложна директорна структура с мнозина символични връзки за всеки runlevel.

Системните настройки се променят чрез редактиране на текстови файлове.

## Допълнително четене

За повече информация посетете главната страница [https://www.archlinux.org/](https://www.archlinux.org/) от където имате достъп до различни ресурси, като анонси, Wiki, потребителски форуми, bugzilla и др.