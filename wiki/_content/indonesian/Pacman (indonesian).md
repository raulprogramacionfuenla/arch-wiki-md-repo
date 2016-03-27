| **Summary**  |
| pacman adalah manajer paket Arch Linux. Manajer paket digunakan untuk memasang, mengupgrade, dan menghapus perangkat lunak. Artikel ini mencakup penggunaan dasar dan tips untuk mengatasi masalah. |
| **Overview** |
| Packages in Arch Linux are built using [makepkg](/index.php/Makepkg "Makepkg") and a custom build script for each package (known as a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")). Once packaged, software can be installed and managed with [pacman](/index.php/Pacman "Pacman"). PKGBUILDs for software in the [official repositories](/index.php/Official_repositories "Official repositories") are available from the [ABS](/index.php/ABS "ABS") tree; thousands more are available from the (unsupported) [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). |
| **Related** |
| [Downgrading Packages](/index.php/Downgrading_Packages "Downgrading Packages") |
| [Improve Pacman Performance](/index.php/Improve_Pacman_Performance "Improve Pacman Performance") |
| [pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends") |
| [pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") |
| [pacman Tips](/index.php/Pacman_Tips "Pacman Tips") |
| **Resources** |
| [libalpm(3) Manual Page](https://www.archlinux.org/pacman/libalpm.3.html) |
| [pacman(8) Manual Page](https://www.archlinux.org/pacman/pacman.8.html) |
| [pacman.conf(5) Manual Page](https://www.archlinux.org/pacman/pacman.conf.5.html) |
| [repo-add(8) Manual Page](https://www.archlinux.org/pacman/repo-add.8.html) |

Manajer paket **[pacman](https://archlinux.org/pacman/)** adalah salah satu fitur utama dari Arch Linux. Menggabungkan sebuah format paket biner sederhana dengan sebuah sistem pembangunan yang mudah digunakan (lihat [makepkg](/index.php/Makepkg "Makepkg") dan [Arch Build System](/index.php/Arch_Build_System "Arch Build System")). Tujuan dari pacman adalah memungkinkan pengaturan paket-paket dengan mudah, baik yang berasal dari repositori resmi Arch maupun yang dibangun sendiri oleh para pengguna.

pacman menjaga sistem tetap up to date dengan sinkronisasi daftar paket dengan server master. Model server/klien juga memungkinkan Anda untuk mengunduh/memasang paket dengan perintah sederhana, lengkap dengan semua dependensi yang diperlukan.

pacman ditulis dalam bahasa pemrograman C dan menggunakan format paket `.pkg.tar.xz`.

## Konfigurasi

Konfigurasi pacman terletak di `/etc/pacman.conf`. Di sinilah pengguna mengkonfigurasi program tersebut agar berjalan sesuai dengan yang diinginkan. Informasi mendalam tentang file konfigurasi dapat ditemukan di [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

### Opsi Umum

Opsi-opsi umum terdapat di bagian `[options]`. Baca man page atau lihat di `pacman.conf` untuk informasi apa yang dapat dilakukan di sini.