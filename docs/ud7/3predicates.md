# Predicate

**Predicate** es una interfaz funcional que se encuentra en el paquete `java.util.function`. Mejora la capacidad de administración del código, ayuda a realizar pruebas unitarias por separado.

Se utiliza en expresiones lambda para comprobar si una condición dada es verdadera o falsa.

En lugar de pasar un booleano con valor true or false,  pasas una referencia de tipo Predicate para determinar de manera dinámica si una condición dada es verdadera, o falsa.

Esta es la estructura de la interfaz `Predicate`:

```java
@FunctionalInterface
public interface Predicate<T> {

    boolean test(T t);
}
```

Como vemos la interfaz `Predicate` utiliza los genéricos para poder decirle que tipo concreto vamos a utilizar.

Ejemplo:

```java
public class EjemploPredicate {
    public static void main(String[] args) {
        Predicate<String> checker = a -> a.startsWith("M");
        System.out.println(checker.test("Miguel"));
    }
}
```

Hemos creado un objeto `Predicate` de tipo `String`. Le damos cuerpo al método `test` con una expresión lambda que se le pasa un argumento y devuelve un booleano.

## Métodos Predicate

La interfaz `Predicate` contiene algunos métodos como:

+ `isEqual(Object targetRef)`: Devuelve un predicado que prueba si dos argumentos son iguales.
+ `and(Predicate other)`: Devuelve un predicado compuesto que representa un AND lógico de este predicado y otro.
+ `or(Predicate other)`: Devuelve un predicado compuesto que representa un OR lógico de este predicado y otro.
+ `negate()`: Devuelve un predicado que representa la negación lógica de este predicado.

Ejemplo:

```java
    Predicate<Integer> greaterThan10 = i -> i > 10;
    Predicate<Integer> lessThan20 = i -> i < 20;
    System.out.println(greaterThan10.and(lessThan20).test(15));

    Predicate<Integer> greaterThanTen = (i) -> i > 10;
    Predicate<Integer> lowerThanTwenty = (i) -> i < 20;
    boolean resul = greaterThanTen.and(lowerThanTwenty).test(15);//true
    boolean resul2 = greaterThanTen.and(lowerThanTwenty).negate().test(15);//false

    Predicate<String> i  = Predicate.isEqual("asdf");
    System.out.println(i.test("java"));//false
```

!!! Note
    Debido al uso extendido de `Predicate` se han añadido las interfaces funcionales `IntPredicate` cuando queremos trabajar con predicados de tipo entero, `DoublePredicate` y `LongPredicate`. También tenemos la interfaz `BiPredicate` que es un caso especial de `Predicate` y recibe dos parámetros en vez de uno.

```java
    IntPredicate predicate = (x) -> {
        if (x == 12345) {
            return true;
        }
        return false;
    };
    
    System.out.println(predicate.test(12345));

    IntPredicate intPredicate1 = predicate.negate();
    System.out.println(intPredicate1.test(12345));

    BiPredicate<String, Integer> filtroLongitud = (x, y) -> {
        return x.length() == y;
    };
    
    boolean result = filter.test("java", 10);
    System.out.println(result); // false
```

## Supplier

`Supplier` es otra interfaz funcional dentro del paquete `java.util.function` que nos provee del método abstracto `**get**`, sin argumentos que devuelve un tipo de dato.

```java
@FunctionalInterface
public interface Supplier<T> {

    T get();
}
```

Esta interfaz también se utiliza con expresiones lambda que no tienen parámetros pero devuelven un resultado:

```java
    Random random = new Random();
    Supplier<Integer> su = () -> random.nextInt();
```

Al igual que ocurría en los predicados con los `Supplier` también disponemos de las clases `IntSupplier`, `DoubleSupplier`, `LongSupplier` y `BooleanSupplier`.

## Consumer

`Consumer` es otra interfaz funcional dentro del paquete `java.util.function` que provee un método que recibe un solo parámetro de tipo genérico y no devuelve nada.

```java
public interface Consumer<T> {
    void accept(T t);
}
```

La expresión lambda asignada a un objeto de tipo `Consumer` se usa para definir su método `**accept(T t)**` que eventualmente aplica la operación dada en su argumento. Los `Consumer` son útiles cuando no necesitan devolver ningún valor, ya que se espera que operen a través de efectos secundarios.

Existen también las interfaces `IntConsumer`, `LongConsumer` y `DoubleConsumer`.

```java
Consumer<Integer> numero = (x) -> System.out.println(x);
numero.accept(5);
```

`BiConsumer` es un caso especial de las expresiones `Consumer`, son aquellas que reciben dos valores como parámetro y no devuelven resultado.

```java
@FunctionalInterface
public interface BiConsumer<T, U> {
    void accept(T t, U u);
}
```

Ejemplo:

```java
BiConsumer<Integer, String> biConsumer = (x, s) -> System.out.println(x + s);
biConsumer.accept(3, " puntos");
```
