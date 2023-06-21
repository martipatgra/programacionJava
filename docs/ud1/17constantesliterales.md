# 💾 Constantes y literales

## Las constantes

Un programa puede contener ciertos valores que no deben cambiar durante su ejecución. Estos valores se llaman constantes.
Definición: Una constante es una zona de memoria que se referencia con un identificador, conocido como nombre de la constante, donde se almacena un valor que no puede cambiar durante la ejecución del programa.

La nomenclatura para definiar las constantes es la siguiente:

+ Todas las letras de cada palabra deben estar en mayúsculas
+ Se separa cada palabra con un _
+ Se declaran similar a las variables, con la diferencia de que el tipo de dato va después de la palabra reservada **final**

```java
    final double PI = 3.141591;
    final int MIN_WIDTH = 4;
    final double TASAS = 0.045;
```

Las constantes hacen que el programa sea más fácil de leer y verificar que sea correcto.
Si es necesario cambiar una constante (por ejemplo, si cambian las tasas), todo lo que tendremos que hacer es cambiar la declaración de la constante. No será necesario buscar en todo el programa cada aparición de ese número específico.

## Los literales

Un literal Java es un valor de tipo entero, real, lógico, carácter, cadena de caracteres o un valor nulo (null) que puede aparecer dentro de un programa.
Por ejemplo: 150, 12.4, “ANA”, null, ‘t’.
Los literales suelen aparecer en la asignación de valores a las variables o formando parte de expresiones aritméticas o lógicas.

![Java](../img/literals.png)
