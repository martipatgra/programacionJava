# Colecciones ordenadas

Vamos a estudiar una variante del `HashMap` y `HashSet`, el `LinkedHashMap` y `LinkedHashSet`.

También están las versiones ordenadas del `HashMap` y el `HashSet` que son `TreeMap` y `TreeSet`.

Como las operaciones entre `Map` y `Set` son muy similares nos centraremos en los mapas.

## `LinkedHashMap`

La clase `LinkedHashMap` es como `HashMap` con una característica adicional de **mantener el orden de elementos insertados en ella**.

`HashMap` proporciona la ventaja de una rápida inserción, búsqueda y borrado, pero NO mantiene el orden en el que se insertan los elementos. Con `LinkedHashMap` se puede acceder a los elementos en su orden de inserción.

### Características

+ Un LinkedHashMap contiene valores basados en la clave.Implementa la interfaz del mapa y extiende la clase HashMap.
+ Contiene solo elementos únicos.
+ Solo puede tener una clave nula pero varios valores nulos.
+ Es lo mismo que `HashMap` con una característica adicional que mantiene el orden de inserción.

Los datos se almacenan en forma de nodos. La implementación de `LinkedHashMap` es muy similar a una lista doblemente enlazada. Por lo tanto, cada nodo del LinkedHashMap está representado como:

![OrderCollections](../img/ud6/linkedhashmap1.png)

+ **Hash**: Todas las claves (keys) de entrada se convierten en un hash, que es una forma más corta de la clave para que la búsqueda y la inserción sean más rápidas.
+ **Key**: Dado que esta clase extiende `HashMap`, los datos se almacenan en forma de par clave-valor. Este parámetro es la clave de los datos.
+ **Value**: Para cada clave, hay un valor asociado con él.
+ **After**: Dado que LinkedHashMap almacena la orden de inserción, contiene la dirección al siguiente nodo de la lista.
+ **Before**: Este parámetro contiene la dirección al nodo anterior de la lista.

## `TreeMap`

Java TreeMap es una estructura de datos que implementa la interfaz `Map<Key,Value>`, se basa en un árbol binario y **ordena por clave**.

`TreeMap` es una implementación de Map que mantiene sus entradas ordenadas según el orden natural de sus claves. Para números significa orden ascendente, para cadenas, orden alfabético. Sin embargo, es posible utilizar un comparador si necesita cambiar la lógica.

`HashMap` le permite almacenar una clave nula y varios valores nulos. `TreeMap` ordena los elementos en orden natural y no permite claves nulas porque el método `compareTo()` arroja `NullPointerException` si se compara con nulo.
