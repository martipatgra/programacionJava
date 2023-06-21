# Necesidad de Java Equals y Hashcode

Los métodos Java `equals()` y `hashCode()` están presentes en la clase `Object`. Como todas las clases heredan de la clase Object de forma automática reciben una implementación predeterminada de equals() y hashCode() sino se sobreescribe.

El método equals() sirve para comparar instancias de clases entre sí. Si usamos colecciones como las que hemos visto en el tema: ArrayList, LinkedList... muchos de sus métodos (contains, remove, indexOf, etc.) llaman al método equals internamente para encontrar el objeto. Es decir, van comparando el objeto con los que hay en la lista.

A veces cuando creamos colecciones donde el tipo de dato es un Objeto definido por nosotros, como Persona, Coche, etc.
Necesitamos de algún método que nos permita comparar objetos de este tipo.

Los métodos Java hashCode() y equals() se utilizan conjuntamente en implementaciones basadas en tablas **Hash** en Java para almacenar y recuperar datos.

# Equals

Lo heredamos automáticamente de Object de la siguiente forma:

```java 
//Dos objetos son iguales, si son el mismo objeto
public boolean equals(Object obj) {
    return (this == obj);
}
```

En ocasiones, queremos cambiar la lógica de la implementación de `Object` por otra lógica que nos diga si dos instancias de una clase **son equivalentes a pesar de tratarse de distintos objetos**. Por ejemplo, teniendo en cuenta los atributos de la clase que nosotros le indiquemos para ello.

En el siguiente ejemplo tenemos la clase **Client**, en nuestra lógica dos objetos de cliente son iguales si son del mismo tipo (Client) y comparten el mismo nombre.

```java title="Client.java"
public class Client {

    private String name;
    private int age;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Client client = (Client) o;
        return Objects.equals(name, client.name);
    }
}
```

# Contrato equals() - hashcode()

Cuando utilicemos estructuras de datos basadas en **_hash tables_** como HashMap, HashSet, LinkedHashMap, LinkedHashSet, Hashtable, ... necesitamos de un contrato equals - hashcode:

> Cuando sobreescribimos el método equals() en nuestra clase para cambiar la lógica que se hereda de la clase Object, tenemos que sobreescribir el método hashCode() de manera que si dos instancias de nuestra clase son iguales según la nueva lógica en equals(), el método hashCode() deberá retornar el mismo valor si lo llamo para dichas instancias.

El método `hashcode()` sirve para comparar objetos de una forma más rápida en estructuras Hash ya que únicamente nos devuelve un número entero. Cuando Java compara dos objetos en estructuras de tipo hash **_primero invoca al método hashcode y luego el equals_**. Si los métodos hashcode de cada objeto devuelven diferente hash no seguirá comparando y considerará a los objetos distintos. En el caso en el que ambos objetos compartan el mismo hashcode Java invocará al método equals() y revisará si se cumple la igualdad.

# Ejemplo

Muchas veces se nos olvida que la invocación a los métodos equals y hashcode forma parte intrínseca del framework de colecciones. Por ejemplo si construimos dos objetos de tipo Client y los añadimos a un HashSet, podemos comprobar que el cliente existe utilizando el método contains dentro del conjunto.

```java title="Main.java"
public static void main(String[] args) {
        Client p1= new Client();
        p1.setName("Patricia");

        Client p2= new Client();
        p2.setName("Chema");

        Client p3= new Client();
        p3.setName("Patricia");

        HashSet<Client> conjunto = new HashSet<>();
        conjunto.add(p1);
        conjunto.add(p2);
        conjunto.add(p3);
        System.out.println(conjunto.contains(p1));//true
        System.out.println(conjunto.size());//2
    }
```

Esto nos devolverá true ya que el HashSet contiene este elemento. Ahora bien si nosotros sobreescribimos de forma incorrecta el hashcode con el siguiente código:

```java
    @Override
    public int hashCode() {
        return (int)(Math.random()*100);
    }

    public static void main(String[] args) {
        Client p1= new Client();
        p1.setName("Patricia");

        Client p2= new Client();
        p2.setName("Chema");

        Client p3= new Client();
        p3.setName("Patricia");

        HashSet<Client> conjunto = new HashSet<>();
        conjunto.add(p1);
        conjunto.add(p2);
        conjunto.add(p3);
        System.out.println(conjunto.contains(p1));//false
        System.out.println(conjunto.size());//3
    }
```

Estaremos calculando al azar el hashcode y dos objetos iguales devolverán hashcodes diferentes. El `HashSet` nos devolverá false cuando invoquemos el método contains aunque sabemos que el elemento existe en el conjunto. Y también agregará duplicado ya que no encuentra el elemento.