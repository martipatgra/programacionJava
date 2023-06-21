# ♾️ Recursividad

**Un método recursivo es un método que se llama a sí mismo**. Un método iterativo es un método que usa un bucle para repetir una acción. En cierto sentido, la recursividad es una alternativa a las estructuras de control iterativas (en bucle).

Por ejemplo, tenemos el siguiente método iterativo:

```java
public void hola(int n) {
    for (int k = 0; k < n; k++) {
        System.out.println("Hola");
    }
} 
```

Una versión recursiva de ese método sería:

```java
public void hola(int n) {
    if(n > 0 ) {
        System.out.println("Hola");
        hola(n − 1); //Llamada recursiva
    }
}
```

Este método es recursivo porque se llama a sí mismo cuando _n_ es mayor que 0. Sin embargo, ten en cuenta que cuando se llama a sí mismo, pasa _n - 1_ como el valor de su parámetro. Si este método se llama inicialmente con n igual a 5, lo siguiente es una pila de lo que sucede. Las indentaciones indican cada vez que el método se llama a sí mismo:

```texto
hola(5)
    imprime "Hola"
    hola(4)
        imprime "Hola"
        hola(3)
            imprime "Hola"
            hola(2)
                imprime "Hola"
                hola(1)
                    imprime "Hola"
                    hola(0)
```

En el ejemplo anterior, es mucho menos eficiente llamar a un método cinco veces que repetir un bucle _for_ cinco veces. Las llamadas a métodos ocupan más memoria que los bucles e implican más sobrecarga computacional, en tareas como pasar parámetros, asignar almacenamiento para las variables locales del método y devolver los resultados del método.

!!! Note
    Los algoritmos y métodos iterativos son generalmente más eficientes que los algoritmos recursivos que hacen lo mismo.

## Recursividad como un enfoque de resolución de problemas

Dado que la recursividad no es realmente necesaria, si un lenguaje de programación tiene bucles, y no es más eficiente que los bucles, ¿por qué es tan importante?

Porque la recursividad es un enfoque eficaz para la resolución de problemas. Es una forma de ver un problema.

La recursividad se basa en dos conceptos clave de resolución de problemas: divide y vencerás y auto-similaridad. En la resolución de problemas recursivos, utilizamos la estrategia de divide y vencerás repetidamente para dividir un gran problema en una secuencia de problemas cada vez más pequeños hasta que llegamos a un problema que es prácticamente trivial de resolver. Lo que nos permite crear esta serie de subproblemas es que cada subproblema es similar al problema original, es decir, cada subproblema es solo una versión más pequeña del problema original.

La capacidad de ver un problema, por uno compuesto por problemas más pequeños y similares es el núcleo del enfoque recursivo.

## Parte recursiva y caso base

Una definición recursiva consta de dos partes: **una parte recursiva** que se repite y reduce el problema en una versión más pequeña del problema original, y un **caso base** o límite no recursivo, que define una condición límite y se utiliza para detener la recursividad.

Veamos esto con un ejemplo:

### EJEMPLO 1: Factorial: N!

Recordamos como se hacía el cálculo de n!:

n! = n * (n-1) * n(n-2) * .... mientras n > 0

Además, 0! se define como 1.

Ejemplos:

+ 4! = 4 * 3 * 2 * 1 = 24
+ 3! = 3 * 2 * 1 = 6
+ 1! = 1
+ 0! = 1

Como vemos en el ejemplo, podemos deducir que el factorial se repite en términos de (n-1) y el único caso donde no se calcula el factorial es 0!, esto nos lleva a que:

> n! = 1             --> if n = 0 //caso base
> 
> n! = n * (n-1)     --> if n > 0 //caso recursivo

De forma que el factorial de un número quedaría codificado de la siguiente forma:

```java
    public static int factorial(int n) {
        if (n <= 0) {
            return 1;
        } else {
            return n * factorial(n-1);
        }
    }
```

#### Traza

```texto
factorial(4)
    4 * factorial(3)
        3 * factorial(2)
            2 * factorial(1)
                1 * factorial(0)
                    return 1
                return 1 * 1 --> 1   
            return 2 * 1 --> 2
        return 3 * 2 --> 6 
    return 4 * 6 --> 24
return 24
```

### EJEMPLO 2: Verificar si un número es palíndromo

Un número es palíndromo si al leerse en ambos sentidos, tanto de izquierda a derecha como de derecha a izquierda, se obtiene el mismo número. Por ejemplo: 121, 1001, etc.

```java
public static int revertir(int n, int reverso) {
    if (n > 0) {
        int ud = n % 10;
        reverso = reverso * 10;
        return revertir(n/10, ud+reverso);
    } else {
        return reverso;
    }
}

public static void main (String[] args) {
    int reverso = revertir(121, 0);
    
    if (reverso == n)
        System.out.println("Son palíndromos.");
    else
        System.out.println("No lo son" );
}

```

### EJEMPLO 3: Revertir un String

Para revertir un String, nos quedamos con el primer carácter que iremos añadiendo al final de la recursividad, y vamos acortando el String para llegar al caso base.

```java
public static String reverseRecursive(String str) {
    if (str.isEmpty()) { //caso base
        return "";
    }
    return reverseRecursive(str.substring(1)) + str.charAt(0);
}
```
