# Expresiones Regulares

Una expresión regular (regex) define un patrón de búsqueda para cadenas. El patrón de búsqueda puede ser cualquier cosa, desde un carácter simple, una cadena fija o una expresión compleja que contenga caracteres especiales que describan el patrón.

Se puede usar una expresión regular para buscar, editar y manipular texto.

La expresión regular se aplica en el texto de izquierda a derecha.

Se usa ampliamente para definir la restricción en cadenas como contraseña y validación de correo electrónico.

Java Regex API proporciona 1 interfaz y 3 clases en el paquete java.util.regex:

+ MatchResult interface
+ Matcher class
+ Pattern class
+ PatternSyntaxException class

## Clases de caracteres y límites de coincidencia

La forma más simple de una expresión regular (regex) es una cadena, un literal, un String. Por ejemplo, "Hola" es una regex que coincide (matches) con la palabra "Hola".

Si solo usáramos literales como patrón para buscar en un String, las regex no serían muy interesantes. Por eso, se crearon las **Character classes & boundary matches**.

Los boundary matches o límites de coincidencia son: ^ (al principio del String), $ (final del String), \b (principio y final palabra).

Una clase caracter es como un comodín y representa un conjunto o clase de caracteres.

| Regex     | Descripción                                                                                                               |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
| .         | Coincide con cualquier carácter.                                                                                          |
| ^pattern  | El símbolo ^ indica al inicio del String. Encuentra la regex que coincide con el patrón dado al comienzo del String.      |
| pattern$  | El símbolo $ indica el final del String. Encuentra la regex que coincide con el patrón dado al final del String.          |
| [abc]     | Los corchetes representan un conjunto. El String debe coincidir con la/s letra/s dentro del corchete.                     |
| [abc][12] | El String debe coincidir con las letras a, b ó c, seguidas de 1 ó 2.                                                      |
| [^abc]    | El símbolo ^ dentro de los corchetes indica negación. El String debe coincidir con cualquier carácter excepto a ó b ó c.  |
| [a-z1-9]  | Rango. Busca coincidir las letras minúsculas de la a a la z (ambas incluidas) y los dígitos del 1 al 9 (ambos incluidos). |
| a\|b      | Encuentra en el String las ocurrencias de a ó b.                                                                          |
| ab        | Encuentra en el String todas las ocurrencias de 'a' seguido de una 'b'.                                                   |

## Meta caracteres

Los siguientes metacaracteres tienen un significado predefinido y hacen que ciertos patrones comunes sean más fáciles de usar. Por ejemplo, puede usar \d como definición simplificada para [0..9].

| Regex     | Descripción                                                                             |
|-----------|-----------------------------------------------------------------------------------------|
| \d        | Cualquier dígito. Equivale a [0-9].                                                     |
| \D        | No dígito. Equivale a [^0-9].                                                           |
| \s        | Espacio en blanco. Equivale a [ \t\n\x0b\r\f]                                           |
| \S        | No espacio en blanco. Equivale a [^\s]                                                  |
| \w        | Una letra mayúscula o minúscula, un dígito o el carácter '\_'. Equivale a  [a-zA-Z0-9_] |
| \W        | Equivale a [^\w]                                                                        |
| \S+       | Varios caracteres que no son espacios en blanco                                         |
| \b        | Límite de una palabra                                                                   |

### Especificación de modos dentro de la expresión regular

Puede agregar los siguientes modificadores de modo al comienzo de la expresión regular. Para especificar múltiples modos, simplemente se juntan: (?ismx).

+ (?i) hace que la expresión regular sea insensible a mayúsculas y minúsculas.
+ (?s) para "modo de una sola línea" hace que el punto coincida con todos los caracteres, incluidos los saltos de línea.
+ (?m) para "modo multilínea" hace que el símbolo de intercalación y el dólar coincidan al principio y al final de cada línea en la cadena de asunto.

## Cuantificadores Regex

Los cuantificadores especifican el número de ocurrencias de un carácter.

Un cuantificador define con qué frecuencia puede ocurrir un elemento. Los símbolos ?, *, + y {} son calificadores.

| Regex     | Descripción                                                                             |
|-----------|-----------------------------------------------------------------------------------------|
| *         | Indica que ocurre 0 ó más veces. Equivale a {0,}.          |
| +         | Indica que ocurre 1 ó más veces. Equivale a {1,}.          |
| ?         | Indica que ocurre 0 ó 1 veces. Equivale a {0,1}.           |
| {X}       | Indica que lo que va justo antes de las llaves {} se repite X número de veces. |
| {X, Y}    | Indica que lo que va justo antes de las llaves {} se repite mínimo X número de veces y máximo Y. |
| *?        | ? después de un cuantificador lo convierte en un cuantificador perezoso (lazy). Intenta encontrar la coincidencia más pequeña. Esto hace que la expresión regular se detenga en la primera coincidencia. |

En la documentación de Oracle podemos ver todas las clases de caracteres que hay para construir una expresión regular.

<https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html>

### Entrena tus Regex

<https://regexcrossword.com/>

## Java Regex Core Classes

La API de expresiones regulares de Java consta de dos clases principales. Estos son:

`Pattern` (java.util.regex.Pattern)
`Matcher` (java.util.regex.Matcher)

## Clase [`Pattern`](https://docs.oracle.com/javase/9/docs/api/java/util/regex/Pattern.html)

La clase `Pattern` se utiliza para crear patrones (expresiones regulares). Un patrón es una expresión regular precompilada en forma de objeto (como una instancia de patrón), capaz de compararse con un texto.

```java
String regex = ".*http://.*";

Pattern pattern = Pattern.compile(regex);
```

## Clase [`Matcher`](https://docs.oracle.com/javase/9/docs/api/java/util/regex/Matcher.html)

La clase `Matcher` se usa para hacer coincidir una expresión regular determinada (ùna instancia de `Pattern`) con un texto varias veces. En otras palabras, buscar múltiples ocurrencias de la expresión regular en el texto. `Matcher` nos dirá en qué parte del texto (índice de caracteres) encontró las ocurrencias. Puede obtener una instancia de Matcher a partir de una instancia de Pattern.

Implementa la interfaz `MatchResult`.

Algunos de los métodos de la clase Matcher son:

+ **boolean matches():** prueba si la expresión regular coincide con el patrón.
+ **booleano find():** encuentra la siguiente expresión que coincide con el patrón.
+ **boolean find(int start):** encuentra la siguiente expresión que coincide con el patrón del número de inicio dado.
+ **String group():** devuelve la subsecuencia coincidente.
+ **int start():** devuelve el índice inicial de la subsecuencia coincidente.
+ **int end():** devuelve el índice final de la subsecuencia coincidente.
+ **int groupCount():** devuelve el número total de la subsecuencia coincidente.

Ejemplo:

```java
StringBuilder html = new StringBuilder("<h1>Head</h1>");
html.append("<h2>Etiqueta h2 de encabezado</h2>");
html.append("<p>Esto es un párrafo en html</p>");
html.append("<h2>Resumen</h2>");
html.append("<p>Fin del html</p>");

Pattern p = Pattern.compile("<h2>");
Matcher m = p.matcher(html);
System.out.println(m.matches());
```

### reset()

El método de la clase Matcher `reset()` restablece el estado de coincidencia internamente en el Matcher. En caso de que haya comenzado a hacer coincidir las ocurrencias en una cadena a través del método `find()`, el Matcher mantendrá internamente un estado sobre qué tan lejos ha buscado a través del texto de entrada. Al llamar a `reset()`, la coincidencia comenzará nuevamente desde el principio del texto.

### group()

Los grupos están marcados con paréntesis en la expresión regular. Por ejemplo:

> (Hola)

Esta expresión regular coincide con el texto Hola. **Los paréntesis no son parte del texto que se compara**. Los paréntesis marcan un grupo. Cuando se encuentra una coincidencia en un texto, puede obtener acceso a la parte de la expresión regular dentro del grupo.

Para acceder a un grupo se utliza el método `group(int groupNo)`. Una expresión regular puede tener más de un grupo. Por lo tanto, cada grupo está marcado con un conjunto separado de paréntesis. Para obtener acceso al texto que coincidió con la subparte de la expresión en un grupo específico, se pasa el número del grupo al método `group(int groupNo)`.

El grupo con el número 0 es siempre la expresión regular completa. Para obtener acceso a un grupo marcado entre paréntesis, debe comenzar con los números de grupo 1.

Ejemplo:

```java
String text    =
  "John writes about this, and John writes about that," +
          " and John writes about everything. "
;

String patternString1 = "(John)";

Pattern pattern = Pattern.compile(patternString1);
Matcher matcher = pattern.matcher(text);

while(matcher.find()) {
  System.out.println("found: " + matcher.group(1)); //el primer grupo de paréntesis
}
```

OUTPUT
> found: John
>  
> found: John
>  
> found: John

## Operadores lógicos

La API de Java Regex admite un conjunto de operadores lógicos que se pueden usar para combinar múltiples subpatrones dentro de una sola expresión regular.

Los operadores lógicos son: el operador and, el operador or y el operador not.

El operador **and** es implícito. Si dos caracteres (u otros subpatrones) se suceden en una expresión regular, eso significa que tanto el primer como el segundo subpatrón coinciden en gran medida con la cadena de destino.

El operador **or** es explícito y está representado por el carácter vertical **|**.

El operador **not** es explícito, está representado por el símbolo **!**, brinda la posibilidad de excluir un patrón. Con esto se puede decir que una cadena no debe ir seguida de otra cadena.

In regex, there is positive lookahead (?=) and negative lookahead (?!):

Positive lookahead (?=) ensures something followed by something else.
Negative lookahead (?!) ensures something NOT followed by something else.

For example, b(?=c) matches a b that is followed by a c. (positive lookahead)
For example, b(?!c) matches a b that is NOT followed by a c. (negative lookahead)

## Ejemplo expresión regular teléfono móvil

```java
//(+34) 655-555-555
String regexTelefono = "^([\\(]{1}[\\+]{1}34[\\)]{1}[ ]{1}[0-9]{3}[\\-]{1}[0-9]{3}[\\-]{1}[0-9]{3})$";

String t1 = "123456789";//no
String t2 = "(+35) 123456-789";//no
String t3 = "(+34) 123-456-789";//si
String t4 = "(+34)123-456-789";//no

System.out.println(t1.matches(regexTelefono));//false
System.out.println(t2.matches(regexTelefono));//false
System.out.println(t3.matches(regexTelefono));//true
System.out.println(t4.matches(regexTelefono));//false
```
