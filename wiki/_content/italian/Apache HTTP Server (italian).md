[LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle) costituisce una combinazione comune di vari software utilizzati in molti server web: **L**inux, **A**pache, **M**ySQL, e **P**HP. Questo documento descrive i passi necessari per configurare un [Apache HTTP Server](http://httpd.apache.org) su un sistema Arch Linux. Spiega inoltre come installare [PHP](/index.php/PHP "PHP") e [MySQL](/index.php/MySQL "MySQL") ed integrarli con il server Apache.

Avendo bisogno di solo un server web per sviluppo e test, [XAMPP](/index.php/XAMPP "XAMPP") potrebbe essere la scelta migliore, oltre che la più facile.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Apache](#Apache)
        *   [2.1.1 Cartelle utente](#Cartelle_utente)
        *   [2.1.2 SSL](#SSL)
        *   [2.1.3 Host virtuali](#Host_virtuali)
        *   [2.1.4 Opzioni avanzate](#Opzioni_avanzate)
    *   [2.2 PHP](#PHP)
        *   [2.2.1 Opzioni avanzate](#Opzioni_avanzate_2)
        *   [2.2.2 Utilizzare php7 con apache2-mpm-worker e mod_fcgid](#Utilizzare_php7_con_apache2-mpm-worker_e_mod_fcgid)
        *   [2.2.3 MySQL/MariaDB](#MySQL.2FMariaDB)
    *   [2.3 MySQL](#MySQL)
*   [3 Vedere anche](#Vedere_anche)
*   [4 Collegamenti esterni](#Collegamenti_esterni)

## Installazione

```
# pacman -S apache php php-apache mysql

```

Questo documento presuppone che verranno installati Apache, PHP e MySQL insieme. Se lo si desidera tuttavia, è possibile installare Apache, PHP e MySQL separatamente e fare riferimento alle relative sezioni in seguito.

**Note:** Nuovi utente e gruppo di default: Invece del gruppo "nobody", apache viene eseguito ora come utente/gruppo "http". È preferibile modificare il file httpd.conf in base a questo cambiamento, anche se è possibile eseguire httpd comunque.

## Configurazione

### Apache

Per motivi di sicurezza, non appena Apache viene avviato dall'utente root (direttamente o tramite script di avvio) passa alla UID/GID specificata in `/etc/httpd/conf/httpd.conf`

*   Verificare l'esistenza degli utenti http, cercando *http* nell'output del seguente comando:

```
 # grep http /etc/passwd

```

*   Creare l'utente http in caso non esista già:

```
 # useradd -d /srv/http -r -s /bin/false -U http

```

	Questo crea l'utente http con la home directory `/srv/http/`, come un account di sistema (-r), con una shell fasulla (-s `/bin/false`) e crea un gruppo con lo stesso nome (-U).

*   Aggiungere questa riga in `/etc/hosts` (se il file non esiste, crearlo):

```
 127.0.0.1 localhost.localdomain localhost

```

	Se si preferisce un hostname differente, posizionarlo alla fine:

```
 127.0.0.1 localhost.localdomain localhost myhostname

```

*   Editare `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`: Se nel primo passo è stato messo un hostname, la variabile `HOSTNAME` deve avere lo stesso valore; altrimenti, usare `"localhost"`:

```
 #
 # Networking
 #
 HOSTNAME="localhost"

```

*   Assicurarsi che l'hostname sia presente in `/etc/hosts` o apache non potrà essere avviato. In alternativa, è possibile editare `/etc/httpd/conf/httpd.conf` e commentare il modulo seguente:

```
 LoadModule unique_id_module        modules/mod_unique_id.so

```

*   Personalizzare ora la propria configurazione: cambiare per lo meno `httpd.conf` e `extra/httpd-default.conf` secondo le proprie esigenze. Per ragioni di sicurezza, sarebbe preferibile modificare **ServerTokens Full** a **ServerTokens Prod** e **ServerSignature On** a **ServerSignature Off** in `extra/httpd-default.conf`.

*   Per avviare il server HTTP lanciare da terminale  :

```
 # /etc/rc.d/httpd start

```

	Apache ora dovrebbe essere attivo. Testarlo visitando [http://localhost/](http://localhost/) da un browser. Si dovrebbe vedere una semplice pagina di test di Apache. In caso di errore 403, decommentare le righe seguenti in `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/httpd-userdir.conf

```

*   Per avviare Apache automaticamente al boot, editare `/etc/rc.conf` e aggiungere il demone **httpd**:

```
 DAEMONS=(... **httpd** ...)

```

#### Cartelle utente

*   Se non si desidera che le cartelle dell'utente siano disponibili sul web (ad es. `~/public_html` sulla macchina usata per l'accesso come [http://localhost/~user/](http://localhost/~user/)), commentare la seguente riga in `/etc/httpd/conf/httpd.conf` dal momento che sono attivate di default:

```
 Include conf/extra/httpd-userdir.conf

```

*   È necessario che le autorizzazioni della home directory siano impostate correttamente in modo che Apache possa collegarvisi. La home directory e `~/public_html/` devono essere eseguibili per gli altri ("resto del mondo"). Questo sembra essere accettabile:

```
 $ chmod o+x ~
 $ chmod o+x ~/public_html

```

*   Il modo più sicuro per condividere la propria cartella home con apache è quello di aggiungere **http user** nel gruppo al quale appartiene la cartella home. Per esempio, se la cartella home e le altre sotto-cartelle appartengono al gruppo **piter**, tutto quello che si deve fare è:

```
 $ usermod -aG piter http

```

*   Naturalmente bisogna assegnare i permessi di *lettura* ed *esecuzione* a `~/`, `~/public_html`, e tutte le altre sotto-cartelle in `~/public_html` ai membri del gruppo (gruppo **piter** in questo caso). Provare qualcosa di simile (**modificando i comandi secondo necessità**):

```
 $ chmod g+xr-w /home/*yourusername*
 $ chmod -R g+xr-w /home/*yourusername*/public_html

```

**Note:** In questo modo non c'è bisogno di dare accesso alla propria cartella ad ogni singolo utente per dare accesso al **http user**. Solo l' **http user** ed altri potenziali utenti del gruppo **piter** avranno accesso alla propria cartella home.

E poi

```
 $ /etc/rc.d/httpd restart

```

per riavviare apache.

#### SSL

Creare certificato autofirmato (è possibile modificare le dimensioni della chiave e giorni di validità)

```
# cd /etc/httpd/conf
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:4096 -out server.key
# openssl req -new -key server.key -out server.csr
# cp server.key server.key.org
# openssl rsa -in server.key.org -out server.key
# openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

```

In `/etc/httpd/conf/httpd.conf` decommentare la riga

```
Include conf/extra/httpd-ssl.conf

```

Riavviare apache

```
# /etc/rc.d/httpd restart

```

#### Host virtuali

Se si desidera più di un host, assicurarsi di avere

```
# Virtual hosts
Include conf/extra/httpd-vhosts.conf

```

in `/etc/httpd/conf/httpd.conf`.

In `/etc/httpd/conf/extra/httpd-vhosts.conf` impostare gli host virtuali secondo l'esempio:

```
NameVirtualHost *:80

#this first virtualhost enables: http://127.0.0.1, or: http://localhost, 
#to still go to /srv/http/*index.html(otherwise it will 404_error).
#the reason for this: once you tell httpd.conf to include extra/httpd-vhosts.conf, 
#ALL vhosts are handled in httpd-vhosts.conf(including the default one),
# E.G. the default virtualhost in httpd.conf is not used and must be included here, 
#otherwise, only domainname1.dom & domainname2.dom will be accessible
#from your web browser and NOT http://127.0.0.1, or: http://localhost, etc.
#

<VirtualHost *:80>
    DocumentRoot "/srv/http"
    ServerAdmin root@localhost
    ErrorLog "/var/log/httpd/127.0.0.1-error_log"
    CustomLog "/var/log/httpd/127.0.0.1-access_log" common
    <Directory /srv/http/>
		    DirectoryIndex index.htm index.html
		    AddHandler cgi-script .cgi .pl
		    Options ExecCGI Indexes FollowSymLinks MultiViews +Includes
		    AllowOverride None
		    Order allow,deny
		    allow from all
	</Directory>
</VirtualHost>

<VirtualHost *:80>
    ServerAdmin your@domainname1.dom
    DocumentRoot "/home/username/yoursites/domainname1.dom/www"
    ServerName domainname1.dom
    ServerAlias domainname1.dom
    <Directory /home/username/yoursites/domainname1.dom/www/>
		    DirectoryIndex index.htm index.html
		    AddHandler cgi-script .cgi .pl
		    Options ExecCGI Indexes FollowSymLinks MultiViews +Includes
		    AllowOverride None
		    Order allow,deny
		    allow from all
	</Directory>
</VirtualHost>

<VirtualHost *:80>
    ServerAdmin your@domainname2.dom
    DocumentRoot "/home/username/yoursites/domainname2.dom/www"
    ServerName domainname2.dom
    ServerAlias domainname2.dom
    <Directory /home/username/yoursites/domainname2.dom/www/>
		    DirectoryIndex index.htm index.html
		    AddHandler cgi-script .cgi .pl
		    Options ExecCGI Indexes FollowSymLinks MultiViews +Includes
		    AllowOverride None
		    Order allow,deny
		    allow from all
	</Directory>
</VirtualHost>

```

Aggiungere i nomi dei propri host virtuali al file `/etc/hosts` (NON è necessario se questi domini sono già vincolati, ma comunque non fa male):

```
127.0.0.1	domainname1.dom
127.0.0.1	domainname2.dom
```

Riavviare Apache:

 `sudo /etc/rc.d/httpd restart` 

Se si impostano gli host virtuali nella propria cartella utente, a volte possono interferire con le impostazioni delle "Userdir" di Apache. Per evitare problemi disabilitare le "Userdir" decommentandole:

```
# User home directories
#Include conf/extra/httpd-userdir.conf
```

Come già detto sopra, fare attenzione, dal momento che si dispone delle autorizzazioni appropriate:

 `sudo chmod 0775 /home/yourusername/` 

Se si dispone di una quantità enorme di host virtuali, sarebbe comodo poterli disabilitare e abilitare facilmente. Si consiglia quindi di creare un file di configurazione per ogni host virtuale e memorizzarli tutti in una cartella, ad es: `/etc/httpd/conf/vhosts`. Per prima cosa creare la cartella:

 `sudo mkdir /etc/httpd/conf/vhosts` 

Quindi inserire i singoli file di configurazione all'interno:

```
sudoedit /etc/httpd/conf/vhosts/domainname1.dom
sudoedit /etc/httpd/conf/vhosts/domainname2.dom
...
```

Come ultimo passo, includere le singole configurazioni a `/etc/httpd/conf/httpd.conf`:

```
#Enabled Vhosts:
Include conf/vhosts/domainname1.dom
#Include conf/vhosts/domainname1.dom
```

È possibile attivare e disattivare ogni singolo host virtuale commentandolo o decommentandolo.

#### Opzioni avanzate

Si potrebbe essere interessati a queste opzioni in `/etc/httpd/conf/httpd.conf`:

```
# Listen 80

```

Questa è la porta su cui Apache rimarrà in ascolto. Per l'accesso a Internet con un router, sarà necessario impostare correttamente la porta.

Se Apache è stato impostato per lo sviluppo locale è possibile che sia accessibile solo dal proprio computer. Modificare quindi questa riga:

```
# Listen 127.0.0.1:80

```

Questo è l'indirizzo email dell'amministratore che può essere trovato nelle pagine di errore:

```
# ServerAdmin sample@sample.com

```

Questa è la directory dove si dovrebbero mettere le proprie pagine web:

```
# DocumentRoot "/srv/http"

```

Modificarla se lo si desidera, ma non dimenticare di cambiare anche la

```
<Directory "/srv/http">

```

compatibilmente con le modifiche apportate a DocumentRoot, o probabilmente si riscontrerà l'errore 403 (mancanza di privilegi) quando si tenta di accedere al nuovo documento root. Non dimenticare di cambiare l'opzione "Deny" da tutte le righe, altrimenti si otterrà nuovamente l'errore 403.

```
# AllowOverride None

```

Questa direttiva nella sezione <Directory> è la causa per cui apache ignora completamente i file `.htaccess`. Se si intende utilizzare la modalità "rewrite" o altre impostazioni nei file `.htaccess`, è possibile consentire che le direttive dichiarate in quel file possano sovrascrivere la configurazione del server. Per maggiori informazioni fare riferimento a [http://httpd.apache.org/docs/current/mod/core.html#allowoverride](http://httpd.apache.org/docs/current/mod/core.html#allowoverride)

**Note:** In caso di problemi con la configurazione si può fare in modo che apache controlli la configurazione con: `apachectl configtest`

### PHP

Per installare [PHP](/index.php/PHP "PHP") sono necessari i package [php](https://www.archlinux.org/packages/?name=php) e [php-apache](https://www.archlinux.org/packages/?name=php-apache).

In `/etc/httpd/conf/httpd.conf`, commentare la riga:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so

```

E decommenta:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

**Nota:** Questa operazione è necessaria perché il package `libphp7.so` incluso in [php-apache](https://www.archlinux.org/packages/?name=php-apache) non funziona con `mod_mpm_event` e richiede `mod_mpm_prefork`. ([FS#39218](https://bugs.archlinux.org/task/39218))

Altrimenti si riceverà il seguente errore:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
httpd.service: control process exited, code=exited status=1
```
Come alternativa, è possibile usare `mod_proxy_fcgi`.

Per abilitare PHP è necessario editare il file `/etc/httpd/conf/httpd.conf`:

*   Aggiungere le seguenti righe al termina della lista `LoadModule`:

```
LoadModule php7_module modules/libphp7.so
AddHandler php7-script php

```

	Inserire la riga seguente alla fine della lista `Include`:

```
Include conf/extra/php7_module.conf

```

Riavviare `httpd.service` tramite [systemd](/index.php/Systemd#Using_units "Systemd").

**Nota:** Se non è visibile `libphp7.so` nella cartella dei moduli Apache (`/etc/httpd/modules`), si può aver dimenticato di installare il pacchetto *php-apache*.

Per testare se PHP è stato configurato corretamente, creare il file `test.php` nella `DocumentRoot` di Apache (e.g. `/srv/http/` or `~/public_html`) con il seguente contenuto:

```
<?php phpinfo(); ?>

```

Per verificarne la corretta esecuzione, ragiungi: [http://localhost/test.php](http://localhost/test.php) o [http://localhost/~myname/test.php](http://localhost/~myname/test.php)

Per configurazioni avanzate di PHP fare riferimento a [PHP](/index.php/PHP "PHP").

#### Opzioni avanzate

*   Aggiungere, se può risultare comodo, un gestore di file per. phtml in `/etc/httpd/conf/extra/php7_module.conf`:

```
 DirectoryIndex index.php index.phtml index.html

```

*   Se si desidera il modulo libGD, installare il pacchetto php-gd e decommentare la seguente riga in `/etc/php/php.ini`:

**Note:** php-gd richiede libpng, libjpeg, e freetype2

```
 ;extension=gd.so

```

a

```
 extension=gd.so

```

	Prestare attenzione a quale estensione si vuole decommentare: spesso è presente un qualche commento esplicativo prima della riga stessa.

*   Se si desidera visualizzare gli errori di debug del codice php, modificare questa riga in `/etc/php/php.ini`:

```
 display_errors=Off

```

a

```
 display_errors=On

```

*   Se si desidera il modulo mcrypt, installare il pacchetto php-mcrypt e decommentare in `/etc/php/php.ini`:

```
 ;extension=mcrypt.so

```

a

```
 extension=mcrypt.so

```

**Warning:** In caso di questo tipo di errore:
```
[XXX Debug] PHP Notice: in file /index.php on line 86: date(): It is not safe to rely on the system'XXXX
[XXX Debug] PHP Notice: in file /index.php on line 86: getdate(): It is not safe to rely on the system's timezone settings.XXXX
```

modificare questa riga in `/etc/php/php.ini`

```
;date.timezone = 

```

a

```
date.timezone = Europe/Berlin

```

**Note:** Ulteriori informazioni riguardo [Time Zone in PHP](http://php.net/manual/en/datetime.configuration.php#ini.date.timezone)

riavviare httpd con

```
# /etc/rc.d/httpd restart

```

#### Utilizzare php7 con apache2-mpm-worker e mod_fcgid

Installare i package [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) e [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

```
# pacman -S mod_fcgid php-cgi

```

Creare la directory fcgid-bin e link simbolico per il wrapper PHP:

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

Creare il file `/etc/httpd/conf/extra/php-fcgid.conf` con il seguente contenuto:

 `/etc/httpd/conf/extra/php-fcgid.conf` 
```
# Required modules: fcgid_module

<IfModule fcgid_module>
    AddHandler php-fcgid .php
    AddType application/x-httpd-php .php
    Action php-fcgid /fcgid-bin/php-fcgid-wrapper
    ScriptAlias /fcgid-bin/ /srv/http/fcgid-bin/
    SocketPath /var/run/httpd/fcgidsock
    SharememPath /var/run/httpd/fcgid_shm
        # If you don't allow bigger requests many applications may fail (such as WordPress login)
        FcgidMaxRequestLen 536870912
        # Path to php.ini – defaults to /etc/phpX/cgi
        DefaultInitEnv PHPRC=/etc/php/
        # Number of PHP childs that will be launched. Leave undefined to let PHP decide.
        #DefaultInitEnv PHP_FCGI_CHILDREN 3
        # Maximum requests before a process is stopped and a new one is launched
        #DefaultInitEnv PHP_FCGI_MAX_REQUESTS 5000
    <Location /fcgid-bin/>
        SetHandler fcgid-script
        Options +ExecCGI
    </Location>
</IfModule>

```

Editare `/etc/httpd/conf/httpd.conf:` abilitando mod_actions.so

```
LoadModule actions_module modules/mod_actions.so

```

E aggiungengo le seguenti righe:

```
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/httpd-mpm.conf
Include conf/extra/php-fcgid.conf

```

**Nota:** Se sono state aggiunte le seguenti righe a `httpd.conf`, rimuoverle:
```
LoadModule php7_module modules/libphp7.so
Include conf/extra/php7_module.conf

```

Riavviare `httpd.service`.

#### MySQL/MariaDB

Seguire le istruzioni in [PHP#MySQL/MariaDB](/index.php/PHP#MySQL.2FMariaDB "PHP") e riavviare `httpd.service` per applicare i cambiamenti.

### MySQL

*   Configurare MySQL come descritto da [MySQL](/index.php/MySQL "MySQL").

*   Editare `/etc/php/php.ini` (reperibile in `/usr/etc` sui sistemi più datati) e decommentare la seguente riga (*Rimuovendo `;`*):

```
 ;extension=mysqli.so
 ;extension=mysql.so

```

	**Attenzione:** Alcuni utenti hanno segnalato errori di battitura su questa riga. Assicurarsi che legga `;extension=mysql.so` e non `;extension=msql.so`.

*   È possibile aggiungere utenti con meno privilegi per gli script web modificando le tabelle nel database `mysql`. Occorre riavviare MySQL per rendere effettive le modifiche. Ricordarsi di controllare la tabella `mysql/users`. Se c'è una seconda voce per root e il proprio hostname è sprovvisto di password, chiunque potrebbe ottenere l'accesso completo da tale host. Vedere la sezione successiva per questo tipo di problematiche.

*   Eseguire in un terminale:

```
 # /etc/rc.d/mysqld start

```

*   Potrebbe anche essere necessario riavviare Apache. Da terminale:

```
 # /etc/rc.d/httpd restart

```

*   MySQL dovrebbe essere in esecuzione ora. Impostare la password di root e testarlo eseguendo:

```
 # mysqladmin -u root password *password*
 # mysql -u root -p

```

	Digitare *exit* per uscire dalla riga di comando del client MySQL

*   Editare `/etc/rc.conf` (per avviare MySQL all'avvio):

```
 DAEMONS=(... **mysqld** ...)

```

Oppure aggiungere questa riga a `rc.local`:

```
 /etc/rc.d/mysqld start

```

*   Potrebbe anche essere necessario modificare `/etc/mysql/my.cnf` e decommentare `skip-networking` da così:

```
 skip-networking

```

a

```
 #skip-networking

```

**Tip:** Si consiglia di installare [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin"), [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench) o [adminer](/index.php/Adminer "Adminer") per lavorare con i database.

## Vedere anche

*   [MySQL](/index.php/MySQL "MySQL") - Articolo wiki per MySQL
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") - Interfaccia web per MySQL tipica degli ambienti LAMP
*   [Adminer](/index.php/Adminer "Adminer") - Un completo strumento di gestione dei database disponibile per MySQL, PostgreSQL, SQLite, MS SQL e Oracle
*   [XAMPP](/index.php/XAMPP "XAMPP") - Server-web autonomo che supporta PHP, Perl e MySQL

## Collegamenti esterni

*   [http://www.apache.org/](http://www.apache.org/)
*   [http://www.php.net/](http://www.php.net/)
*   [http://www.mysql.com/](http://www.mysql.com/)
*   [http://www.akadia.com/services/ssh_test_certificate.html](http://www.akadia.com/services/ssh_test_certificate.html)
*   [http://wiki.apache.org/httpd/CommonMisconfigurations](http://wiki.apache.org/httpd/CommonMisconfigurations)