# El Script del Inspector Legrasse

*Duración aproximada: 1h*

Vais a continuar con el caso del profesor George Gammel Angel. Se han encontrado varias pistas en la pila de documentos que hay que descifrar cuya clave conocía unicamente el profesor. Para ayudarte con tu tarea se te ha puesto como compañero al inspector Lagresse.

# Warnings

+ Soy consciente de la dificultad de esta práctica, pero es importante que la intentéis terminar por vuestro propio pie, de esta forma sabré establecer la dificultad del examen correctamente

+ Supongo que sabéis leer y prestar atención durante la lectura de oraciones larga. Intentad comprender el enunciado y realizar los ejercicios.

+ Soy conocedor de cualquier tipo de ayuda externa o *mythos* que podáis usar. No os arriesguéis.

+ Cualquier uso indebido de este ejercicio supondrá un 0 en la práctica.

+ Estos ejercicios son muy parecidos a los realizados previamente, y muy similares a los que realizareis en el examen. 

+ Las rutas son muy importantes, no seguirlas supondrá un 0 en la práctica.

## Misión I

Se ha descubierto que el profesor estaba observando los semáforos cerca del rio Providence. Existen 3 puentes que conducen a la Universidad los cuales están regulados por semáforos. Los semáforos están gestionados por un Manicomio cercano de Main Street. 

El profesor tiene unas notas exhaustivas indicando que cuando un semáforo se establece en verde, el resto se pone en rojo. Tras una investigación, se ha encontrado el siguiente script que se encarga de la gestión de los semáforos.

El inspector Lagresse te pide que arregles el script para que cumpla con la función indicada.

`/smr/som/scripts/dia2/mision1.sh`

```bash
#!/bin/bash

SEMAFORO_1="AMBAR"
SEMAFORO_5="AMBAR"
SEMAFORO_9="AMBAR"

echo "Bienvenido al sistema de Gestión de Trafico"
sleep 1
echo "---> Accediendo a Main Street"
sleep 0.5
echo "Indique que semáforo desea establecer a Verde"
echo "- 1"
echo "- 5"
echo "- 7" 
echo -n "Numero de semáforo ? : "
read SEMAFORO_ACTUAL


###
# FRAGMENTOS PERDIDOS
###

echo "Semáforo de la calle 1 : $SEMAFORO_1"
echo "Semáforo de la calle 1 : $SEMAFORO_5"
echo "Semáforo de la calle 1 : $SEMAFORO_9"

exit 0
```

## Misión II

Siguiendo la investigación en Main Street, se puede encontrar unos almacenes donde se almacenan varios contenidos provenientes de Boston. No tardáis en descubrir que varios almacenes pertenecen al Manicomio cercano. Siguiendo las notas del profesor el inspector Lagresse ha localizado los 3 almacenes.

Todos tienen un horario muy estricto permitiendo unicamente su acceso durante 5 minutos. Se adjunta un horario. 

| Minutos |Almacén |
|-|-|
|0-4 | Rus |
5-9| Netro
10-14|Cronte
|15-19 | Rus |
20-24| Netro
25-29|Cronte
|30-34 | Rus |
35-39 |Netro
40-44|Cronte
|45-49 | Rus |
50-54| Netro
55-59|Cronte

El script deberá comprobar que hora es y en función de dicha hora que almacén esta activo

Con el fin de comprobar que almacén esta activado habrá que usar un enlace simbólico y cuando se deba quitar el acceso habrá que borrar dicho enlace. 

`/smr/som/scripts/dia2/mision2.sh`
```bash
#!/bin/bash

mkdir -p $HOME/Providence/Hangares/Rus
mkdir -p $HOME/Providence/Hangares/Netro
mkdir -p $HOME/Providence/Hangares/Cronte

#### 
## FRAGMENTOS PERDIDOS
###

ls -l $HOME/Providence/Hangares/Habilitado

exit 0
```
