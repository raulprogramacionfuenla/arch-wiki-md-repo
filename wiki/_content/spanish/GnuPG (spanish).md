Artículos relacionados

*   [pacman/Package signing (Español)](/index.php/Pacman/Package_signing_(Espa%C3%B1ol) "Pacman/Package signing (Español)")
*   [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)")

[GnuPG](http://www.gnupg.org) permite cifrar y firmar tus datos y comunicaciones, incluye un sistema versátil de gestión de claves, así como módulos de acceso para toda clase de directorios de claves públicas.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Variables de Entorno](#Variables_de_Entorno)
    *   [2.1 GNUPGHOME](#GNUPGHOME)
    *   [2.2 GPG_AGENT_INFO](#GPG_AGENT_INFO)
*   [3 Archivo de configuración](#Archivo_de_configuración)
*   [4 Gestión básica de claves](#Gestión_básica_de_claves)
    *   [4.1 Crear una clave](#Crear_una_clave)
    *   [4.2 Gestionar una clave](#Gestionar_una_clave)
    *   [4.3 Rotar subclaves](#Rotar_subclaves)
    *   [4.4 Importar una clave](#Importar_una_clave)
    *   [4.5 Listar claves](#Listar_claves)
*   [5 Cifrar y descifrar](#Cifrar_y_descifrar)
    *   [5.1 Asimétrico](#Asimétrico)
    *   [5.2 Simétrico](#Simétrico)
    *   [5.3 Cifrar una contraseña](#Cifrar_una_contraseña)
*   [6 Firmas](#Firmas)
    *   [6.1 Crear una firma](#Crear_una_firma)
        *   [6.1.1 Firmar un documento](#Firmar_un_documento)
        *   [6.1.2 Firma sencilla de un archivo o mensaje](#Firma_sencilla_de_un_archivo_o_mensaje)
        *   [6.1.3 Crear una firma independiente](#Crear_una_firma_independiente)
    *   [6.2 Verificación de firmas](#Verificación_de_firmas)
*   [7 gpg-agent](#gpg-agent)
    *   [7.1 Configuración](#Configuración)
    *   [7.2 Recargar el agente](#Recargar_el_agente)
    *   [7.3 pinentry](#pinentry)
    *   [7.4 Iniciar gpg-agent con el usuario systemd](#Iniciar_gpg-agent_con_el_usuario_systemd)
    *   [7.5 Frase de acceso desatendida](#Frase_de_acceso_desatendida)
    *   [7.6 Agente SSH](#Agente_SSH)
*   [8 Reuniones de firmado de claves](#Reuniones_de_firmado_de_claves)
    *   [8.1 caff](#caff)
*   [9 Smartcards](#Smartcards)
    *   [9.1 Instalaciones solo con GnuPG](#Instalaciones_solo_con_GnuPG)
    *   [9.2 GnuPG junto con OpenSC](#GnuPG_junto_con_OpenSC)
*   [10 Resolución de problemas](#Resolución_de_problemas)
    *   [10.1 su](#su)
    *   [10.2 El agente se queja del final del archivo](#El_agente_se_queja_del_final_del_archivo)
    *   [10.3 Permisos de configuración de KGpg](#Permisos_de_configuración_de_KGpg)
    *   [10.4 Conflictos entre gnome-keyring y gpg-agent](#Conflictos_entre_gnome-keyring_y_gpg-agent)
    *   [10.5 mutt y gpg](#mutt_y_gpg)
    *   [10.6 Llaves "perdidas", actualizando a gnupg versión 2.1](#Llaves_"perdidas",_actualizando_a_gnupg_versión_2.1)
*   [11 Ver también](#Ver_también)

## Instalación

[Instala](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") [gnupg](https://www.archlinux.org/packages/?name=gnupg), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Esto instalará también [pinentry](https://www.archlinux.org/packages/?name=pinentry), una colección de diálogos sencillos para introducción de PINs o contraseñas que GnuPG utiliza para la introducción de frases de acceso. *pinenetry* está señalado por el enlace simbólico `/usr/bin/pinentry`, que por defecto apunta a `/usr/bin/pinentry-gtk-2`.

## Variables de Entorno

### GNUPGHOME

GnuPG usa `$GNUPGHOME` para localizar el directorio donde se almacenan todos los archivos de configuración. Por defecto `$GNUPGHOME` no está establecida y en su lugar se usa tu `$HOME`, por lo que encontrarás un directorio `~/.gnupg` inmediatamente después de la instalación de GnuPG. Puedes cambiar esta configuración por defecto añadiendo esta línea a uno de tus [archivos de inicio](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)"):

```
export GNUPGHOME="*/path/to/directory*"

```

**Nota:** Por defecto, el directorio gnupg tiene sus permisos establecidos en *700* y los archivos que contiene tienen sus permisos establecidos en *600*. Solo el propietario del directorio tiene permiso para leer, escribir y acceder a los archivos (*r*,*w*,*x*). Esto es así por razones de seguridad y no debería cambiarse. En el caso de que este directorio o cualquiera de los archivos en su interior no siga esta medida de seguridad, recibirás advertencias sobre un archivo inseguro y sobre los permisos del directorio de inicio.

### GPG_AGENT_INFO

Se usa `GPG_AGENT_INFO` para localizar el *agente gpg*. Está compuesto de tres campos delimitados por dos puntos:

1.  ruta al Socket de Dominio Unix
2.  PID de gpg-agent
3.  versión de protocolo establecida en 1

Ejemplo: `GPG_AGENT_INFO=/tmp/gpg-eFqmSC/S.gpg-agent:7795:1`. Cuando se inicia gpg-agent, esta variable se establece al valor correcto.

**Nota:** Según el [anuncio de GnuPG 2.1](https://www.gnupg.org/faq/whats-new-in-2.1.html): Con GnuPG 2.1 la necesidad de `GPG_AGENT_INFO` se ha eliminado por completo y esta variable se ignora. En su lugar, se usa un socket de dominio Unix con el nombre fijo `$GNUPGHOME/S.gpg-agent`. El agente también se inicia respondiendo a la petición de cualquier herramienta que requiera los servicios del agente.

## Archivo de configuración

Por defecto es `~/.gnupg/gpg.conf`. Si deseas cambiar la ubicación por defecto, ejecuta gpg mediante `$ gpg --homedir *ruta/al/archivo*` o usa la variable `$GNUPGHOME`.

Añade a este archivo todas las opciones que quieras. Encontrarás un archivo de muestra en `usr/share/gnupg/gpg-conf.skel`.

El siguiente es un archivo de configuración básico:

 `~/.gnupg/gpg.conf` 
```
default-key *nombre*      # útil en caso de que gestiones varias claves y quieras usar una por defecto
keyring *archivo*         # añadirá *archivo* a la lista actual de anillos de claves
trustdb-name *archivo*    # usa *archivo* en lugar de la base de datos de confianza por defecto
homedir *dir*             # establece el nombre del directorio de inicio de gnupg en *dir* en lugar de ~/.gnupg
display-charset utf-8       # ignora las traducciones y supone que el SO usa una codificación nativa UTF-8
keyserver *nombre*        # usa *nombre* como tu servidor de claves
no-greeting                 # suprime el mensaje inicial de copyright
armor                       # crea una salida ASCII blindada. Por defecto se usa el formato binario OpenPGP

```

Si deseas configurar algunas opciones por defecto para usuarios nuevos, coloca los archivos de configuración en `/etc/skel/.gnupg/`. Cuando se añada un nuevo usuario al sistema, los archivos de este directorio se copiarán a su directorio de inicio de GnuPG. También hay un sencillo *script* llamado *addgnupghome* que puedes usar para crear nuevos directorios de inicio de GnuPG para los usuarios ya existentes:

```
# addgnupghome usuario1 usuario2

```

Esto añadirá los respectivos `/home/user1/.gnupg` y `/home/user2/.gnupg` y copiará los archivos del directorio `/etc/skel/.gnupg/`. El script ignora a los usuarios que ya tengan un directorio de inicio de GnuPG.

## Gestión básica de claves

**Nota:** Siempre que se requiera un *`<user-id>`* en un comando, este se puede especificar mediante el ID de la clave, la huella, una parte del nombre o del correo electrónico, etc. GnuPG es flexible con esto.

### Crear una clave

Configura GnuPG para que use en primer lugar los algoritmos más fuertes:

 `~/.gnupg/gpg.conf` 
```
personal-digest-preferences SHA512
cert-digest-algo SHA512
default-preference-list SHA512 SHA384 SHA256 SHA224 AES256 AES192 AES CAST5 ZLIB BZIP2 ZIP Uncompressed
personal-cipher-preferences TWOFISH CAMELLIA256 AES 3DES

```

Genera una clave privada escribiendo en un terminal:

```
$ gpg --full-gen-key

```

**Nota:** La opción `--full-gen-key` está disponible desde [gnupg](https://www.archlinux.org/packages/?name=gnupg)-2.1.0.

Se te harán varias preguntas. En general, la mayoría de usuarios querrán tanto una clave RSA (solo firma) como una clave RSA (solo cifrado). Un tamaño de clave de 2048 es suficiente. El uso de 4096 ["no nos da casi nada, pero nos cuesta mucho."](https://www.gnupg.org/faq/gnupg-faq.html#no_default_of_rsa4096)

Aunque tener una fecha de caducidad para las subclaves no es necesario técnicamente, se considera una buena práctica. Un periodo de un año normalmente es suficientemente bueno para un usuario medio. De esta forma, incluso aunque pierdas acceso a tu anillo de claves, otros usuarios podrán saber que este ya no es válido. Ten en cuenta que puedes extender la fecha de caducidad después de la creación de la clave sin tener que crear una nueva clave.

### Gestionar una clave

*   La ejecución del comando `gpg --edit-key *<user-id>*` te mostrará un menú que te permite hacer la mayoría de las tareas relacionadas con la gestión de una clave. El siguiente es un ejemplo de como establecer una fecha de caducidad:

```
$ gpg --edit-key *<user-id>*
> key *number*
> expire *yyyy-mm-dd*
> save
> quit

```

Algunos comandos útiles:

```
> passwd       # cambiar la frase de acceso
> clean        # compactar cualquier ID de usuario que ya no sea utilizable (p.ej. revocado o caducado)
> revkey       # revocar una clave
> addkey       # añadir una subclave a esta clave
> expire       # cambiar la fecha de caducidad

```

*   Generar una versión ASCII de tu clave pública (p.ej. para distribuirla por e-mail):

```
$ gpg --armor --output public.key --export *<user-id>*

```

*   Registrar tu clave en un servidor de claves PGP público, para que otros puedan obtener tu clave sin tener que contactarte directamente:

```
$ gpg  --keyserver pgp.mit.edu --send-keys *<user-id>*

```

*   Firmar y cifrar para el usuario Bob.

```
$ gpg -se -r Bob *file*

```

*   hacer una firma de texto plano.

```
$ gpg --clearsign *file*

```

### Rotar subclaves

**Advertencia:** **Nunca** borres tus claves caducadas o revocadas a menos que tengas una buena razón. Hacer esto impediría que pudieras descifrar archivos cifrados con la vieja subclave. Por favor, borra **solo** claves caducadas o revocadas de otros usuarios para mantener limpio tu anillo de claves.

Si has configurado tus subclaves para que caduquen después de un tiempo, puedes crear subclaves nuevas. Haz esto unas cuantas semanas antes de la caducidad para permitir a otros que actualicen su anillo de claves.

**Nota:** No necesitas crear una nueva clave solo porque haya caducado. Puedes alargar la fecha de caducidad.

*   Crear una nueva subclave (repetir tanto para la clave de firma como para la de cifrado).

```
$ gpg --edit-key *<user-id>*
> addkey

```

Y responde a las preguntas que te haga a continuación (ver la sección anterior para más información).

*   Guardar los cambios.

```
> save

```

*   Subir la clave a un servidor de claves.

```
$ gpg  --keyserver pgp.mit.edu --send-keys *<user-id>*

```

**Nota:** Revocar subclaves caducadas es innecesario y podría decirse que una mala costumbre. Si revocas claves frecuentemente, es posible que otros pierdan la confianza en ti.

### Importar una clave

*   Importar una clave pública a tu anillo de claves públicas:

```
$ gpg --import public.key

```

*   Importar una clave privada a tu anillo de claves secretas:

```
$ gpg --import private.key

```

*   Importar una clave de un servidor de claves (si se omite '--keyserver', se usa el servidor por defecto):

```
$ gpg --recv-keys <keyid> --keyserver pgp.mit.edu

```

### Listar claves

*   Claves en tu anillo claves públicas:

```
$ gpg --list-keys

```

*   Claves en tu anillo de claves secretas:

```
$ gpg --list-secret-keys

```

## Cifrar y descifrar

Cuando se cifra y se descifra es posible tener en uso más de una clave privada. Si esto ocurre necesitas seleccionar la clave activa. Esto se puede hacer usando la opción `-u *<user-id>*` o la opción `--local-user *<user-id>*`. Esto hace que se use la clave especificada en lugar de la clave por defecto.

Existen dos métodos convencionales de cifrado/descifrado, [asimétrico y simétrico](https://es.wikipedia.org/wiki/Cifrado_(criptograf%C3%ADa)#Tipos_de_cifrado_según_sus_claves). Los usos principales van a ser explicados en las siguientes secciones.

#### Asimétrico

Necesita [importar la clave](#Importar_una_clave) del recipiente antes de cifrar (opción `--encrypt` o `-e`) un archivo o un mensaje a este (opción `--recipient` o `-r`). Adicionalmente se necesita [#Crear una clave](#Crear_una_clave) si no lo ha hecho.

Para cifrar un archivo con el nombre *doc*, ejecute:

```
$ gpg --recipient *user-id* --encrypt *doc*

```

Para descifrar un archivo con el nombre *doc*.gpg con su clave pública, use el parámetro `--decrypt` o `-d`:

```
$ gpg --output *doc* --decrypt *doc*.gpg

```

*gpg* le preguntará por su contraseña y después descifrara y escribirá la información de *doc*.gpg a *doc*. Si el parámetro `-o` (`--output`) se omite, *gpg* escribirá la información a stdout.

**Sugerencia:**

*   Agregue `--armor` para cifrar un archivo usando ASCII armor (apropiado para copiar y pegar el mensaje en formato de texto)
*   Use `-R *user-id*` o `--hidden-recipient *user-id*` en lugar de `-r` para no poner la clave del recipiente en el mensaje cifrado. Esto ayuda a ocultar el recipiente del mensaje y es una medida limitada de protección contra el análisis de trafico.
*   Agregue `--no-emit-version` para prevenir la impresión de la versión, también se puede modificar este parámetro en el archivo de configuración.
*   Es posible usar gnupg para cifrar documentos delicados con su propio *user-id* como recipiente o usando el parametro `--default-recipient-self`; de cualquier manera, esto solo se puede hacer un archivo a la vez, aunque se pueden comprimir varios archivos en un tarball y después cifrar el tarball. Vea tambien [Disk encryption (Español)#Métodos disponibles](/index.php/Disk_encryption_(Espa%C3%B1ol)#Métodos_disponibles "Disk encryption (Español)") si quiere cifrar directorios enteros o incluso todo sus sistema de archivos.

#### Simétrico

Cifrado simétrico no requiere la generación de claves y puede ser usada para cifrar datos con una contraseña. Simplemente use `--symmetric` o `-c` para efectuar el cifrado:

```
$ gpg -c *doc*

```

Por ejemplo:

*   Para cifrar `*doc*` de manera simétrica con una contraseña
*   Usando el algoritmo AES-256 para cifrar la contraseña
*   Usando el algoritmo SHA-512 para ofuscar la contraseña
*   Ofusca la contraseña en 65536 iteraciones

```
$ gpg -c --s2k-cipher-algo AES256 --s2k-digest-algo SHA512 --s2k-count 65536 *doc*

```

Para descifrar un archivo `*doc*.gpg` simetricamente cifrado usando una contrasena y para poner los archivos resultantes `*doc*` en el mismo directorio, ejecute:

```
$ gpg --output *doc* --decrypt *doc*.gpg

```

### Cifrar una contraseña

Puede ser útil cifrar una contraseña, de forma que no quede escrita en texto plano en un archivo de configuración. Un buen ejemplo es la contraseña de tu correo electrónico.

Primero crea un archivo con tu contraseña. **Necesitas** dejar **una** línea en blanco después de la contraseña, ya que si no GnuPG devolverá un mensaje de error cuando evalúe el archivo.

Después ejecuta:

```
$ gpg -e -a -r *<user-id>* *tu_archivo_de_contraseña*

```

`-e` es para cifrar, `-a` para una salida blindada (salida ASCII), `-r` para el ID de usuario del destinatario.

Tras hacer esto tendrás un nuevo archivo `*tu_archivo_de_contraseña*.asc`.

## Firmas

Firmas certifican y marcan el tiempo en documentos. Si el documento es modificado, la verificación de la firma fallará. A diferencia de criptografía regular que usa claves públicas para cifrar un documento, firmas son creadas con la clave privada del usuario. El recipiente de un documento firmado verifica dicha firma con la clave publica del remitente.

### Crear una firma

#### Firmar un documento

Para firmar un documento use el parámetro `--sign` o `-s`:

```
 $ gpg --output *doc*.sig --sign *doc*

```

`*doc*.sig` contiene una versión comprimida del documento original `*doc*` y la firma en formato binario, pero el archivo no esta cifrado. Es posible combinar la firma con [cifrado](#Cifrar_y_descifrar).

#### Firma sencilla de un archivo o mensaje

Para firmar un archivo sin comprimirlo en formato binario ejecute:

```
 $ gpg --output *doc*.sig --clearsign *doc*

```

En este caso el documento original `*doc*` y la firma son guardados en de la forma `*doc*.sig`, la cual es simple de leer.

#### Crear una firma independiente

Para crear una firma que puede ser distribuida de manera separada al archivo, use el parámetro `--detach-sig`:

```
 $ gpg --output *doc*.sig --detach-sig *doc*

```

En este caso la firma es guardada en `*doc*.sig`, pero el contenido de `*doc*` no es guardado allí. Este método es usado generalmente en la distribución de proyectos de software, permitiendo a los usuarios verificar que el programa no ha sido modificado por un tercero.

### Verificación de firmas

Para verificar una firma use el parámetro `--verify`:

```
 $ gpg --verify *doc*.sig

```

Donde `*doc*.sig` es el documento firmado conteniendo la firma que se quiere verificar.

Si se esta verificando una firma independiente, la firma y el documento tiene que estar presentes para la verificación. Por ejemplo, para verificar el ISO de Arch Linux ejecute:

```
 $ gpg --verify archlinux-*version*.iso.sig

```

donde `archlinux-*version*.iso` debe estar ubicado en el mismo directorio.

También se puede especificar el archivo fuente en el segundo argumento del comando:

```
 $ gpg --verify archlinux-*version*.iso.sig */ruta/a/*archlinux-*version*.iso

```

Si un archivo ha sido cifrado ademas de ser firmado, simplemente [descifre](#Cifrar_y_descifrar) el archivo y su firma será verificada.

## gpg-agent

*gpg-agent* se usa principalmente como demonio para solicitar y almacenar en cache la contraseña de la llave. Esto es útil si se usa GnuPG desde un programa externo como un cliente de correo. [gnupg](https://www.archlinux.org/packages/?name=gnupg) viene con [systemd/user](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)") sockets, los cuales estan activados por defecto. Estos sockets son `gpg-agent.socket`, `gpg-agent-extra.socket`, `gpg-agent-browser.socket`, `gpg-agent-ssh.socket`, y `dirmngr.socket`.

*   El socket pricipal `gpg-agent.socket` es usado por *gpg* para conectar al demonio de *gpg-agent*.
*   EL uso recomendado de `gpg-agent-extra.socket` en un sistema local es habilitar un socket de dominio Unix que reenvía desde un sistema remoto. Esto habilita el uso de *gpg* en el sistema remoto sin exponer las llaves privadas al sistema remoto. Vea [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1) para más detalles.
*   El socket `gpg-agent-ssh.socket` puede ser usado por [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)") para guardar las [Llaves SSH](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)") que han sido agregadas con *ssh-add* en cache. Consulte [#Agente SSH](#Agente_SSH) para la configuración necesaria.
*   El socket `dirmngr.socket` inicia un demonio de GnuGP que maneja conexiones con servidores de llaves.

**Nota:** Si se usa una configuración diferente a la usada por defecto [#Variables de Entorno](#Variables_de_Entorno), necesitara [editar](/index.php/Edit "Edit") los archivos de los sockets para usar los valores de `gpgconf --list-dirs`.

### Configuración

Se puede configurar **gpg-agent** mediante el archivo `~/.gnupg/gpg-agent.conf`. Las opciones de configuración están listadas en [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1). Por ejemplo puedes cambiar el tiempo de vida de la caché para las claves no usadas:

 `~/.gnupg/gpg-agent.conf` 
```
default-cache-ttl 3600

```

### Recargar el agente

Después de cambiar la configuración, recarga el agente redirigiendo la cadena `RELOADAGENT` a `gpg-connect-agent`:

```
$ echo RELOADAGENT | gpg-connect-agent

```

El terminal debería mostrar `OK`.

### pinentry

Finalmente, el agente necesita saber cómo solicitar la contraseña al usuario. Esto se puede establecer en el archivo de configuración de gpg-agent.

Por defecto se usa un diálogo gtk. Hay otras opciones (ver `info pinentry`). Para cambiar la implementación del diálogo, usa la opción de configuración `pinentry-program`:

 `~/.gnupg/gpg-agent.conf` 
```

# PIN entry program
# pinentry-program /usr/bin/pinentry-curses
# pinentry-program /usr/bin/pinentry-qt4
# pinentry-program /usr/bin/pinentry-kwallet

pinentry-program /usr/bin/pinentry-gtk-2

```

**Sugerencia:** Para usar `/usr/bin/pinentry-kwallet` tienes que instalar el paquete [kwalletcli](https://aur.archlinux.org/packages/kwalletcli/)

Después de hacer este cambio regarga el gpg-agent.

### Iniciar gpg-agent con el usuario systemd

Es posible usar el [Systemd/User](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)") para iniciar el agente.

Crea un archivo de unidad de systemd:

 `~/.config/systemd/user/gpg-agent.service` 
```
[Unit]
Description=GnuPG private key agent
IgnoreOnIsolate=true

[Service]
Type=forking
ExecStart=/usr/bin/gpg-agent --daemon --homedir=%h/.config/gnupg 
ExecStop=/usr/bin/pkill gpg-agent
Restart=on-abort

[Install]
WantedBy=*MyTarget*.target
```

**Nota:**

*   Puedes necesitar establecer algunas variables de entorno para el servicio, por ejemplo `GNUPGHOME`. Ver [Systemd/User](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)") para más detalles.
*   Si tu directorio de inicio de GnuPG es ~/.gnupg, no es necesario especificar su ruta.
*   `gpg -agent` no usará el socket estándar, sino que escuchará a un socket llamado `S.gpg-agent` ubicado en tu directorio de inicio de GnuPG. De esta forma nos podemos olvidar de cualquier script para leer una archivo de entorno y obtener la ruta del socket aleatorio creado en `/tmp`.

**Sugerencia:**

Para asegurarte de que gpg-agent está ejecutándose y esperando una conexión, simplemente ejecuta este comando: `$ gpg-connect-agent`. Si tu configuración es válida, aparecerá un *prompt* (escribe *bye* y *quit* para cerrar la conexión y salir)

### Frase de acceso desatendida

A partir de GnuPG 2.1.0 se requiere el uso de gpg-agent y pinentry; esto puede romper la compatibilidad hacia atrás para frases de acceso redirigidas desde STDIN usando la opción `--passphrase-fd 0`. Para tener la misma funcionalidad que en versiones anteriores, se deben hacer dos cosas:

Primero, editar la configuración de gpg-agent para permitir el modo *loopback* de pinentry:

 `~/.gnupg/gpg-agent.conf`  `allow-loopback-pinentry` 

Reinicia el proceso gpg-agent si está en ejecución para que el cambio tenga efecto.

Segundo, la aplicación debe ser actualizada para incluir un parámetro para usar el modo *loopback*, como este:

```
$ gpg --pinentry-mode loopback ...

```

...o, si esto no es posible, añadir la opción en la configuración:

 `~/.gnupg/gpg.conf`  `pinentry-mode loopback` 
**Nota:** Es posible que establecer la configuración **pinentry-mode loopback** en *gpg.conf* pueda afectar a otras funcionalidades. Por ello se recomienda usar la opción de la línea de comandos siempre que sea posible. [[1]](https://bugs.g10code.com/gnupg/issue1772)

### Agente SSH

*gpg-agent* tiene una emulación de agente OpenSSH. Si ya usa el paquete GnuPG, podría considerar usar su agente para almacenar también sus [claves SSH](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)"). Además, algunos usuarios pueden preferir la ventana para introducir el PIN que el agente GnuPG proporciona como parte de su administración de contraseña.

## Reuniones de firmado de claves

Para permitir a los usuarios validar claves en los servidores y en sus anillos de claves (es decir, asegurarse de que sus propietarios son quienes dicen ser), PGP/GPG usa la conocida como "Red de Confianza". Se celebran eventos de hackers que pretenden mantener esta Red de Confianza, incluyendo reuniones de firmado de claves.

El protocolo de firmado de claves [Zimmermann-Sassaman](https://en.wikipedia.org/wiki/Zimmermann%E2%80%93Sassaman_key-signing_protocol "wikipedia:Zimmermann–Sassaman key-signing protocol") es una forma muy efectiva de hacer esto. [Aquí](http://www.cryptnet.net/fdp/crypto/keysigning_party/en/keysigning_party.html) encontrarás un artículo que explica cómo hacerlo.

### caff

Para un proceso más fácil de firmado de claves y envío de firmas a los propietarios después de una reunión de firmado de claves, puedes usar la herramienta *caff*. Se puede instalar desde el AUR mediante el paquete [caff-svn](https://aur.archlinux.org/packages/caff-svn/), pero habrá muchas dependencias al instalarla desde el AUR. En su lugar, puedes instalarla desde CPAN con

```
cpanm Any::Moose
cpanm GnuPG::Interface

```

Para enviar las firmas a sus propietarios necesitas un [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent"). Si no tienes ya uno, instala [msmtp](/index.php/Msmtp "Msmtp").

## Smartcards

**Nota:** [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) y [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) tienen que estar instalados, y el servicio [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") incluído `pcscd.service` tiene que estar arrancado.

GnuPG usa *scdaemon* como interfaz para tu lector de *smartcard*. Por favor, consulta la página del manual para más detalles.

### Instalaciones solo con GnuPG

Si no prevés utilizar otras tarjetas aparte de las basadas en GnuPG, deberías comprobar el parámetro `reader-port` en `~/.gnupg/scdaemon.conf`. El valor '0' se refiere al primer puerto serie disponible y el valor '32768' (por defecto) se refiere al primer lector USB.

### GnuPG junto con OpenSC

Si vas a usar cualquier smartcard con un driver opensc (p.ej. los lectores de DNI electrónico de algunos países) deberías prestar atención a la configuración de GnuPG. Recién instalado podrías recibir un mensaje como este cuando uses `gpg --card-status`

```
gpg: selecting openpgp failed: ec=6.108

```

Por defecto, scdaemon intentará contectar directamente con el dispositivo. Esta conexión fallará si el lector está siendo usado por otro proceso. Por ejemplo: el demonio pcscd usado por OpenSC. Para hacer frente a esta situación deberíamos usar le mismo driver subyacente que opensc de forma que puedan trabajar bien juntos. Para indicarle a scdaemon que use pcscd deberías quitar `reader-port` de `~/.gnupg/scdaemon.conf`, especificar la ubicación de la librería `libpcsclite.so` y desactivar ccid para asegurarnos de que se usa pcscd:

 `~/.gnupg/scdaemon.conf` 
```
pcsc-driver /usr/lib/libpcsclite.so
card-timeout 5
disable-ccid

```

Por favor, comprueba [scdaemon(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/scdaemon.1) si no usas OpenSC.

## Resolución de problemas

### su

Cuando usas `pinentry`, debes tener los permisos adecuados en el dispositivo terminal que uses (p.ej. `/dev/tty1`). Sin embargo, con *su* (o *sudo*), la propiedad sigue siendo del usuario original, y no del nuevo. Esto significa que pinentry fallará, incluso como root. La solución es cambiar los permisos del dispositivo en algún momento antes del uso de pinentry (es decir, usar gpg con un agente). Si usas gpg como root, simplemente cambia la propiedad a root justo antes de usar gpg:

```
chown root /dev/ttyN  # donde N es el tty actual

```

y después cámbialo de nuevo tras usar gpg la primera vez. Es probable que haya que hacer lo mismo con `/dev/pts/`.

**Nota:** El propietario de tty *debe* corresponderse con el usuario para el cual se ejecuta pinentry. Ser parte del grupo `tty` **no es** suficiente.

### El agente se queja del final del archivo

El programa pinentry por defecto es pinentry-gtk-2, que necesita una sesión de DBus para funcionar correctamente. Ver [permisos de sesión](/index.php/General_troubleshooting_(Espa%C3%B1ol)#Permisos_de_sesión "General troubleshooting (Español)") para más detalles.

En su lugar, puedes usar `pinentry-qt`. Consulte [#pinentry](#pinentry).

### Permisos de configuración de KGpg

Ha habido problemas para que [kgpg](https://www.archlinux.org/packages/?name=kgpg) sea capaz de acceder a las opciones de `~/.gnupg/`. Un problema puede estar originado por un archivo de opciones obsoleto. Ver este [informe de error](https://bugs.kde.org/show_bug.cgi?id=290221).

Otro usuario informó de que *KGpg* no conseguía arrancar hasta que se cambiaron los permisos de `~/.gnupg` a `drwxr-xr-x`. Si necesitas esta solución provisional, asegúrate de que los contenidos del directorio mantienen los permisos `-rw-------`. Mejor aún, envía un informe de error a los [desarrolladores](https://bugs.kde.org/buglist.cgi?quicksearch=kgpg).

### Conflictos entre gnome-keyring y gpg-agent

Mientras que el anillo de claves de Gnome implementa un componente de agente GPG, desde la versión 2.1 de GnuPG, se ignora la variable de entorno `GPG_AGENT_INFO`, de forma que el anillo de claves de Gnome ya no se puede usar como agente GPG.

### mutt y gpg

Para que solo se te pida la contraseña de GnuPG una vez por sesión, desde GnuPG 2.1., ver [este hilo del foro](https://bbs.archlinux.org/viewtopic.php?pid=1490821#p1490821).

### Llaves "perdidas", actualizando a [gnupg](https://www.archlinux.org/packages/?name=gnupg) versión 2.1

Cuando `$ gpg --list-keys` no consigue mostrar las claves que solía mostrar, y las aplicaciones se quejan de claves inexistentes o no válidas, algunas claves pueden no haberse migrado al nuevo formato.

Por favor, lee ["GnuPG invalid packet workaround"](http://jo-ke.name/wp/?p=111). Básicamente, dice que hay un error con las claves en los viejos archivos `pubring.gpg` y `secring.gpg`, que ahora se han sustituido por el nuevo archivo `pubring.kbx` y el subdirectorio `private-keys-v1.d/` y sus archivos. Tus claves perdidas se pueden recuperar con las siguientes órdenes:

```
$ cd
$ cp -r .gnupg gnupgOLD
$ gpg --export-ownertrust > otrust.txt
$ gpg --import .gnupg/pubring.gpg
$ gpg --import-ownertrust otrust.txt
$ gpg --list-keys

```

## Ver también

*   [La guía de GNU Privacy Guard](http://gnupg.org/gph/es/manual.html)
*   [Un tutorial de GnuPG más exhaustivo](http://blog.sanctum.geek.nz/series/linux-crypto/) (en inglés).
*   [Preguntas frecuentes de GnuPG](https://www.gnupg.org/faq/gnupg-faq.html) (en inglés).
*   [recomendaciones y mejores prácticas para gpg.conf](https://help.riseup.net/en/security/message-security/openpgp/gpg-best-practices) (en inglés).
*   [Torbirdy gpg.conf](https://github.com/ioerror/torbirdy/blob/master/gpg.conf)