# Functions

En el apartado de [Expresiones lambda](2lambda.md) vimos como crear expresiones lambda a partir de un método definido por el programador. Esto se hacía utilizando la interfaz funcional `Function` que se encuentra del paquete `java.util.function`.

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```

`Function` recibe dos valores de distinto tipo cuando se crea el objeto, el método recibe un parámetro de entrada que coincide con el primer tipo específico y devuelve un valor del tipo especificado del objeto que coincide con el segundo valor.

```java
Function<Integer, String> function = num -> {
    if(num % 3 == 0 && num % 5 == 0){
        return num + " divisible entre 3 y 5";
    }else{
        return num + " no es divisible entre 3 y 5";
    }
};

System.out.println(function.apply(25));//devuelve un String
```

Si tenemos dos funciones y queremos usar el resultado de una para la siguiente función podemos concatenarlas utilizando `andThen`.

```java
Function<Integer, Integer> suma = x -> x + 2;
Function<Integer, Integer> mul = x -> x * 3;
Function co = suma.andThen(mul);
System.out.println(co.apply(4)); //imprime 18 = (4 + 2) * 3
```

## UnaryOperator

`UnaryOperator` es una interfaz funcional que extiende de `Function`.

```java
@FunctionalInterface
public interface UnaryOperator<T> extends Function<T, T> {
    static <T> UnaryOperator<T> identity() {
        return t -> t;
    }
}
```

`UnaryOperator` se crea con un tipo de dato, recibe un parámetro y devuelve un resultado del mismo tipo de su argumento.

```java
UnaryOperator<Integer> func2 = x -> x * 2;
int resultado = func2.apply(2);
System.out.println(resultado);//imprime 4
```

Existen también las interfaces derivadas `IntUnaryOperator`, `DoubleUnaryOperator`, etc.

## Resumen de las interfaces funcionales dentro de java.util.function

![Lambda](../img/ud7/7summary.png)
