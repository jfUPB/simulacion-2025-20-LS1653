# Unidad 2


## 🛠 Fase: Apply

### Describe el concepto de tu obra generativa:
Mi obra consiste en un sistema de movimiento generado aleatoriamente en el que múltiples objetos orbitan alrededor del mouse. Estos objetos se desplazan dentro de una órbita definida por la posición del cursor, y su comportamiento cambia dinámicamente dependiendo de la interacción del usuario y las colisiones entre ellos.

Cuando dos objetos colisionan, se destruyen entre sí y el fondo de la pantalla cambia de color, tomando como base una mezcla de los colores aleatorios asignados a dichos objetos. Inmediatamente después, nuevos objetos son generados para mantener constante la población en pantalla.

Además, con un clic izquierdo del mouse, se invierte la dirección de la órbita, haciendo que los objetos comiencen a alejarse del cursor en lugar de acercarse. El movimiento de fondo también está animado mediante ruido Perlin (noise), el cual, de manera esporádica y con base en una aleatoriedad normalizada, pinta el fondo con nuevos colores que generan una atmósfera envolvente y fluida.

Como agregado, con la tecla "m" se podran generar más objetos y con la tecla "p" se para el traso generado con noise.

### ¿Cómo piensas aplicar el marco MOTION 101 y por qué?
Voy a utilizar el marco 101 al generar el movimiento por default de los objetos y tambien con el movimiento orbital generado por el mouse, esto por que puedo afectar la dirección de movimiento de manera más sencilla mediante vectores.

### ¿Qué algoritmo de aceleración vas a utilizar? ¿Por qué?
Voy a utilizar los tres algoritmos vistos en la actividad 7, todo esto para generar una orbita caotica que se genere más impacto visual.

### El contenido generado debe ser interactivo. Puedes utilizar mouse, teclado, cámara, micrófono, etc, para variar los parámetros del algoritmo en tiempo real.
Con la tecla "m" se podran generar más objetos y con la tecla "p" se para el traso generado con noise, Tambien al dar click se invertira la fuerza de atracción del mouse.

### El código de la aplicación.

``` js

```

### Un enlace al proyecto en el editor de p5.js.



### Una captura de pantalla representativa de tu pieza de arte generativo.
