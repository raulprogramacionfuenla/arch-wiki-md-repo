**Estado de la traducción**
Este artículo es una traducción de [su](/index.php/Su "Su"), revisada por última vez el **2018-10-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Su&diff=0&oldid=549221) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Usuarios y grupos](/index.php/Users_and_Groups_(Espa%C3%B1ol) "Users and Groups (Español)")
*   [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)")

La [utilidad](/index.php/Core_utility_(Espa%C3%B1ol) "Core utility (Español)") [su](https://en.wikipedia.org/wiki/es:Su_(Unix) (usuario sustituto) se utiliza para asumir la identidad de otro usuario en el sistema, el superusuario *(root)* por defecto.

Véase [PAM](/index.php/PAM_(Espa%C3%B1ol) "PAM (Español)") para las formas de configurar el comportamiento de *su*.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Sudo, una alternativa](#Sudo,_una_alternativa)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Shell de inicio de sesión](#Shell_de_inicio_de_sesión)
    *   [4.2 su y wheel](#su_y_wheel)

## Instalación

su es parte del paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux).

## Utilización

Para asumir el inicio de sesión de otro usuario, pase el nombre de usuario que desea convertir a su, como sigue:

```
# su *usuario*

```

Se le pedirá la contraseña del usuario que está invocando.

Si no se pasa ningún nombre de usuario, su asume que es el superusuario *(root)* y la contraseña por la que se le preguntará será la de superusuario.

Para más información, véase [su(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/su.1).

## Sudo, una alternativa

[sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") es un programa más configurable que puede proporcionar una funcionalidad similar a su, y puede ser un reemplazo para su, según los requisitos específicos y los modelos de amenaza. El sistema sudo le pedirá su propia contraseña, o ninguna si está configurado de esa manera, en lugar de la del usuario objetivo (la cuenta de usuario que está intentando usar). De esta forma, no tiene que compartir contraseñas entre los usuarios, y si alguna vez necesita excluir a un usuario que tiene acceso de administrador (o acceso a cualquier otra cuenta, según el caso), no tiene que cambiar la contraseña del superusuario, que es una inconveniencia para todos los demás; solo necesita revocar el acceso de sudo de dicho usuario.

Si sudo ha sido configurado para permitir al usuario ejecutar el shell de superusuario, el usuario puede ejecutar `sudo -s` o `sudo -i` para imitar a `su` o `su -l` respectivamente, y proporcionando su propia contraseña (o ninguna) en lugar de la contraseña del superusuario. Del mismo modo, `sudo -u john -i` imita a `su -l john` si tiene permiso para ejecutar el shell de John.

## Consejos y trucos

### Shell de inicio de sesión

El comportamiento predeterminado de su es permanecer dentro del directorio vigente y de mantener las variables del entorno del usuario original (en lugar de cambiar a los del nuevo usuario).

Consideraciones importantes a tener en cuenta:

*   A veces puede ser ventajoso para un administrador del sistema utilizar la cuenta shell de un usuario normal y no la suya propia. En particular, a veces, la manera más eficiente para resolver el problema de un usuario, es iniciar sesión en la cuenta de ese usuario a fin de reproducir o depurar el problema.

*   Sin embargo, en muchas situaciones no es deseable, o incluso puede ser peligroso para el superusuario, estar operando desde la cuenta de la shell de un usuario normal y con las variables del entorno de esa cuenta, más que desde las suyas propias. Podría darse el caso de que, sin intención, desde la cuenta shell de un usuario normal, el superusuario instalara un programa o hiciera cambios en el sistema que no tendrían el mismo resultado que si se hicieran durante el uso de la cuenta del superusuario. Por ejemplo, podría instalar un programa de modo que el mismo le diera al usuario normal el poder para dañar accidentalmente el sistema u obtener acceso no autorizado a determinados datos.

Por lo tanto, es aconsejable que los usuarios administradores, así como cualquier otro usuario que está autorizado a utilizar su (y se sugiere que sean pocos, si los hay) adquieran el hábito de utilizar la orden su con la opción `-l`/`--login`. Esto tiene dos efectos:

1.  Cambiar desde el directorio en curso al directorio home del nuevo usuario (por ejemplo, a `/root` en el caso de que el usuario destinatario sea el superusuario) para *acceder* como ese usuario.
2.  Cambiar las variables del entorno a las del nuevo usuario según lo indicado en su propio archivo `~/.bashrc`. Es decir, si el primer argumento que se pasa a su es un guión, el directorio y el entorno en curso cambiarán a los que se obtendrían si el nuevo usuario hubiera iniciado su propia sesión en realidad (en lugar de hacerse cargo de la sesión ya existente).

Por lo tanto, los administradores, generalmente, deben utilizar su de la siguiente manera :

```
$ su -l

```

Un resultado idéntico se produce añadiendo el nombre del superusuario:

```
$ su -l root

```

Del mismo modo, lo anterior se puede hacer con cualquier otro usuario (por ejemplo, para un usuario llamado archie):

```
# su -l archie

```

Es posible que desee añadir un alias en `~/.bashrc` como sigue:

```
alias su='su -l'

```

### su y wheel

su de BSD permite únicamente a los miembros del [grupo de usuario](/index.php/User_group_(Espa%C3%B1ol) "User group (Español)") `wheel` asumir la identidad del superusuario por defecto. Este no es el comportamiento por defecto de su en GNU, pero dicho comportamiento puede ser imitado usando [PAM](/index.php/PAM_(Espa%C3%B1ol) "PAM (Español)"). Descomente la línea apropiada en `/etc/pam.d/su` y `/etc/pam.d/su-l`:

```
auth required pam_wheel.so use_uid

```