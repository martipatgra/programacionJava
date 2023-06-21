# Clases anidadas (Nested classes)

En Java, al igual que los métodos, las variables de una clase también pueden tener otra clase como miembro. Java permite escribir una clase dentro de otra. La clase escrita dentro se denomina **clase anidada o clase interna**, y la clase que contiene la clase interna se denomina **clase externa**.

## Sintaxis

La clase `Outer_Demo` es la clase externa y la clase `Inner_Demo` es la clase interna.

```java
class Outer_Demo {
   class Inner_Demo {
   }
}
```

Las clases anidadas se dividen en dos tipos:

+ Clases anidadas no estáticas: son las llamadas clases internas (inner classes).
+ Clases estáticas anidadas.

```java
class OuterClass {
    ...
    class InnerClass {
        ...
    }
    static class StaticNestedClass {
        ...
    }
}
```

![InnerClass](../img/ud6/innerclass1.png)

Una clase anidada es un miembro de su clase envolvente. Las clases anidadas no estáticas (clases internas) tienen acceso a otros miembros de la clase envolvente, incluso si se declaran como privadas.
Las clases anidadas estáticas no tienen acceso a otros miembros de la clase envolvente. Como miembro de `OuterClass`, una clase anidada se puede declarar `private`, `public`, `protected`.

## ¿Por qué usar clases anidadas?

1. **Es una forma de agrupar lógicamente las clases que solo se usan en un lugar**: si una clase es útil solo para otra clase, entonces es lógico incrustarla en esa clase y mantener las dos juntas. Anidar tales "clases de ayuda" hace que su paquete sea más optimizado.

2. **Aumenta la encapsulación**: sabemos que una clase no se puede declarar `private`, pero si tenemos la clase como miembro de otra clase, entonces la clase interna se puede hacer privada. Y esto también se usa para acceder a los miembros privados de una clase.

3. **Puede conducir a un código más legible y mantenible**: anidar clases pequeñas dentro de clases de nivel superior coloca el código más cerca de donde se usa.

## Clase Interna (Inner Class) - No estática clase anidada

Al igual que con los métodos y variables de instancia, una clase interna está asociada con una instancia de su clase envolvente y tiene acceso directo a los métodos y campos de ese objeto. Además, debido a que una clase interna está asociada con una instancia, **no puede definir ningún miembro estático en sí misma**.

Las clases internas son de tres tipos dependiendo de cómo y dónde se definan:

1. Clase  - Inner Class
2. Clase interna de método local - Method-local Inner Class
3. Clase interna anónima - Anonymous Inner Class

### Inner class

Crear una clase interna es bastante simple. Solo hay que escribir una clase dentro de una clase. A diferencia de una clase, una clase interna puede ser privada y una vez que declaras privada una clase interna, no se puede acceder a ella desde un objeto fuera de la clase.

Los objetos que son instancias de una clase interna existen dentro de una instancia de la clase externa.

```java
class OuterClass {

    private int num = 32;

    class InnerClass {
        
        public int getNum() {
            return num;
        }

    }
}

public class Main {

   public static void main(String args[]) {
      OuterClass outer = new OuterClass();
      
      OuterClass.InnerClass inner = outer.new InnerClass();
      System.out.println(inner.getNum());
   }
}
```

Una instancia de `InnerClass` solo puede existir dentro de una instancia de `OuterClass` y tiene acceso directo a los métodos y campos de su instancia adjunta.

**Para instanciar una clase interna, primero debe instanciar la clase externa.**

### Clase interna de método local

En Java, podemos escribir una clase dentro de un método y esta será de tipo local. Al igual que las variables locales, el alcance de la clase interna está restringido dentro del método.

Una clase interna local de método solo se puede instanciar dentro del método donde se define la clase interna.

```java
public class Outerclass {
    
    void my_Method() {
        int num = 23;

        // method-local inner class
        class MethodInner_Demo {
            public void print() {
                System.out.println("This is method inner class "+num);
            }   
        } // end of inner class

        // Accessing the inner class
        MethodInner_Demo inner = new MethodInner_Demo();
        inner.print();
   }
   
   public static void main(String args[]) {
      Outerclass outer = new Outerclass();
      outer.my_Method();
   }
}
```

### Clase interna anónima

Una clase interna declarada sin un nombre de clase se conoce como clase interna anónima. En el caso de clases internas anónimas, las declaramos y las instanciamos al mismo tiempo. Por lo general, se utilizan siempre que necesite anular el método de una interfaz o clase abstracta.

Las clases anónimas permiten hacer el código más conciso. Permiten declarar e instanciar una clase al mismo tiempo. Son como clases locales excepto que no tienen nombre. **Se usa si se necesita usar una clase local solo una vez.**

#### _Ejemplo_ 1

```java
interface Greeting {
    public void greet();
    public void greetSomeone(String someone);
}

class Main {
    public static void main(String[] args) {
        //Anonymous class
        Greeting frenchGreeting = new Greeting() {
            String name = "tout le monde";
            public void greet() {
                greetSomeone("tout le monde");
            }
            public void greetSomeone(String someone) {
                name = someone;
                System.out.println("Salut " + name);
            }
        };
    }
}
```

#### _Ejemplo_ 2

```java
abstract class AnonymousInner {
   public abstract void mymethod();
}

public class OuterClass {

   public static void main(String args[]) {

      AnonymousInner inner = new AnonymousInner() {
         public void mymethod() {
            System.out.println("This is an example of anonymous inner class");
         }
      };
      inner.mymethod();
   }
}
```

## Clases Anidadas Estáticas

Una clase interna estática es una clase anidada que es un miembro estático de la clase externa. Se puede acceder a ella sin instanciar la clase externa, usando otros miembros estáticos. Al igual que los miembros estáticos, una clase anidada estática no tiene acceso a las variables de instancia ni a los métodos de la clase externa.

```java
class MyOuter {
   static class NestedDemo {
   }
}
```

Crear una instancia de una clase anidada estática es un poco diferente de crear una instancia de una clase interna.

```java
class Outer {
    private int x = 0;

    static class Inner {
        private int y = 9;

        public int getY() {
            return y;
        }
    }
}
public class StaticNestedClass {
    public static void main(String[] args) {
        Outer.Inner inner = new Outer.Inner();
        System.out.println(inner.getY());
    }
}
```

### _Ejemplo combinado_ Clase interna y clase estática interna

```java
class OuterClass {

    private String outerField = "Outer field";
    private static String staticOuterField = "Static outer field";

    class InnerClass {
        void accessMembers() {
            System.out.println(outerField);
            System.out.println(staticOuterField);
        }
    }

    static class StaticNestedClass {
        void accessMembers(OuterClass outer) {
            // Compiler error: Cannot make a static reference to the non-static
            //     field outerField
            //System.out.println(outerField);
            System.out.println(outer.outerField);
            System.out.println(staticOuterField);
        }
    }

    public static void main(String[] args) {
        System.out.println("Inner class:");
        System.out.println("------------");
        OuterClass outerObject = new OuterClass();
        OuterClass.InnerClass innerObject = outerObject.new InnerClass();
        innerObject.accessMembers();

        System.out.println("\nStatic nested class:");
        System.out.println("--------------------");
        StaticNestedClass staticNestedObject = new StaticNestedClass();
        staticNestedObject.accessMembers(outerObject);
    }
}
```
