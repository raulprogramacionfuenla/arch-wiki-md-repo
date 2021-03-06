หน้านี้ได้รวบรวมความเหมือนและความแตกต่างระหว่าง Arch และ Distribution (หรือ Distro) อื่นๆ เนื่องจากคำถามนี้ได้รับความนิยมและถูกถามเป็นอย่างมาก ดังนั้นคำตอบที่เป็นมาตรฐานจึงเป็นเรื่องที่ดี ข้อแนะนำคือ วิธีการเปรียบเทียบที่ดีที่สุดคือการติดตั้งและลองใช้งาน Arch และ Distro อื่นๆ แล้วเปรียบเทียบกันด้วยตัวของคุณเอง Arch มีชุมชนผู้ใช้งานที่ยอดเยี่ยม ที่พร้อมจะช่วยเหลือผู้ใช้ใหม่ๆ ข้อสรุปข้างล่างนี้มีจุดประสงค์เพื่อให้ข้อมูลที่เพียงพอในการตัดสินใจว่า Arch เหมาะสมกับคุณหรือไม่

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Arch กับ Gentoo](#Arch_กับ_Gentoo)
*   [2 Arch กับ Crux](#Arch_กับ_Crux)
*   [3 Arch กับ Sorcerer/Lunar-linux/Sourcemage](#Arch_กับ_Sorcerer/Lunar-linux/Sourcemage)
*   [4 Arch กับ Rock](#Arch_กับ_Rock)
*   [5 Arch กับ T2](#Arch_กับ_T2)
*   [6 Arch กับ Distro ที่เป็น Graphic](#Arch_กับ_Distro_ที่เป็น_Graphic)
*   [7 Arch กับ Slackware](#Arch_กับ_Slackware)
*   [8 Arch กับ Debian](#Arch_กับ_Debian)
*   [9 Arch กับ Ubuntu](#Arch_กับ_Ubuntu)
*   [10 Arch กับ RPM-based Distros](#Arch_กับ_RPM-based_Distros)
*   [11 Arch กับ Fedora](#Arch_กับ_Fedora)
*   [12 Arch กับ Mandriva](#Arch_กับ_Mandriva)
*   [13 Arch กับ SUSE](#Arch_กับ_SUSE)
*   [14 Arch กับ Frugalware](#Arch_กับ_Frugalware)

## Arch กับ Gentoo

เพราะว่า Arch ส่งต่อ Package ที่เป็น Binary หรืออยู่ในรูปที่สามารถใช้งานได้เลย ดังนั้นมันจึงใช้เวลาในการติดตั้งน้อยกว่า Gentoo

Gentoo มี Package เยอะกว่าและเปิดโอกาสให้คุณเลือก Version ของ Package ที่คุณต้องการที่จะติดตั้ง แต่ Arch ทำให้คุณใช้งานได้ทั้ง Binary Package หรือสร้างโปรแกรมจาก Source และติดตั้ง Package ที่ไม่ได้อยู่ใน Repository ได้ง่ายกว่าการใช้งาน ebuild

Gentoo สามารถปรับแต่งประสิทธิภาพได้มากกว่า Arch เนื่องจากแต่ละ Package จะถูกสร้างโดยการ Compile ให้เหมาะสมกับ Platform ที่คุณใช้อยู่ ในขณะที่ Arch ได้ถูกออกแบบมาให้ใช้งานได้กับ i686 เท่านั้น (แม้ว่าโครงการสนับสนุน i586 และ x86_64 กำลังอยู่ระหว่างการพัฒนา)

ถึงวันนี้ ยังไม่มีข้อพิสูจน์ใด ที่บ่งบอกว่า Gentoo เร็วกว่า Arch

## Arch กับ Crux

Arch Linux นั้นสืบทอดมาจาก Crux. Judd ผู้ก่อตั้ง Arch Linux ได้สรุปความแตกต่างดังนี้:

	"ผมเคยใช้ Crux มาก่อนที่จะเริ่มพัฒนา Arch โดยหลายส่วนของ Arch เริ่มต้นมาจาก Crux หลังจากนั้นผมได้สร้าง pacman และ makepkg ขึ้นมาเพื่อทดแทน bash script ที่ใช้ในการสร้าง package (ตอนแรกผมสร้าง Arch ขึ้นมาโดยใช้ระบบไฟล์ LFS)ดังนั้น Distro สองอันนี้จึงแตกต่างกันอย่างสิ้นเชิง แต่ในทางเทคนิคแล้วมันเหมือนกัน Arch และ Crux มีพื้นฐานที่คล้ายกัน แต่ Crux จะตรวจสอบ Dependency ในระดับเบื้องต้นเท่านั้น ทำให้ Crux ตัดปัญหาที่เรามีไปได้หลายส่วน เนื่องจากมันมีชุดของ Package ที่เรียบง่าย ที่ปรับแต่งมาสำหรับการใช้งาน"

โปรดดู [ที่กระทู้นี้](https://bbs.archlinux.org/viewtopic.php?t=3608&start=270#133721) สำหรับความประทับใจของผู้ใช้ในแต่ละ Distro

## Arch กับ Sorcerer/Lunar-linux/Sourcemage

Sorcerer/Lunar-linux/Sourcemage (SLS) เป็น distro ที่มีพื้นฐานมาจาก source code คล้ายๆ กับ Gentoo ซึ่งแต่ละตัวมีรากฐานมาจากอันเดียวกัน SLS distro ใช้ชุดของ script พื้นฐานในการจัดการ package และใช้ global configuration ในการตั้งค่าการคอมไพล์โปรแกรมแต่ละตัว ซึ่งคล้ายคลึงกับระบบ ABS ของ Arch

เครื่องมือต่างๆ ของ SLS จะตรวจสอบ Dependency อย่างละเอียด และยังไม่มี binary package สำหรับ SLS distro แต่มันสามารถเรียกใช้งาน package ที่ถูกติดตั้งไปก่อนหน้าได้อย่างง่ายดาย

การติดตั้ง SLS นั้นรวมถึงการติดตั้งระบบพื้นฐาน หรือ base system (คล้ายคลึงกับ Arch ที่ปรับแต่งมาสำหรับ i686, CLI และ เมนูจาก ncurses) หลังจากนั้นผู้ใช้สามารถสร้าง base system ได้ในภายหลัง และมันจะไม่ติดตั้ง WM/DE/DM และ Xserver ระหว่างการติดตั้งระบบ แต่มันมีวิธีที่ง่ายในการติดตั้งชุดโปรแกรมเหล่านี้ในภายหลัง

SLS มีประวัติศาสตร์ที่ค่อนข้างซับซ้อน หากท่านต้องการอ่านเพิ่มเติม สามารถหาได้จากที่นี่: [http://wiki.sourcemage.org/Our_History](http://wiki.sourcemage.org/Our_History)

Lunar Linux: [http://lunar-linux.org/](http://lunar-linux.org/) SourceMage: [http://www.sourcemage.org/](http://www.sourcemage.org/) Sorcerer: [http://sorcerer.berlios.de/](http://sorcerer.berlios.de/)

## Arch กับ Rock

???

## Arch กับ T2

???

## Arch กับ Distro ที่เป็น Graphic

Graphical distro หลายๆ ตัวมีความคล้ายคลึงกัน และ Arch ดูจะแตกต่างจาก Distro เหล่านี้เป็นอย่างมาก Arch ทำงานเป็น text based และอ้างอิง command line และมันยังเป็น distro ที่ดี หากคุณต้องการที่จะเรียนรู้ Linux

Graphical distro ช่วยเหลือผู้ใช้ด้วยการใส่ตัวติดตั้งที่เป็น GUI (Graphical User Interface) เช่น Anaconda จาก Fedora และระบบการตั้งค่าที่เป็น GUI เช่น Yast ของ SuSE รายละเอียดต่างๆ ของแต่ละ distro ได้ถูกแสดงอยู่ทางด้านล่าง

## Arch กับ Slackware

Slackware และ Arch ต่างเป็น distro ที่เรียบง่าย ทั้งคู่ใช้ init script ในรูปแบบของ BSD แต่ Arch มีระบบจัดการ Package ที่ทันสมัยกว่าเมื่อเทียบกับเครื่องมาตรฐานที่มากับ Slackware ที่สมารถทำให้ได้การปรับปรุงระบบแบบอัตโนมัติ

Slackware ดูจะอนุรักษ์นิยมมากกว่าเมื่อเปรียบเทียบในระยะเวลาการออกแจกจ่ายให้ใช้งาน ซึ่ง Slackware จะเน้นที่ Pacakge ที่เสถียร แต่ Arch จะเน้นที่ความใหม่ของ Package

Arch สามารถทำงานได้กับ i686 เท่านั้นในขณะที่ Slackware สามารถทำงานได้บน i486 Arch เป็นระบบที่ดีมากสำหรับผู้ใช้งาน Slackware ที่ต้องการระบบการจัดการ Package ที่มีประสิทธิภาพและ Package ที่ทันสมัย

## Arch กับ Debian

Arch เรียบง่ายกว่า Debian แต่มันมี Package น้อยกว่า Arch สนับสนุนการสร้าง Package ของผู้ใช้ได้ดีกว่า Debian และ Arch ยังผ่อนปรนมากกว่า เมื่อต้องทำงานกับ package ที่เป็น non-free

Arch ถูกปรับแต่งมาให้ใช้งานได้กับ i686 และยังทำงานได้เร็วกว่า Debian (แม้ว่าจะไม่มีหลักฐานยืนยันก็ตาม) Package ของ Arch ยังทันสมัยมากกว่าของ Debian (ชุด current ของ arch ยังทันสมัยว่า ชุด testing ของ debian)

## Arch กับ Ubuntu

Arch มีพื้นฐานที่เรียบง่ายกว่า Ubuntu ถ้าคุณต้องการสร้าง Kernel ของคุณเอง หรือลองใช้งานซอฟท์แวร์จาก CVS หรือสร้างโปรแกรมจาก Source Arch ดูจะเหมาะสมกับคุณมากกว่า แต่ถ้าคุณต้องการเริ่มใช้งานอย่างรวดเร็ว Ubuntu ดูจะเป็นทางเลือกที่ดีกว่า โดยรวมแล้ว นักพัฒนาโปรแกรมและผู้ไฝ่รู้ใน Linux น่าจะชอบ Arch มากกว่า Ubuntu

## Arch กับ RPM-based Distros

Package แบบ RPM สามารถพบได้จากหลายๆ ที่ แต่ Package เหล่านี้มักอ้างอิงถึง library เก่าๆ และสร้างปัญหาในเวลาต่อมา นอกจากนี้ยังมีความสับสนระหว่าง RPM ของ Red hat และ RPM ของ Mandriva

Pacman มีประสิทธิภาพและเชื่อถือได้มากกว่า RPM

## Arch กับ Fedora

Fedora แยกตัวมาจาก Red Hat และยังเป็นหนึ่งใน distro ที่ได้รับความนิยมมากที่สุดในปัจจุบัน Fedora มีชุมชนผู้ใช้ที่มีขนาดใหญ่ และยังมี package ที่ได้ถูกสร้างมาเรียบร้อยแล้วอีกเป็นจำนวนมาก เช่นเดียวกันกับ RPM-based distro ทั่วไปที่มีปัญหากับการจัดการ Package Fedora มีเครื่องมือที่ชื่อว่า Yum เป็นส่วนควบคุมในการติดตั้ง RPM และจัดการกับปัญหา dependency

นอกจากนี้ Fedora ยังได้รับความนิยมมากขึ้นเนื่องจากได้นำเอา package ที่สร้างจาก SELinux และ GCJ เข้าไปรวมในระบบ ทำให้ไม่ต้องการ Java Runtime Environment

และมันยังไม่มีความสามารถในการใช้งาน MP3 เนื่องจากปัญหาทางกฎหมายที่อาจจะตามมา

## Arch กับ Mandriva

Mandriva (เดิมชื่อ Mandrake) ที่เคยได้รับความนิยมจากระบบการติดตั้งที่ทันสมัย เป็น distro ที่ใช้งานได้ง่าย แต่สามารถสร้างปัญหาได้ในเวลาต่อมา อีกปัญหาหนึ่งคือมันเป็น RPM-Based distro ที่ได้ถูกกล่าวถึงไปแล้วทางด้านบน Arch ให้อิสรภาพกับผู้ใช้ที่มากขึ้น และปัญหาที่น้อยลง ผู้ใช้จะได้เรียนรู้ที่จะใช้ Linux จริงๆ จาก Arch

## Arch กับ SUSE

SUSE ได้รับความนิยมจากระบบปรับแต่ง Yast ซึ่งมันเป็นจุดศูนย์รวมสำหรับการตั้งค่าที่ผู้ใช้ต้องการ Arch ยังไม่มีเครื่องมือแบบนี้เนื่องจากมันขัดต่อ [TheArchWay](/index.php/TheArchWay "TheArchWay")

SUSE เหมาะสมกับผู้ใช้งานที่มีประสบการณ์น้อย หรือผู้ที่ต้องการชีวิตที่เรียบง่ายแต่ยังคงไว้ซึ่งประสิทธิภาพ นอกจากนี้ SUSE ยังไม่สนับสนุน MP3 ทันทีหลังจากการติดตั้ง แต่มันสามารถติดตั้งได้อย่างง่ายดายผ่าน Yast

## Arch กับ Frugalware

Arch เป็นระบบปฏิบัติการที่ใช้งานเป็น text based และใช้งานส่วนใหญ่ผ่านทาง command-line (ผู้ใช้เองควรมีความพยายามที่จะเรียนรู้ด้วย) Frugalware มีพื้นฐานมาจาก Slackware และมีการสนับสนุนภาษาอื่นๆที่ดีกว่า Frugalware ยังมีคู่มือการใช้งานเป็นภาษาท้องถิ่นที่มากกว่า และ Frugalware ยังอ้างว่าตัวเองเร็วกว่า Arch

ทั้งคู่ใช้ pacmac แต่ package ของทั้งคู่ดูจะไม่สามารถใช้งานด้วยกันได้