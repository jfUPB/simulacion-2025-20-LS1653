# Unidad 4

## Actividad 1

### Artista y videos

[Memo Akten](https://www.memo.tv/)

[Simple Harmonic Motion](https://www.memo.tv/works/simple-harmonic-motion/)

[Superradiance](https://superradiance.net/)
## Actividad 2
[Angulos ejemplo](https://editor.p5js.org/juanferfranco/sketches/R1iTVQjzm)
### ¿Qué está pasando en esta simulación? ¿Cuál es la interacción?
Lo que ocurre en esta simulación es que se esta dibujando una linea que conecta dos puntos y al oprimir space esta linea junto con los dos puntos comiensan a girar en un angulo especifico sin separarce de dicha conección. 

### Nota que en cada frame se está trasladando el origen del sistema de coordenadas al centro de la pantalla. ¿Por qué crees que se hace esto?
Se traslada el origen al centro para simplificar la rotación de la figura alrededor de su propio eje central.

### Cuál es la relación entre el sistema de coordenadas y la función rotate().
rotate() siempre gira respecto al origen del sistema de coordenadas actual, y por eso casi siempre se combina con translate() para reposicionar ese origen donde queremos que ocurra la rotación.

[MOvimiento con angulos](https://editor.p5js.org/natureofcode/sketches/bZqHGYbRQ)

### ¿Qué hace la función heading()?
heading() devuelve el ángulo de un vector en radianes respecto al eje positivo X (horizontal hacia la derecha).

### ¿Qué hace la función push() y pop()? Realiza algunos experimentos para entender su funcionamiento.
push() guarda el estado actual de la transformación (traslación, rotación, escala, estilos gráficos).
pop() restaura el estado guardado.

Esto sirve para que transformaciones como translate() o rotate() no afecten a todo lo que se dibujes después.

### ¿Qué hace rectMode(CENTER)? Realiza algunos experimentos para entender su funcionamiento.
Se usa para que a la hora de girar se haga de manera natural desde el centro del objeto si se le quita el "CENTER" comienza a girar desde una esquina lo cual hace menos inmersivo el movimiento.

### ¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad? Trata de dibujar en un papel el vector de velocidad y cómo se relaciona con el ángulo de rotación y la operación de traslación y rotación.
El ángulo de rotación (angle) proviene de this.velocity.heading().
Eso significa que el rectángulo rota para “apuntar” en la dirección de su velocidad.
Matemáticamente, es el mismo ángulo que forma el vector de velocidad con el eje X.

## Actividad 3
