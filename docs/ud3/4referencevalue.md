# 🌎 Paso de argumentos por valor y referencia

## Argumentos paso por valor

Un parámetro es un "mensaje unidireccional" que la persona que llama usa para enviar valores a un método.

Dentro del cuerpo de un método, un parámetro se usa como cualquier variable. Se puede utilizar en expresiones aritméticas, en sentencias de asignación, etc.

Sin embargo, los cambios realizados en el parámetro no tienen ningún efecto fuera del cuerpo del método. Un parámetro es una copia local de cualquier valor que la persona que llama haya pasado al método. Cualquier cambio realizado afectará solo a esta copia local.

Esto ocurre cuando se pasa una dato de tipo primitivo.

Por ejemplo:

```java
------Clase Cuenta
    public void cambiarCantidad(double cantidad) {
        cantidad -= 20;
    }
------------------Clase Main
    public static void main() {
        Cuenta cuenta = new Cuenta("Pepe", "pepe@gmail.com", "873463774");
        int cantidad = 50;

        cuenta.ingresar(cantidad);
        System.out.println(cantidad);//imprime 50
        cuenta.cambiarCantidad(cantidad);
        System.out.println(cantidad);//imprime 50
    }
```

_cantidad_ es el nombre de la variable para el valor 50 que se ha enviado al método cambiarCantidad(). Ese método cambia el valor de la cantidad, pero esto no tiene ningún efecto sobre ninguna otra variable fuera del método.

Cuando el método regresa a su llamador (main), el valor del parámetro cantidad se olvida.

**Una variable local** es una variable que se declara dentro del cuerpo de un método.

El alcance de una variable local comienza desde donde se declara y termina al final del bloque en el que se encuentra. Recuerde que un bloque es un grupo de declaraciones entre llaves, {}.

Así es como funciona el paso de parámetros por valor:

1. Cuando la persona invoca un método, es persona proporciona una lista de valores (los parámetros) en la lista de parámetros del método.
2. Cuando el método invocado comienza a ejecutarse, estos valores se copian en los parámetros formales o argumentos.
3. El método invocado utiliza los parámetros formales para acceder a estos valores copiados.
4. Cualquier cambio que realice el método en el valor contenido en un parámetro formal cambia solo esa copia.
5. El método invocado no puede utilizar un parámetro formal para enviar un valor a la persona que ha invocado el método.

Como hemos visto un cambio en un parámetro dentro del método no afecta a ninguna variable desde donde se invocó. Entonces, ¿cómo puede un método enviar un valor a la persona que lo invoca?

Para devolver un valor único a la persona que invoca, un método invocado puede utilizar la declaración de retorno **return** junto con el valor que se devolverá.

## Paso por referencia

Las referencias a objetos o variable de referencia pueden ser parámetros. Esto sigue siendo una llamada por valor, pero ahora el valor es una referencia de objeto. Esta referencia se puede utilizar para acceder al objeto y posiblemente cambiarlo.

```java
public class Test {

    public static void ingresarCienEuros(Cuenta cuenta) {
        System.out.println("El balance es " + cuenta.getBalance());
        cuenta.ingresar(100);
        System.out.println("El balance es " + cuenta.getBalance());
    }

    public static void main(String[] args) {
        Cuenta c = new Cuenta();
        System.out.println("El balance es " + cuenta.getBalance());
        ingresarCienEuros(c);
        System.out.println("El balance es " + cuenta.getBalance());
    }
}
```

Las variables de instancia pública de los objetos se pueden cambiar mediante cualquier método que tenga una referencia al objeto. Como se ha hecho en el ejemplo anterior en la variable de instancia _balance_.

## Resumen

Un parámetro formal es una variable en una declaración de método. Siempre consta de un tipo seguido de un identificador de variable. Un argumento es un valor que se pasa a un método a través de un parámetro formal cuando se invoca el método. Los parámetros de un método limitan el tipo de información que se puede pasar a un método.

1. El paso de parámetros siempre se realiza por valor.

2. Si el parámetro de un método es un tipo de datos primitivo, el método puede cambiar el valor contenido en su parámetro, pero ese cambio no tiene ningún efecto en otros lugares.

3. Sin embargo, si el parámetro de un método es una referencia a un objeto, el método puede usar la referencia para acceder al objeto y luego cambiar las variables de instancia del objeto (a menos que sean privadas o en un paquete diferente).

4. Por supuesto, incluso si un método tiene una referencia a un objeto, el objeto se puede cambiar solo si el objeto permite que se realicen cambios.
