# Keyword Final

Generalmente, usamos la palabra reservada `final` para definir valores constantes. Pero en realidad, los campos o atributos finales no son constantes porque pueden modificarse. Pero **SOLO una vez y cualquier modificación debe realizarse antes de que finalice el constructor de la clase**.

Ejemplo:
Podemos asignarle final a un campo de la clase y declararlo por primera vez en el constructor.

```java
public class TestFinal {

    private final int numero;

    public TestFinal(int n) {
        numero = n;
    }
}
```

```java
public class TestFinal {

    private final int numero = 0;

    public TestFinal() {
    }
}
```

Ambos códigos hacen lo mismo.

Cuando declaramos un atributo como final, IntelliJ es listo y no nos deja implementar el método setter de ese atributo.

Cuando queremos crear una variable constante de la que ya conocemos su valor, normalmente usamos `static final` y la nombramos en mayúsculas. Pero una variable final que cambia para cada instancia de la clase, no se nombra en mayúsculas.

## Final en la definición de clase

Si añadimos la palabra `final` al crear una clase, lo que hacemos es **NO permitir que se pueda extender de esa clase**. Es decir, no puede tener hijos que hereden de ella.

Ejemplo:

```java
public final class Coche {

}
```

## Final en la definición de métodos

A veces queremos, heredar de una clase, pero **no queremos que se puedan sobreescribir o anular todos los métodos de la clase padre** en los hijos porque a lo mejor son métodos que tienen una cierta funcionalidad que no cambia. Es decir, queremos prevenir que modifiquen su comportamiento. Para realizar esto declaramos los métodos como final.

{++Los únicos métodos que no pueden declararse como final son los constructores, ya que no se heredan.++}

```java
class Perro {

    @Override
    public void mover() {
        
    }

}
public class Animal {

    public final void comer() {
        //este método no puede sobreescribirse en los hijos
    }

    public void mover() {
        //este método se puede sobreescribir
    }
}
```

## Bloque estáticos

El bloque estático se usa para inicializar las variables estáticas. Este bloque se ejecuta cuando la clase se carga en la memoria. Una clase puede tener varios bloques estáticos, que se ejecutarán en la misma secuencia en la que se escribieron en el programa. Se ejecutan antes que los constructores.

Los bloques estáticos de inicialización son equivalentes a los constructores.
Los constructores como bien sabemos son constructores de instancias de la clase, como no son estáticos, se ejecutan cada vez que se crea una nueva instancia de la clase.

Como hemos dicho, el equivalente a los constructores en su versión estática, son los bloques estáticos de inicialización, la diferencia es que el bloque estático SOLO se ejecuta una vez cuando se carga la clase.

Al igual que las variables finales pueden inicializarse en el constructor. Las variables estáticas finales pueden hacerlo en los bloques estáticos de inicialización.

```java
class Test {

   private static int num;
   private static final int x;

   static{
      num = 68;
      x = 9;
  }

}
```
