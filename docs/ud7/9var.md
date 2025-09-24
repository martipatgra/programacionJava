# Keyword var

`var` es una palabra clave introducida en Java 10 como parte de las mejoras en el sistema de inferencia de tipos para las variables locales. 

**El uso de var permite que el compilador infiera automáticamente el tipo de una variable en función del tipo de dato al que se asigna.** Esto puede hacer que el código sea más conciso y legible al reducir la redundancia en la declaración de variables.

Por ejemplo, antes de la introducción de var, podrías declarar una variable así:

```java
List<String> lista = new ArrayList<String>();
```

Con var, la declaración se simplificaría de la siguiente manera:

```java
var lista = new ArrayList<String>();
```
En este caso, el compilador infiere que lista es del tipo ArrayList<String> basándose en el tipo de dato utilizado en el lado derecho de la asignación.

## Consideraciones importantes en el uso de `var`

- **Inferencia de Tipo**. El compilador infiere el tipo de la variable en función del tipo de dato a la derecha de la asignación. No se puede utilizar `var` para variables de instancia de clases, parámetros de métodos, variables de array, o variables con valores null sin asignar.

- **Uso Responsable**. Se recomienda su uso con moderación y en situaciones donde el tipo es obvio o donde la inferencia de tipo mejora la legibilidad del código.

- **Código más Conciso**. Puede hacer que el código sea más conciso y eliminar la redundancia en declaraciones de variables.

```java
// Ejemplo de uso de var para eliminar la redundancia
List<String> nombres = Arrays.asList("Alice", "Bob", "Charlie");
for (var nombre : nombres) {//no repetimos que el tipo es String
    System.out.println(nombre);
}
```