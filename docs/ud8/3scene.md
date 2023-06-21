# JavaFX Scene

Para mostrar cualquier cosa en un escenario `Stage` se necesita una escena `Scene`. **Un `Stage` solo puede mostrar una escena a la vez, pero es posible intercambiar la escena en tiempo de ejecución.** Al igual que un escenario en un teatro se puede reorganizar para mostrar varias escenas durante una obra, un objeto de escenario (stage) en JavaFX puede mostrar varias escenas (una a la vez) durante la vida útil de una aplicación JavaFX.

Quizás se pregunte por qué una aplicación JavaFX tendría más de una escena por etapa. Imagina un juego de computadora. Un juego puede tener múltiples "pantallas" para mostrar al usuario. Por ejemplo, una pantalla de menú inicial, la pantalla principal del juego (donde se juega el juego), una pantalla de finalización del juego y una pantalla de puntuación más alta. Cada una de estas pantallas puede ser representada por una escena diferente. Cuando el juego necesita cambiar de una pantalla a la siguiente, simplemente adjunta la escena correspondiente al objeto Stage de la aplicación JavaFX.

Una escena está representada por un objeto `Scene` dentro de una aplicación JavaFX.

!!! Note
    Para que un objeto `Scene` sea visible debe configurarse en un `Stage`.

## Scene Graph

Todos los componentes visuales (controls, layouts, etc.) deben adjuntarse a un `Scene` para ser mostrados, y ese `Scene` debe adjuntarse a un `Stage` para que la escena completa sea visible. El objeto gráfico total final de todos los controles, layouts, etc. adjuntos a un `Scene` se denomina **gráfico de escena (Scene Graph)**.

Consta de todos los nodos que se adjuntan a un objeto de Scene determinado. Cada objeto Scene tiene su propio gráfico de escena.

El Scene Graph tiene un único nodo raíz. Se pueden adjuntar otros nodos al nodo raíz en una estructura de datos similar a un árbol (un árbol es una especie de gráfico).

### Crear un Scene

Para crear un objeto `Scene` lo haremos a través de su constructor. Como parámetro, se debe pasar el componente raíz de la GUI de JavaFX que actuará como la vista raíz que se mostrará dentro de la escena.

```java
VBox  vBox  = new VBox();
Scene scene = new Scene(vBox);
```

### Establecer un Scene en un Stage

Para hacer visible un `Scene` debe asignarse a un `Stage`.

```java
VBox vBox = new VBox(new Label("A JavaFX Label"));
Scene scene = new Scene(vBox);

Stage stage = new Stage();
stage.setScene(scene);
```

**Un Scene se puede adjuntar a un solo Stage a la vez, y el Stage también puede mostrar solo un Scene a la vez.**

### Scene Mouse Cursor

Es posible configurar el cursor del mouse de un `Scene`. Se establece el cursor del mouse de una escena a través del método `setCursor()`.

```java
scene.setCursor(Cursor.OPEN_HAND);
```

La clase `javafx.scene.Cursor` contiene muchas constantes que puede usar para especificar qué cursor del mouse desea mostrar. Algunas de estas constantes son:

+ Cursor.OPEN_HAND
+ Cursor.CLOSED_HAND
+ Cursor.CROSSHAIR
+ Cursor.DEFAULT
+ Cursor.HAND
+ Cursor.WAIT
+ Cursor.MOVE

Puede consultar el resto en la documentación oficial de JavaFX.
