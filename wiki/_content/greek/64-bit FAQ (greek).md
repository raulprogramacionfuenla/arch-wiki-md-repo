Εδώ συχνές ερωτήσεις-απαντήσεις για την αρχιτεκτονική x86_64 στο Arch Linux

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Πώς μπορώ να εγκαταστήσω το Arch64;](#Πώς_μπορώ_να_εγκαταστήσω_το_Arch64;)
*   [2 Πόσο πλήρης είναι η μεταφορά στην 64bit αρχιτεκτονική; Θα έχω όλα τα πακέτα απο το αντίστοιχο 32bit περιβάλλον ;](#Πόσο_πλήρης_είναι_η_μεταφορά_στην_64bit_αρχιτεκτονική;_Θα_έχω_όλα_τα_πακέτα_απο_το_αντίστοιχο_32bit_περιβάλλον_;)
*   [3 Το 64bit σημαίνει μεγάλη αύξηση σε ταχύτητα ;](#Το_64bit_σημαίνει_μεγάλη_αύξηση_σε_ταχύτητα_;)
*   [4 Προσοχή όταν αναβαθμίζετε το πακετο glibc από την έκδοση <2.4 !](#Προσοχή_όταν_αναβαθμίζετε_το_πακετο_glibc_από_την_έκδοση_<2.4_!)
*   [5 Πώς ενημερώνω για πιθανά bugs;](#Πώς_ενημερώνω_για_πιθανά_bugs;)
*   [6 Υπάρχει mailing list;](#Υπάρχει_mailing_list;)
*   [7 Τί repos πρέπει να χρησιμοποιήσω;](#Τί_repos_πρέπει_να_χρησιμοποιήσω;)
*   [8 Πώς μπορώ να βρω PKGBUILDS για το χτίσιμο πακέτων για την αρχιτεκτονική 64bit ;](#Πώς_μπορώ_να_βρω_PKGBUILDS_για_το_χτίσιμο_πακέτων_για_την_αρχιτεκτονική_64bit_;)
*   [9 Πώς μπορώ να χτίσω 64bit πακέτα απο έτοιμα 32bit PKGBUILDs;](#Πώς_μπορώ_να_χτίσω_64bit_πακέτα_απο_έτοιμα_32bit_PKGBUILDs;)
*   [10 Πώς μπορώ να προσθέσω patches σε ήδη υπάρχοντα PKGBUILDs για χρήση με το Arch64;](#Πώς_μπορώ_να_προσθέσω_patches_σε_ήδη_υπάρχοντα_PKGBUILDs_για_χρήση_με_το_Arch64;)
*   [11 Μπορώ να χτίσω πακέτα για την αρχιτεκτονική 32bit (i686) μεσα σε περιβάλλον 64bit (x86_64) ;](#Μπορώ_να_χτίσω_πακέτα_για_την_αρχιτεκτονική_32bit_(i686)_μεσα_σε_περιβάλλον_64bit_(x86_64)_;)
*   [12 Μπορώ να τρέξω 32bit εφαρμογές μεσα στο 64bit Arch σύστημα μου;](#Μπορώ_να_τρέξω_32bit_εφαρμογές_μεσα_στο_64bit_Arch_σύστημα_μου;)
*   [13 Μπορώ να "αναβαθμίσω" το σύστημα μου σε 64bit, από ένα σύστημα 32bit, χωρίς επανεγκατάσταση ;](#Μπορώ_να_"αναβαθμίσω"_το_σύστημα_μου_σε_64bit,_από_ένα_σύστημα_32bit,_χωρίς_επανεγκατάσταση_;)

## Πώς μπορώ να εγκαταστήσω το Arch64;

Απλά χρησιμοποιείστε το [επίσημο CD εγκατάστασης για το Arch64](https://www.archlinux.org/download/).

## Πόσο πλήρης είναι η μεταφορά στην 64bit αρχιτεκτονική; Θα έχω όλα τα πακέτα απο το αντίστοιχο 32bit περιβάλλον ;

Τα αποθετήρια (repositories) [extra] και [core] είναι πλήρως μεταγλωττισμένα στην 64bit αρχιτεκτονική και σχεδόν up-to-date, δηλαδή μόλις λίγες ώρες ή μερες πίσω σε ανανεωση απο το Arch i686\. Οι TUs προσπαθούν να μεταφέρουν και το [community] αποθετήριο πλήρως και στην 64bit αρχιτεκτονική.

Το port στην 64bit αρχιτεκτονική είναι πλήρες για καθημερινή desktop και server χρήση.

## Το 64bit σημαίνει μεγάλη αύξηση σε ταχύτητα ;

Για εφαρμογές που χρησιμοποιούν αμειγώς 64bit μητρώα (όπως μεγάλες βάσεις δεδομένων κλπ) αυτό είναι αλήθεια, στις περισσότερες περιπτώσεις. Ορισμένες μάλιστα εφαρμογές multimedia θα εκτελούνται εμφανώς γρηγορότερα. Εάν γνωρίζετε μία εφαρμογή που να εκτελείται γρηγορότερα όταν χρησιμοποιούνται οι CPU επεκτάσεις SSE3, μπορείτε να ξαναχτίσετε το πακέτο μόνοι σας. Εμείς κάνουμε compilation σε προγράμματα μόνο με SSE2 support (με march=x86_64) and -O2 βελτιστοποιήσεις. Για περισσότερα διαβάστε [http://forums.gentoo.org/viewtopic.php?t=221045](http://forums.gentoo.org/viewtopic.php?t=221045) ή [http://www.thejemreport.com/mambo/content/view/74/74/](http://www.thejemreport.com/mambo/content/view/74/74/) .

Για το υπόλοιπο σύστημα: Δεν κάνει και καμιά ιδιαίτερη διαφορά.

Ως γνωστόν, τα 64bit συστήματα, καταφέρνουν να φέρουν υψηλότερες επιδόσεις, ιδίως σε υψηλό φόρτο, με οποιοδήποτε 64bit capable επεξεργαστή (Core2Duo ή νεότερο επεξεργαστή Intel με Intel64, Athlon64 ή νεότερο επεξεργαστή AMD με AMD64)

## Προσοχή όταν αναβαθμίζετε το πακετο glibc από την έκδοση <2.4 !

Είναι σημαντικό να αναβαθμίσετε το glibc απο έκδοση <2.4 και πρέπει να γίνει ξεχωριστά απο το υπόλοιπο σύστημα. Γι'αυτό κάνετε μόνο

```
  pacman -Syy glibc 

```

και εάν είναι επιτυχής η αναβάθμιση κάνετε

```
 pacman -Su 

```

Μπορεί να μην πετύχει η προσθαφαίρεση βιβλιοθηκών και πρέπει να χρησιμοποιήσετε το pacman.static για να το διορθώσετε.

## Πώς ενημερώνω για πιθανά bugs;

Απλά να χρησιμοποιήσετε το Arch Flyspray αλλά επισημάνετε ότι χρησιμοποιείτε x86_64 εάν πιστεύετε ότι είναι πρόβλημα μεταφοράς πακέτων στα 64bit.

## Υπάρχει mailing list;

Ναι, δείτε εδώ μία[mailing list για τα Arch ports σε αλλη αρχιτεκτονική](https://archlinux.org/mailman/listinfo/arch-ports).

## Τί repos πρέπει να χρησιμοποιήσω;

Όλα τα επίσημα repos λειτουργούν σωστά για την 64bit αρχιτεκτονική.

## Πώς μπορώ να βρω PKGBUILDS για το χτίσιμο πακέτων για την αρχιτεκτονική 64bit ;

Χρησιμοποιείται το ***ABS*** όπως στο 32bit Arch. Προτεινόμενο μέρος για τοποθέτηση των PKGBUILDs είναι το */var/abs*. Το *abs* κατεβάζει όλες τις καταχωρήσεις στο Arch CVS από το archlinux.org που έχουν ως tag CURRENT-64.

## Πώς μπορώ να χτίσω 64bit πακέτα απο έτοιμα 32bit PKGBUILDs;

Τα PKGBUILDs του Arch 32bit είναι κοινά με του Arch 64bit. Μπορείτε να βρείτε 32-bit PKGBUILDs που δεν έχουν ακόμη μεταφερθεί ως ports στην 64bit αρχιτεκτονική απο το CVS: [https://www.archlinux.org/cvs/](https://www.archlinux.org/cvs/)

## Πώς μπορώ να προσθέσω patches σε ήδη υπάρχοντα PKGBUILDs για χρήση με το Arch64;

Προστίθεται αυτή η μεταβλητή:

```
arch=('i686' 'x86_64') 

```

Προσθέστε μικρά patches κατευθείαν στο source πακέτο και στο τμήμα για τα MD5SUMs για χρήση σε τελειως διαφορετικά sources:

```
[ "$CARCH" = "x86_64" ] && source=(${source[@]} 'other source')
[ "$CARCH" = "x86_64" ] && md5sums=(${md5sums[@]} 'other md5sum')

```

Προσθέστε αυτό στο τμήμα για το χτίσιμο του πακέτου (build area):

```
[ "$CARCH" = "x86_64" ] && (patch -Np0 -i ../foo_x86_64.patch || return 1)

```

Ή όταν κάνετε μεγαλύτερες αλλαγές:

```
if [ "$CARCH" = "x86_64" ]; then
    configure/patch/sed      # for x86_64
  else configure/patch/sed   # for i686
fi

```

Για τους developers:

```
cvs commit -m "x86_64 updated/fixed or whatever"
cvs tag -cFR CURRENT-64 foo-package-directory (ακόμη και για τα extra, community, unstable and testing repositories)

```

## Μπορώ να χτίσω πακέτα για την αρχιτεκτονική 32bit (i686) μεσα σε περιβάλλον 64bit (x86_64) ;

Ναι. Χρειάζεται να φτιάξετε ενα i686 chroot περιβάλλον (για χρήση και του i686 CD δειτε περισσότερα εδώ [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")). Εγκαταστήστε το linux32 πακέτο για να κάνετε το chrooted περιβάλλον να συμπεριφέρεται σαν πραγματικό i686 περιβάλλον. Μετά χρησιμοποιείστε το script που ακολουθεί για να κάνετε login στο chrooted περιβάλλον σαν root

**Προσοχή ! Να βάλετε τα δικά σας mountpoints απαραιτήτως**:

```
#!/bin/bash
mount --bind /dev /path-to-your-chroot/dev
mount --bind /dev/pts /path-to-your-chroot/dev/pts
mount --bind /dev/shm /path-to-your-chroot/dev/shm
mount -t proc none /path-to-your-chroot/proc
mount -t sysfs none /path-to-your-chroot/sys
linux32 chroot /path-to-your-chroot

```

Εάν τα πακέτα με το source βρίσκονται στο x86_64 σύστημα προσθέστε

```
 "mount --bind /path-to-your-stored-sources /path-to-your-chroot/path-to-your-stored-sources" 

```

για να μοιράζετε sources από το μητρικό στο chrooted σύστημα για το χτίσιμο των δικών σας πακέτων μέσω του /etc/makepkg.conf.

## Μπορώ να τρέξω 32bit εφαρμογές μεσα στο 64bit Arch σύστημα μου;

Ναι.

1) Εγκαταστήστε τις lib32-* βιβλιοθήκες από το community repo..

2) Ή να φτιάξετε ένα chrooted περιβάλλον με 32bit σύστημα:

Εκκινείστε το Arch64, εκκινείστε τον X (π.χ. startx), ανοίξτε terminal (π.χ. xterm)

**Προσοχή, χρησιμοποιείστε τα δικά σας mountpoints.**

```
xhost +local:
su
mount /dev/sda1 /mnt/arch32
mount --bind /proc /mnt/arch32/proc
chroot /mnt/arch32
su your32bitusername
/usr/bin/command-που-θέλετε-να-τρέξετε # ή π.χ.: /opt/mozilla/bin/firefox

```

Ορισμένες 32bit εφαρμογές (όπως το OpenOffice) χρειάζονται οπωσδήποτε πρόσθετα πακέτα για το χτίσιμο τους. Οι εξής γραμμές πρέπει να προσθεθούν στο rc.local για να επιβεβαιώσετε ότι θα τρέξουν 32-bit εφαρμογές χωρίς πρόβλημα (υποθέτωντας ότι το /mnt/arch32 είναι mounted στο /etc/fstab):

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
#comment the following line if you do not use the same home folder
mount --bind /home /mnt/arch32/home

```

Μετά πατήστε στο terminal

```
xhost +localhost
sudo chroot /mnt/arch32 su your32bitusername /opt/openoffice/program/soffice

```

## Μπορώ να "αναβαθμίσω" το σύστημα μου σε 64bit, από ένα σύστημα 32bit, χωρίς επανεγκατάσταση ;

Όχι. Όμως, μπορείτε να εγκαταστήσετε το Arch64 CD, κάνετε mount τον δίσκο , κάνετε backup ό,τι χρειάζεστε και εγκαταστήστε κρατώντας ό,τι δεν είναι 32bit compiled, όπως και mountpoints που δεν θα έχουν πρόβλημα συμβατότητας (π.χ.: /home & /etc) και εγκαταστήστε.