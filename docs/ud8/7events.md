# Eventos

Cada vez que un usuario interactúa con la aplicación (nodos), se dice que ha ocurrido un evento. Existe un `UIThread` que está escuchando cuando lanzamos la aplicación. Cuando el usuario hace algo el UIThread que está escuchando, mira a ver si se lanza un evento, y si es así, envía el evento al controlador de eventos (event handler). El Event Handler se ejecuta en el subproceso del hilo UIThread. Mientras se ejecuta un evento del UIThread el usuario no puede interactuar con la aplicación.

Por ejemplo, hacer clic en un botón, mover el mouse, ingresar un carácter a través del teclado, seleccionar un elemento de la lista, desplazarse por la página, etc. son ejemplos de actividades que provocan que suceda un evento.

Un evento notifica que ha ocurrido algo importante. Los eventos suelen ser la parte "primitiva" de un sistema de eventos (también conocido como bus de eventos). Generalmente, un sistema de eventos tiene las siguientes 3 responsabilidades:

1. Trigger an event (disparar un evento),
2. Notify listeners (notificar a los oyentes partes interesadas) sobre el evento y
3. Handle the event (manejar o procesar el evento).

El mecanismo de notificación de eventos lo realiza la plataforma JavaFX automáticamente. Por lo tanto, solo consideraremos cómo disparar eventos, escuchar eventos y cómo manejarlos.

## Tipos de eventos

+ **Eventos en primer plano** (foreground events): requieren la interacción directa de un usuario. Se generan como consecuencia de la interacción de una persona con los componentes gráficos en una interfaz gráfica de usuario. Por ejemplo, hacer clic en un botón, mover el mouse, ingresar un carácter a través del teclado, seleccionar un elemento de la lista, desplazarse por la página, etc.
+ **Eventos de fondo** (background events): no requieren la interacción del usuario final. Las interrupciones del sistema operativo, fallas de hardware o software, vencimiento del temporizador, finalización de la operación son ejemplos de eventos en segundo plano.

## Eventos en JavaFX

La clase denominada `Event` del paquete `javafx.event` es la clase base para un evento. Una instancia de cualquiera de sus subclases es un evento. JavaFX proporciona una amplia variedad de eventos. Algunos de ellos se enumeran a continuación.

+ **Mouse event**: evento de entrada que ocurre cuando se hace clic en el mouse. Está representado por la clase denominada `MouseEvent`. Incluye acciones como hacer clic con el mouse, presionar el mouse, soltar el mouse, mover el mouse, objetivo ingresado con el mouse, objetivo salido del mouse, etc.

+ **Key event**: evento de entrada que indica que se produjo una pulsación de tecla en un nodo. Está representado por la clase denominada `KeyEvent`. Este evento incluye acciones como pulsación de tecla, liberación de tecla y escritura de tecla.

+ **Drag event**: evento de entrada que ocurre cuando se arrastra el mouse. Está representado por la clase llamada `DragEvent`. Incluye acciones como arrastrar para insertar, arrastrar para soltar, etc.

+ **Window event**: evento relacionado con las acciones de mostrar/ocultar ventanas. Está representado por la clase llamada `WindowEvent`.

## Manejo de eventos (Event Handling)

Es el mecanismo que controla el evento y decide qué debe suceder, si ocurre un evento. Tiene el código que se conoce como event handler que se ejecuta cuando ocurre un evento.

En JavaFX cada evento tiene:

1. **Target**: el nodo en el que se produjo un evento. Un objetivo puede ser una ventana, una escena y un nodo.

2. **Source**: la fuente a partir de la cual se genera el evento. Por ejemplo, el mouse es la fuente del evento.

3. **Type**: tipo del evento ocurrido; en el caso de un evento del mouse, el tipo de evento es presionar el mouse y soltar el mouse.

Supongamos que tenemos una aplicación que tiene botones. Si hace clic en un botón, la source será el mouse, el target será el nodo del botón presionado y el tipo de evento generado será el clic del mouse.

## Fases del manejo de eventos

Cada vez que se genera un evento, JavaFX pasa por las siguientes fases.

### Route construction (Construcción de rutas)

Cada vez que se genera un evento, la ruta predeterminada/inicial del evento está determinada por la construcción de una cadena de envío de eventos. Es el camino desde el escenario hasta el Nodo fuente.

A continuación se muestra la cadena de envío de eventos para el evento generado, cuando hacemos clic en el botón en el escenario anterior: Stage -> Scene -> Button

## Event capturing phase (Fase de captura de eventos)

Después de la fase anterior se dispara el evento. Este evento viaja a todos los nodos de la cadena de despacho anterior (de arriba a abajo). Si alguno de estos nodos tiene registrado un filtro (**filter**) para el evento generado, se ejecutará. Si ninguno de los nodos en la cadena de despacho tiene un filtro para el evento generado, entonces se pasa al nodo de destino y finalmente el nodo de destino procesa el evento.

## Event bubbling phase (Fase de propagación de eventos)

Aquí el evento viaja desde el nodo de destino hasta el nodo de Stage (de abajo hacia arriba). Si alguno de los nodos de la cadena de envío de eventos tiene un controlador (**handler**) registrado para el evento generado, se ejecutará. Si ninguno de estos nodos tiene controladores para manejar el evento, entonces el evento llega al nodo raíz y finalmente se completará el proceso.

## Event handlers and filters

Los filter y handlers de eventos son aquellos que contienen la lógica de la aplicación para procesar un evento. Un nodo puede registrarse en más de un controlador/filtro (handler/filter).

Como se mencionó anteriormente, durante el evento, el procesamiento es un filtro que se ejecuta y durante la fase de propagación del evento, se ejecuta un controlador. Todos los controladores y filtros implementan la interfaz EventHandler del paquete javafx.event.

## Añadir y eliminar un event filter

Para agregar un filtro de eventos a un nodo, debe registrar este filtro utilizando el método `addEventFilter()` de la clase Node.

```java
//Creating the mouse event handler 
EventHandler<MouseEvent> eventHandler = new EventHandler<MouseEvent>() { 
   @Override 
   public void handle(MouseEvent e) { 
      System.out.println("Hello World"); 
      boton.setFill(Color.DARKSLATEBLUE);  
   } 
};   
//Adding event Filter 
boton.addEventFilter(MouseEvent.MOUSE_CLICKED, eventHandler);
```

Para eliminar un filter hacemos:

```java
boton.removeEventFilter(MouseEvent.MOUSE_CLICKED, eventHandler);
```

## Añadir y eliminar event handler

Para agregar un controlador de eventos a un nodo, debe registrar este controlador mediante el método `addEventHandler()` de la clase Node, como se muestra a continuación.

```java
//Creating the mouse event handler 
EventHandler<MouseEvent> eventHandler = 
   new EventHandler<MouseEvent>() { 
   
   @Override 
   public void handle(MouseEvent e) { 
      System.out.println("Hello World"); 
      boton.setFill(Color.DARKSLATEBLUE);             
   } 
};    
//Adding the event handler 
boton.addEventHandler(MouseEvent.MOUSE_CLICKED, eventHandler);
```

Para eliminar:

```java
boton.removeEventHandler(MouseEvent.MOUSE_CLICKED, eventHandler);
```

[Controllers JavaFX](https://docs.oracle.com/javase/8/javafx/api/javafx/fxml/doc-files/introduction_to_fxml.html#controllers)