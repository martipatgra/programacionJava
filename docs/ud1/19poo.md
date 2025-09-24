# 💾 Introducción a la Programación Orientada a Objetos (POO)

La **programación modular** consiste en dividir un programa en módulos para hacerlo más legible y manejable.  
La **POO (Programación Orientada a Objetos)** parte de esa idea, pero da un paso más allá al introducir el **concepto de objeto**, lo que supone un gran avance en **modularización, reutilización y organización del código**.

---

## 🔑 Fundamentos de la POO
Los cuatro pilares básicos de la POO son:

- **Abstracción** 🧩: simplificar la realidad representando solo los aspectos esenciales de un objeto.  
- **Encapsulación** 🔒: ocultar los detalles internos y exponer solo lo necesario mediante atributos privados y métodos públicos.  
- **Herencia** 🧬: crear nuevas clases basadas en clases existentes, reutilizando y extendiendo su funcionalidad.  
- **Polimorfismo** 🎭: capacidad de un objeto de comportarse de diferentes formas según el contexto (sobrecarga y sobreescritura de métodos).  

![Java](../img/Object-Oriented-Programming.png)

---

## 🟢 Concepto de objeto
Entonces, ¿qué es un objeto? Al igual que en el mundo real, un objeto es cualquier cosa. Un objeto puede ser una cosa física, como un coche, o una cosa mental, como una idea.

Un **objeto** es una entidad que combina **atributos** (datos), **métodos** (comportamientos) e **identidad** (nombre único a un objeto y permite que un objeto interactúe con otros objetos) 

Ejemplo en Java:

```java
public class Coche {
    // Atributos
    String marca;
    int velocidad;

    // Método
    void acelerar() {
        velocidad += 10;
    }
}
```

Aquí, `Coche` es una **clase**, y a partir de ella podremos crear **objetos** (instancias).

```java
Coche miCoche = new Coche();
miCoche.marca = "Toyota";
miCoche.acelerar();
```

---

## 🏗️ Atributos y acciones
- **Atributos**: describen el estado del objeto.  
  Ejemplo: `marca`, `modelo`, `color`.  
- **Acciones (métodos)**: describen lo que el objeto sabe hacer.  
  Ejemplo: `acelerar()`, `frenar()`, `arrancar()`.  

---

## 🌟 Características básicas de la POO
- Modularidad (el código se organiza en clases).  
- Reutilización (herencia y polimorfismo).  
- Facilidad de mantenimiento (encapsulación y abstracción).  
- Mayor legibilidad y cercanía con el mundo real.  

---

## ⚙️ Creación y destrucción de objetos
- **Creación**: con la palabra clave `new`.  
  ```java
  Coche coche1 = new Coche();
  ```

- **Destrucción**: en Java, los objetos que ya no se usan son eliminados automáticamente por el **Garbage Collector** (no hace falta liberarlos manualmente).  

---

## 🖥️ Uso de objetos
Para acceder a **atributos** y **métodos** se utiliza el operador `.`:

```java
Coche coche2 = new Coche();
coche2.marca = "Ford";   // acceso a atributo
coche2.acelerar();       // llamada a método
```

Más adelante veremos la visibilidad de los métodos y atributos de los objetos.

---

## 🚗 Ejemplo completo: Clase `Coche`
```java
public class Coche {
    // Atributos
    String marca;
    int velocidad;

    // Constructor
    public Coche(String marca) {
        this.marca = marca;
        this.velocidad = 0;
    }

    // Métodos
    public void acelerar() {
        velocidad += 10;
    }

    public void frenar() {
        velocidad -= 10;
    }

    public void mostrarInfo() {
        System.out.println("Marca: " + marca + " | Velocidad: " + velocidad);
    }
}

// Uso en main
public class Main {
    public static void main(String[] args) {
        Coche coche1 = new Coche("Toyota");
        coche1.acelerar();
        coche1.mostrarInfo();
    }
}
```

---

## 📋 Resumen
- La POO organiza programas en **clases** y **objetos**.  
- Un objeto combina **estado** (atributos) y **comportamiento** (métodos).  
- Sus pilares son **abstracción, encapsulación, herencia y polimorfismo**.  
- En Java, los objetos se crean con `new` y se gestionan automáticamente con el **Garbage Collector**.  
- Permite escribir código más **modular, reutilizable y cercano al mundo real**.
