En Bash se pueden hacer operaciones matemáticas sencillas, aunque únicamente se puede operar con números enteros. Tenemos varios métodos.

# `let`

Se pueden hacer operaciones usando la palabra reservada let

```bash
let suma=2+3
echo $suma
```

# Dobles paréntesis

También podemos usar *(())* para realizar las operaciones.

```bash
echo $((a=2+3))
```
También podemos introducir operaciones dentro de otras operaciones.

```bash
echo $((2 + $((2+3))))
```

# `bc`

bc es una herramienta que funciona como una calculadora científica y tiene la ventaja de que nos permite trabajar usando números reales. Es una herramienta muy completa que nos permite crear condicionales, bucles, etc. Aunque en este fichero vamos a ver unicamente las operaciones que deberéis utilizar en el trabajo.

Si queremos hacer una operación es suficiente con poner esta estructura, bc ya establecerá los decimales en función de los números introducidos. Si ponemos un decimal, el resultado tendrá un decimal, con dos decimales, dos y así.

```bash
z=$('2.1*3.4' | bc)
echo $z
```

En el trabajo *(../Administración/Añil.md)* os encontrareis con un punto donde tendréis que dar un valor entre 0.75 y 1.25. Hay varias formas pero la idea es la siguiente.
Generáis un numero positivo aleatorio entre 0 y 50, una vez ha sido generado lo multiplicáis por 0.01 (dividir entre 100) y se lo sumáis a 0.75.
Con esa expresión generareis el número que necesitáis.

