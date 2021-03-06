**Состояние перевода:** На этой странице представлен перевод статьи [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems"). Дата последней синхронизации: 27 декабря 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=CUPS/Printer-specific_problems&diff=0&oldid=560538).

Ссылки по теме

*   [CUPS (Русский)](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)")
*   [CUPS/Решение проблем](/index.php/CUPS/%D0%A0%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC "CUPS/Решение проблем")

Эта статья содержит инструкции по настройки [CUPS](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)") для конкретных моделей принтеров. Если ваш принтер не упомянается здесь, или если ни один из перечисленных драйверов не работает, посмотрите на сайте [OpenPrinting](http://www.openprinting.org/printers).

**Примечание:** Если вы добавите принтер в этот список, подумайте о том, чтобы внести свой вклад в [OpenPrinting](https://wiki.linuxfoundation.org/openprinting/database/databaseintro) - таким образом и для пользователей других дистрибутивов эта информация будет полезна!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Brother](#Brother)
    *   [1.1 Сетевые принтеры](#Сетевые_принтеры)
    *   [1.2 Специализированные драйверы](#Специализированные_драйверы)
        *   [1.2.1 Установка вручную из пакетов RPM](#Установка_вручную_из_пакетов_RPM)
    *   [1.3 Обновление прошивки](#Обновление_прошивки)
*   [2 Canon](#Canon)
    *   [2.1 CARPS](#CARPS)
    *   [2.2 USB через IP (BJNP)](#USB_через_IP_(BJNP))
    *   [2.3 cnijfilter](#cnijfilter)
*   [3 Dell](#Dell)
*   [4 Epson](#Epson)
    *   [4.1 Утилиты](#Утилиты)
        *   [4.1.1 escputil](#escputil)
        *   [4.1.2 mtink](#mtink)
        *   [4.1.3 Stylus-toolbox](#Stylus-toolbox)
    *   [4.2 Специализированные драйверы](#Специализированные_драйверы_2)
        *   [4.2.1 Avasys](#Avasys)
*   [5 HP](#HP)
    *   [5.1 HPLIP](#HPLIP)
    *   [5.2 foo2zjs](#foo2zjs)
*   [6 Konica Minolta](#Konica_Minolta)
    *   [6.1 foo2zjs](#foo2zjs_2)
*   [7 Lexmark](#Lexmark)
    *   [7.1 Утилиты](#Утилиты_2)
    *   [7.2 Специализированный драйверы](#Специализированный_драйверы)
*   [8 Oki](#Oki)
*   [9 Ricoh](#Ricoh)
*   [10 Samsung](#Samsung)
*   [11 Xerox или FujiXerox](#Xerox_или_FujiXerox)
    *   [11.1 Специализированные драйверы](#Специализированные_драйверы_3)
        *   [11.1.1 Phaser 3100MFP](#Phaser_3100MFP)
        *   [11.1.2 Phaser 6000B](#Phaser_6000B)
        *   [11.1.3 Phaser 6125N](#Phaser_6125N)

## Brother

| Принтер | Драйвер/фильтр | Примечание |
| DCP-135C | [brother-dcp135c](https://aur.archlinux.org/packages/brother-dcp135c/) |
| DCP-150C | [brother-dcp150c](https://aur.archlinux.org/packages/brother-dcp150c/) |
| DCP-7020 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. |
| DCP-7030 | [brother-dcp7030](https://aur.archlinux.org/packages/brother-dcp7030/) |
| DCP-7065DN | [brother-dcp7065dn](https://aur.archlinux.org/packages/brother-dcp7065dn/) |
| DCP-J515W | [brother-dcp-j515w](https://aur.archlinux.org/packages/brother-dcp-j515w/) |
| FAX-2820 | [brother-cups-wrapper-laser](https://aur.archlinux.org/packages/brother-cups-wrapper-laser/) |
| FAX-2840 | [brother-fax2840](https://aur.archlinux.org/packages/brother-fax2840/) | Или [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") - работает в основном с `hpijs-pcl5e.ppd`. То же, что и HL-2170W. |
| FAX-2940 | [brother-fax2940](https://aur.archlinux.org/packages/brother-fax2940/) |
| HL-2030 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/) |
| HL-2035 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Должен быть совместим с любыми драйверами для HL-2030. |
| HL-2040 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или [brother-hl2040](https://aur.archlinux.org/packages/brother-hl2040/) |
| HL-2130 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") (с использованием драйвера HL-2140) | Или [hplip](https://www.archlinux.org/packages/?name=hplip) |
| HL-2140 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или [brother-hl2140](https://aur.archlinux.org/packages/brother-hl2140/) |
| HL-2170W | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. |
| HL-2230 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | То же, что и HL-2170W. Выберите HL-2170W в качестве драйвера в администраторе CUPS при добавлении принтера. |
| HL-2250DN | [brother-hl2250dn](https://aur.archlinux.org/packages/brother-hl2250dn/) |
| HL-2270DW | [brother-hl2270dw](https://aur.archlinux.org/packages/brother-hl2270dw/) |
| HL-2280DW | [brother-hl2280dw](https://aur.archlinux.org/packages/brother-hl2280dw/) |
| HL-2340DW | [brother-hll2340dw](https://aur.archlinux.org/packages/brother-hll2340dw/) |
| HL-3045CN | Установите драйвер Brother. |
| HL-3140CW | [brother-hl3140cw](https://aur.archlinux.org/packages/brother-hl3140cw/) | Используйте драйвер IPP и Brother, чтобы избежать сокращения страниц и бесконечных распечаток |
| HL-3150CDW | [brother-hl3150cdw](https://aur.archlinux.org/packages/brother-hl3150cdw/) |
| HL-3170CDW | [brother-hl3170cdw](https://aur.archlinux.org/packages/brother-hl3170cdw/) |
| HL-4150CDN | [brother-hl4150cdn](https://aur.archlinux.org/packages/brother-hl4150cdn/) |
| HL-5140 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. |
| HL-5340 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Используйте драйвер *Generic PCL 6/PCL XL Printer - CUPS+Gutenprint* ([gutenprint](https://www.archlinux.org/packages/?name=gutenprint) и [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds)). Или драйвер Brother, который может привести к сбою печати с ошибками postscript. |
| HL-L2300D | [brother-hll2300d](https://aur.archlinux.org/packages/brother-hll2300d/) |
| HL-L2350DW | [brother-hll2350dw](https://aur.archlinux.org/packages/brother-hll2350dw/) |
| HL-L2380DW | [brother-hll2380dw](https://aur.archlinux.org/packages/brother-hll2380dw/) |
| HL-L2395DW | [brother-hll2395dw](https://aur.archlinux.org/packages/brother-hll2395dw/) | Используйте протокол `socket`'а, как описано в разделе [#Сетевые принтеры](#Сетевые_принтеры). |
| HL-L5100DN | Драйвер Foomatic для HP LaserJet | Эта модель будет эмулировать HP LaserJet. Используйте протокол `lpd`, как описано в разделе [#Сетевые принтеры](#Сетевые_принтеры). |
| MFC-420CN | [brother-mfc-420cn](https://aur.archlinux.org/packages/brother-mfc-420cn/) |
| MFC-440CN | [brother-mfc-440cn](https://aur.archlinux.org/packages/brother-mfc-440cn/) |
| MFC-7360N | [brother-mfc7360n](https://aur.archlinux.org/packages/brother-mfc7360n/) |
| MFC-7460DN | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Используйте драйвер *Generic PCL 6 Printer wide margin - CUPS+Gutenprint* с адрессом `ipp://hostname-or-ip/pcl_p1`. |
| MFC-7840W | [brother-mfc-7840w](https://aur.archlinux.org/packages/brother-mfc-7840w/) |
| MFC-9320CW | Установите драйвер Brother. |
| MFC-9332CDW | [brother-mfc-9332cdw](https://aur.archlinux.org/packages/brother-mfc-9332cdw/) |
| MFC-9840CDW | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") | Или драйвер Brother. Этот принтер также работает с универсальным драйвером PCL-6 из пакета [gutenprint](https://www.archlinux.org/packages/?name=gutenprint). Используйте **pcl_p1**, как адрес принтера при использовании драйвера PCL-6. |
| MFC-J470DW | [brother-mfc-j470dw](https://aur.archlinux.org/packages/brother-mfc-j470dw/) |
| MFC-J4710DW | [brother-mfc-j4710dw](https://aur.archlinux.org/packages/brother-mfc-j4710dw/) |
| MFC-J480DW | [brother-mfc-j480dw](https://aur.archlinux.org/packages/brother-mfc-j480dw/) | Используйте протокол `ipp://`, как описано в разделе [#Сетевые принтеры](#Сетевые_принтеры). |
| MFC-J5520DW | [brother-mfc-j5520dw](https://aur.archlinux.org/packages/brother-mfc-j5520dw/) |
| MFC-J5910DW | [brother-mfc-j5910dw](https://aur.archlinux.org/packages/brother-mfc-j5910dw/) |
| MFC-J650DW | Установите драйвер Brother. |
| MFC-J885DW | [brother-mfc-j885dw](https://aur.archlinux.org/packages/brother-mfc-j885dw/) |
| MFC-J985DW | [brother-mfc-j985dw](https://aur.archlinux.org/packages/brother-mfc-j985dw/) |
| MFC-L2700DW | [brother-mfc-l2700dw](https://aur.archlinux.org/packages/brother-mfc-l2700dw/) | Пожалуйста, посмотрите также комментарии на странице пакета в aur. |
| QL-500 | [brother-ql500](https://aur.archlinux.org/packages/brother-ql500/) |
| QL-570 | [brother-ql570](https://aur.archlinux.org/packages/brother-ql570/) |
| QL-580N | [brother-ql580n](https://aur.archlinux.org/packages/brother-ql580n/) |
| QL-650TD | [brother-ql650td](https://aur.archlinux.org/packages/brother-ql650td/) |
| QL-700 | [brother-ql700](https://aur.archlinux.org/packages/brother-ql700/) |
| QL-710W | [brother-ql710w](https://aur.archlinux.org/packages/brother-ql710w/) |
| QL-720NW | [brother-ql720nw](https://aur.archlinux.org/packages/brother-ql720nw/) |
| QL-1050 | [brother-ql1050](https://aur.archlinux.org/packages/brother-ql1050/) |
| QL-1050N | [brother-ql1050n](https://aur.archlinux.org/packages/brother-ql1050n/) |
| QL-1060 | [brother-ql1060n](https://aur.archlinux.org/packages/brother-ql1060n/) |
| TD-2020 | [brother-td2020](https://aur.archlinux.org/packages/brother-td2020/) |
| TD-2120N | [brother-td2120n](https://aur.archlinux.org/packages/brother-td2120n/) |
| TD-2130N | [brother-td2130n](https://aur.archlinux.org/packages/brother-td2130n/) |
| TD-4000 | [brother-td4000](https://aur.archlinux.org/packages/brother-td4000/) |
| TD-4100N | [brother-td4100n](https://aur.archlinux.org/packages/brother-td4100n/) |
| Принтер | Драйвер/фильтр | Примечание |

### Сетевые принтеры

Для сетевых принтеров используйте `ipp://**printer_ip**/ipp/port1` в качестве адреса принтера. Для некоторых старых принтеров это может не сработать. Если не сработало, попробуйте `lpd://**printer_ip**/BINARY_P1`.

Некоторые принтеры используют протокол сокета. Для этих принтеров используйте `socket://**printer_ip**:9100`. Для http используйте `http://**printer_ip**/POSTSCRIPT_P1`.

### Специализированные драйверы

Brother предоставляет специализированные драйверы на своем веб-сайте либо в исходном архиве, так и в формате rpm или deb. [Сборка драйверов принтера Brother](/index.php/Packaging_Brother_printer_drivers "Packaging Brother printer drivers") охватывает создание [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") из существующих пакетов RPM.

**Примечание:** Исходные пакеты могут быть лучшей альтернативой пакетам rpm, если они содержат все необходимые файлы.

#### Установка вручную из пакетов RPM

**Важно:** В идеале это должно быть автоматизировано в [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)")

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [rpmextract](https://www.archlinux.org/packages/?name=rpmextract) и извлеките оба пакета rpm с помощью `rpmextract.sh`. Извлечение обоих файлов создаст каталог var и usr - переместите содержимое обоих каталогов в соответствующие корневые каталоги.

Запустите файл оболочки CUPS в `/usr/local/Brother/cupswrapper`. Это должно автоматически установить и настроить ваш принтер brother.

Для некоторых драйверов может потребоваться установить 32-битные библиотеки из [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)").

### Обновление прошивки

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [net-snmp](https://www.archlinux.org/packages/?name=net-snmp) и запустите:

```
snmpwalk -c public $PRINTER_IP | grep -A 1 3.6.1.4.1.2435.2.4.3.99.3.1.6.1.2

```

На этом этапе у вас будут соответствующие данные, чтобы получить ссылку на прошивку от Brother. Файл должен выглядеть примерно так:

 `request.xml` 
```
 <REQUESTINFO>
    <FIRMUPDATETOOLINFO>
        <FIRMCATEGORY>MAIN</FIRMCATEGORY>
        <OS>LINUX</OS>
        <INSPECTMODE>1</INSPECTMODE>
    </FIRMUPDATETOOLINFO>

    <FIRMUPDATEINFO>
        <MODELINFO>
            <SELIALNO></SELIALNO>
            <NAME>MFC-9330CDW</NAME>
            <SPEC>0401</SPEC>
            <DRIVER></DRIVER>
            <FIRMINFO>
                <FIRM>
                    <ID>MAIN</ID>
                    <VERSION>R1506121801:4504</VERSION>
                </FIRM>
                <FIRM>
                    <ID>SUB1</ID>
                    <VERSION>1.07</VERSION>
                </FIRM>
                <FIRM>
                    <ID>SUB2</ID>
                    <VERSION>L1505291600</VERSION>
                </FIRM>
            </FIRMINFO>
        </MODELINFO>
        <DRIVERCNT>1</DRIVERCNT>
        <LOGNO>2</LOGNO>
        <ERRBIT></ERRBIT>
        <NEEDRESPONSE>1</NEEDRESPONSE>
    </FIRMUPDATEINFO>
 </REQUESTINFO>

```

Отправьте этот файл Brother:

```
curl -X POST -d @request.xml [https://firmverup.brother.co.jp/kne_bh7_update_nt_ssl/ifax2.asmx/fileUpdate](https://firmverup.brother.co.jp/kne_bh7_update_nt_ssl/ifax2.asmx/fileUpdate) -H "Content-Type:text/xml" > response.xml

```

В `response.xml` вы найдете тег `<PATH>`, содержащий URL-адрес загрузки прошивки. Затем загрузите прошивку, нажмите ее на принтер и дайте принтеру обработать ее. Прежде чем это сделать, измените пароль администратора на что-то известное, он будет использоваться как пользователь для входа на сайт FTP (ОЧЕНЬ плохая практика, не делайте этого).

```
wget [http://update-akamai.brother.co.jp/CS/LZ4266_W.djf](http://update-akamai.brother.co.jp/CS/LZ4266_W.djf)
ftp $PRINTER_IP
 bin
 hash
 send LZ4266_W.djf
 bye

```

При этом принтер перезагрузится, и последняя версия прошивки будет установлена и (надеюсь) проблемы с печатью будут решены.

## Canon

Существует много возможных драйверов для принтеров Canon. [Многие принтеры Canon](http://gimp-print.sourceforge.net/p_Supported_Printers.php) поддерживаются [gutenprint](https://www.archlinux.org/packages/?name=gutenprint). Некоторые из принтеров Canon LBP, iR и MF используют драйвер, поддерживающий протоколы UFR II/UFR II LT/LIPSLX, который доступен как [cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/) или [cndrvcups-lb-bin](https://aur.archlinux.org/packages/cndrvcups-lb-bin/). Другие используют драйверы [#CARPS](#CARPS), [#cnijfilter](#cnijfilter) ([cnijfilter2](/index.php/AUR "AUR") / [cnijfilter2-bin](/index.php/AUR "AUR")) или [Canon CAPT](/index.php/Canon_CAPT "Canon CAPT").

| Принтер | Драйвер/фильтр | Примечание |
| iP4300 | [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) | Или используйте драйвер [TurboPrint](http://www.turboprint.info/). |
| LBP810 | [Canon CAPT](/index.php/Canon_CAPT "Canon CAPT") |
| LBP1120 |
| LBP1210 |
| LBP2900 |
| LBP3000 |
| LBP3010 |
| LBP3018 |
| LBP3050 |
| LBP3100 |
| LBP3108 |
| LBP3150 |
| LBP3200 |
| LBP3210 |
| LBP3250 |
| LBP3300 |
| LBP3310 |
| LBP3500 |
| LBP5000 |
| LBP5050 series |
| LBP5100 |
| LBP5300 |
| LBP6000 |
| LBP6018 |
| LBP6020 |
| LBP6200 |
| LBP6300 |
| LBP6300n |
| LBP6310dn |
| LBP7010C |
| LBP7018C |
| LBP7200Cdn (сетевой режим) |
| LBP7200C series |
| LBP7210Cdn |
| LBP9100C |
| MF635Cx | [cndrvcups-lb-bin](https://aur.archlinux.org/packages/cndrvcups-lb-bin/) |
| MF4720w |
| MG4200 series | [cnijfilter-mg4200](https://aur.archlinux.org/packages/cnijfilter-mg4200/) | Избегайте добавления принтера через [веб интерфейс](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Веб_интерфейс "CUPS (Русский)"), т.к. он не найдет файл PPD. |
| MX490 | [cnijfilter2](https://aur.archlinux.org/packages/cnijfilter2/)
[cnijfilter2-bin](https://aur.archlinux.org/packages/cnijfilter2-bin/) |
| MX492 |
| TS8050 | Без [cnijfilter2](https://aur.archlinux.org/packages/cnijfilter2/) печать завершится ошибкой фильтра или вы можете получить "рендеринг завершен", а принтер ничего не напечатает |
| TS9020 | [canon-ts9020](https://aur.archlinux.org/packages/canon-ts9020/) |
| Принтер | Драйвер/фильтр | Примечание |

Некоторые принтеры Canon будут использовать аналогичную настройку для iP4500, поэтому рассмотрите возможность изменения пакета [cnijfilter-ip4500](https://aur.archlinux.org/packages/cnijfilter-ip4500/) для других аналогичных принтеров.

### CARPS

Некоторые из принтеров Canon используют проприетарный драйвер Canon Advanced Raster Printing System (CARPS). [Rainbow Software](http://www.rainbow-software.org/2014/01/23/cups-driver-for-canon-carps-printers/) удалось перепроектировать формат данных CARPS и успешно создать драйвер CUPS CARPS, который доступен как [carps-cups](https://aur.archlinux.org/packages/carps-cups/). На странице [GitHub](https://github.com/ondrej-zary/carps-cups) проекта представлен список поддерживающих принтеров.

### USB через IP (BJNP)

Некоторые принтеры Canon используют проприетарный протокол USB по протоколу IP BJNP для связи по сети. Для этого есть бэкэнд CUPS, который доступен как [cups-bjnp](https://aur.archlinux.org/packages/cups-bjnp/).

### cnijfilter

Некоторые принтеры используют поддержку драйверами cnijfilter протокола `cnijnet`. Чтобы выяснить [URI принтера](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#URI_принтера "CUPS (Русский)") выполните

```
$ cnijnetprn --search auto

```

После используйте `cnijnet:/` URI из вывода, например: `cnijnet:/18-0C-AC-C6-1D-EE`.

## Dell

| Принтер | Драйвер/фильтр | Примечание |
| 1250C | [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/) | Смотрите [http://cybercom.net/~dcoffin/hbpl](http://cybercom.net/~dcoffin/hbpl), патч был объединен в восходящий поток. Принтер также работает с драйвером [Xerox Phaser 6000B](#Phaser_6000B). |
| C1660NW | [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/) | Принтер также работает с [Драйвером Xerox Phaser 6000B](#Phaser_6000B). |
| E515,

E515dw

 | Установите [драйвер Dell](http://downloads.dell.com/FOLDER03040853M/1/Printer_E515dw_Driver_Dell_A00_LINUX.zip). | Должны быть установлены как *e515dwcupswrapper-3.2.0-1.i386.deb*, так и *e515dwlpr-3.2.0-1.i386.deb*. Вы можете написать [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)"), используя [debtap](https://aur.archlinux.org/packages/debtap/), или использовать [dpkg](https://aur.archlinux.org/packages/dpkg/) (использование dpkg не рекомендуется, так как файлы не будут управляться с помощью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")). Драйвер работает как на платформах x86_64, так и на i386, но может потребоваться [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)"). |
| S1130n | [dell-unified-printer-driver](https://aur.archlinux.org/packages/dell-unified-printer-driver/) | Драйвер конфликтует с samsung-unified-driver-printer (оба создают rastertospl и libscmssc.so) |
| 1130 |
| 1133 |
| 1135n |
| 1815 |
| 2145cn |
| 2335dn |
| 2355dn |
| 5330 |
| B1160 |
| B1160w |
| B1165nfw |
| B1260dn |
| B1265dfw |
| B1265dnf |
| B2365dnf |
| Принтер | Драйвер/фильтр | Примечание |

## Epson

[epson-inkjet-printer-escpr](https://www.archlinux.org/packages/?name=epson-inkjet-printer-escpr) и [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) - это набор драйверов для струйных принтеров Epson Inkjet (ESC/P-R) для Linux..

| Принтер | Драйвер/фильтр | Примечание |
| AcuLaser CX11(NF) | [epson-alcx11-filter](https://aur.archlinux.org/packages/epson-alcx11-filter/) |
| AcuLaser C900 | Этот принтер использует драйвер Epson с URI устройства '**usb://EPSON/AL-C900'**, и для его запуска может понадобиться служба pipsplus. |
| EP-50V | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| EP-879A |
| EP-880A |
| ET-2700 | [epson-inkjet-printer-escpr](https://www.archlinux.org/packages/?name=epson-inkjet-printer-escpr) |
| ET-2750 |
| ET-3700 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| ET-3750 |
| ET-4750 |
| EW-M571T | [epson-inkjet-printer-escpr](https://www.archlinux.org/packages/?name=epson-inkjet-printer-escpr) |
| EW-M670FT | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| L380 | [epson-inkjet-printer-201601w](https://aur.archlinux.org/packages/epson-inkjet-printer-201601w/) |
| L382 |
| L4150 | [epson-inkjet-printer-escpr](https://www.archlinux.org/packages/?name=epson-inkjet-printer-escpr) |
| L4160 |
| L6160 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| L6170 |
| L6190 |
| LP-S5000 | Этот принтер требует [специализированный драйвер от Avasys](#Avasys). |
| PM-520 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| PX-M5080F |
| PX-M5081F |
| PX-M680F |
| PX-M7070FX |
| PX-M780F |
| PX-M781F |
| PX-M884F |
| PX-S5080 |
| PX-S7070X |
| PX-S884 |
| TX125 | [epson-inkjet-printer-n10-nx127](https://aur.archlinux.org/packages/epson-inkjet-printer-n10-nx127/) |
| WF-3720 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| WF-4720 |
| WF-4730 |
| WF-4740 |
| WF-7210 |
| WF-7710 |
| WF-7720 |
| WF-C869R |
| XP-446 | [epson-inkjet-printer-escpr](https://www.archlinux.org/packages/?name=epson-inkjet-printer-escpr) |
| XP-5100 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| XP-6000 |
| XP-8500 |
| XP-15000 |
| Принтер | Драйвер/фильтр | Примечание |

### Утилиты

#### escputil

escputil является частью пакета [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) и выполняет некоторые служебные функции на принтерах Epson, таких как очистка сопел.

#### mtink

Это монитор состояния принтера, который позволяет получить оставшееся количество чернил, распечатать тестовые шаблоны, сбросить принтер и очистить сопло. Он использует интуитивно понятный графический интерфейс пользователя.

#### Stylus-toolbox

Это графический интерфейс с использованием драйверов escputil и cups. Он поддерживает почти все USB-принтеры Epson и отображает количество чернил, может очищать и выравнивать печатающие головки и печатать тестовые образцы.

### Специализированные драйверы

#### Avasys

**Важно:** Этот раздел включает установку пакетов без [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). В идеале эти направления должны быть автоматизированы с помощью [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)").

"Исходный" код драйвера доступен на [веб-сайте avasys](http://www.avasys.jp) с японским языком. Он содержит 32-битный двоичный код, который вызовет проблему в 64-битной системе.

*   [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [psutils](https://www.archlinux.org/packages/?name=psutils), [bc](https://www.archlinux.org/packages/?name=bc), [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5) ([lib32-libstdc++5](https://aur.archlinux.org/packages/lib32-libstdc%2B%2B5/) для 64-битной).

*   Загрузите исходный код драйвера.
*   Скомпилируйте и установите драйвер.

```
$ ./configure --prefix=/usr
$ make
# make install

```

Если у вас есть проблемы в 64-битной системе, могут потребоваться некоторые другие библиотеки lib32\. Пожалуйста, исправьте эту страницу, если это так.

## HP

Смотрите также [CUPS/Решение проблем#Проблемы с HP](/index.php/CUPS/%D0%A0%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC#Проблемы_с_HP "CUPS/Решение проблем").

Большинство принтеров HP будут работать с [hplip](https://www.archlinux.org/packages/?name=hplip), но некоторые - при использование [hpoj](https://aur.archlinux.org/packages/hpoj/). Также некоторые лазерные принтеры поддерживаются [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/).

| Принтер | Драйвер/фильтр | Примечание |
| DeskJet 710C | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 712C |
| DeskJet 720C |
| DeskJet 722C |
| DeskJet 820se |
| DeskJet 820Cxi |
| DeskJet 1000Cse |
| DeskJet 1000Cxi |
| LaserJet P1606dn | [hplip](https://www.archlinux.org/packages/?name=hplip) + [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) | или [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/), или [AirPrint](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#CUPS "CUPS (Русский)"). |
| LaserJet Pro MFP M126nw | [hplip](https://www.archlinux.org/packages/?name=hplip) + [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) |
| Photosmart 2575 | [hplip](https://www.archlinux.org/packages/?name=hplip) | Или используйте драйвер hpijs с [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)"). |
| Принтер | Драйвер/фильтр | Примечание |

### HPLIP

**Примечание:** Начиная с hplip v3.17.11 hpijs больше не доступен. Если у вас есть принтеры, использующие hpijs, они не смогут работать. Вы должны перенастроить их и выбрать новый драйвер hpcups вместо hpijs.

[hplip](https://www.archlinux.org/packages/?name=hplip) предоставляет драйверы для принтеров HP DeskJet, OfficeJet, Photosmart, Business Inkjet и некоторых принтеров LaserJet, а также предоставляет простой в использовании инструмент настройки. Смотрите список поддерживаемых принтеров [здесь](https://developers.hp.com/hp-linux-imaging-and-printing/supported_devices/index).

Чтобы запустить средство настройки с графическим интерфейсом пользователя:

```
# hp-setup -u

```

Чтобы запустить средство настройки с интерфейсом командной строки:

```
# hp-setup -i

```

Чтобы настроить непосредственно конфигурацию подключенного к сети принтера HP:

```
# hp-setup -i *<ip address>*

```

Чтобы запустить systray spool manager:

```
$ hp-systray

```

Чтобы создать URI для заданного IP-адреса:

```
# hp-makeuri *<ip address>*

```

Файлы PPD находятся в `/usr/share/ppd/HP/`.

Если ваш принтер [перечислен как требующий бинарный плагин](https://developers.hp.com/hp-linux-imaging-and-printing/binary_plugin.html), установите пакет [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Если требуется бинарный плагин [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/), вам нужно [запустить](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D1%8C "Запустить") службу `org.cups.cupsd.service` перед распознаванием PPD [hplip](https://www.archlinux.org/packages/?name=hplip).

**Примечание:**

[hplip](https://www.archlinux.org/packages/?name=hplip) зависит от [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine), который запрещает появление списка драйверов при добавлении принтера в CUPS через веб-интерфейс (следующая ошибка: "Не удается получить список драйверов принтера"). Возможные обходные пути:

*   **Либо:** Установите первым [hplip](https://www.archlinux.org/packages/?name=hplip), затем извлеките файл PPD, соответствующий вашему принтеру, из `/usr/share/ppd/HP/`. Далее удалите [hplip](https://www.archlinux.org/packages/?name=hplip) полностью, а также любые ненужные зависимости. Наконец, установите принтер вручную через веб-интерфейс CUPS, выбрав файл PPD, который вы извлекли, а затем переустановите [hplip](https://www.archlinux.org/packages/?name=hplip). После перезагрузки у вас должен быть полностью работающий принтер.
*   **Или:** Удалите [hplip](https://www.archlinux.org/packages/?name=hplip), [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) и [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) вместе с любыми ненужными зависимостями. Переустановите [hplip](https://www.archlinux.org/packages/?name=hplip) и перезапустите CUPS. Установите ваш принтер с помощью веб-интерфейса CUPS, который теперь сможет автоматически найти драйверы. Перезагрузка не требуется.

### foo2zjs

[foo2zjs](http://foo2zjs.rkkda.com/) поддерживает некоторые принтеры HP LaserJet. По состоянию на июнь 2018 года пакет hplip конфликтует с пакетом [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/), как описано на [форуме в этом посте](https://bbs.archlinux.org/viewtopic.php?pid=1662809) и [FS#58815](https://bugs.archlinux.org/task/58815).

## Konica Minolta

| Принтер | Драйвер/фильтр | Примечание |
| Minolta Magicolor 1600W | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") |
| Minolta Magicolor 1680MF |
| Minolta Magicolor 1690MF |
| Minolta Magicolor 2480MF |
| Minolta Magicolor 2490MF |
| Minolta Magicolor 2530DL |
| Minolta Magicolor 4690MF |
| Принтер | Драйвер/фильтр | Примечание |

### foo2zjs

Упомянутый выше [#foo2zjs](#foo2zjs) для некоторых принтеров HP также поддерживает некоторые принтеры Minolta.

## Lexmark

### Утилиты

Lexmark предоставляет утилиту с именем lexijtools с драйверами.

### Специализированный драйверы

Lexmark предоставляет драйверы Linux для всего своего оборудования. Требуются следующие пакеты:

*   [cups](https://www.archlinux.org/packages/?name=cups)
*   [sane](https://www.archlinux.org/packages/?name=sane)
*   [ncurses](https://www.archlinux.org/packages/?name=ncurses)
*   [libusb](https://www.archlinux.org/packages/?name=libusb)
*   [libxext](https://www.archlinux.org/packages/?name=libxext)
*   [libxtst](https://www.archlinux.org/packages/?name=libxtst)
*   [libxi](https://www.archlinux.org/packages/?name=libxi)
*   [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5)
*   [krb5](https://www.archlinux.org/packages/?name=krb5)
*   [lua](https://www.archlinux.org/packages/?name=lua) (для установщика)
*   [Java](/index.php/Java_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Java (Русский)") (для установщика и некоторых инструментов Lexmark)

Драйверы необходимо [загрузить](http://support.lexmark.com/index?page=driversdownloads) с веб-сайта Lexmark. Предпочтительно создать пакет (смотрите [Создание пакетов](/index.php/%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5_%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2 "Создание пакетов")) и установить его. Вот [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)"), который все еще нуждается в доработке, но дает представление о том, что нужно сделать.

 `PKGBUILD` 
```
# Contributor: Todd Partridge (Gen2ly) toddrpartridge (at) yahoo

pkgname=cups-lexmark-Z2300-2600
pkgver=1
pkgrel=1
pkgdesc="Lexmark Z2300 and 2600 Series printer driver for cups"
arch=('i686')
url="http://www.lexmark.com/"
license=('custom')
depends=('cups' 'glibc' 'ncurses' 'libusb' 'libxext' 'libxtst' 'libxi' 'libstdc++5' 'krb5' 'lua' 'java-runtime')
conflicts=('z600' 'cjlz35le-cups' 'cups-lexmark-700')
source=(lexmark-inkjet-08-driver-1.0-1.i386.tar.gz.sh)
md5sums=(3c37eb87e3dad4853bf29344f9695134)

package() {
  # Extract installer
  sh lexmark-inkjet-08-driver-1.0-1.i386.tar.gz.sh --target Installer-Files
  cd Installer-Files
  mkdir Driver
  tar xvvf instarchive_all --lzma -C Driver/
  cd Driver
  tar xv lexmark-inkjet-08-driver-1.0-1.i386.tar.gz -C $pkgdir
}

```

Имейте в виду, что вы можете использовать автоматический установщик, но при этом оставленные изменения нельзя устранить через [Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). PPD будет установлен в `/usr/local/lexmark/lxk08/etc/` или аналогично, в зависимости от модели принтера.

## Oki

| Принтер | Драйвер/фильтр | Примечание |
| C110 | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") |
| MC561 | [foomatic-db-nonfree](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") |
| Принтер | Драйвер/фильтр | Примечание |

## Ricoh

Если ваше устройство черно-белое, установите [openprinting-ppds-pxlmono-ricoh](https://aur.archlinux.org/packages/openprinting-ppds-pxlmono-ricoh/), а если цветное - [openprinting-ppds-pxlcolor-ricoh](https://aur.archlinux.org/packages/openprinting-ppds-pxlcolor-ricoh/). Обратите внимание, что копировальные устройства Ricoh иногда называются Savin, Gestetner, Lanier, Rex-Rotary, Nashuatec и/или IKON. Итак, если у вас есть устройство с одним из этих брендов, оно также поддерживается этими драйверами.

*   [Список поддерживаемых черно-белых моделей](https://www.openprinting.org/driver/pxlmono-Ricoh)
*   [Список поддерживаемых цветных моделей](https://www.openprinting.org/driver/pxlcolor-Ricoh)

Для принтеров виндоус (серии Ricoh SP100 и SP200) попробуйте [ricoh-sp100-git](https://aur.archlinux.org/packages/ricoh-sp100-git/).

| Принтер | Драйвер/фильтр | Примечание |
| SP 112 | [ricoh-sp100-git](https://aur.archlinux.org/packages/ricoh-sp100-git/) |
| SP 201n | [ricoh-sp100-git](https://aur.archlinux.org/packages/ricoh-sp100-git/) |
| 213W | *Generic PCL Laser* | Получите код WPS, удерживая кнопку Wi-Fi в течение 2 секунд, а затем нажмите кнопку выключения/включения. |
| Принтер | Драйвер/фильтр | Примечание |

## Samsung

Для принтеров, требующим драйверы *cnijfilter*, найдите правильный драйвер [в AUR](https://aur.archlinux.org/packages.php?K=cnijfilter)

| Принтер | Драйвер/фильтр | Примечание |
| ML-2010 | [splix](https://www.archlinux.org/packages/?name=splix) |
| SCX-4200 | [splix](https://www.archlinux.org/packages/?name=splix) |
| Новые принтеры? | [samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) |
| Принтер | Драйвер/фильтр | Примечание |

## Xerox или FujiXerox

| Принтер | Драйвер/фильтр | Примечание |
| DocuPrint 203A | [hplip](https://www.archlinux.org/packages/?name=hplip) | Используйте драйвер **DocuPrint P8e(hpijs)** или драйвер Brother на веб-сайте FujiXerox (смотрите [#Brother](#Brother) для получения дополнительной информации о том, как установить специализированные драйверы Brother). |
| Phaser 3100MFP | Установите драйвер Xerox | Подробнее смотрите [#Phaser 3100MFP](#Phaser_3100MFP). |
| Phaser 6115MFP | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") |
| Phaser 6121MFP | [foomatic](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic "CUPS (Русский)") |
| Принтер | Драйвер/фильтр | Примечание |

### Специализированные драйверы

#### Phaser 3100MFP

**Важно:** Этот раздел включает в себя установку пакетов без [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). В идеале эти направления должны быть автоматизированы с помощью [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)").

После того, как вы загрузили драйверы, выполните установку драйвера и примите лицензию:

```
# cd printer
# ./XeroxPhaser3100.install

```

Обратите внимание, что драйвер 32-битный, поэтому в системе x86_64 потребуется некоторые 32-битные библиотеки.

Для сканера создайте каталог /etc/sane.d, если он еще не существует, потому что это необходимо установщику:

```
# mkdir -p /etc/sane.d

```

Теперь установите драйвер:

```
# cd scanner/
# ./XeroxPhaser3100sc.install

```

Опять же, при установке x86_64 потребуются 32-битные библиотеки.

#### Phaser 6000B

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [xerox-phaser-6010](https://github.com/aur-archive/xerox-phaser-6010) (архивированный из AUR). Драйвер может потребовать более ранние версии [nettle](https://www.archlinux.org/packages/?name=nettle) и [gnutls](https://www.archlinux.org/packages/?name=gnutls) поскольку двоичный blob связан с более старыми версиями разделяемых библиотек, предоставляемых этими пакетами. Самые старые хорошо известные версии `nettle-2.7.1-1` и `gnutls-3.3.13-1`.

#### Phaser 6125N

**Важно:** Этот раздел включает в себя установку пакетов без [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). В идеале эти направления должны быть автоматизированы с помощью [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)").

FujiXerox не поддерживает Linux на этой модели. Есть старый [rpm-пакет](http://onlinesupport.fujixerox.com/tiles/common/hc_drivers_download.jsp?system=%27Linux%27&shortdesc=null&xcrealpath=http://www.fujixeroxprinters.com/downloads/uploaded/dpc525a_linux_.0.0.tar_81c2.zip), но, похоже, он не работает.

Известно, что слегка адаптированный [специализированный драйвер](https://rickvanderzwet.nl/trac/personal/wiki/XeroxPhaser6125N) работает из коробки.

Чтобы установить tarball, запустите

```
# tar -C / --keep-newer-files -xvzf cups-xerox-phaser-6125n-1.0.0.tar.gz

```