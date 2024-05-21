## Code


```
### [python](https://www.python.org/)  
<img style="float: left;" src="https://upload.wikimedia.org/wikipedia/commons/9/95/Saccharomyces_cerevisiae_SEM.jpg" width = 30%> <br>
```

```
from IPython.core.display import Image, display
display(Image('descargas/bio.jpg', width=300, unconfined=True))
```


#########################

```
## Funciones integradas

|Función|Descripción|
|---|---|
|`set()`|Devuelve un conjunto|
|`dict()`|Devuelve un diccionario|
|`help()`|Da información sobre módulos|
|`min()`|Devuelve el valor mínimo de una lista, arreglo o Dataframe|
|`dir()`|Devuelve las variables definidas|
|`enumerate()`|Enumera una lista empezando por cero|
|`input()`|Función interactiva para ingresar valores|
|`int()`|Devuelve núemros enteros|
|`str()`|Devuelve un string o cadena de caracteres|
|`sum()`|Suma los valores de una lista o arreglo|
|`pow()`|Devuelve un valor elevado a la potencia X|
|`float()`|Devuelve un número de punto flotante|
|`print()`|Imprimir una variable|
|`tuple()`|Devuelve una tupla (una lista inmutable)|
|`len()`|Devuelve la longitud de un objeto|
|`type()`|Devuelve el tipo del objeto|
|`list()`|Devuelve una lista|
|`range()`|Devuelve un rango de números|
|`zip()`|Vuelve iterables dos elementos iterables|
|`reversed()`|Devuelve el reverso de una lista|
|`max()`|Devuelve el valor máximo de una lista, arreglo o Dataframe|
|`round()`|Redondea un número de punto flotante|


#### Al definir variables tratar de no usar algún nombre de las funciones integradas, porque si después se desea usar la función original esto genera un error porque la función ya no existe
```


#----------------------------------------------------------------------------------------

```
# <font color = red>Ejercicio:</font>
* ### 1. En seguida se definen algunas variables con varios objetos.
* ### 2. Usando las funciones `print()` y `type()`, imprime e identifica qué tipo de objeto contienen las variables, la respuesta escríbela como un comentario 
* ### 3. Cuál es la longitud de la secuencia de nucleótidos
* ### 4. Cúal es el resultado de sumar la variable6 con la variable11
* ### 5. A qué organismo lleva el enlace de lavariable10, cuántos aminoácidos tiene la proteína que muestra y cuántos nucleótidos.
```

```
variable1 = 3.141592653589793
variable2 = 100
variable3 = {'peptide1':'MTTNEEFIRTQIF', 'peptide2':'GTVFEITN', 'peptide3':'RYNDLNPVG'}
variable4 = '100.01'
variable5 = 'atgaccactaacgaggaattcattaggacacagatattcggtacagttttcgagatcacaaatagatacaatgatttaaaccccgt'
variable6 = [1.1, 2.1, 3.0, 4.0, 5.2, 6, 2, 6.5, 10, 3]
variable7 = sum(variable6)
variable8 = set(variable5)
variable9 = int(pow(5.2, 4) - 0.1616000000001)
variable10 = 'https://www.genome.jp/dbget-bin/www_bget?sce:YLR113W'
variable11 = (1.1,2.1,3.0,4.0,5.2,6)
```



```
# Comparaciones
|Operation|Meaning|
|---|---|
|`<`|strictly less than|
|`<=`|less than or equal|
|`>`|strictly greater than|
|`>=`|greater than or equal|
|`==`|equal|
|`!=`|not equal|
|`is`|object identity|
|`is not`|negated object identity|

#### Los resultados boleanos siempre devuelven `False` o `True`
```
