# Unidad 1

## 🤔 Fase: Reflect

### Actividad 9
#### Parte 1: recuperación de conocimiento (Retrieval Practice)
##### Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?
La diferencia fundamental entre estas dos funciones es que la random() genera datos con probabilidades teoricamente iguales, mientras que el noise() genera datos semi aleatorios osea que aunque parescan aleatorios los datos generados en realidad estan realacionados con los datos antes generados lo cual nos da una sensación de un camino o secuencia casi predecible o incluso organica, yo usaria el random() para generar números definir un número ganador de una loteria, mientras que el nois() lo usaria para generar algoritmos de movimiento imitando un poco la realidad.

##### Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?
La distribución de probabilidad es el chance de que salga un valor en especifico teniendo muchos valores posibles por salir osea esta define que es lo más probable que ocurra luego de ejecutar una acción, la diferencia visual entre ambas es que un distribución uniforme al generar datos con una misma probabilidad teorica generara un movimiento parecido a una espiral que no sabe como salir de un mismo punto, osea tenderia a quedarse enserrado cerca del mismo punto de origen pues como todos los datos pueden salir con la misma probabilidad eso genera que se quede atrapado en tender a dar vueltas en si mismo, por otro la do con una distribución normal al ser una probabilidad que favorece un rango de datos en especifico lo que veriamos es tender los resultados como una linea que se curva de vez en cuando pero que no genere giros inesperados casi nunca, es como ver un camino, puede tener curvas, pero no siempre segira hacia adelante.

##### ¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple
Las funciones de la aleatoriedad en el arte generativo según mi comprensión es, primero crear algo cambiante en el tiempo que se mantenga interesante a la vista del observador y que pueda llegar a generar diferentes sensaciones a me dida que va cambiando, lo segundo es poder darle vida al arte pues este al no ser igual a medida que pasa el tiempo permite hacer que dichos cambios puedan ser más realistas o más artificiales según la intención del artista, y a ese es el punto que quiero llegar la aleatoridad puede ser usada para enfatizar intenciones he ideas que el artista quiere transmitir al observador.

##### Piensa en tu obra final (Actividad 08). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.
Yo use el nois() el caul me genera números semialeatorios debido a que los números generados por esta función siguen una secuencia que busca que los valores sigan cierto patron para suavizar su movimiento, osea se puede decir que los números generados con nois tratan de estar relacionados para mantener un camino y cambio más suave. Yo elegi utilizar nois() para imitar el trazo de un lapíz, dedido a que como genera numeros relacionados, este genera acciones suavez y movimientos continuos lo cual se asemeja justamente al trazo de una persona con un lapiz, por esta misma razón es que era la mejor opción usar el nois() pues los demás metodos de randomización general movimientos erraticos, o monodireccionales (direcciones muy estaticas) y lo que necesitava era una imitación de un suave trazo.

##### ¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?

### Actividad 10

### Actividad 11
