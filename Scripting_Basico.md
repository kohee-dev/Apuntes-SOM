---
Author: Alejandro Bartolomé
Title: Scripting Básico
---

Los Scripts son ficheros que contienen una secuencia de ordenes que serán ejecutadas en orden por parte del Sistema Operativo.

Estas ordenes incluiran una serie de instrucciones y comparaciones que nos permiten resolver un problema determinado.

Soy consciente de la dificultad de estos ejercicios pero si le dedicais una hora al dia podeis resolverlos sin problema.

# Editor
---

Para crear un Script deberemos editar un fichero de texto sencillo. Algunos de los editores más conocidos son los siguientes.

- notepad
- nano
- vim
- gedit
- vscode

Recomiendo utilizar nano para los ejercicios.

# Creando un Script

Primero crearemos un Script sencillo.

Para ello crearemos un directorio y allí haremos las prácticas. 

````shell
$ mkdir ~/scripts
$ nano MiPrimerScript.sh
````

Nos creará una carpeta scripts en nuestro directorio personal y allí crearemos un fichero llamado `MiPrimerScript.sh`

Una vez se nos abra el editor nano crearemos el programa más famoso de todos los tiempos: el ["**Hello World**"](https://en.wikipedia.org/wiki/"Hello,_World!"_program)

Para crear un script, siempre deberá comenzar por la siguiente linea.

````
#!/bin/bash
````

De esta forma escogeremos el interprete que se encargará de ejecutar el programa. En este caso, el interprete es "bash".

Luego pondremos todas las instrucciones necesarias para escribir por pantalla un mensaje que diga "Hello World" y terminaremos con exit 0 para asegurar al usuario que no ha habido ningun error. Con todas las instrucciones quedará lo siguiente.


````shell
#!/bin/bash

echo " Hello World "

exit 0
````

Si tenéis cualquier duda con algo del código avisadme sin problema.

Ahora guardaremos el fichero y actualizaremos los permisos para que tenga permisos de ejecución. Esto se puede hacer por cualquiera de las siguientes formas.

````shell
$ chmod +x MiPrimerScript.sh
$ chmod 700 MiPrimerScript.sh
````

Una vez hecho esto ya podemos ejecutar el código. Para ello lo haremos con el siguiente comando.

````shell
./MiPrimerScript.sh
````

# Teoría: Argumentos, Variables y Condicionales

## Argumentos

Los argumentos nos permiten introducir información al código cuando lo ejecutemos. Son una herramienta muy poderosa cuando queramos usar varios elementos que puedan variar de ejecución a ejecución.

Para utilizar un argumento bastará con emplear el carácter $ seguido de un numero, que indicara su posición en la llamada al script.

**Por ejemplo**

````shell
#!/bin/bash

echo "Hola $1"

exit 0
````

Con la llamada

````shell
$ ./hola.sh Alejandro
````

Tendrá la salida

> Hola Alejandro


Esto se debe a que en el echo estamos escribiendo Hola seguido por el argumento en primera posición, por lo tanto la salida del código será Hola y lo que indiquemos en la llamada a la función, en este caso Alejandro.

## Variables

Las variables nos permiten almacenar información durante el tiempo de ejecución de nuestro programa.

Para crearlas bastará con indicar el nombre de la variable y seguido su valor. Luego, para acceder a su valor tendremos que poner $ y el nombre de la variable.

**Por ejemplo**

````shell
#!/bin/bash

variable=mundo
variable2=hola

echo "$variable2 $variable"

variable2=Adios

echo "$variable2 $variable"
````

El siguiente código tendrá la salida.

````shell
hola mundo
Adios mundo
````

## Condicionales

Los condicionales nos permiten modificar el flujo de ejecución del programa. Por lo general, la estructura es la siguiente. 

````shell

if [condición]
then
    #instrucciones
elif [condición2]
then
    #instrucciones
elif [condición3]
then
    #instrucciones
.
.
.
else
    #instrucciones
fi

````

Al llegar a esta estructura el programa realizará las instrucciones indicadas por la parte cuya condición sea cierta.
Si ninguna condición se cumple nunca se realizarán las instrucciones dentro del else.

# Scripting en Arcilla

[Lectura recomendada](https://www.hplovecraft.com/writings/texts/fiction/cc.aspx)

Acabas de ser contratado como detective privado en Rhode Island para investigar la muerte del conocido profesor George Gammel Angel de la Universidad de Brown. Aunque los testigos afirman que fue asaltado cerca del puerto, su nieto sospecha que pudo haber algo más.

# Warnings

+ Soy consciente de la dificultad de esta práctica, pero es importante que la intentéis terminar por vuestro propio pie, de esta forma sabré establecer la dificultad del examen correctamente

+ Supongo que sabéis leer y prestar atención durante la lectura de oraciones larga. Intentad comprender el enunciado y realizar los ejercicios.

+ Soy conocedor de cualquier tipo de ayuda externa o *mythos* que podáis usar. No os arriesguéis.

+ Cualquier uso indebido de este ejercicio supondrá un 0 en la práctica.

+ Estos ejercicios son muy parecidos a los realizados previamente, y muy similares a los que realizareis en el examen. 

+ Las rutas son muy importantes, no seguirlas supondrá un 0 en la práctica.

## Misión I

Crea un script `MisiónI.sh` en el directorio `~/smr/som/scripts/dia1`. Este script deberá comprobar si existen los siguientes ficheros:

+ `CTHULLU CULT.txt`, si no existe deberá crearlo y escribir lo siguiente en su interior. 

````
1925—Dream and Dream Work of H. A. Wilcox, 7 Thomas St., Providence, R.I.

Narrative of Inspector John R. Legrasse, 121 Bienville St., New Orleans, La., at 1908 A. A. S. Mtg.—Notes on Same, & Prof. Webb’s Acct.
````

+ `Atlantis and the Lost Lemuria`, si no existe deberá crearlo y escribir lo siguiente en su interior.

```
By W. Scott-Elliot
```

## Misión II

Puesto que la lectura de los ficheros puede llevar varios dias, realiza un script para ayudar con la investigación. El script `MisionII.sh` deberá poder aceptar 2 argumentos, el primero será la ruta a un fichero y el segundo una palabra.

+ Se deberá indicar el número de apariciones de la palabra en el fichero. 
+ Si el fichero no existe deberá mostrar el siguiente error: "Debo buscar en otro lado"

**Ejemplos de ejecución**
```
$ ./MisionII.sh /no/existe/esta/ruta hola
> Debo buscar en otro lado
```

```
$ ./MisionII.sh /home/alejandro/smr/som/bash/scripts/CTHULLU CULT.txt A.
> La palabra A. aparece 3 veces
```

## Misión III

La investigación ha sido larga, pero aún es necesario recopilar la información obtenida mediante un informe del dia, crea un script llamado `MisionIII.sh` que muestre la siguiente información:

+ Detective (Usuario)
+ Hora actual
+ Tiempo de trabajo (Uptime de la máquina)
+ Carga de trabajo (Cantidad de memoria RAM libre y Cantidad de espacio en disco libre)
+ Herramientas utilizadas (IP2 de la máquina (No la 127.0.0.x))
+ Documentos investigados (nº de ficheros en el directorio actual)

Todos los apartados deberán de mostrarse bajo un titulo personalizado.

**Ejemplo de ejecución**

```
$ ./MisionIII.sh

=== DETECTIVE ===
Alejandro

=== HORA ===
Thu Jan 30 18:53:30 UTC 2025

=== TIEMPO DE TRABAJO ===
...

```
