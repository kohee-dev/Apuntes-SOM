En bash hay varias estructuras de datos. Hoy vamos a ver las Listas y los Diccionarios.

# Listas

Como su nombre indica, una lista es un conjunto de elementos. Para entenderlo bien vamos a usar como ejemplo una lista de la compra.

<center>

|Lista de la compra|
|:-:|
|Tomates|
|Patatas|
|Carne picada|
|Pimientos|
|Pimienta|
|Cebollas|

</center>

Como podéis ver tenemos un titulo (lista de la compra) seguido de un conjunto de elementos.

En Bash una lista *(o array)* es muy parecida, hay varias formas de definirlas pero vamos a utilizar por ahora la más sencilla.

```bash
lista_compra=('Tomates' 'Patatas' 'Carne Picada' 'Pimientos')

```

Con esa estructura ya tendríamos creada una lista en Bash.

## Otras formas de definir arrays

Como he mencionado antes, hay más formas de definir arrays. Aunque la primera la más sencilla, es importante conocer el resto de formas.

### Forma 1: Variable a variable.

Podemos definir una lista definiendo cada uno de sus elementos

**Por ejemplo**

```bash
lista_compra[0]=Tomates
lista_compra[1]=Patatas
```

### Forma 2: Mediante palabra clave.

Podemos utilizar la palabra clave `declare`.

**Por ejemplo**

```bash
declare -a lista_compra=('Tomates' 'Patatas' 'Carne Picada' 'Pimientos')
```

### Forma 3: Directamente.

También podemos hacerlo directamente

**Por ejemplo**

```bash
lista_compra=('Tomates' 'Patatas' 'Carne Picada' 'Pimientos')
```

E incluso puedo evitar poner comillas.

**Por ejemplo**

```bash
lista_compra=(Tomates Patatas Carne\ Picada Pimientos)
```

Podeis fijaros en que he puesto `\` para asegurarme que Carne Picada sea un elemento y no dos distintos.

## Obtener elementos de arrays

Si quisiésemos acceder a los distintos elementos de una lista bastaría con lo siguiente.

```bash
echo ${lista_compra[0]} #Tomates
echo ${lista_compra[1]} #Patatas
```

Aunque también puedes hacer 

```bash
echo $lista_compra #Tomates
```

Pero solo obtendrías el primer elemento de la lista.

Asi que la pregunta que nos tendríamos que hacer es la siguiente: ¿Como consigo todos los elementos de una lista?

Aquí entran en juego los bucles:

Si quisiese acceder a todos los elementos que tengo guardados en una lista tendría que usar la siguiente instrucción.

```bash
for i in "${lista_compra[@]}"
do
    print $i
done
```

Podéis hacer la prueba sin comillas en el array, ¿Que diferencia hay?

### Obtener más elementos de arrays

Por supuesto, no es la única forma de acceder a los elementos de un array, también se pueden devolver varios de golpe si utilizamos la siguiente instrucción.

```bash
echo ${lista_compra[@]:1:3}
```

Con esta instrucción devolveremos los elementos desde la posición 1 a la posición 3.

O también podemos hacer lo siguiente:

```bash
echo "Jaque"
echo ${lista_compra[0]:2:4}
```

¿Cual es la salida? ¿Por qué?

## ¿Cuántos elementos tiene mi array?

Para saber cuantos elementos hay de algo en Bash basta con usar `#` asi que si quieres saber cuantas cosas tienes en tu lista basta con seguir el siguiente ejemplo:

```bash
echo ${#lista_compra[@]}
```

Aunque también puedes conocer cuantas letras tiene cada elemento si en lugar de usar `@` te refieres a algún elemento del array.

## Operaciones con Arrays

### Adición

Siempre se pueden añadir nuevos elementos a un array, eso se puede hacer de la siguiente forma

```bash
lista_compra=(Cebollas "${lista_compra[@]}") #Al principio
lista_compra=("${lista_compra[@]}" Pimienta) #Al final
lista_compra=("${lista_compra[@]:0:2}" Atún "${lista_compra[@]:3}") # Despues del 3er elemento
```

### Borrado

También se pueden quitar elementos de un array, y se puede hacer de dos formas:

```bash
unset lista_compra[1] #Elimina el segundo elemento
lista_compra=(${lista_compra[0]} ${lista_compra[@]:2}) # Elimina el segundo elemento
lista_compra=(${lista_compra[@]/Cebolla/}) # Elimina cebolla de la lista
```

### Reemplazo

Para reemplazar basta con realizar la siguiente instrucción

```bash
echo ${lista_compra[@]/Cebolla/Cebollino} #Cambia cebolla por cebollino
```

Probad las distintas formas. ¿Hay alguna que os guste más? ¿Tiene algún inconveniente?

## Más operaciones

### Conseguir los n primeros términos de un array

```bash
lista_pequeña=${lista_compra[@]::n} #Cambiad n por los elementos que necesiteis
```

### Conseguir los n últimos términos de un array

PD: No os asusteis, tiene sentido
```bash
lista_pequeña=(${lista_compra[@]:$((${#lista_compra[@]}-n))}) #Cambiad n por los elementos que necesiteis
```
Es exactamente igual, con la diferencia que necesitamos primero saber el numero de elementos del array para cogerlos a partir de ahi.

Si os sirve de ayuda `array_nuevo = array:elementos-n`

### Borrado

Para borrar un array basta con la siguiente instrucción.

```bash
unset lista_compra
```

# Diccionarios

Un diccionario es similar a una lista con el detalle de que le podemos asignar un valor a cada elemento. Funciona exactamente igual que un diccionario, buscas una palabra y te devuelve su significado.

Volviendo al ejemplo de la lista de la compra, supongamos que ponemos el precio de cada producto.

<center>

|Lista de la compra| Precio|
|:-:|:-:|
|Tomates|5
|Patatas|6
|Carne picada|2
|Pimientos|1
|Pimienta|0.5
|Cebollas|3

</center>

A diferencia de los arrays hay que declararlos de forma explicita pero tienen una gran ventaja frente a los anteriores.

```bash
declare -A lista_compra #Creamos un diccionario
lista_compra[Tomates]=5
lista_compra[Patatas]=6
lista_compra[Pimientos]=1
```

De esta forma estableces una relación clave-valor entre los distintos elementos del diccionario.

Ahora si quieres mostrar un valor podemos hacer lo siguiente

```bash 
echo ${lista_compra[Tomate]} #5
```

Y para obtener todas todos los elementos podemos hacer lo siguiente

```bash
echo ${lista_compra[@]} #Muestra todos los valores
echo ${lista_compra[*]} #Igual que el anterior

echo ${!lista_compra[@]} #Muestra todas las claves
echo ${!lista_compra[*]} #Igual que el anterior
```

## Iterar por un diccionario

Si quieres recorrer todos los valores de un diccionario puedes hacerlo de esta forma. Es particularmente útil para determinar, por ejemplo, el coste total de la compra
```bash
for i in ${lista_compra[@]}
do
    echo $i
done
```

Luego también se puede iterar por las claves de la siguiente manera.

```bash
for i in ${!lista_compra[@]}
do
    echo "El precio de $i es ${lista_compra[$i]}"
done
```

## ¿Cuántos elementos tiene mi diccionario?

```bash
echo ${#lista_compra[@]}
```

## Operaciones con diccionarios

### Eliminado

Si quieres eliminar una pareja clave-valor se hace con la siguiente instrucción

```bash
unset lista_compra[Tomate]
```

### Adición

Si quieres añadir un nuevo valor a un array se puede hacer como al principio, aunque tambien se puede hacer de esta forma para añadir varios de forma simultanea

```bash
lista_compra+=([Pimienta]=0.5 [Cebollas]=3)
```

Si intentas añadir una clave que ya existe, lo que va a suceder es que vas a cambiar el valor que tiene asignado por el nuevo valor. Esto es bastante util.

```bash
lista_compra+=[Cebollas]=4
```

## Eliminar un diccionario

```bash
unset lista_compra
```

## Casos especiales

¿Y la carne picada?¿La esta ignorando? Si

Es posible definir una clave que contenga un espacio, pero al ejecutar el `unset` dará un error.

Esta es la forma de solucionarlo.

```bash
clave='Carne Picada'
unset lista_compra["$clave"]
```



