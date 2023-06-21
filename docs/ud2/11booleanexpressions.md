# Expresiones booleanas

Las sentencias if del capítulo anterior incluían preguntas simples de verdadero / falso (expresiones booleanas) como num<10 o jugadores==1. A menudo, las expresiones booleanas simples no son suficientes. Este capítulo trata sobre expresiones booleanas más complicadas.

## **&&**

El operador **AND &&** es un operador lógico. Un operador lógico examina dos valores verdadero / falso y genera un único valor verdadero / falso.

Por ejemplo cuando necesitas verificar más de una expresión.

```java
    if (harina == 100 && azucar >= 65) {

    }
```

Cada parte es una expresión relacional. Una expresión relacional es un tipo de expresión booleana que usa un operador relacional para calcular un valor verdadero o falso.

Las expresiones se evalúan de izquierda a derecha, así, tan pronto se detecta el primer false, la expresión entera se convierte en false y no se evalúa el resto de expresiones.

## **||**

El operador **OR ||** se usa en una expresión booleana para verificar que haya al menos una verdadera. Si solo un lado es verdadero, toda la expresión es verdadera. Si ambos lados son falsos, toda la expresión es falsa.

```java
    if (ahorrosMensuales > 1000 || préstamo == 3000) {

    }
```

## **!**

El operador **NOT !** cambia de verdadero a falso y de falso a verdadero. Esto puede parecer una tontería, pero a menudo es útil. A veces es más natural expresar una condición de una manera particular, pero la lógica del programa requiere lo contrario de lo que ha escrito.

```java
    if (!(precio < 35)) {

    }
```
