Toto je seznam Pacman GUI frontendů, Pacman/AUR pohlížečů balíčků a tray ohlašovatelů. Je také rozdělen na Gtk2 a Qt kategorie.

**Warning:** Žádný z těchto nástrojů není oficiálně podporován vývojáři Arch Linuxu.

## Contents

*   [1 Pacman Frontendy](#Pacman_Frontendy)
    *   [1.1 GNOME/GTK+](#GNOME.2FGTK.2B)
        *   [1.1.1 GNOME PackageKit](#GNOME_PackageKit)
    *   [1.2 KDE/Qt](#KDE.2FQt)
        *   [1.2.1 KPackageKit](#KPackageKit)
        *   [1.2.2 AppSet](#AppSet)
    *   [1.3 NCurses](#NCurses)
        *   [1.3.1 pcurses](#pcurses)
*   [2 Pacman/AUR Prohlížeč balíčků](#Pacman.2FAUR_Prohl.C3.AD.C5.BEe.C4.8D_bal.C3.AD.C4.8Dk.C5.AF)
    *   [2.1 PkgBrowser](#PkgBrowser)
*   [3 Tray ohlašovatelé](#Tray_ohla.C5.A1ovatel.C3.A9)
    *   [3.1 Archup](#Archup)
    *   [3.2 Aarchup](#Aarchup)
    *   [3.3 pacman-notifier](#pacman-notifier)
    *   [3.4 Pacupdate](#Pacupdate)
    *   [3.5 Yapan](#Yapan)
    *   [3.6 ZenMan](#ZenMan)
    *   [3.7 Yaourt-Dzen Notifier](#Yaourt-Dzen_Notifier)
*   [4 Neaktivní projekty](#Neaktivn.C3.AD_projekty)

# Pacman Frontendy

## GNOME/GTK+

### GNOME PackageKit

GNOME PackageKit je na distribuci nezávislá sbírka nástrojů na správu balíčků. Využívá pacman-glib backend (ve vývoji), poskytuje tyto možnosti:

*   Instalace a odinstalace z repositářů.
*   Automatické obnovování databáze balíčků a upozornění na aktualizaci.
*   Instalace z tarů.
*   Vyhledávání balíčků podle jména, popisu, kategorie nebo souboru.
*   Zobrazení závislostí, souborů a obrácených závislostí.
*   Inorování IgnorePkgs a držení HoldPkgs.
*   Nahlašování doplňkových závislostí, .pacnew souborů...

Je možné změnit odstraňování z -Rc na -Rsc pomocí GConf klíče /apps/gnome-packagekit/enable_autoremove.

Známé problémy:

*   Občas se packagekit daemon zastaví když jsou instalační scripty hodoty. Pokud se to stane, packagekitd proces může mít potomka se stejným jménem (packagekitd), který má dalšího s názvem sh. Je bezpečné zabít potomka packagekitd, pokud jeho potomek sh je zombie. Nicméně tím ztratíte výstup skriptů. Problém opraven s pacmanem 3.5.
*   Nekteré chyby nejsou ohlášeny GNOME PackageKitem.
*   PackageKit nenajde repositáře pokud je `Architecture` nastaveno na `auto` v `/etc/pacman.conf`. Změňte to na `Architecture = i686` popř. `Architecture = x86_64` k odstranění chyby.

Balíčky:

```
pacman -S gnome-packagekit gnome-settings-daemon-updates

```

**Tip:** Pokud nechcete instalovat PulseAudio, můžete naistalovat [gnome-settings-daemon-nopulse](https://aur.archlinux.org/packages/gnome-settings-daemon-nopulse/) z AURu.

## KDE/Qt

### KPackageKit

KPackageKit - pacman GUI frontend, jehož rozhraní pacmana využívá pacman-glib a packagekit-qt. Tento grafický nástroj umožňuje z KDE systemsettings provádět následující úkony:

*   Instalace, odinstalace a aktualizace balíčků
*   Vyhledávání a filtrace balíčků
*   Získání informací o balíčcích
*   Obnoivení databáze balíčků
*   Výběr repositářů k aktualizaci
*   Automatické obnovení databáze (Hodiny, dny...)
*   Automatické aktualizace balíčků

KPackageKit - relativně nový frontend pro pacmana, funguje bez větších problémů, snadno použitelný, jednoduchost a dobrá integrace do KDE (a PolicyKit).

Známé problémy:

*   Viz [#GNOME PackageKit](#GNOME_PackageKit)

**AUR:** [https://aur.archlinux.org/packages.php?ID=20413](https://aur.archlinux.org/packages.php?ID=20413)
**Snímky obrazovky** [http://kde-apps.org/content/show.php/KPackageKit?content=84745](http://kde-apps.org/content/show.php/KPackageKit?content=84745)

### AppSet

AppSet - rozšířený a na funkce bohatý GUI frontend správce balíčků. Má tyto funkce:

*   Kategorie softwaru (hry, kancelář, multimedia, internet atd.)
*   Zobrazuje domovské stránky balíčků v zabudovaném prohlížeči
*   Zobrazuje informace o distribuci v zabudovaní čtečce
*   Aktualizace, instalace a odinstalace balíčků
*   Zobrazuje dostupné aktualizace v trayi
*   Automatické aktualizace databáze
*   Informuje o závislostech (např: při pokusu o odstranění balíčku který je potřeba jiným)
*   Příkaz k vyčištění cache (uvolní místo na disku)
*   Chytrý spouštěč který používá nainstalované programy pro zisk oprávnění k instalaci (hledá kdesu, gksu, případně xterm a sudo)
*   AUR s Packer backendem

AppSet potřebuje jen QT knihovny k instalaci. Může být použit v jakémkoliv prostření. Nyní podporuje jen Archlinux (pacman).

**Domovská stránka:** [http://appset.sourceforge.net/](http://appset.sourceforge.net/)
**AUR:** [appset-qt](https://aur.archlinux.org/packages/appset-qt/)
**Snímky obrazovky** [http://sourceforge.net/project/screenshots.php?group_id=376825](http://sourceforge.net/project/screenshots.php?group_id=376825)

## NCurses

### pcurses

Správce balíčků v curses, obsahuje:

*   regexp filtrování a hledání jakýchkoli vlastností balíčku
*   volitelné barvy
*   upravitelné řazení
*   externí příkazy pro úpravy seznamu balíčků
*   uživatelem definovatelné makra a klávesové zkratky

**Domovská stránka:** [https://github.com/schuay/pcurses](https://github.com/schuay/pcurses)
**AUR:** [pcurses](https://www.archlinux.org/packages/?name=pcurses)
**Snímky obrazovky** [https://bbs.archlinux.org/viewtopic.php?id=122749](https://bbs.archlinux.org/viewtopic.php?id=122749)

# Pacman/AUR Prohlížeč balíčků

### PkgBrowser

Pkgbrowser - program k hledání a prohlížení Arch balíčků, zobrazuje detaily o označeném balíčku.

*   Hledání a prohlížení Arch balíčků i z AUR
*   Pouze informační aplikace, nedokáže instalovat, odinstalovat ani aktualzovat balíčky
*   Záměrně je to doplněk pro CLI správu balíčků pres pacmana
*   Další detaily o používání přístupné přes help menu

**Fórum:** [https://bbs.archlinux.org/viewtopic.php?id=117297](https://bbs.archlinux.org/viewtopic.php?id=117297)
**AUR:** [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)
**Snímky obrazovky a zdrojový kód:** [http://code.google.com/p/pkgbrowser/](http://code.google.com/p/pkgbrowser/)

# Tray ohlašovatelé

### Archup

Archup - malý C program informující na dostupné aktualizace systému. Používá GTK+ a libnotify k zobrazení upozornění na aktualizace.

*   Domovská stránka: [archup](/index.php/Archup "Archup"), [http://www.nongnu.org/archup/](http://www.nongnu.org/archup/)
*   AUR: [archup](https://aur.archlinux.org/packages/archup/)
*   Snímky obrazovky: [http://www.nongnu.org/archup/](http://www.nongnu.org/archup/), [http://developer.berlios.de/dbimage.php?id=4687](http://developer.berlios.de/dbimage.php?id=4687) , [http://developer.berlios.de/dbimage.php?id=4688](http://developer.berlios.de/dbimage.php?id=4688)

### Aarchup

Aarchup - fork archupu. Nabízí stejné možnosti a nějaké navíc (viz [https://bbs.archlinux.org/viewtopic.php?id=119129](https://bbs.archlinux.org/viewtopic.php?id=119129)).

*   Domovská stránka: [https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/)
*   AUR: [aarchup](https://aur.archlinux.org/packages/aarchup/)
*   Snímky obrazovky: [http://i.imgur.com/yTNvg.png](http://i.imgur.com/yTNvg.png)

### pacman-notifier

Napsán v Ruby, používá Gtk. Zoprazuje ikonu v trayi a vyskakovací upozornění (libnotify) o aktualizacích.

*   Domovská stránka: [https://github.com/v01d/pacman-notifier/wiki](https://github.com/v01d/pacman-notifier/wiki)
*   AUR: [pacman-notifier](https://aur.archlinux.org/packages/pacman-notifier/)
*   Snímky obrazovky: [https://github.com/v01d/pacman-notifier/wiki](https://github.com/v01d/pacman-notifier/wiki)

### Pacupdate

Pacupdate - malý program upozorňující na aktualizace. Po nalezení aktualizace zobrazí upozornění v trayi.

*   Domovská stránka: [http://code.google.com/p/pacupdate/](http://code.google.com/p/pacupdate/)
*   AUR: [pacupdate-svn](https://aur.archlinux.org/packages/pacupdate-svn/)
*   Snímky obrazovky:

### Yapan

Yapan - Yet Another Package mAnager Notifier - napsán v C++ a Qt. Zobrazuje ikonu v trayi, vyskakovací okno s upozorněními na aktualizace a podporu pro ostatní správce balíčků např: clyde, yaourt...

*   Domovská stránka: [https://bitbucket.org/otsug/yapan/wiki/Home](https://bitbucket.org/otsug/yapan/wiki/Home) , [https://bbs.archlinux.org/viewtopic.php?id=113078](https://bbs.archlinux.org/viewtopic.php?id=113078)
*   AUR: [yapan](https://aur.archlinux.org/packages/yapan/)
*   Snímky obrazovky: [https://bitbucket.org/otsug/yapan/wiki/Home](https://bitbucket.org/otsug/yapan/wiki/Home)

### ZenMan

PacMan frontend (tray hlídač aktualizací) v GTK/GNOME/zenity/libnotify.

*   Domovská stránka:
*   AUR: [zenman](https://aur.archlinux.org/packages/zenman/)
*   Snímky obrazovky: [http://show.harvie.cz/screenshots/zenman-screenshot-2.png](http://show.harvie.cz/screenshots/zenman-screenshot-2.png)

### Yaourt-Dzen Notifier

Velmi jednoduchý 14 řádkový shell script zobrazující počet dostupných aktualizací v názvu dzen2 okna a seznam těchto aktualizací v podřízeném okně. Používá yaourt, dzen2 a inotify-tools.

*   Domovská stránka: [http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2](http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2)
*   AUR:
*   Snímky obrazovky: [http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2](http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2)

# Neaktivní projekty

*   [GtkPacman](http://gtkpacman.berlios.de/)
*   [Guzuta](http://guzuta.berlios.de/)
*   [Shaman](http://chakra-project.org/wiki/index.php/Shaman)
*   [PacmanManager](https://opensvn.csie.org/PacmanManager/)
*   [pacmon](http://code.google.com/p/pacmon/)
*   [Paku](https://gna.org/projects/paku/)
*   [YAPG](http://www.kde-apps.org/content/show.php/YAPG+-+Yet+Another+Pacman+Gui+?content=60052)
*   [zenity_pacgui](http://sourceforge.net/projects/zenitypacgui/)