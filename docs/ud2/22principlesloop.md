# 🖲️ Principios y buenas prácticas de bucles en Java (while, do-while, for)

## 🧭 Elegir el tipo de bucle adecuado
- **`for`** ➜ sabes (o puedes calcular) **cuántas iteraciones** habrá. Índice claro.
- **`while`** ➜ repites **mientras** se cumpla una condición que **puede empezar falsa**.
- **`do-while`** ➜ necesitas **ejecutar al menos una vez** (menús, validaciones iniciales).
- **`for-each` (enhanced)** ➜ recorrer colecciones/arrays **sin usar índice** ni modificar la colección.

> 🔑 *Regla práctica*: “**¿Conozco el número de pasos?**” → `for`. “**¿Depende de una condición externa?**” → `while` / `do-while`.

---

## 🧰 Patrón universal de un bucle
```java
// 1) Inicialización (estado)
int i = 0; int suma = 0; // ...

// 2) Condición (permite continuar)
while (i < n) {
    // 3) Trabajo (procesar 1 paso)
    suma += datos[i];

    // 4) Actualización (acercarse al fin)
    i++;
}
```
- **Inicialización**: qué vamos a recorrer y hasta dónde, se define el valor inicial de las variables que se usarán y modificarán dentro del bucle.     
- **Invariante**: propiedad que **se mantiene** en cada vuelta (p.ej., “`suma` contiene la suma de los `i` primeros elementos”).  
- **Condición de salida**: debe **volverse falsa** con el tiempo.  
- **Actualización**: cambia el estado para **acercarse al final**.

---

## ✅ Resumen exprés
- **Antes**: define *inicialización*, *invariante*, *condición de salida*, *actualización*.
- **Durante**: vigila límites e índices; evita off‑by‑one y mezcla peligrosa de `Scanner`.
- **Después**: comprueba resultados con casos pequeños y añade *tests*.
