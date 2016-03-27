## Contents

*   [1 Kodeky Gstreamer](#Kodeky_Gstreamer)
*   [2 Užitečné multimediální přehrávače](#U.C5.BEite.C4.8Dn.C3.A9_multimedi.C3.A1ln.C3.AD_p.C5.99ehr.C3.A1va.C4.8De)
    *   [2.1 VLC](#VLC)
    *   [2.2 MPlayer](#MPlayer)
*   [3 Další zdroje](#Dal.C5.A1.C3.AD_zdroje)
    *   [3.1 codecs-all z archlinuxfr](#codecs-all_z_archlinuxfr)
    *   [3.2 Přehrávání videí s posledními kodeky RealMedia (RV10...RV40)](#P.C5.99ehr.C3.A1v.C3.A1n.C3.AD_vide.C3.AD_s_posledn.C3.ADmi_kodeky_RealMedia_.28RV10...RV40.29)

## Kodeky Gstreamer

Pokud shledáte, že nemůžete přehrávat běžné zvukové (jako třeba MP3) nebo video soubory, možná nemáte nainstalované správné kodeky pro jejich přehrávání. Multimediální přehrávěče používající backend **gstreamer** (jako třeba Totem) budou schopny přehrát většinu multimediálních souborů po instalaci těchto kodeků:

```
# pacman -S gstreamer0.10-bad gstreamer0.10-ugly gstreamer0.10-ffmpeg gstreamer0.10-ugly-plugins

```

V případě, že chcete nainstalovat **všechny** kodeky pro Gstreamer, můžete použít následující příkaz (za předpokladu, že máte nainstalován awk):

```
# pacman -S `pacman -Ss gstreamer | grep -e '^extra/gstreamer0.10' | awk '{print $1}'`

```

**Note:** Balík **codecs** je zastaralý a není nadále potřeba!

## Užitečné multimediální přehrávače

### VLC

Stále můžete shledat, že některé soubory (hlavně video soubory Windows) se v Totemu nepřehrají správně. **VLC** je víceúčelový multimediální přehrávač, jenž má mnoho vlastních kodeků a může ty záludné video soubory zvládnout, stejně jako DVD filmy s menu.

```
# pacman -S vlc

```

### MPlayer

Mplayer též přehraje mnoho souborů. Zjišťuji, že občas přehraje věci, které se nepřehrají ve VLC.

```
# pacman -S mplayer

```

Je zde také užitečný plugin, který integruje mplayer do webových prohlížečů. Nainstalujete ho pomocí:

```
# pacman -S mplayer-plugin

```

## Další zdroje

### codecs-all z archlinuxfr

Repozitář archlinuxfr poskytuje balíček codecs-all, který se zdá kompletnější než běžný balíček codecs z oficiálních repozitářů Arch Linuxu.

### Přehrávání videí s posledními kodeky RealMedia (RV10...RV40)

Přehrávání videí zakódovaných posledními kodeky RealMedia vám pravděpodobně selže, hlavně když přicházejí v exotických formátech jako kontejner Matroska kontejnery (to jest video soubory *.mkv). FFmpeg podporuje RV kodeky nativně, jelikož jsou tyto kodeky postupně reverse-engineerovány. Můžete zkusit nainstalovat ffmpegs-svn z AUR.

Další možnost je jít na [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html). Někde vprostřed stránky můžete stáhnout balíčky s binárními kodeky. Zvolte vhodný pro svoji architekturu a stáhněte jej (v čase psaní tohoto článku verze 20071007 obsahuje cook.so, drvc.so a sipr.so). Rozbalte soubory a - jako root - je zkopírujte do /usr/lib/codecs. Pravděpodobně budete muset nechat přepsat stávající soubory.