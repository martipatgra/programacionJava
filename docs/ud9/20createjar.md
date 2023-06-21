# Cómo crear un jar en IntelliJ

1. Vamos a File --> Project Structure

![artifact](../img/ud9/13artifact.png)

2. En la sección Artifacts, seleccionamos el símbolo "+" y seleccionamos el formato .jar --> "From modules with dependencies"

![artifact](../img/ud9/14artifact.png)

4. Le decimos cuál es la clase main y aceptamos.

![artifact](../img/ud9/15artifact.png)

5. Todavía no hemos construido el .jar. Para crearlo vamos al menú "Build" --> "Build Artifact".

![artifact](../img/ud9/16artifact.png)

6. Seleccionamos "Build".

![artifact](../img/ud9/17artifact.png)

El .jar estará en la carpeta del proyecto dentro de /out/artifacts/...