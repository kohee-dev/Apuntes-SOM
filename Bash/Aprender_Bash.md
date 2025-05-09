Completa los siguientes ejercicios de Bash.

*Disclaimer*
Estos ejercicios están pensados para que os hagáis preguntas sobre el lenguaje, comenzando por un nivel muy bajo incrementando de forma progresiva en dificultad. Pensad que hay cosas que todavía no sabéis hacer y hay cosas que os van a resultar muy sencillas, pero es importante que paséis por todos los ejercicios.

El objetivo de esta tarea no es ser entregada, es ser resuelta. Intentad resolverla por vuestra cuenta. 

¡Mucho animo!

# Introducción; Dia I

## Comentarios y variables

### Ejercicio I

Haz un comentario de una línea que diga "Los comentarios hacen el código legible".

### Ejercicio II

Haz un comentario de varias lineas que diga:
"Los comentarios hacen el código legible
fácil de reutilizar y aportan información"

### Ejercicio III

Crea 4 variables: NOMBRE, APELLIDO, EDAD y NACIONALIDAD. Asignale los valores correspondientes y muéstralas por pantalla.

### Ejercicio IV 

Crea una variable que sea NOMBRE_COMPLETO. Asignale tu nombre y apellidos.

### Ejercicio V

Crea la variable NUMEROS. Asignale "1    2   3  4 5" y muéstrala por pantalla.

## Variables de entorno

### Ejercicio VI

Utiliza un `echo` para mostrar la definición de las variables de entorno.

### Ejercicio VII

Muestra la shell que esta usando el usuario.

### Ejericio VIII

Muestra el directorio de trabajo.

### Ejercicio IX 

Muestra la ruta del directorio HOME.

### Ejercicio X 

Muestra el nombre del usuario.

## Comillas

### Ejercicio XI

Crea una variable que contenga lo siguiente: "Estoy entre comillas dobles"

Ahora muestra la variable en un `echo` cuyo contenido se encuentre entre comillas dobles (`"`) y en otro con comillas simples (`'`).

## Repaso

### Ejercicio XII

Crea dos variables MI_EDAD y TU_EDAD. Asignales los valores para que muestre lo siguiente:
```bash
"Tengo 75 años
Y tu tienes 40 años"
```

### Ejercicio XIII

Declara dos variables y no les asignes valores.

# Condicionales; Dia II

## Comparaciones de valores.

### Ejercicio XIV

Comprueba si dos variables son iguales.

### Ejercicio XV

Comprueba si dos variables no son iguales.

### Ejercicio XVI

Indica, de dos variables, cual es la mayor.

### Ejercicio XVII

Indica, de dos variables, si la primera es mayor, menor o igual que la segunda.

### Ejercicio XVIII

Indica, de dos variables, cual de las dos es la menor y cuanta distancia hay entre ambas.

```Bash
$ diferencia 3 5

La variable menor es 3 y tiene una diferencia con 5 de 2.
```

## Comprobaciones de ficheros

### Ejercicio XIX

Comprueba si existe el fichero /tmp/hola.txt.

### Ejercicio XX

Comprueba si existe el fichero /tmp/adios.txt y si no existe crealo.

### Ejercicio XXI

Comprueba si existe el fichero ./script.sh. 
    
+ Si no existe créalo
+ Si existe realiza las siguientes comprobaciones:
    - Si el usuario tiene permisos de lectura.
    - Si el usuario tiene permisos de escritura.
    - Si el usuario tiene permisos de ejecución.

### Ejercicio XXII

Modifica los permisos por medio del modo octal o numérico de ./script.sh para que:
+ El usuario tenga permisos de lectura y escritura.
+ El grupo tenga permisos de lectura y ejecución.
+ El resto de usuarios tengan permisos de ejecución.

### Ejercicio XXIII

Modifica los permisos por medio del modo simbolico de ./script.sh para que:
+ Todos los usuarios puedan ejecutar.
+ El grupo lectura.
+ Solo el usuario pueda modificar el archivo.


### Ejercicio XXIV

Modifica el propietario del fichero ./script.sh a "nobody" y el grupo a "nogroup".

## Condiciones

### Ejercicio XXV

Crea 3 condiciones que sean verdaderas.

### Ejercicio XXVI

Crea 3 condiciones que sean falsas.


# Operaciones; Dia III

## Operaciones simples

### Ejercicio XXVII

Muestra la salida de $3 + 2$.

### Ejercicio XXVIII

Muestra la salida de $3 \times 2$.

### Ejercicio XXIX

Muestra la salida de $^3/_2$.

### Ejercicio XXX

Cual es la diferencia entre usar `let` y `(())`.

### Ejercicio XXXI

Usa `bc` para mostrar la salida de $^3/_2$ con un decimal.

## Operaciones

### Ejercicio XXXII

Crea un script que reciba 2 parámetros y los muestre por pantalla.

### Ejercicio XXXIII

Crea un script que reciba 2 parámetros y los sume.

### Ejercicio XXXIV

Crea un script que reciba 2 parámetros y los multiplique.

# Bucles; Dia IV

### Ejercicio XXXV

Crea un script que cuente del 1 al 10

### Ejercicio XXXVI

Crea un script que cuente del 10 al 1

### Ejercicio XXXVII

Crea un script que muestre el abecedario usando un bucle for

### Ejercicio XXXVIII

Crea una variable `casa="salon cocina baño habitacion"`

Utiliza un bucle para que la salida sea la siguiente. 

```bash
$ ./script.sh
salon cocina baño habitacion
```

Revisa que es IFS.

# Ejercicios Finales

### Ejercicio XXXIX

Usando el siguiente fichero:

file.txt
````
Esta es la linea 1
Esta es la linea 2
````

Utiliza un bucle para mostrar el contenido del fichero linea a linea

### Ejercicio XL

Crea un script que reciba una variable y diga si un string esta vacío o no.

*Reto* Intenta hacerlo sin usar else.

### Ejercicio XLI

Crea un numero aleatorio entre el 1 y el 10. *Utiliza la operación resto.*

### Ejercicio XLII

Crea un script llamado adivinar.sh que pida al usuario un numero, el numero deberá ser creado aleatoriamente. Si el usuario acierta, deberá salir un mensaje indicando que ha acertado, si falla deberá informar del error y pedir otro número.

### Ejercicio XLIII

Crea un script que recorra el directorio /home/user y diga si cada elemento es un fichero o un directorio.

### Ejercicio XLIV

Crea una función suma() que reciba 2 números y los sume.

### Ejercicio XLV 

Crea una función multiplicar() que reciba 2 números y los multiplique. Esta función tendrá que usar la función suma().

### Ejercicio XLVI

En un fichero diferente crea una función potencia() que reciba 2 números y eleve el primero al segundo. Esta función tendrá que usar la función multiplicar().

### Ejercicio XLVII

Muestra todos los ficheros ejecutables del directorio actual

### Ejercicio XLVIII

Muestra todos los ficheros con extension .sh del directorio actual.

### Ejercicio XLIX

Usando la instrucción date; crea una función que devuelva el dia de la semana que es.

date.sh
```bash
$ ./date.sh
Hoy es Viernes.
```


### Ejercicio L

Crea un generador de scripts. 

El script deberá pedir un nombre y crear un fichero con ese nombre y extension .sh, luego deberá poner "!/bin/bash" en la primera línea. Luego deberá modificar los permisos para que pueda ser ejecutado.