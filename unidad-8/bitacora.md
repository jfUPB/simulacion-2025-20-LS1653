# Evidencias de la unidad 8
## Actividad 01
### a) conecxión imagen-sonido
En Dimension N, la relación entre el sonido y la imagen se siente profundamente integrada. Los visuales parecen reaccionar a las frecuencias más graves mediante pulsaciones lentas y expansiones de color, mientras que los sonidos agudos producen líneas finas, fractales o destellos de luz que vibran en la pantalla. No se trata solo de la sincronía rítmica, sino de una conexión con el sonido: cuando la música se vuelve más densa o caótica, los visuales se saturan, se fragmentan y se expanden como si el sonido los estuviera impulsando desde dentro.


En Sónar+D CCCB 2020, la conexión es más atmosférica. Aquí la música de Carles Viarnès, más pianística y etérea, se traduce en paisajes digitales que fluyen suavemente. Los colores cambian con la armonía, las transiciones visuales responden a la intensidad del sonido, y se perciben movimientos ondulantes que siguen los crescendos y los silencios. En lugar de reaccionar al ritmo, los visuales acompañan la estructura emocional de la música.

### b) Explica qué elementos te parecieron generativos y por qué crees que cada visualización sería única.
En ambos casos, los visuales de Alba G. Corral presentan características claramente generativas:

Uso de formas orgánicas que evolucionan de manera continua y no repetitiva.

Patrones que se deforman y transforman con el tiempo, probablemente guiados por algoritmos que responden a la amplitud o las frecuencias del sonido.

Texturas vivas, que emergen, desaparecen y mutan, creando la sensación de que el sistema tiene cierta autonomía.

En Dimension N, las figuras abstractas parecen tener comportamiento propio: crecen, colisionan, se disuelven, como si cada ejecución fuera irrepetible.

En Sónar+D, el flujo visual recuerda a un “pintar con código”, donde el azar y el cálculo coexisten: las variaciones no son totalmente predecibles, lo que sugiere un sistema sensible y adaptativo.

Por estas razones, es evidente que cada performance sería única, incluso si la música fuera la misma. Las visuales generativas dependen de valores aleatorios, del entorno sonoro en vivo, y de la interpretación manual de la artista en tiempo real.


### c)Reflexión sobre la sensación de “liveness”.
La sensación de liveness en los trabajos de Alba G. Corral es muy fuerte. Los visuales están siendo generados en tiempo real provoca una conexión directa entre el público, la música y la imagen.
No se siente como un video pregrabado, sino como una improvisación audiovisual, donde el sonido guía a la imagen y la imagen reinterpreta al sonido. Esta interacción crea un diálogo vivo entre disciplinas, en el que el código se convierte en un instrumento expresivo más.

En ambos casos, la experiencia transmite presencia y reacción inmediata: los visuales respiran con la música, se emocionan con ella y se transforman en sincronía. Esa cualidad viva y efímera es lo que convierte a las obras generativas de Alba G. Corral en performances irrepetibles.


## Actividad 02
### Pieza musical elegida

Título: La Hija de las Estrellas
Artista: SAUROM
Enlace: https://youtu.be/tuArrB6YfGE?si=Gk_SPp8rmr40a1te

Elegí esta canción debido a su dinámica narrativa y estructura cambiante, que combina momentos suaves y melódicos con secciones intensas llenas de energía. Esto permite traducir visualmente las transiciones musicales a través de diferentes comportamientos de las formas, colores y partículas en pantalla.
Su naturaleza épica y fantástica también inspira un mundo visual místico, donde la música guía el movimiento del color y la forma.

### Concepto visual
El concepto sera en base en el viaje de una estrella que nace, brilla, explota y renace.
A través de la visualización, busco representar la energía y emociones contenidas en la canción:

Momentos suaves: La cámara recorre un espacio lleno de luz tenue y ondas que fluyen lentamente, como un cosmos en calma.

Momentos intensos: Explosiones de color, formaciones que se expanden como supernovas, y figuras que se transforman según el ritmo.

Transiciones: Los cambios de frecuencia harán que el entorno se mueva y deforme, como si el espacio mismo respirara con la música.

Visualmente será tratara de hacer una mezcla de ondas, partículas y campos de flujo (flow fields), combinados para generar movimientos orgánicos y sincronizado con la música.

### Inputs
Los inputs que se usare para interpretar la música en tiempo real serán:

``` markdown
| **Input**                              | **Descripción**                                    | **Efecto visual asociado**                                         |
|----------------------------------------|----------------------------------------------------|--------------------------------------------------------------------|
| Amplitud general (nivel de volumen)    | Captura la energía global de la canción.           | Cambia el brillo y saturación del fondo, genera pulsaciones de luz.|
| Frecuencias graves (bajos)             | Detectadas con FFT.                                | Aumentan el tamaño o explosividad de las partículas; simulan las ondas de impacto.|
| Frecuencias medias-altas (instrumentos y voz) | Responden a los detalles melódicos.         | Activan deformaciones de malla, colores cambiantes y movimientos de los “rayos” visuales.|
| Intensidad rítmica (beat o picos)      | Picos detectados por variaciones rápidas de energía.| Cambia la imagen o tono de fondo automáticamente, simulando cambios de atmósfera.|
```

### Algoritmos y técnicas 
Se utilizara una combinación de técnicas generativas vistas durante el curso:

Flow Fields:
Para mover los objetos (buques, partículas, ondas) con trayectorias fluidas que se deforman según la música.
Cada frecuencia influirá en la dirección y fuerza de los vectores del campo.

Flocking Behavior (comportamiento de enjambre):
Para simular cómo las partículas o elementos luminosos se agrupan y separan con el ritmo.

Partículas con física simple:
Usadas para representar explosiones estelares y expansión energética.

Interacción con FFT (Fast Fourier Transform):
Para vincular frecuencias específicas con transformaciones visuales (color, tamaño, posición, rotación, etc.).

Transición dinámica de fondos:
Cuando la intensidad de la música aumenta, cambia el fondo de forma automática, representando un cambio de “atmósfera” o capítulo visual.

### Boceto conceptual

Imagino la escena como un universo vivo:

En el fondo, una malla ondulante que se distorsiona con la música, como si el espacio vibrara.
En primer plano, formas y partículas que representan energía estelar, flotando y girando con el ritmo.
En momentos de calma, el color se enfría (azules, violetas, blancos suaves).
En los clímax, el color se calienta (rojos, dorados, naranjas brillantes) y todo se acelera.
Cada vez que la música alcanza un punto máximo, una supernova visual inunda la pantalla, marcando el impacto sonoro.

### Boceto

<img width="550" height="375" alt="image" src="https://github.com/user-attachments/assets/e01d73d3-c8f2-4495-8dc9-cd65c78a1618" />

### Boceto inspiracional generado a mi petición por chatgpt

<img width="246" height="207" alt="image" src="https://github.com/user-attachments/assets/a7c02eec-0ef4-421d-a226-4ac1553dc357" />


## Actividad 03
``` js

```

[Mi obra](https://editor.p5js.org/estebanpuerta2006/sketches/rpFwA0Byp)

## Auto evaluación
### Mi nota:

### Mi defensa:

