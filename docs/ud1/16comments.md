# 💾 Comentarios en Java

Los **comentarios** son ignorados por el compilador y se usan para añadir notas dentro del código.  
Sirven para explicar **qué hace el programa** o **por qué se ha hecho algo de cierta manera**.  

👉 Sin embargo:  
- ✨ Un **código bien escrito** no necesita casi comentarios.  
- 🌀 Un código **muy comentado** puede ser difícil de leer.  
- ⚠️ Los **códigos mal escritos** necesitan comentarios para poder entenderlos.  

---

## 💬 Comentarios de una línea

Se escriben con `//` y terminan al final de la línea. 

```java
//Variable que almacena la gravedad
int gravity; // Variable que almacena la gravedad
```

Puedes usarlos: 
  
- En una línea independiente.    
- Al final de una instrucción.      

---

## 📝 Comentarios multilínea

Se escriben con `/* ... */` y pueden ocupar varias líneas.

```java
   /*
      Clase que almacena en la base de datos
      los datos de una persona.
   */
   public class Persona {
      ...
   }
```

---

## 📖 Comentarios de documentación (JavaDoc)

En Java existe un tercer tipo de comentarios: los JavaDoc, que empiezan con `/**` y se usan para generar documentación automática.

```java
/**
 * Clase Persona que representa a un individuo.
 * @author TuNombre
 * @version 1.0
 */
public class Persona {
    private String nombre;

    /**
     * Constructor de Persona.
     * @param nombre Nombre de la persona
     */
    public Persona(String nombre) {
        this.nombre = nombre;
    }

    /**
     * Devuelve el nombre de la persona.
     * @return nombre
     */
    public String getNombre() {
        return nombre;
    }
}
```

---

📌 Buenas prácticas

- ✅ Usa comentarios para explicar el “por qué”, no el “qué”.
- ✅ Mantén los comentarios actualizados: un comentario desactualizado es peor que ninguno.
- ✅ **Utiliza nombres de variables, métodos y clases claros** antes que añadir comentarios innecesarios. Un código bien escrito no necesita comentarios.
- ❌ **No uses comentarios para repetir lo que el código ya dice por sí mismo.**

Ejemplo malo ❌:
```java
int x = 10; // asigna 10 a x
```

Ejemplo bueno ✅:
```java
// Regla de negocio: un usuario solo puede cambiar su email 1 vez cada 24h
boolean puedeCambiar = ultimaModificacion.plusHours(24).isBefore(now);
```