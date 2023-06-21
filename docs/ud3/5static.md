# 🌎 Variables, métodos y clases estáticas

Una clase, método o campo declarado como estático puede ser accedido o invocado sin la necesidad de tener que instanciar un objeto de la clase.

Para entender mejor que son las variables y métodos estáticos vamos a ver las diferencias de cada uno de ellos con variables y métodos de instancia.

## Variables estáticas

Si una variable se declara estática, hay exactamente una copia de esa variable creada sin importar cuántas veces se instancia su clase.

+ Se declaran usando la palabra reservada **static**.
+ **Cada instancia de la clase comparte la misma variable estática**, por lo que si se realizan cambios en esa variable estática todas las demás instancias de esa clase verá el efecto de ese cambio.
+ No se usan muy amenudo.

```java
class Persona {
    private static String name;

    public Persona(String name) {
        Persona.name = name;
    }

    public void printName() {
        System.out.println(name);
    }
}

public class Main {
    public static void main(String[] args) {
        Persona p1 = new Persona("Patricia");
        Persona p2 = new Persona("Maxi");
        p1.printName();//imprime Maxi
        p2.printName();//imprime Maxi
    }
}
```

### Variables constantes estáticas

También se puede declarar un variable constante (final) como estática, esto significa que solo habrá una copia de la constante aunque hayan muchas instancias de esa clase.
Son también llamadas **constantes de clase**:

```java
private static final int NUMERO_JUGADORES = 2;
```

No todas las constantes son constantes de clase. Es decir, no todas las constantes se declaran estáticas. Sin embargo, la idea de asociar constantes con una clase tiene sentido. Ya que te permite ahorrar recursos de memoria, al crear una única copia de la constante.

Otra ventaja de las constantes de clase es que se pueden usar antes de que existan instancias de la clase. Por ejemplo, una constante de clase (a diferencia de una constante de instancia) se puede usar durante la instanciación de objetos:

```java
public class Game {

    public static final int MULTIPLAYER = 2;
    public static final int ONE_PLAYER = 1;

    private int numeroJugadores;

    public Game(int jugadores) {
        this.numeroJugadores = jugadores;
    }

    public static void main(String[] args) {
        Game game = new Game(Game.MULTIPLAYER);
    }
}
```

## Variables de instancia

+ Las variables de instancia también son conocidas como campos o atributos.
+ Las variables de instancia **pertenecen a una instancia de la clase**.
+ **Cada instancia tiene su propia copia** de una variable de instancia, así que cada instancia puede tener un valor(estado) diferente.
+ Las variables de instancia **representan el estado de una instancia**.

```java
class Persona {
    private String name;

    public Persona(String name) {
        this.name = name;
    }

    public void printName() {
        System.out.println(name);
    }
}

public class Main {
    public static void main(String[] args) {
        Persona p1 = new Persona("Patricia");
        Persona p2 = new Persona("Maxi");
        p1.printName();//imprime Patricia
        p2.printName();//imprime Maxi
    }
}
```

## Métodos estáticos

+ Los métodos estáticos son declarados usando el modificador **static**.
+ No se puede acceder desde los métodos estáticos a métodos de instancia o variables de instancia directamente.
+ Para invocar a un método estático se utiliza el nombre de la clase + "." + el nombre del método, o solamente el nombre del método si está en la misma clase.(VEASE EJEMPLO)
+ Normalmente se usan para operaciones que no requieren ningún dato de instancia de la clase, es decir, nada que venga de this.
+ Dentro de un método estático no podemos usar la palabra _this_.
+ Cada vez que veas un método que **no utilice variables de instancia**, significa que ese método debería declararse como estático.
+ Por ejemplo, el main es declarado como estático y es llamado por la JVM cuando se lanza la aplicación.

```java
public class Calculadora {
    public static void printSuma(int a, int b) {
        System.out.println(a+b);
    }
}

public class Main {
    public static void main(String[] args) {
        Calculadora.printSuma(5, 6);
        printHolaMundo();
    }

    public static void printHolaMundo() {
        System.out.println("Hola mundo.");
    }
}
```

## Métodos de instancia

+ Los métodos de instancia pertenecen a una instancia específica de la clase.
+ Para usar un método de instancia tenemos que instanciar un objeto de la clase primero, normalmente utilizando la palabra resevada **new**.
+ Los métodos de instancia pueden acceder a otros métodos de instancia y variables de instancia directamente.
+ Los métodos de instancia pueden también acceder a **métodos estáticos y variables estáticas**.

## ¿Método estático o método de instancia?

Cuando voy a crear un método y tengo dudas sobre si crearlo estático o de instancia debo seguir la siguiente lógica:

¿El método usa algún campo o variable de instancia o invoca en su interior a algún método de instancia?

+ SI --> Entonces debería crear un método de instancia.
+ NO --> Debería crear un método estático.

## Clases estáticas

En el lenguaje Java, no podemos crear una clase externa como una clase estática, pero existe el privilegio de crear una clase interna anidada como una clase estática.

+ Una clase interna estática nunca puede acceder a un miembro no estático de la clase externa.
+ Una clase interna estática no necesita ninguna referencia de clase externa para acceder a las variables miembro.
+ La clase estática nunca se puede instanciar. Por lo tanto, los métodos son directamente accesibles por el nombre de la clase.

```java
public class Estatica {
    static int i = 1;
    int j = 9;

    public static void main(String[] args) {
        Estatica s = new Estatica();
        //s.ClaseInterna.printNum(); NO ES CORRECTO
        //Estatica.ClaseInterna.printNum(); SI se podría hacer
        ClaseInterna.printNum();
    }

    public static class ClaseInterna {
        public static void printNum() {
            System.out.println(i);
            //System.out.println(j); //NO PODEMOS ACCEDER A ATRIBUTOS NO ESTÁTICOS
        }
    }
}
```

## Bloques estáticos

Es posible declarar bloques de código como estáticos, de tal manera que sean ejecutados cuando se cargue la clase. Este tipo de bloques se conocen como bloques de inicialización estáticos (static initializer block). Si no se declara un bloque de este tipo de forma explícita, el compilador Just-in-Time combina todos los campos estáticos en un bloque y los ejecuta durante la carga de clases.

```java
public class Objeto {
 
    private static int campo1;
 
    static {
        campo1 = 10;
    }
}
```

## Imports estáticos

Una de las características incluidas en Java 5 fué la capacidad de importar los métodos y variables estáticas de un módulo y acceder a ellos como si hubieran sido declarados en la propia clase. Es especialmente útil, y mejora la legibilidad, cuando se están definiendo test unitarios, ya que la mayoría de los métodos de aserción de JUnit son estáticos.

```java
import static java.lang.Math.PI;

public static void main(String[] args) {
    double a = PI;
}
```
