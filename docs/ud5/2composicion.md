# Composición

La composición es otro componente de la programación orientada a objetos y es muy utilizada.

Es el mecanismo en el cual una clase se construye a partir de otros objetos de igual o distinto tipo, pudiéndolos combinar para obtener la funcionalidad deseada. En la composición la nueva clase, mantiene una relación “Usa/Tiene un”, con los objetos que son parte de la clase.

Vamos a ver un ejemplo de la clase `Car` que extiende `Vehicle`:

```java
public class Vehicle {

    private String name;
}

public class Car extends Vehicle {

    private int doors;
    private int seats;

    public Car(int doors, int seats) {
        this.doors = doors;
        this.seats = seats;
    }
}
```

Estas dos clases tienen una relación de herencia, el significado es que un coche **es un** vehículo.

Pero la composición es diferente a la herencia también es un tipo de relación.
Por ejemplo, pensemos en un ordenador. Un ordenador se compone de una CPU, pantalla, ratón y teclado. Pero una pantalla no es un ordenador, un ratón no es un ordenador. Decimos que un ordenador **tiene una** pantalla, un ordenador **tiene un** teclado, etc. Eso es la composición, un todo que se construye con partes.

Vamos a ver como se implementa esto:

```java
public class Procesador {

    private String modelo;
    private int ramSlots;
    private int cardSlots;

    public Procesador(String modelo, int ramSlots, int cardSlots) {
        this.modelo = modelo;
        this.ramSlots = ramSlots;
        this.cardSlots = cardSlots;
    }

    public void presionarBotonEncendido() {
        System.out.println("Iniciando el pc");
    }

    public void cargarPrograma(String nombre) {
        System.out.println(nombre);
    }

    public String getModelo() {
        return modelo;
    }

    public void setModelo(String modelo) {
        this.modelo = modelo;
    }

    public int getRamSlots() {
        return ramSlots;
    }

    public void setRamSlots(int ramSlots) {
        this.ramSlots = ramSlots;
    }

    public int getCardSlots() {
        return cardSlots;
    }

    public void setCardSlots(int cardSlots) {
        this.cardSlots = cardSlots;
    }
}

public class Monitor {

    private String modelo;
    private String resolucion;
    private int tam;

    public Monitor(String modelo, String resolucion, int tam) {
        this.modelo = modelo;
        this.resolucion = resolucion;
        this.tam = tam;
    }

    public void dibujarPixel(int x, int y) {
        System.out.println("Pixel en " + x + y);
    }

    public String getModelo() {
        return modelo;
    }

    public void setModelo(String modelo) {
        this.modelo = modelo;
    }

    public String getResolucion() {
        return resolucion;
    }

    public void setResolucion(String resolucion) {
        this.resolucion = resolucion;
    }

    public int getTam() {
        return tam;
    }

    public void setTam(int tam) {
        this.tam = tam;
    }
}

public class Teclado {

    private String color;
    private int teclas;

    public Teclado(String color, int teclas) {
        this.color = color;
        this.teclas = teclas;
    }

    public void pushKey(char key) {
        System.out.println("Se ha presionado la tecla " + key);
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getTeclas() {
        return teclas;
    }

    public void setTeclas(int teclas) {
        this.teclas = teclas;
    }
}

```

Hemos creado las clases `Monitor`, `Teclado` y `Procesador`.
Ahora vamos a crear una clase `Ordenador` que se compondrán de las otras tres clases de la forma:

```java
public class Ordenador {

    private Procesador procesador;
    private Teclado teclado;
    private Monitor monitor;

    public Ordenador(Procesador procesador, Teclado teclado, Monitor monitor) {
        this.procesador = procesador;
        this.teclado = teclado;
        this.monitor = monitor;
    }

    public Procesador getProcesador() {
        return procesador;
    }

    public void setProcesador(Procesador procesador) {
        this.procesador = procesador;
    }

    public Teclado getTeclado() {
        return teclado;
    }

    public void setTeclado(Teclado teclado) {
        this.teclado = teclado;
    }

    public Monitor getMonitor() {
        return monitor;
    }

    public void setMonitor(Monitor monitor) {
        this.monitor = monitor;
    }
}
```

Ya hemos implementado nuestras clases que componen un `Ordenador`. Ahora vamos a ver como utilizarlas:

```java
public class Main {

    public static void main(String[] args) {
        Procesador procesador = new Procesador("Intel", 2, 3);
        Monitor monitor = new Monitor("Philips", "1024x900", 24);
        Teclado teclado = new Teclado("Negror",90);

        Ordenador ordenador = new Ordenador(procesador, teclado, monitor);
    }
}
```

Se ha creado un objeto de la clase `Ordenador` a partir de las otras clases. En herencia teníamos acceso a los atributos de la clase padre, pero ahora con composición para acceder a los métodos o atributos de las partes a partir de `Ordenador` lo haremos usando los métodos getters que tenemos en la clase y nos permite acceder a `Teclado`, `Monitor` y `Procesador`.

```java
    public static void main(String[] args) {
        Procesador procesador = new Procesador("Intel", 2, 3);
        Monitor monitor = new Monitor("Philips", "1024x900", 24);
        Teclado teclado = new Teclado("Negror",90);

        Ordenador ordenador = new Ordenador(procesador, teclado, monitor);
        ordenador.getMonitor().dibujarPixel(34, 56);
        ordenador.getProcesador().cargarPrograma("Demo");
        ordenador.getTeclado().pushKey('X');
    }
```

## Ocultar funcionalidad de los objetos parte

Otro escenario viable es el cual nos permita ocultar la funcionalidad, y no le permitamos al programa acceder directamente a los objetos que componen el todo.
Para ello, lo primero que haremos será modificar la visibilidad de los getters y ponerlos `private`, de manera que no se pueda acceder desde fuera a `Teclado`, `Monitor` o `Procesador` pero si podamos acceder internamente.

```java
public class Ordenador {

    private Procesador procesador;
    private Teclado teclado;
    private Monitor monitor;

    public Ordenador(Procesador procesador, Teclado teclado, Monitor monitor) {
        this.procesador = procesador;
        this.teclado = teclado;
        this.monitor = monitor;
    }

    private Procesador getProcesador() {
        return procesador;
    }

    private Teclado getTeclado() {
        return teclado;
    }

    private Monitor getMonitor() {
        return monitor;
    }
}
```

Una vez oculta la información veamos como podemos acceder a ella en el main. Creamos un método en la clase `Ordenador` que accederá a las distintas partes.

```java
public class Ordenador {

    private Procesador procesador;
    private Teclado teclado;
    private Monitor monitor;

    public Ordenador(Procesador procesador, Teclado teclado, Monitor monitor) {
        this.procesador = procesador;
        this.teclado = teclado;
        this.monitor = monitor;
    }

    public void encender() {
        getProcesador().presionarBotonEncendido();
        dibujarLogo();
    }

    private void dibujarLogo() {
        monitor.dibujarPixel(12, 23);
    }

    private Procesador getProcesador() {
        return procesador;
    }

    private Teclado getTeclado() {
        return teclado;
    }

    private Monitor getMonitor() {
        return monitor;
    }
}
```

En el `main` accederemos a este método:

```java
    public static void main(String[] args) {
        Procesador procesador = new Procesador("Intel", 2, 3);
        Monitor monitor = new Monitor("Philips", "1024x900", 24);
        Teclado teclado = new Teclado("Negror",90);

        Ordenador ordenador = new Ordenador(procesador, teclado, monitor);
        ordenador.encender();
    }
```
