# 🦄 Genéricos

Antes de Java 5 cuando introducíamos objetos en una colección estos se guardaban como objetos de tipo `Object`, aprovechando el polimorfismo para poder introducir cualquier tipo de objeto en la colección. Esto nos obligaba a hacer un casting al tipo original al obtener los elementos de la colección.

```java
public class Ejemplo {  
  public static void main(String[] args) {  
    List lista = new ArrayList();  
    lista.add("Hola mundo");  
  
    String cadena = (String) lista.get(0);  
    System.out.println(cadena);  
  }  
} 
```

Esta forma de trabajar no solo nos ocasiona tener que escribir más código innecesariamente, sino que es propenso a errores porque carecemos de un sistema de comprobación de tipos. Si introdujeramos un objeto de tipo incorrecto el programa compilaría pero lanzaría una excepción en tiempo de ejecución al intentar convertir el objeto en `String`:

```java
public class Ejemplo {  
  public static void main(String[] args) {  
    List lista = new ArrayList();  
    lista.add(22);  
  
    String cadena = (String) lista.get(0);  
    System.out.println(cadena);  
  } 
} 
```

Desde Java 5 contamos con una característica llamada generics que puede solventar esta clase de problemas. Los generics son una mejora al sistema de tipos que nos permite programar abstrayéndonos de los tipos de datos.

**Genéricos** significa **tipos parametrizados**. La idea es permitir que **_el tipo_** (`Integer`, `String`, etc., y tipos definidos por el usuario) **sea un parámetro** para métodos, clases e interfaces. Utilizando Generics, es posible crear clases que trabajen con diferentes tipos de datos. Una entidad como clase, interfaz o método que opera en un tipo parametrizado es una entidad genérica.

Gracias a los generics podemos especificar el tipo de objeto que introduciremos en la colección, de forma que el compilador conozca el tipo de objeto que vamos a utilizar, evitándonos así el casting. Además, gracias a esta información, el compilador podrá comprobar el tipo de los objetos que introducimos, y lanzar un error en tiempo de compilación si se intenta introducir un objeto de un tipo incompatible, en lugar de que se produzca una excepción en tiempo de ejecución.

Para utilizar generics con nuestras colecciones tan solo tenemos que indicar el tipo entre **el operador Diamond <>** a la hora de crearla. A estas clases a las que podemos pasar un tipo como {++«parámetro»++} se les llama **clases parametrizadas, clases genéricas o simplemente genéricas (generics)**.

```java
public class Ejemplo {  
  public static void main(String[] args) {  
    List<String> lista = new ArrayList<String>();  
    lista.add("Hola mundo");  
  
    String cadena = lista.get(0);  
    System.out.println(cadena);  
  }  
} 
```

El código anterior no compilaría, si intentáramos insertar en la lista un número `lista.add(14);`, nos daría un error de compilación de tipos.

!!! Note
    **Algo a tener en cuenta es que el tipo parámetro debe ser una clase; no podemos utilizar tipos primitivos.**

## 🦄 Clases genéricas

Al crear una clase que utiliza o contiene algún atributo genérico, me obliga a añadir este tipo de genérico en la definición de clase. **Por convención se suele utilizar una sola letra mayúscula para el tipo genérico**.

Es decir, si mi clase tiene un atributo `T elemento` genérico que no sé qué tipo de dato va a ser, entero, double, float.... le pongo una letra y con esto le digo que ese atributo es de tipo genérico, puede ser cualquier tipo de dato.

```java
public class Box<T> {

  private T elemento;

  public T get() { return elemento; }
  public void set(T elemento) { this.elemento = elemento; }

}
```

Según las convenciones los nombres de los parámetros de tipo usados comúnmente son los siguientes:

+ E: elemento de una colección.
+ K: clave.
+ N: número.
+ T: tipo.
+ V: valor.
+ S, U, V etc: para segundos, terceros y cuartos tipos.

En el momento de la instanciación de un tipo genérico indicaremos el argumento para el tipo, en este caso Box contendrá una referencia a un tipo Integer.

```java
//Las dos formas son válidas:
Box<Integer> integerBox1 = new Box<Integer>();
Box<Integer> integerBox2 = new Box<>();

Box<String> textoBox = new Box<>();
```

Estamos creando objetos de la clase `Box`, tanto de tipo Integer como String.

A veces querremos limitar los tipos que pueden ser usados empleando lo que se denomina **bounded type**. Con \<T extends Number\> el tipo T debe extender la clase Number.
Java permite múltiples límites o bounded type: `<T extends B1 & B2 & B3>`.
`Box` es una clase y `B1` y `B2` son interfaces. Primero siempre debe ir la clase y luego las interfaces.
Recuerda que Java NO permite la herencia múltiple, por tanto, SOLO se puede extender de una clase, pero puede implementar varias interfaces en la declaración del bounded type.

## 🦄 Métodos genéricos

Al igual que ocurre con las clases, si me creo un método genérico, es decir, que recibe tipos de datos genéricos **_únicos que no están definidos en la clase_**, tengo que especificar en la signatura del método esos genéricos:

> Ejemplo

```java
public static <T, R> void executeFunction(List<T> lista, Function<T,R> function) {
  for(T t: lista) {
    System.out.println(function.apply(t));
  }
}

```