**pdnsd** es un servidor DNS (*Domain Name System*) diseñado con el propósito de realizar lo que se conoce como *local caching* (almacenamiento local) de información relevante a este protocolo, funcionalidad que *bind* y *dnsmasq* no poseen; de hecho, la **p** indica su cualidad de *persistant*.

Principalmente, pdsnd actúa como intermediario (*proxy*) entre el sistema y los servidores de nombre (*nameservers*), gestionando tanto las consultas (*queries*) realizadas como sus respectivas respuestas (*responses*). Configurándolo apropiadamente, podrá incrementar la rapidez de su navegación, aprovechando así aún más su conexión actual.

## Contents

*   [1 Características](#Características)
*   [2 Instalación](#Instalación)
*   [3 Configuración](#Configuración)
    *   [3.1 Preparación](#Preparación)
    *   [3.2 Formato](#Formato)
    *   [3.3 Servidores DNS](#Servidores_DNS)
    *   [3.4 OpenDNS](#OpenDNS)
    *   [3.5 Seguridad](#Seguridad)
    *   [3.6 Examinación](#Examinación)
    *   [3.7 Configuración del Sistema](#Configuración_del_Sistema)
        *   [3.7.1 Líneas Generales](#Líneas_Generales)
        *   [3.7.2 Para Usuarios de Banda Ancha](#Para_Usuarios_de_Banda_Ancha)
*   [4 Extras](#Extras)
    *   [4.1 Compartiendo el Servidor en la Red Local](#Compartiendo_el_Servidor_en_la_Red_Local)
    *   [4.2 Bloqueo de Nombres](#Bloqueo_de_Nombres)
*   [5 Preguntas Frecuentes](#Preguntas_Frecuentes)
*   [6 Enlaces Externos](#Enlaces_Externos)

### Características

Entre otras cosas, **pdnsd** es capaz de:

*   Realizar múltiples consultas simultáneas a diversos servidores de nombre.
*   Guardar (*caching*) las respuestas recibidas en su propia base de datos, evitando así las consultas repetitivas e incrementando en consecuencia la rapidez en el proceso de resolución de direcciones.
*   Albergar registros de nombres "ficticios", permitiéndole, por ejemplo, crear sus propias direcciones para utilizarlas en su red local.

Por otra parte, recuerde que, al ser un servidor, puede atarlo (*bind*) a una dirección IP específica para compartirlo entre varios ordenadores. Además, es altamente configurable, como podrá ver más adelante.

## Instalación

pdnsd se encuentra disponible en los repositorios de Arch. Para instalarlo, ejecute: `# pacman -S pdnsd` 

## Configuración

### Preparación

El fichero de configuración que viene incluido en el paquete necesitará algunas modificaciones si desea utilizarlo como está. Comience copiándolo: `# cp /etc/pdnsd.conf.sample /etc/pdnsd.conf` 

### Formato

El fichero `pdnsd.conf` utiliza un formato simple, pero en algunos aspectos diferente a aquellos con los que usted pudo toparse, dado que posee una colección de secciones de diversos tipos.

El formato establece que:

*   Las secciones deben encerrarse entre llaves: **{}** y no podrán anidarse.
*   Las opciones y sus respectivos valores deben especificarse como sigue: `nombre_de_la_opción=valor;`
    Note que el punto y coma (**;**) **NO** es opcional.
*   Los comentarios con las siguientes formas serán admitidos:
    *   **# <comentario>**
        Todo lo que incluya en lugar de *<comentario>* será ignorado hasta el final de la línea.
    *   **/* <comentario> */**
        En este caso, todo lo que reemplace a *<comentario>* será ignorado hasta los últimos dos caracteres del formato anterior, incluyéndolos.

### Servidores DNS

Necesitará especificar, por supuesto, a qué servidores DNS pdnsd consultará. Tenga en cuenta que la configuración más apropiada dependerá de la clase de conexión que posea.

Los usuarios con conexión de banda ancha quizá deban utilizar la primer sección de servidores como punto de partida para ajustar la misma a sus necesidades, mientras que a aquellos poseedores de conexiones *dial-up* (por módem telefónico) quizá les sea conveniente comenzar por la segunda entrada, dejando el resto comentado.

Le presentamos ahora los tres campos requeridos de esta sección (`server`):

*   **label**
    La opción *label* (etiqueta) debe ser única y se utiliza para identificar la sección. Es completamente arbitraria, puede establecer el valor que desee.
*   **ip**
    Es utilizada por defecto en el ejemplo destinado principalmente a los usuarios con conexión de banda ancha. Le indica a pdnsd cuáles son los servidores a consultar. En su valor puede especificar varios, separados por comas (**,**), pudiendo haber espacios entre ellas.
*   **file**
    Esta opción puede ser utilizada en lugar de *ip* para especificar una lista de direcciones IP de servidores. Su valor es la ruta de un fichero cuyo formato sea idéntico al de `/etc/resolv.conf`.
    Uno de los ejemplos provistos establece que pdnsd debe utilizar el fichero `/etc/ppp/resolv.conf` ya que el cliente PPP por defecto guarda en éste las direcciones de los servidores DNS indicados.

El resto de la sección `server` no requiere cambios. Para más información sobre el fichero de configuración y la lista de opciones disponibles, visite el manual en Internet, [en inglés](http://www.phys.uu.nl/~rombouts/pdnsd/doc.html).

### OpenDNS

El fichero `/etc/pdnsd.conf` incluye ejemplos con las opciones para utilizar OpenDNS ya establecidas; si lo desea puede remover o comentar el resto de las secciones (teniendo la precaución de no borrar la parte necesaria de la sección `global` que se encuentra al principio del mismo) quedándose sólo con OpenDNS.

Tenga en cuenta que si utiliza OpenDNS puede tener problemas al resolver Google. Quizá necesite denegar algunos resultados provistos por estos servidores, tales como los que en lugar de contener la dirección real de Google contienen direcciones a servidores intermediarios (*proxy*) pertenecientes al mismo OpenDNS, (el tiempo de respuesta puede aumentar de 15ms a 75ms o más). Las direcciones IP exactas de esos servidores varían pero usted puede sin embargo ejecutar un comando como `nslookup www.google.com 208.67.222.222` para averiguarlas. Se dará cuenta si los resultados de OpenDNS lo dirigen a un servidor intermediario, ya que obtendrá como respuesta algo similar a `google.navigation.opendns.com`. Una vez que usted conozca esas direcciones IP, puede reemplazarlas en `pdnsd.conf` por aquellas ya rechazadas en la sección `server` del ejemplo para OpenDNS; evite, no obstante, modificar los prefijos al hacer el cambio. Para el autor, esas direcciones han sido `208.67.216.230` y `208.67.216.231`.

### Seguridad

La configuración por defecto posee una falla de seguridad. El servidor corre como `nobody`, que es una cuenta de usuario estándar cuyo propósito es dar permisos mínimos a las aplicaciones que la utilicen. En lo que concierne a pdnsd, esta no es una buena idea, ya que el servidor (*daemon*) requiere permisos de lecto-escritura para su propio fichero de *cache*. En consecuencia, si un usuario malintencionado encuentra una vulnerabilidad en otro proceso corriendo como `nobody`, podrá inyectar información DNS falsa en este fichero, originando todo tipo de inconvenientes.

A fin de evitar este riesgo, le convendrá crear un usuario propio de pdnsd. Por ejemplo:

```
# groupadd pdnsd
# useradd -r -d /var/cache/pdnsd -g pdnsd -s /bin/false pdnsd

```

**Nota:** Se sugirió `/var/cache/pdnsd` como directorio principal del usuario ya que será en donde pdnsd guardará el fichero de *cache*.

Vuelva ahora a `/etc/pdnsd.conf`. Es tiempo de editar la sección `global`, ubicada al inicio del mismo. Modifique `run_as` de `nobody` a `pdnsd` (o al usuario que haya creado anteriormente). Le convendrá modificar también `strict_setuid` para mayor seguirdad; cambie su valor a `on`.

Todavía el servidor se encuentra muy limitado: necesita escribir en el directorio `/var/cache`, pero no puede hacerlo dado que requiere privilegios de *root*. Devuélvale algo de funcionalidad haciendo:

```
# chown -R pdnsd:pdnsd /var/cache/pdnsd
# chmod 700 /var/cache/pdnsd
# chmod 600 /var/cache/pdnsd/pdnsd.cache

```

**Nota:** En el primer comando, reemplace *pdnsd:pdnsd* por el usuario y grupo creados anteriormente.

### Examinación

En este punto ya debería tener un servidor capaz de funcionar. Ejecute lo siguiente para verificarlo: `# /etc/rc.d/pdnsd start` Puede evaluar su funcionamiento mediante `nslookup` (programa incluido en el paquete `dnsutils`): `$ nslookup www.google.com 127.0.0.1` Ejecute: `$ dig archlinux.org|grep "Query time"` Si todo funciona, deberá ver una lista de direcciones IP asociadas a *www.google.com*; además, el tiempo de consulta deberá estar cerca del milisegundo.

### Configuración del Sistema

Es momento de configurar su sistema para aprovechar su nuevo servidor DNS. Recuerde que los siguientes pasos están basados en el fichero de configuración por defecto. Siéntase libre de realizar las modificaciones que necesite.

#### Líneas Generales

Si usted utiliza DHCP (*Dynamic Host Configuration Protocol*) para configurar su red, deberá editar `/etc/resolv.conf.head` (o directamente `/etc/resolv.conf`) añadiendo a pdnsd como primera entrada:

```
# pdnsd cache en localhost
nameserver 127.0.0.1
```

Resta añadir `pdnsd` a la lista de *daemons* en `/etc/rc.conf`, inmediatamente después de `network`, ya que depende de éste para correr, como sucede con otros servidores.

Reinicie ahora la red (recuerde que pdnsd debería estar corriendo): `# /etc/rc.d/network restart` 

#### Para Usuarios de Banda Ancha

Muchos usuarios poseen conexiones de banda ancha en donde los servidores DNS son lentos o no confiables y desean utilizar pdnsd para justamente minimizar la cantidad de consultas (*queries*) necesarias. Luego de seguir las instrucciones anteriores, incluir las siguientes opciones en `/etc/pdnsd.conf` le ayudará a incrementar el desempeño del servidor en este caso particular.

Dentro de la sección `global`:
```
neg_rrs_pol=on;
par_queries=1;
```
Dentro de la sección `server`:
```
proxy_only=on;
purge_cache=off;
```

Le explicaremos cada opción a continuación:

*   `neg_rrs_pol=on` indica que las respuestas *negativas* (vea las especificaciones del protocolo DNS para *negative response*) no serán descartadas, incluso si éstas no son *authoritatives*. Esto es importante ya que la observación de varias respuestas DNS revelerá que existe un gran número de *requests* (pedidos o consultas) sobre registros AAAA (vinculados a IPv6) que nunca serán respondidas puesto que muchos dominios aún no utilizan IPv6; lo mismo sucede con los registros MX. Sin esta política (*negative caching*) habilitada, esta clase de consultas serán realizadas aún luego de haber guardado el nombre de dominio correspondiente a la principal de las mismas. Es importante que en conjunción a esta opción se especifique `proxy_only=on;` para minimizar la cantidad total de consultas que se enviarán.

*   La opción `par_queries=1;` es útil si especifica más de un servidor DNS en la sección `server`. Indica la cantidad de consultas que pdnsd realizará simultáneamente. Si alguno de los servidores consultados falla, pdnsd consultará al siguiente en la lista (o a los siguientes simultáneamente, en caso que haya especificado un número mayor que uno). Esta opción puede aumentar el tráfico de paquetes en su red, úsela con precaución.

*   `proxy_only=on;` indica que pdnsd sólo acutará como intermediario, es decir, se dedicará únicamente a gestionar las consultas y sus respuestas. Si esta opción es deshabilitada, pdnsd intentará actuar como un servidor DNS real, resolviendo *jerárquicamente* (*hierarchical resolution*) los nombres de dominio, es decir, resolviendo hasta toparse con el servidor *authoritative* (*con autoridad*). Como se dijo anteriormente, habilitar esta opción ayuda a reducir el tráfico de paquetes DNS, incrementando el desempeño en general.

*   Por su parte, `purge_cache=off` indica que pdnsd no borrará entradas antiguas del *cache*, es decir, que se hayan conservado por más tiempo que el estipulado por sus valores TTL (*Time To Live*) correspondientes. Esto puede ser muy útil, por ejemplo, ante un problema con los servidores provistos por su ISP, ya que de todas formas podrá continuar accediendo a los registros que pdnsd guardó en su *cache*.

## Extras

### Compartiendo el Servidor en la Red Local

Si posee varios ordenadores en su red, quizá desee utilizar pdnsd para todos ellos. Esto le permitirá centralizar el tráfico DNS utilizando un mismo *cache* y un mismo servidor. Para habilitar esta opción, agregue en la sección `global` del fichero de configuración `/etc/pdnsd.conf` la siguiente línea: `server_ip=<ip>`, siendo *<ip>* la dirección IP a la que se conectarán los demás ordenadores, (otra opción es utilizar `interface` para establecer el nombre de una interfaz de red en lugar de una IP; *eth0* es un ejemplo).

### Bloqueo de Nombres

pdnsd le permite bloquear dominios y nombres de huésped (*hostname*) de los cuales no devolverá resultados; otorgándole así la posibilidad de usarlo también como un primitivo bloqueador de contenidos o anuncions, entre otras cosas.

Cree una nueva sección `neg` en el fichero `/etc/pdnsd.conf` especificando las siguientes opciones requeridas:

*   `name`
    Indica el nombre del *host* o dominio a bloquear.
*   `types`
    Puede ser establecido como *domain* a fin de bloquear automáticamente todos los *hosts* de un mismo dominio.

Recuerde que puede consultar siempre la documentación para más información, incluyendo la *man page*: [pdnsd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdnsd.8) y [pdnsd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdnsd.conf.5). Asimismo, tenga en cuenta que el fichero de configuración por defecto provee ejemplos y comentarios explicativos.

## Preguntas Frecuentes

*   **P) No percibo diferencias en la rapidez. ¿Por qué?**
    La rapidez se evidenciará únicamente en el proceso de resolución de direcciones, que por supuesto afecta al tiempo que tardará en conectarse a un servidor dado. La tasa de transferencia (o rendimiento, que mucha gente entiende como *rapidez*; en inglés: *throughput*) no se verá afectada. La diferencia es más evidente al navegar por Internet, ya que típicamente se realizan pequeñas descargas desde distintos servidores. En conexiones más lentas, especialmente en el caso de *dial-up*, el cuello de botella (*bottleneck*) se da en el rendimiento, por lo que no notará, porcentualmente hablando, gran diferencia como en otros casos.

*   **P) ¿Por qué es más lento ahora que antes?**
    Seguramente usted tiene deshabilitada la opción `proxy_only` en el fichero `/etc/pdnsd.conf`. Por defecto, pdnsd frecuentemente consulta a varios servidores DNS sobre el mismo nombre de dominio con el propósito de obtener la respuesta más precisa posible. Habilitar la opción antedicha evitará este comportamiento y le será útil si decide quedarse con los servidores DNS provistos por su ISP.

## Enlaces Externos

*   Documentación de pdnsd, en inglés: [pdnsd Documentation](http://www.phys.uu.nl/~rombouts/pdnsd/doc.html)

*   Artículo en Wikipedia, en español, sobre el protocolo [DNS](https://es.wikipedia.org/wiki/Domain_Name_System).