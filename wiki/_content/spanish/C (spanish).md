**Estado de la traducción**
Este artículo es una traducción de [C](/index.php/C "C"), revisada por última vez el **2018-10-07**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=C&diff=0&oldid=546459) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El kernel [Linux](/index.php/Linux_(Espa%C3%B1ol) "Linux (Español)") y las herramientas de usuario [GNU](/index.php/GNU_(Espa%C3%B1ol) "GNU (Español)") están escritos principalmente en [C](https://en.wikipedia.org/wiki/es:C_(lenguaje_de_programaci%C3%B3n) "wikipedia:es:C (lenguaje de programación)").

Arch Linux utiliza la [Biblioteca de C de GNU](https://en.wikipedia.org/wiki/GNU_C_Library "wikipedia:GNU C Library") ([glibc](https://www.archlinux.org/packages/?name=glibc)) como la biblioteca estándar de C; es parte de [base](https://www.archlinux.org/groups/x86_64/base/).

Puede usar [GNU toolchain](/index.php/GNU_toolchain "GNU toolchain") o [LLVM toolchain](/index.php/LLVM_toolchain "LLVM toolchain") para desarrollar software en C/[C++](https://en.wikipedia.org/wiki/C%2B%2B "wikipedia:C++")/[Objective-C](https://en.wikipedia.org/wiki/es:Objective-C "wikipedia:es:Objective-C").

## Contents

*   [1 Herramientas útiles](#Herramientas_.C3.BAtiles)
    *   [1.1 Analizadores de código estático](#Analizadores_de_c.C3.B3digo_est.C3.A1tico)
*   [2 Compiladores alternativos](#Compiladores_alternativos)
*   [3 Implementaciones de libc alternativas](#Implementaciones_de_libc_alternativas)
*   [4 Bibliotecas](#Bibliotecas)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Herramientas útiles

*   **[Valgrind](https://en.wikipedia.org/wiki/Valgrind "wikipedia:Valgrind")** — Herramienta para ayudar a encontrar problemas de gestión de memoria en los programas.

	[http://valgrind.org/](http://valgrind.org/) || [valgrind](https://www.archlinux.org/packages/?name=valgrind)

*   **[distcc](/index.php/Distcc "Distcc")** — Front-end de compilación distribuida de GCC.

	[https://github.com/distcc/distcc](https://github.com/distcc/distcc) || [distcc](https://www.archlinux.org/packages/?name=distcc)

*   **rr** — Herramienta ligera de grabación y depuración determinística para C/C++, utiliza [GDB](/index.php/GDB "GDB").

	[https://rr-project.org/](https://rr-project.org/) || [rr](https://aur.archlinux.org/packages/rr/)

### Analizadores de código estático

*   **[Cppcheck](https://en.wikipedia.org/wiki/Cppcheck "wikipedia:Cppcheck")** — Una herramienta para el análisis de código estático de C/C++.

	[http://cppcheck.sourceforge.net/](http://cppcheck.sourceforge.net/) || [cppcheck](https://www.archlinux.org/packages/?name=cppcheck)

*   **[Splint](https://en.wikipedia.org/wiki/Splint_(programming_tool) "wikipedia:Splint (programming tool)")** — Una herramienta para verificar de forma estática los programas de C en busca de vulnerabilidades de seguridad y errores de programación.

	[http://repo.or.cz/splint-patched.git](http://repo.or.cz/splint-patched.git) || [splint](https://www.archlinux.org/packages/?name=splint)

*   [Clang](/index.php/Clang "Clang") tiene el analizador estático `scan-build`.

## Compiladores alternativos

*   **[TCC](https://en.wikipedia.org/wiki/Tiny_C_Compiler "wikipedia:Tiny C Compiler")** — Compilador C diminuto, dice ser más rápido que GCC.

	[https://bellard.org/tcc/](https://bellard.org/tcc/) || [tcc](https://www.archlinux.org/packages/?name=tcc)

*   **[ACK](https://en.wikipedia.org/wiki/Amsterdam_Compiler_Kit "wikipedia:Amsterdam Compiler Kit")** — Amsterdam Compiler Kit.

	[http://tack.sourceforge.net/](http://tack.sourceforge.net/) || [ack-git](https://aur.archlinux.org/packages/ack-git/)

*   **[PCC](https://en.wikipedia.org/wiki/Portable_C_Compiler "wikipedia:Portable C Compiler")** — Compilador portátil de C.

	[http://pcc.ludd.ltu.se/](http://pcc.ludd.ltu.se/) || [pcc](https://aur.archlinux.org/packages/pcc/)

*   **[SDCC](https://en.wikipedia.org/wiki/Small_Device_C_Compiler "wikipedia:Small Device C Compiler")** — Compilador de ANSI C *retargettable*.

	[http://sdcc.sourceforge.net/](http://sdcc.sourceforge.net/) || [sdcc](https://www.archlinux.org/packages/?name=sdcc)

Véase también [Wikipedia:List of compilers#C compilers](https://en.wikipedia.org/wiki/List_of_compilers#C_compilers "wikipedia:List of compilers").

## Implementaciones de libc alternativas

*   **[musl](https://en.wikipedia.org/wiki/musl "wikipedia:musl")** — Implementación ligera de la biblioteca estándar de C.

	[http://www.musl-libc.org/](http://www.musl-libc.org/) || [musl](https://www.archlinux.org/packages/?name=musl)

## Bibliotecas

*   **[GLib](https://en.wikipedia.org/wiki/GLib "wikipedia:GLib")** — Biblioteca de sistema de bajo nivel por [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), incluye [GObject](https://en.wikipedia.org/wiki/GObject "wikipedia:GObject") y [GIO](https://en.wikipedia.org/wiki/GIO "wikipedia:GIO").

	[https://wiki.gnome.org/Projects/GLib](https://wiki.gnome.org/Projects/GLib) || [glib](https://aur.archlinux.org/packages/glib/)

*   [GStreamer](/index.php/GStreamer "GStreamer") – estructura multimedia basado en tuberías

Véase también:

*   [GTK+/Development#C](/index.php/GTK%2B/Development#C "GTK+/Development")
*   [Desktop notifications#C](/index.php/Desktop_notifications#C "Desktop notifications")
*   [Libcanberra#C](/index.php/Libcanberra#C "Libcanberra")
*   [Archiving and compression#Compression libraries](/index.php/Archiving_and_compression#Compression_libraries "Archiving and compression")
*   [Wikipedia:Category:C libraries](https://en.wikipedia.org/wiki/Category:C_libraries "wikipedia:Category:C libraries")

## Véase también

*   [man page](/index.php/Man_page "Man page"): sección 2 para las llamadas del sistema
*   [man page](/index.php/Man_page "Man page"): sectión 3 para las funciones de la biblioteca
*   [GCC y Make – Compilando, enlazando y construyendo aplicaciones C/C++](https://www3.ntu.edu.sg/home/ehchua/programming/cpp/gcc_make.html)
*   [SEI CERT C Coding Standard](https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard)
*   [##C canal IRC en Freenode](http://iso-9899.info/)