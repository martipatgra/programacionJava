# 🥳 try-with-resources

La sentencia **_try-with-resources_** es una sentencia try que declara uno o más recursos (resources). Un recurso es un objeto que debe cerrarse después de que el programa termine con él. La instrucción try-with-resources garantiza que cada recurso se cierre al final de la instrucción. Cualquier objeto que implemente java.lang.AutoCloseable, que incluye todos los objetos que implementen java.io.Closeable, se puede utilizar como recurso, por lo que no sería necesario realizar la sentencia `recurso.close()`.

Antes de Java SE 7, se podía usar un bloque `finally` para asegurarse de que un recurso se cerraba, independientemente de si el try generaba excepción o no.

El siguiente ejemplo, creamos el objeto `FileWriter` en la línea 2, en vez de hacerlo en la 4 porque el `finally` de la línea 8 se encuentra en otro scope y la variable `fw` no existe.

```java hl_lines="2 4 8"
public static void main(String[] args) {
        FileWriter fw =null;
        try {
            fw = new FileWriter("prueba.txt");
            fw.write("texto de prueba");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (fw != null) {
                    System.out.println("El fichero se cierra");
                    fw.close();
                }
            }catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```

Al hacer el `close()` manualmente, vemos que el código queda bastante engorroso, ya que la sentencia close lanza una excepción que hay que capturar. Con try-with-resources el código queda más limpio.

!!! important "Importante diferencia entre try-with-resources y try con finally 🤔"
    Existe una ligera mejora al usar try-with-resources. Si en el código anterior se lanzara una excepción al escribir el fichero, ésta se capturaría y se ejecutaría el finally a continuación. Si éste a su vez, lanzara también una excepción al llamar al método `close`, se reenviaría esta, NO la primera que se generó. Esto cambia ligeramente en el try-with-resources, puesto que enviaría la primera excepción que se generó. Lo cual tiene sentido, puesto que fue la causante del error.

Así quedaría el código usando try-with-resources:

```java
public static void main (String[] args) throws IOException {
    try(FileWriter fw = new FileWriter("prueba.txt");
        FileWriter fw2 = new FileWriter("prueba2.txt");) {
        //si quisiera poner un segundo writer quedaría así

        fw.write("texto de prueba");
    }
}
```

!!! note "Nota 🤓"
    Podemos declarar varios recursos dentro de un mismo try como se ve en el ejemplo.