# Expresiones lambda

Las expresiones lambda es una característica importante que fue añadida en Java 8. Es muy útil, ayuda a iterar, filtrar y extraer datos de la colección.

Una expresión lambda es un bloque corto de código que toma parámetros y devuelve un valor. Las expresiones lambda son similares a los métodos, pero no necesitan un nombre y se pueden implementar directamente en el cuerpo de un método.

La expresiones lambda de Java son tratadas como una función, por lo que el compilador no crea un archivo .class.

La expresión lambda proporciona la implementación de una interfaz funcional. Una interfaz funcional es aquella que tiene **UN SOLO método abstracto**. Las interfaces funcionales en Java incluyen la anotación `@FunctionalInterface`.

## Sintaxis

Dado que las expresiones lambda son efectivamente solo métodos, las expresiones lambda pueden tomar parámetros como los métodos.

La expresión lambda de Java **consta de tres componentes**.

1. Parámetros - lista de argumentos: una expresión lambda puede tener cero o cualquier número de argumentos.

2. Token de flecha: se utiliza para vincular la lista de argumentos y el cuerpo de la expresión.

3. Cuerpo: Contiene expresiones y declaraciones para la expresión lambda.

**Las expresiones lambda se pueden almacenar en variables si el tipo de variable es una interfaz que tiene un solo método.** La expresión lambda debe tener la misma cantidad de parámetros y el mismo tipo de retorno que ese método.

### Cero parámetros

Los paréntesis no tienen contenido en el medio. Eso es para indicar que la expresión lambda no recibe parámetros.

> () -> {body}

```java
interface Saludo{  
    public String say();  
}  

public class Main {

  public static void main(String[] args) {  
      Saludo s=()->{  
          return "Hola";  
      };  
      System.out.println(s.say());  
  }  
}  
```

### Un parámetro

Cuando una expresión lambda recibe un solo parámetro, también se puede omitir los paréntesis, de forma que quedaría así:

> (p1) -> {body}

> p1 -> {body}

```java
interface Saludo{  
    public String say(String nombre);  
}

public class Main {

  public static void main(String[] args) { 
    //sin omitir paréntesis 
      Saludo s = (nombre)->{  
          return "Hola " + nombre;  
      };  
      System.out.println(s.say("Patri"));


      // Omitir paréntesis
      Saludo s2 = nombre ->{  
          return "Hola, " + nombre;  
      };  
      System.out.println(s2.say("Patri"));  
  }
}  
```

### Múltiples parámetros

Si el método con el que coincide su expresión lambda de Java recibe varios parámetros, los parámetros deben enumerarse entre paréntesis. Así es como se ve en código Java:

> (p1, p2) -> {body}

```java
interface Sumable{  
    int add(int a,int b);  
}  
  
public class Main {  
    public static void main(String[] args) {  
          
        Sumable ad1=(a,b)->(a+b);  
        System.out.println(ad1.add(10,20));  
          
        // con tipo de datos  
        Sumable ad2=(int a,int b)->(a+b);  
        System.out.println(ad2.add(100,200));  
    }  
} 
```

### Tipo de parámetros

En ocasiones, puede ser necesario especificar tipos de parámetros para una expresión lambda si el compilador no puede inferir los tipos de parámetros del método de interfaz funcional con el que coincide la lambda.

```java
(Coche coche) -> System.out.println("El coche es: " + coche.getName());
```

### Cuerpo de las expresiones lambda

El cuerpo de una expresión lambda y, por lo tanto, el cuerpo de la función/método que representa, se especifica a la derecha de -> en la declaración lambda.

Si la expresión lambda consta de varias líneas, se puede encerrar el cuerpo de la función lambda dentro de los corchetes { }.

```java
 (oldValue, newValue) -> {
    System.out.println("Old value: " + oldValue);
    System.out.println("New value: " + newValue);
  }
```

### Devolver un valor en las expresiones lambda

Al igual que con los métodos puedes devolver un valor, en las expresiones lambda también. Se hace agregando una declaración de retorno al cuerpo de la función lambda.

```java
interface Saludo{  
  public String say(String name);  
}

public class Main {
  public static void main(String[] args) {  
        
    // Lambda expression with single parameter.  
    Saludo s1 = (name)->{  
        return "Hello, " + name;  
    };
    System.out.println(s1.say("Patri"));  
  }
}
```

En las expresiones lambda, si solo hay una sentencia, **puede o no** usar la palabra `return`. Pero si la expresión lambda tiene varias sentencias se debe poner la palabra `return`.

```java
interface Sumable{  
    int add(int a,int b);  
}
public class Main {  
    public static void main(String[] args) {  
          
        // Lambda expression sin palabra clave return
        Sumable ad1 = (a,b)->(a + b);  
        System.out.println(ad1.add(10,20));  
          
        // Lambda expression con la palabra clave return
        Sumable ad2 = (a,b)->{  
                        return (a + b);   
                        };  
        System.out.println(ad2.add(100,200));  
    }  
} 
```

El compilador sabe que la expresión `a + b` es el valor de retorno de la expresión lambda (de ahí el nombre de expresiones lambda, ya que las expresiones devuelven un valor de algún tipo).

### Bucle for-each

```java
public static void main(String[] args) {  
          
    List<String> list = new ArrayList<String>();  
    list.add("java");
    list.add("lambda");
    list.add("test");  
          
    list.forEach(  
        (n)->System.out.println(n)  
    );  
}
```

## Escenario sin expresiones lambda

```java
interface Saludo { 
    public void saludar();  
}  
public class LambdaExpressionExample {  
    public static void main(String[] args) {  
        String nombre = "Patri";
  
        //sin expresiones lambda, Saludo se implementa usando clases anónimas
        Saludo s = new Saludo(){  
            public void saludar(){System.out.println("Hola " + nombre);}  
        };  
        s.saludar();  
    }  
}  
```

## Escenario con expresiones lambda

```java
@FunctionalInterface  //Esto es opcional
interface Saludo {  
    public void saludar();  
}  
  
public class LambdaExpressionExample2 {  
    public static void main(String[] args) {  
        String nombre = "Patri";
          
        //con expresiones lambda
        Saludo s2 = ()-> {
            System.out.println("Hola " + nombre);  
        };
        s2.saludar();  
    }  
}  
```

## Crear una expresión lambda a partir de un método

Para definir una expresión lambda de un método que no está definido en ninguna interfaz funcional, tenemos que utilizar la clase `Function`. A la clase Function se le especifican dos tipos de parámetros entre `<>`, el primero es el parámetro de entrada de la función, y el segundo es el parámetro de salida que devuelve la función o método.

```java
    {
        int total = 0;
        for (int i = 0; i < texto.length(); i++) {
            total+=texto.charAt(i);
        }
        return total;
    };

    //Queremos crear una expresión lambda que realice lo que está entre { }

    Function<String, Integer> funcionLambda = (s) -> {
            int total = 0;
            for (int i = 0; i < texto.length(); i++) {
                total+=texto.charAt(i);
            }
            return total;
        };
```

Para ejecutar el código en el interior de la expresión lambda, utilizaremos el método `apply`:

```java
System.out.println(funcionLambda.apply("Programación"));
```
