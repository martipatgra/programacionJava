# 🖲️ Bucles `while` y `do-while` con condicionales `if` en Java

En muchos programas se combinan **bucles de repetición** (`while`, `do-while`) con **sentencias condicionales** (`if`, `if-else`).  
Esto permite ejecutar **diferentes acciones dentro del bucle** dependiendo de las condiciones. E implementar la lógica de un programa.

---

## 📌 Usar `if` dentro de un bucle

El `if` se utiliza para **tomar decisiones** en cada iteración del bucle.  
De esta forma, el flujo dentro del bucle puede variar según los datos.

Ejemplo sencillo:

```java
int i = 0;
while (i < 5) {
    if (i % 2 == 0) {
        System.out.println(i + " es par");
    } else {
        System.out.println(i + " es impar");
    }
    i++;
}
```
**Salida:**
```
0 es par
1 es impar
2 es par
3 es impar
4 es par
```

---

## 🔍 Ejemplo con `do-while` e `if`

```java
Scanner sc = new Scanner(System.in);
int numero;
do {
    System.out.print("Introduce un número (0 para salir): ");
    numero = sc.nextInt();

    if (numero > 0) {
        System.out.println("Es positivo");
    } else if (numero < 0) {
        System.out.println("Es negativo");
    } else {
        System.out.println("Fin del programa");
    }

} while (numero != 0);
```
👉 El programa **se repite mientras `numero != 0`**. Dentro del bucle, con `if` comprobamos si el número es positivo, negativo o cero.

---

## 🧰 Uso típico: Menús con opciones

Los menús suelen combinar `do-while` con `if` o `switch`.  
Ejemplo con `if`:

```java
Scanner sc = new Scanner(System.in);
int opcion;

do {
    System.out.println("=== MENÚ ===");
    System.out.println("1. Saludar");
    System.out.println("2. Despedir");
    System.out.println("0. Salir");
    System.out.print("Elige opción: ");
    opcion = sc.nextInt();

    if (opcion == 1) {
        System.out.println("¡Hola!");
    } else if (opcion == 2) {
        System.out.println("¡Adiós!");
    } else if (opcion != 0) {
        System.out.println("Opción inválida");
    }

} while (opcion != 0);
```
> 🔑 Muy usado en **programas interactivos** donde el usuario puede elegir acciones.

---

## 🧪 Ejemplo práctico: contar positivos y negativos

```java
Scanner sc = new Scanner(System.in);
int numero, positivos = 0, negativos = 0;

System.out.println("Introduce números (0 para salir):");
do {
    numero = sc.nextInt();
    if (numero > 0) {
        positivos++;
    } else if (numero < 0) {
        negativos++;
    }
} while (numero != 0);

System.out.println("Positivos: " + positivos);
System.out.println("Negativos: " + negativos);
```
👉 Aquí el `if` **diferencia casos** dentro del bucle y acumula estadísticas.

---

## 🎯 Ejemplo con condiciones compuestas

Podemos usar operadores lógicos (`&&`, `||`) dentro del `if`:

```java
int i = 1;
while (i <= 10) {
    if (i % 2 == 0 && i % 3 == 0) {
        System.out.println(i + " es múltiplo de 2 y de 3");
    }
    i++;
}
```
**Salida:**
```
6 es múltiplo de 2 y de 3
```

---

## 🧠 Errores típicos a evitar 🚧
- ❌ **Olvidar actualizar la variable** → bucle infinito.
- ❌ **Confundir condición del bucle y del if** (ej: `while (x > 0)` pero dentro restamos sin control).
- ❌ No cubrir todos los casos en el `if` → situaciones sin tratar.

---

## ✅ Resumen exprés
- `while` y `do-while` permiten repetir código.  
- `if` dentro de un bucle decide **qué hacer en cada vuelta**.  
- Muy útil para **menus, validaciones, contadores, juegos**.  
- Vigila las condiciones y actualizadores para evitar bucles infinitos.  