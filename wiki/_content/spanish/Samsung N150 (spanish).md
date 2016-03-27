Este artículo describe la instalación y configuración del 64-bit Arch Linux en la netbook Samsung N150\. Este material, basado en el output de dmidecode, puede ser también de utilidad para los modelos N210 y N220.

# Sobre el hardware

La netbook Samsung N150 viene equipada con el CPU [Intel Atom](https://en.wikipedia.org/wiki/Intel_Atom "wikipedia:Intel Atom") N450 ("Pineview") con [Intel GMA 3100 GPU](/index.php/Intel "Intel") integrada y chipset "Pine Trail". A diferencia del procesador Intel Atom series N2xx y Z , el N450 soporta el conjunto de instrucciones x86_64\. Aunque la información DMI sugiere que la placa madre acepta hasta 8 GiB RAM, el controlador de memoria integrado en el Atom N450 puede soportar un máximo de 2 GiB . Dado que el hardware está limitado a 32_bit, el principal beneficio de correr la versión de 64_bit de Arch en este sistema es sacar ventaja del paquete AUR construido en sistemas de 64_bit más potentes del mismo propietario.

Las versiones comercializadas de la N150 (al menos hasta Marzo de 2010) incluyen la edición "starter" de un sistema operativo propietario por lo cual incluye sólo 1 GiB RAM en la forma de una única tarjeta DDR2 667 Mhz SODIMM, que puede ser reemplazada por el usuario. De acuerdo a la información de DMI, la unidad contiene dos mini slots PCI express, uno de los cuales está ocupado por la tarjeta wireless Atheros AR9285 incluida. Otras versiones de este modelo aparentemente están equipadas con un adaptador 3G WAN en el otro slot.