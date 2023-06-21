# Referencia a métodos en expresiones lambda

**Una referencia a métodos** o _métodos referenciados_ proporciona una forma de referirse a un método sin ejecutarlo. Se relaciona con expresiones lambda porque también requiere un contexto de tipo de objetivo que consiste en una interfaz funcional compatible.

En el caso de que todo lo que haga la expresión lambda sea **llamar a otro método con los parámetros pasados ​​a la expresión lambda**, la implementación de Java lambda proporciona una forma más corta de expresar la llamada al método, que es usando **::**.

Veamos un ejemplo:

```java
public interface Impresora{
    void imprimir(String s);
}
```

Si usáramos lambda sin referencias a métodos, lo haríamos de la siguiente forma:

```java
Impresora impresora = s -> System.out.println(s);
```

Dado que todo lo que hace el cuerpo lambda es reenviar el parámetro String al método System.out.println(), podemos reemplazar la declaración lambda anterior con una referencia de método utilizando {++::++}. De forma que quedaría:

```java
Impresora impresora = System.out::println;
```

```java
List<String> names = new ArrayList();
names.add("Andrea");
names.add("Luisa");
names.add("Diego");
names.add("Paúl");
names.add("Dario");
names.forEach(System.out::println);
```

Observa los dos puntos dobles **::** . Estos le indican al compilador de Java que se trata de **una referencia de método**. El método al que se hace referencia es lo que viene después de los dos puntos dobles. Cualquier clase u objeto que posea el método al que se hace referencia viene antes de los dos puntos dobles.

Podemos hacer referencia a los siguientes tipos de métodos:

+ Método estático
+ Método con parámetros de objeto
+ Método de instancia
+ Constructor

## Referencias a métodos estáticos

Los métodos más fáciles de referenciar son los métodos estáticos. Veamos un ejemplo:

```java
public interface Finder {
    int find(String s1, String s2);
}

public class MyClass{
    public static int doFind(String s1, String s2){
        return s1.lastIndexOf(s2);
    }
}
```

La referencia al método estático `doFind` se haría con:

```java
Finder finder = MyClass::doFind;
```

Dado que los parámetros de los métodos `Finder.find()` y `MyClass.doFind()` coinciden, es posible crear una expresión lambda que implemente `Finder.find()` y haga referencia al método `MyClass.doFind()`.

## Referencia a métodos con parámetro

También puede hacer referencia a un método con parámetros de objeto de la clase al método que se llama.

```java
public interface Finder {
    int find(MyClass mc, String s1, String s2);
}

class MyClass {
    public int check(String s1, String s2) {
        return s1.indexOf(s2);
    }
}

//dentro del main
//Aunque es un método de instancia, no estático
//podemos llamarlo con la clase porque en la interfaz
//está añadido un parámetro de tipo MyClass
Finder finder = MyClass::check;
```

Si quisiéramos hacerlo con una expresión lambda sin usar referencia de métodos que llama a String.indexOf() para buscar sería:

```java
Finder finder = (s1, s2) -> s1.indexOf(s2);
```

Su equivalente utilizando referencia de métodos con parámetro de objeto en la expresión lambda sería:

```java
Finder finder = String::indexOf;
int numero = finder.find("Hola", "a");
```

Observe cómo la versión abreviada hace referencia a un solo método. El compilador de Java intentará hacer coincidir el método al que se hace referencia con el primer tipo de parámetro, utilizando el segundo tipo de parámetro como parámetro del método al que se hace referencia.

## Referencia a métodos de instancia

En tercer lugar, también es posible hacer referencia a un método de instancia desde una definición lambda.

```java
public interface Deserializer {
    int deserialize(String v1);
}
```

Esta interfaz representa un componente que es capaz de "deserializar" un String en un int.

```java
public class StringConverter {
    public int convertToInt(String v1){
        return Integer.valueOf(v1);
    }
}
```

El método `convertToInt()` tiene la misma signatura que el método `deserialize()` del método de la interfaz `Deserializer`. Por eso, podemos crear una instancia de StringConverter y hacer referencia a su método convertToInt() desde una expresión lambda de Java.

```java
StringConverter stringConverter = new StringConverter();
Deserializador des = stringConverter::convertToInt;
```

La expresión lambda creada por la segunda de las dos líneas hace referencia al método convertToInt de la instancia de StringConverter creada en la primera línea.

## Referencias a constructores

Finalmente, es posible hacer referencia a un constructor de una clase. Para ello, se escribe el nombre de la clase seguido de **::new**:

```java
-- Nomenclatura
MiClase::new
```

```java
Supplier<Usuario> usu = Usuario::new;
//Construye un objeto de tipo usuario que es devuelto por método get();
Usuario usuario = usu.get();
```

Veamos otro ejemplo utilizando `BiFunction`:

```java
class Pruebas {
    public static void main(String[] args) {
        BiFunction<String, Integer, Usuario> crearUsuario = Usuario::new;
        Usuario u = crearUsuario.apply("Patricia", 12);
    }
}
class Usuario {
    private String nombre;
    private int edad;

    public Usuario(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}
```
