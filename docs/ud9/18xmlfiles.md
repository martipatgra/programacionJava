# Ficheros XML

XML es la abreviatura de Extensible Markup Language y es un formato de intercambio de datos establecido. XML fue definido en 1998 por el World Wide Web Consortium (W3C). A diferencia de otros lenguajes, XML da soporte a bases de datos, siendo útil cuando varias aplicaciones deben comunicarse entre sí o integrar información.

## Estructura de un documento XML

Un documento XML consta de elementos, cada elemento tiene una etiqueta de inicio, contenido y una etiqueta de finalización.
Una etiqueta consiste en una marca hecha en el documento, que señala una porción de este como un elemento. Un pedazo de información con un sentido claro y definido. Las etiquetas tienen la forma `<nombre>`, donde *nombre* es el nombre del elemento que se está señalando.

## Documento XML válido

Los documentos denominados como «bien formados» (del inglés well formed) son aquellos que cumplen con todas las definiciones básicas de formato y pueden, por lo tanto, analizarse correctamente por cualquier analizador sintáctico (parser) que cumpla con la norma. Esto significa que debe aplicarse a las siguientes condiciones:

1. Cada etiqueta de apertura tiene una etiqueta de cierre.
2. Todas las etiquetas están completamente anidadas.
3. Los documentos XML solamente permiten un elemento raíz del que todos los demás sean parte, es decir, solo pueden tener un elemento inicial.
4. El XML es sensible a mayúsculas y minúsculas.

## Partes de un documento XML

### Prólogo

Aunque no es obligatorio, los documentos XML pueden empezar con unas líneas que describen la versión XML, el tipo de documento y otras cosas.

El prólogo de un documento XML contiene:

+ Una declaración XML. Es la sentencia que declara al documento como un documento XML.
+ Una declaración de tipo de documento. Enlaza el documento con su DTD (definición de tipo de documento), o el DTD puede estar incluido en la propia declaración o ambas cosas al mismo tiempo.
+ Uno o más comentarios e instrucciones de procesamiento.
Ejemplo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

### Cuerpo

A diferencia del prólogo, el cuerpo no es opcional en un documento XML, el cuerpo debe contener solo un elemento raíz, característica indispensable también para que el documento esté bien formado. Sin embargo es necesaria la adquisición de datos para su buen funcionamiento.

### Elementos

Los elementos XML pueden tener contenido (más elementos, caracteres o ambos), o bien ser elementos vacíos.

### Atributos

Los elementos pueden tener atributos, que son una manera de incorporar características o propiedades a los elementos de un documento. Deben ir entre comillas.

```xml
<person sex="female">
  <firstname>Patricia</firstname>
  <lastname>Marti</lastname>
</person>
```

En el ejemplo, el elemento `person` tiene un atributo `sex`.

### Comentarios

Comentarios a modo informativo para el programador que han de ser ignorados por el procesador. Los comentarios en XML tienen el siguiente formato:

```xml
  <!-- Comment -->
```

## Ejemplo de un documento XML

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no">

<!-- This is a comment -->

<products> 
    <product> 
        <name>Cereales</name> 
        <price>3.45</price> 
    </product> 
    <product> 
        <name>Colacao</name> 
        <price>1.45</price> 
    </product> 
    <product> 
        <name>Agua mineral</name> 
        <price>1.00</price> 
    </product> 
</products>
```

## Url XML

[El estándar XML](https://www.w3.org/TR/REC-xml/)

## Java XML

Java permite usar analizadores XML como DOM, SAX, StAX y JDOM para leer y escribir documentos XML; Además, JAXB para convertir XML a/desde objetos.

En general, existen dos modelos de programación para trabajar con documentos XML: DOM y SAX (Streaming).

### DOM

El modelo de objeto de documento (DOM) utiliza nodos para representar los documentos XML completos como una estructura de árbol y almacenarlos en la memoria.

DOM es bueno para manipular el archivo XML pequeño, como leer, escribir y modificar la estructura XML; DOM NO es para analizar o manipular archivos XML grandes porque construir la estructura XML completa en la memoria consume mucha memoria.

### SAX

La API simple para XML (SAX) permite leer el archivo XML de principio a fin, es decir, de manera secuencial.

El SAX es rápido y eficiente, requiere mucha menos memoria que DOM porque SAX no crea una representación interna (estructura de árbol) de los datos XML, como lo hace un DOM.

### StAX

Streaming API for XML (StAX) está basado en eventos, permite leer y escribir documentos XML. StAX ofrece un modelo de programación más simple que SAX y una gestión de memoria más eficiente que DOM.

## Ejemplo lectura XML desde una API

```java
private static Document loadXMLDocument(String url)  {
    try (InputStream input = new URL(url).openStream()) {
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        DocumentBuilder builder = factory.newDocumentBuilder();
        return builder.parse(input);
    } catch (Exception e) {
        throw new RuntimeException(e);
    }
}

```

## Escritura de un documento XML

```java
private static void writeXml(Document doc,
                                 OutputStream output)
        throws TransformerException {

    TransformerFactory transformerFactory = TransformerFactory.newInstance();
    Transformer transformer = transformerFactory.newTransformer();
    transformer.setOutputProperty(OutputKeys.INDENT, "yes");
    DOMSource source = new DOMSource(doc);
    StreamResult result = new StreamResult(output);
    transformer.transform(source, result);

}
```
