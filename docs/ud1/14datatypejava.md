# 💾 Tipos de datos

Un tipo de datos es un conjunto de valores y un conjunto de operaciones definidas en ellos.
Se pueden clasificar en primitivos y objetos.

![Java](../img/primitives.png)

---

## 🧩 Tipos primitivos

Los **primitivos son los más básicos y fundamentales, vienen integrados en Java**.  
Especifican **el tipo de valor almacenado en una variable y el tamaño en memoria**.  

👉 Existen **8 tipos primitivos** en Java: `byte`, `short`, `int`, `long`, `float`, `double`, `boolean` y `char`.

---

### 🔸 byte

Como su propio nombre denota, emplea un solo byte (8 bits) de almacenamiento.

- **Tamaño:** 8 bits  
- **Rango:** [-128, 127]  
- Se usa raramente, ocupa muy poca memoria.

```java
  byte b = 2;
```

### 🔸 short

- **Tamaño**: 16 bits
- **Rango**: [-32.768, 32.767]

```java
  short s = 3467;
```

### 🔸 int

- **Tamaño**: 32 bits
- **Rango**: [-2.147.483.648, 2.147.483.647]
- ✅ **Es el entero predeterminado en Java**.

```java
        int maxValor = 2147483647;
        // Desde Java 7 puedes usar guiones bajos
        int maxValue = 2_147_483_647;
```

### 🔸 long

Es el tipo entero de mayor tamaño.

- **Tamaño**: 64 bits
- **Rango**: [-9.223.372.036.854.775.808, 9.223.372.036.854.775.807]
- **Se indica con una L al final**.

```java
  long myLongNumber = 500L;
```

### 🔸 float

Tiene una parte flotante que sirve para expresar números decimales. No se recomienda mucho su uso.

- **Tamaño**: 32 bits
- **Rango**: ±1.4E-45 a ±3.4028235E38
- **Decimales de precisión simple.**
- **Se indica con una f al final.**

```java
  float f = 4;
  float f = 4f;
```

### 🔸 double

Se recomienda su uso. Muchas librerías internas de Java, relacionadas con operaciones matemáticas, usan double.

- **Tamaño**: 64 bits
- **Rango**: ±4.9E-324 a ±1.7976931348623157E308
- ✅ **Es el decimal predeterminado en Java**.

```java
  double d = 5.0;
  double d = 5d;
```

### 🔸 char

Se utiliza para almacenar caracteres (letras, números, signos, etc.) individuales.

- **Tamaño**: 16 bits
- **Permite almacenar caracteres Unicode** (hasta 65.535).
- **Útil para representar letras, símbolos y emojis**.

Unicode es un estándar de codificación internacional que nos permite representar diferentes idiomas; y la forma en que funciona es usando una combinación de los dos bytes que un char ocupa en la memoria, que puede representar hasta 65535 diferentes tipos de caracteres. [Unicode table.](https://elcodigoascii.com.ar/)

```java
  char c = 'P';
  char u = '\u00A2';//print unicode character
```

⚡ Un carácter precedido por una barra invertida (\) es una secuencia de escape y tiene un significado especial para el compilador. La siguiente tabla muestra las secuencias de escape de Java:

![Java](../img/scapedsequences.png)

### 🔸 boolean

- **Representa solo dos valores posibles**: true o false.
- **Tamaño no definido exactamente en Java** (depende de la JVM).
- Tiene la finalidad de facilitar el trabajo con valores "verdadero/falso" (booleanos), resultantes por regla general de evaluar expresiones.

```java
  boolean isMyNamePatri = true;
```

---

# Tipos de datos primitivos en Java

| Tipo   | Tamaño en bits | Valor mínimo                      | Valor máximo                       | Ejemplo            |
|--------|----------------|-----------------------------------|------------------------------------|--------------------|
| byte   | 8              | -128                              | 127                                | `byte b = 100;`    |
| short  | 16             | -32,768                           | 32,767                             | `short s = 1000;`  |
| int    | 32             | -2,147,483,648                    | 2,147,483,647                      | `int i = 100000;`  |
| long   | 64             | -9,223,372,036,854,775,808        | 9,223,372,036,854,775,807          | `long l = 100000L;`|
| float  | 32             | ≈ ±1.4E-45                        | ≈ ±3.4028235E38                     | `float f = 3.14f;` |
| double | 64             | ≈ ±4.9E-324                       | ≈ ±1.7976931348623157E308           | `double d = 3.14;` |
| char   | 16             | 0 ( '\u0000' )                    | 65,535 ( '\uffff' )                 | `char c = 'A';`    |
| boolean| 1 bit*         | `true` / `false`                  | —                                  | `boolean b = true;`|

\* El tamaño de `boolean` no está especificado exactamente en Java; internamente depende de la JVM, pero conceptualmente ocupa 1 bit.

---

## 📦 Wrapper classes en Java (clases contenedores)

Las clases contenedoras o **Wrapper classes** proporcionan una forma de utilizar tipos de datos primitivos como objetos. 

Son muy útiles para operaciones avanzadas y colecciones (ej. ArrayList).

En Java, tenemos una Wrapper class para cada uno de los 8 tipos de datos primitivos. Gracias a esto, podemos realizar operaciones en un dato primitivo.

| Tipo primitivo | Wrapper class | Métodos útiles |
|----------------|---------------|----------------|
| byte           | Byte          | `Byte.parseByte("1")`, `Byte.MIN_VALUE` (-128), `Byte.MAX_VALUE` (127) |
| short          | Short         | `Short.parseShort("12")`, `Short.MIN_VALUE` (-32,768), `Short.MAX_VALUE` (32,767) |
| int            | Integer       | `Integer.parseInt("123")`, `Integer.MIN_VALUE` (-2,147,483,648), `Integer.MAX_VALUE` (2,147,483,647) |
| long           | Long          | `Long.parseLong("9999")`, `Long.MIN_VALUE` (-9,223,372,036,854,775,808), `Long.MAX_VALUE` (9,223,372,036,854,775,807) |
| float          | Float         | `Float.parseFloat("3.14")`, `Float.MIN_VALUE` (≈1.4E-45), `Float.MAX_VALUE` (≈3.4028235E38) |
| double         | Double        | `Double.parseDouble("2.71")`, `Double.MIN_VALUE` (≈4.9E-324), `Double.MAX_VALUE` (≈1.7976931348623157E308) |
| boolean        | Boolean       | `Boolean.parseBoolean("true")`, `Boolean.TRUE`, `Boolean.FALSE` |
| char           | Character     | `Character.isLetter('a')`, `Character.MIN_VALUE` (`'\u0000'`), `Character.MAX_VALUE` (`'\uffff'`) |

```java
   int minimoValorInt = Integer.MIN_VALUE;
   int i = Integer.parseInt("123");   // 123 (int)
```

---

📐 Cuándo usar `float` vs `double`

| Tipo   | Precisión | Memoria | Uso recomendado |
|--------|-----------|---------|-----------------|
| float  | ~7 cifras decimales | 32 bits | - Arrays grandes de números decimales (ahorro memoria) <br> - Gráficos 2D/3D, librerías que lo requieran (OpenGL, motores de juego) <br> - Dispositivos con memoria limitada |
| double | ~15 cifras decimales | 64 bits | - Cálculos matemáticos y científicos <br> - Finanzas y datos sensibles a la precisión <br> - Es el **tipo decimal predeterminado** en Java |

---
