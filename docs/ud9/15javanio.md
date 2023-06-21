# java.nio

+ `java.nio.file.Path`: Es una interfaz que localiza un fichero o directorio mediante una ruta dependiente del sistema.
+ `java.nio.file.Files`: En combinación con `Path`, realiza operaciones en ficheros o directorios.
+ `java.nio.file.FileSystem`: Proporciona una interfaz para el sistema de ficheros y una fábrica para crear `Path` y otros objetos que acceden al sistema de ficheros.
+ Todos los métodos que acceden al sistema de ficheros lanzan una excepción de tipo `IOException`.

## `Path`

Ofrece una API completamente nueva para trabajar con E/S. Además, al igual que la clase `File`, `Path` también crea un objeto que se puede usar para ubicar un archivo en un sistema de archivos.

`Path` puede realizar todas las operaciones que se pueden realizar con la clase `File`.

Muchos ficheros utilizan la notación "." para denotar el directorio actual y ".." para denotar el directorio del padre.

## `FileSystems`. Cargar un fichero con FileSystems

```java
Path path = FileSystems.getDefault().getPath("fichero.txt");
```

## Escritura en un fichero

```java
Path p = FileSystems.getDefault().getPath("ficPrueba.txt");
try(BufferedWriter bw = Files.newBufferedWriter(p)) {
    for (int i = 0; i < 10; i++) {
        bw.write(String.valueOf(i));
    }
} catch (IOException e) {
    throw new RuntimeException(e);
}
```

## Lectura de un fichero

Con buffer:

```java
Path p = FileSystems.getDefault().getPath("ficPrueba.txt");
try (BufferedReader br = Files.newBufferedReader(p)) {
    String input;
    while ((input = br.readLine()) != null) {
        System.out.println(input);
    }
} catch (IOException e) {
    throw new RuntimeException(e);
}

Path p = FileSystems.getDefault().getPath("ficPrueba.txt");
try {
    List<String> lines = Files.readAllLines(p);
    for (String line: lines) {
        System.out.println(line);
    }
} catch (IOException e) {
    throw new RuntimeException(e);
}
```

## Listar todos los directorios con Files.walk

Es importante utilizar el try with resources para cerrar el stream. Viene especificado en la documentación oficial

!!! Note Nota
    This method must be used within a try-with-resources statement or similar control structure to ensure that the stream's open directories are closed promptly after the stream's operations have completed.

```java
List<Path> result;
try (Stream<Path> walk = Files.walk(path)) {
    result = walk.filter(Files::isDirectory)
            .collect(Collectors.toList());
}

```