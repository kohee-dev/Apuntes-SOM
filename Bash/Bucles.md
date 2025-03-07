En Bash tenemos 3 formas de hacer bucles: For, While y Until. En este documento vamos a aprender como hacer cada una de ellas.

# For

Hay varias formas de establecer un bucle for, pero todas ellas funcionan de la misma forma: Todo lo que esté dentro del bucle se va a repetir un numero de veces (iteraciones) establecidos por una condición.

## Bucles for (Al estilo C)

````bash
for (( inicializar; condición; incremento ))
do
    #Comandos
done
````

En este caso se establece un punto de *inicio* que tendrá que alcanzar la *condición* indicada por medio del *incremento*. Por verlo en un ejemplo

```bash
for (( i=0 ; i < 10 ; i++ ))
do
    echo "Hola"
done
```

De esta forma diremos hola 10 veces, porque i comienza en 0 e incrementará de 1 en 1 ***(i++)*** hasta llegar a 10.

## Bucles for (Usando listas)

Esta forma es especialmente util cuando se emplean listas de archivos o cadenas. La sintaxis es la siguiente:

```bash
for i in [LISTA]
do
    #Comandos
done
```

De esta forma el bucle tendrá tantas iteraciones como elementos haya en la lista. Por ejemplo:

```bash
for i in  0 1 2 3 4 5 6 7 8 9
do
    echo "Hola"
done
```

Este bucle hará lo mismo que el anterior.

Otra cosa a tener en cuenta es que esta última forma nos permite hacer bucles mucho más útiles puesto que también podemos, por ejemplo, recorrer todos los archivos y directorios de un directorio especifico.

```bash
for i in $(ls /var/smr/*)
do
    echo $i 
done
```

## Bucles for (mixtos)

Esta forma nos permite crear una lista para recorrer como nosotros le indiquemos, usando una sintaxis muy parecida a la de C. Para usarlos se escribe de la siguiente forma

````bash
for i in {inicio..fin..incremento}
do
    #Comandos
done
````

Incluso si no indicamos el incremento irá desde el primer numero al segundo de uno en uno. Por ejemplo:

```bash
for i in {0..9}
do
    echo "Hola"
done
```
Hace lo mismo que antes

```bash
for i in {0..10..2}
do 
    echo "Hola"
done
```
Sería equivalente a poner 0 2 4 6 8 10 después del **in**


# While

El bucle While es mucho más intuitivo que el for en el sentido que unicamente hay que establecer una condición y mientras la condición sea **VERDADERA** se va a repetir su contenido de forma indefinida. La sintaxis es la siguiente:

```bash
while [condición]
do
    #Comandos
done
```

Por ejemplo

```bash
#!/bin/bash

num=1
while [ $num -le 10 ]
do
    echo $((3*$num))
    num=$(($num+1))
done
```
Nos dirá la tabla del 3 puesto que estaremos imprimiendo por pantalla 3x1, 3x2, 3x3, y asi sucesivamente hasta 3x10

# Until

El bucle until es exactamente igual que el bucle while con la diferencia de que se ejecutará mientras la condición sea **FALSA**. Aquí dejo la sintaxis

```bash
until [ condicion ]
do
    #Comandos
done
```
A continuación os pongo el mismo ejemplo de antes

```bash
#!/bin/bash

num=1
until [ $num -gt 10 ]
do
    echo $((3*$num))
    num=$(($num+1))
done
```

# Arrays

Los Arrays son una forma de almacenar información dentro de una variable. De momento no nos interesa saber mucho de ellos, pero la forma de recorrerlos es la siguiente.

```bash
#!/bin/bash

primos=(2 3 5 7 11 13 17 19 23 29)

for i in "${primos[@]}"
do
    print $i
done
```

Se accede a sus elementos por medio del valor entre los corchetes, pero al recorrerlos hay que usar @. Repito que volveremos a este punto más adelante.