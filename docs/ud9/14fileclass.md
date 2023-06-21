# File vs Path

En Java, `Path` y `File` son clases responsables de las operaciones de E/S de ficheros. Realizan las mismas funciones pero pertenecen a diferentes paquetes.

## Clase `File`

Las primeras versiones de Java incluyen el paquete `java.io`, que contiene casi todas las clases que podríamos necesitar para realizar operaciones de entrada y salida. La clase `File` es una representación abstracta de nombres de rutas de ficheros, directorios y métodos para manipularlos.

Un objeto `File` NO es el fichero real. No contiene los datos que contiene el fichero. Es un objeto que contiene métodos que afectan a un archivo o directorio en particular y las funciones para la manipulación real del archivo.

Ejemplo en Windows:

```java
File f = new File("C:\\Users\\temp\\data.txt");
```

En Linux el carácter separador es `/`.

## Constructor de `File`

```java
File(String pathName) //Constructor
```

`pathName` es una secuencia de nombres de directorio seguidos de un nombre de archivo. Los nombres de los directorios están separados por un carácter especial. La sintaxis de los nombres de directorio, separadores y nombres de archivo depende del sistema operativo.

!!! Warning
    Construir un objeto de la clase File NO CREA UN FICHERO

### Desventajas de la clase `File`

+ Manejo de errores
El problema más común es el manejo deficiente de errores. Muchos métodos no nos dicen ningún detalle sobre el problema encontrado o incluso lanzan excepciones.

+ Compatibilidad con metadatos
Los metadatos pueden incluir permisos, propietario del fichero y atributos de seguridad. Debido a esto, la clase `File` no admite enlaces simbólicos en absoluto, y el método rename() no funciona de manera consistente en diferentes plataformas.

+ Escalabilidad y rendimiento de métodos
También hay un problema de rendimiento porque los métodos de la clase File no escalan. Conduce a problemas con algunos directorios con una gran cantidad de archivos. Enumerar el contenido de un directorio podría provocar un bloqueo, lo que provocaría problemas de recursos de memoria.
Debido a algunos de estos inconvenientes, Oracle desarrolló la API NIO2 mejorada.

### Path vs File

Cuando construimos un objeto `File` lo hacemos a través del constructor, mientras que en la clase `Path` se usa un método estático.

```java
File file = new File("ada.txt");
Path path = Paths.get("ada.txt");
```
