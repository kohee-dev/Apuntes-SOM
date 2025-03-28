En Bash podemos crear funciones. Las funciones son una estructura que nos va a permitir ahorrar tiempo y trabajo puesto que podemos reutilizar el código sin tener que repetirlo una y otra vez. Esto de no repetir código es una práctica recomendada asi que utilizar funciones es algo muy importante. 

*¿Por que es una practica recomendada?* 

Si has repetido código en varias partes de tu proyecto y tienes un error tienes que solucionarlo en todas las partes donde has cometido dicho error, pero si esa **funcionalidad** esta dentro de una función, de pronto toda la tarea de solucionar errores se vuelve mucho más sencilla.

# Declarar Funciones

Para poder declarar una función bastaría con la siguiente pieza de codigo.

```bash
mi_primera_funcion(){
    #Esta funcion dice hola mundo
    echo "Hola Mundo"
}
```

También se pueden declarar de otras formas, como todo en una misma línea o el nombre precedido de la palabra clave `function` pero esta es la más sencilla.

# Uso de Funciones

Para usar una función es suficiente con escribir el nombre de la función para ejecutar todo lo que se encuentra entre llaves.

```bash
mi_primera_funcion
```

La ultima ejecución me diría "Hola Mundo"

# Puntos importantes

Hay dos cosas que hay que tener en cuenta cuando usemos funciones.

* Declarar una función y ejecutar una función son dos acciones distintas. Si declaramos una función no se va a ejecutar hasta que la llamemos en el código.

* Primero hay que declarar una función y luego se puede llamar. No se puede utilizar una función antes de que se haya declarado.


# Ámbito de las variables

¿Recordamos todos el uso de variables verdad?

Las funciones también pueden hacer uso de las variables definidas en el código, pero tienen una palabra reservada `local` que les permite utilizar una variable únicamente dentro de la función. 

A continuación os propongo un ejemplo para que lo veais bien.

```bash
#!/bin/bash

var1="fuera"
var2="fuera"

funcion_variables(){
    var1="dentro"
    local var2="dentro"
    var3="dentro"
    local var4="dentro"
    echo $var1 $var2 $var3 $var4
}

echo $var1 $var2
funcion_variables
echo $var1 $var2 $var3 $var4

```

*¿Que resultado sale? ¿Por que sale ese resultado?*

Es importante que tengáis muy en mente el ámbito de las variables porque de lo contrario os va a causar más de un quebradero de cabeza cuando estéis buscando fallos en vuestro código.

# Argumentos

Las funciones pueden recibir argumentos.

Por ejemplo:

```bash
#!/bin/bash

suma(){
    local resultado=$(($1+$2))
    echo $resultado
}
resultado=$(suma 2 3)
echo $resultado
```

Ademas de los habituales, podemos emplear los siguientes argumentos en nuestro código.

- `$#`: Representa el número de argumentos
- `$0`: Representa el nombre del script
- `$1`-`$9`: Los 9 primeros argumentos
- `$@`: Todos los argumentos que se han pasado al script
- `$?`: La salida del ultimo proceso que se ha ejecutado
- `$$`: El ID del proceso.

# Devolver salidas

Pongamos el ejemplo previo de suma. Quiero que la función me diga cual es el resultado de la operación.

Hay varias formas de hacer esto

### Return

La palabra reservada return nos permite devolver un valor entre 0 y 255. Principalmente se utiliza para determinar que tal ha ido la ejecución del programa y debería ser utilizada para ello.

Si queremos obtener el valor que hemos devuelto por return bastaría con usar `$?`

### Variables Globales

Es una práctica habitual, el mayor problema que tienen es que con un código complicado o con muchos ficheros puede llegar a incrementar su complejidad bastante.

### Variables locales

Esta es la forma que utilicé en `suma` y la que vamos a emplear nosotros en clase. Devolvemos la salida que queremos con un echo y la guardamos en una variable lista para ser usada.

# Reutilizar

Por supuesto, la idea de las funciones es no tener que volver a escribir el código una y otra vez. Para ello tenemos una palabra reservada `source` que nos ofrece una solución para esto.

Supongamos que la función `suma` se encuentra en el fichero `suma.sh`.

Si yo tuviese que utilizar la función suma en otro código distinto tendría que hacer lo siguiente. 

```bash
source ./suma.sh

echo $(suma 2 3)
```

Y así podría continuar usando la función que tanto me costó hacer previamente.





