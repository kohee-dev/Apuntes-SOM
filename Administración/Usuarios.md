*Warning*

Este documento es teoría, estudiadlo bien :wink:

# Usuarios

En un sistema Linux podemos encontrar varios tipos de usuarios pero por norma general se dividen en 3 categorías.

## Root

Tambien llamado Superusuario o Administrador y siempre tiene UID (User ID)=0 (cero). 

Tiene privilegios sobre todo el sistema y acceso a ficheros y directorios independientemente de su propietario.

Puede realizar varias tareas como:
*  Administrar cuentas de usuario.
*  Detener el sistema
* Instalar software
* Modificar y reconfigurar el kernel, controladores, etc.

## Cuentas del sistema
Tambien llamados Usuarios Especiales o cuentas nologin. Pueden ser bin, daemon, adm, lp, sync, &c

No tienen los mismos privilegios que root pero si asumen distintos privilegios de root con el fin de proteger al sistema de varias formas de vulnerar su seguridad.

Se crean automáticamente y son cuentas que no están pensadas para iniciar sesión con ellas.

Su UID suele estar comprendida entre 1 y 100

## Usuarios individuales

Cada usuarios tiene un directorio HOME y tienen privilegios completos sobre ese directorio.

Por seguridad se recomienda trabajar con este tipo de usuarios y cuando se necesiten realizar operaciones con root acceder mediante el comando `su`

Actualmente se les asigna una UID superior a 500 aunque en Ubuntu se les asigna a partir de 1000.


### Como trabajar con usuarios

Hay una seríe de comandos de gran utilidad a la hora de trabajar con usuarios.

|Comando|Función|Descripción|
|:-:|:-|:-|
|who|Muestra quién está conectado|Muestra información acerca de los usuarios que están actualmente conectados, con sesión abierta, en el sistema.|
|whoami|Muestra que usuario estás usando|Muestra el nombre de usuario asociado con el identificador de usuario efectivo que se está usando.|
|su|Convertirse en otro usuario|Permite ejecutar comandos con un usuario y grupo sustituto. Es decir, permite actual en el sistema como otro usuario.|
|id|Muestra información de un usuario|Muestra el usuario real y efectivo así como identificación de grupos a los que pertenece dicho usuario.|
|sudo|Ejecutar un comando como root|Permite ejecutar comandos como superusuario (root) o como otro usuario, siempre que el usuario esté permitido.|
|groups|Muestra grupos de un usuario|Muestra los grupos a los que pertenece el usuario.|
|passwd|Cambia la contraseña|Permite cambiar la contraseña de las cuentas de usuario|


---
Para trabajar con usuarios tenemos que tener en cuenta 3 ficheros.

## `/etc/passwd`

Aquí se encuentran todos los usuarios listados.

La información está repartida en 7 campos y delimitada por ":"

|Campo|Contenido|
|:-:|:-|
|1|Es el nombre del usuario, identificador de inicio de sesión (login). Tiene que ser único.|
|2|La 'x' indica la contraseña encriptada del usuario, además también indica que se está haciendo uso del archivo `/etc/shadow`, si no se hace uso de este archivo, este campo se vería algo así como: *ghy675gjuXCc12r5gt78uuu6R*.|
|3|Número de identificación del usuario (UID). Tiene que ser único. 0 para root, generalmente las cuentas o usuarios especiales se numeran del 1 al 100 y las de usuario normal del 101 en delante, en las distribuciones mas recientes esta numeración comienza a partir del 500.|
|4|Numeración de identificación del grupo (GID). El que aparece es el número de grupo principal del usuario, pero puede pertenecer a otros, esto se configura en `/etc/groups`.|
|5|Comentarios o el nombre completo del usuario.|
|6|Directorio de trabajo (Home) donde se sitúa al usuario después del inicio de sesión.|
|7|Shell que va a utilizar el usuario de forma predeterminada.|

## `/etc/shadow`

Anteriormente en passwd se encontraban las contraseñas cifradas, pero esto causaba el problema de que con los ordenadores actuales se pudiese acceder a ese archivo con facilidad y descifrar todas esas contraseñas. El archivo shadow se creo con el fin de resolver ese problema, puesto que no solo se encuentran cifradas sino que, ademas, sólo root puede acceder a ese fichero.

Tiene su información separada en 9 campos delimitados por ":" al igual que passwd

|Campo|Contenido|
|:-:|:-|
|1|	Nombre de la cuenta del usuario.|
|2|Contraseña cifrada o encriptada, un '*' indica cuenta de 'nologin'.|
|3|Días transcurridos desde el 1/ene/1970 hasta la fecha en que la contraseña fue cambiada por última vez.|
|4|Número de días que deben transcurrir hasta que la contraseña se pueda volver a cambiar.|
|5|Número de días tras los cuales hay que cambiar la contraseña. (-1 significa nunca). A partir de este dato se obtiene la fecha de expiración de la contraseña.|
|6|Número de días antes de la expiración de la contraseña en que se le avisará al usuario al inicio de la sesión.|
|7|	Días después de la expiración en que la contraseña se inhabilitara, si es que no se cambio.|
|8|Fecha de caducidad de la cuenta. Se expresa en días transcurridos desde el 1/Enero/1970 (epoch).|
|9|Reservado.|

## `/etc/groups`

Este archivo guarda la relación de los grupos a los que pertenecen los usuarios del sistema, contiene una línea para cada usuario con tres o cuatro campos por usuario:

|Campo|Contenido|
|:-:|:-|
|1|Indica el usuario.|
|2|'x' indica la contraseña del grupo, que no existe, si hubiera se mostraría un 'hash' encriptado.|
|3|Es el Group ID (GID) o identificación del grupo.|
|4|Es opcional e indica la lista de grupos a los que pertenece el usuario.|


---

Como ya hemos mencionado previamente shadow protege las contraseñas, pero si por cualquier motivo quisiésemos que las contraseñas volviesen a passwd con el riesgo que eso conlleva podríamos usar el comando `pwunconv` y si quisiésemos volver a la configuración más segura podríamos usar `pwconv`

Ya hemos acabado con las definiciones.

## Como crear un usuario.

Podemos usar el comando useradd

### `Useradd`

Para crear un usuario bastaría con la siguiente instrucción:

```bash
$ useradd Alejandro
```

Por supuesto tenemos varias opciones:


* -c: añade un comentario al momento de crear al usuario, campo 5 de /etc/passwd
* -d: directorio de trabajo o home del usuario, campo 6 de /etc/passwd
* -e: fecha de expiración de la cuenta, formato AAAA-MM-DD, campo 8 de /etc/shadow
* -g: número de grupo principal del usuario (GID), campo 4 de /etc/passwd
* -G: otros grupos a los que puede pertenecer el usuario, separados por comas.
* -r: crea una cuenta del sistema o especial, su UID será menor al definido en /etc/login.defs en la variable UID_MIN, además no se crea el directorio de inicio.
* -s: shell por defecto del usuario cuando ingrese al sistema. Si no se especifica, bash, es el que queda establecido.
* -u: UID del usuario, si no se indica esta opción, automáticamente se establece el siguiente número disponible a partir del último usuario creado.


¿Que hace esta instrucción?

```bash
useradd -d /usr/alex -s /bin/bash -u 1200 -c "Alejandro Bartolomé Fernández" alex
```

### Diferencias entre `Useradd` y `Adduser`

El comando useradd nos permite crear cuentas del sistema a bajo nivel. Adduser es mucho más intuitivo pero es recomendable conocer ambos. 

## Como modificar un usuario

### `Usermod`

Usermod permite modificar o actualizar un usuario o cuenta ya existente. Sus opciones más comunes o importantes son las siguientes

* -c: añade o modifica el comentario, campo 5 de /etc/passwd
* -d: modifica el directorio de trabajo o home del usuario, campo 6 de /etc/passwd
* -e: cambia o establece la fecha de expiración de la cuenta, formato AAAA-MM-DD, campo 8 de /etc/shadow
* -g: cambia el número de grupo principal del usuario (GID), campo 4 de /etc/passwd
* -G: establece otros grupos a los que puede pertenecer el usuario, separados por comas.
* -l :cambia el login o nombre del usuario, campo 1 de /etc/passwd y de /etc/shadow
* -L: bloque la cuenta del usuario, no permitiendolé que ingrese al sistema. No borra ni cambia nada del usuario, solo lo deshabilita.
* -s: cambia el shell por defecto del usuario cuando ingrese al sistema.
* -u: cambia el UID del usuario.
* -U: desbloquea una cuenta previamente bloqueada con la opción -L.

## Como borrar un usuario.

### `Userdel`

Hay 3 formas:

```bash
userdel sergio
```
Elimina el usuario de `/etc/passwd` y `/etc/shadow` pero mantiene la información de la cuenta.

```bash
userdel -r alex
```
Elimina el usuario de `/etc/passwd` y `/etc/shadow` ademas de su directorio de trabajo.

```bash
userdel -f alex
```

# Grupos 

En Linux, un grupo es una agrupación de usuarios. Crearlos y gestionarlos es de las cosas más sencillas que se pueden hacer en el sistema, sobre todo cuando estamos tratando con permisos.

## Crear grupos

Un grupo se puede crear usando la siguiente instrucción

```bash
sudo groupadd alumnos
```

## Cambiar su GID (Group ID)
Es importante destacar que le puedo cambiar la GID

```bash
#Cambiamos la GID de alumnos a 1010
sudo groupadd -g 1010 alumnos
```

## Cambiar su Nombre
```bash
#Cambia el nombre de alumnos a profesores
sudo groupadd -n profesores alumnos
```

## Añadir y quitar usuarios a grupos 

### Añadir usuarios

```bash
#Añade el usuario alex al grupo profesores
sudo usermod --append --groups profesores alex
sudo usermod -aG profesores alex
```

### Quitar usuarios

```bash
#Quita el usuario alex del grupo profesores
sudo gpasswd --delete alex profesores
```


## Eliminar grupos

```bash
#Elimina el grupo profesores
sudo groupdel profesores
```
