# Unidad 1

## 🤔 Fase: Reflect

### Actividad 9
#### Autoevaluación
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
Es el plasmar con una linea, puntos o figuras los datos generados por una función de aleatoriedad, osea estamos dando seguimiento de manera visual a los datos que nos esta regresando la función que hayamos utilizado, dependiendo de la funación que se utilice dicha caminata puede variar en estilo, rigides y dirección, en el caso de una caminato con “Lévy flight” se puede notar que los pasos plasmados obtienen un distancia más grande entre ellos pero mantiene un movimiento muy similar al que se obtendri al usar la función random() solo que con datos más separados entre si.

####Parte 2: reflexión sobre tu proceso (Metacognición)
##### ¿Cuál fue el concepto más abstracto o difícil de “visualizar” para ti en esta unidad? ¿Qué hiciste para finalmente comprenderlo?
El concepto más abstracto para mi fue el del nois() debido a que es raro decir que un valor que es aleatorio en realidad no es tan aleatorio pues este valor sera definido por los valores anteriores a el y a su vez es uun poco más dificil de programar, sin embargo al realizar varios experimentos con los ejemplos del libor virtual puede comprender su mecanica y fue facíl definirle una utilidad a futuro.

##### Describe un momento durante el desarrollo de tu obra final (Actividad 08) en el que un “error” o un resultado inesperado te llevó a una idea creativa interesante.
Estava tratando de modificar el fondo en tiempo real, pero lo que ocasionaba es que se elimina el traso que generava con nois(), esto me llevo a pensar en utilizar esta forma de eliminar el trazo como una forma de reiniciar el lienzo con un fondo nuevo para aumentar el interes del observador.

##### Al combinar diferentes técnicas de aleatoriedad, ¿Cuál fue el mayor desafío? ¿La interacción entre los sistemas, el control de los parámetros, el rendimiento?
Mis dos mayores problemas fue el rendimiento, pues yo queria agregar más trazos a la vez sin embargo esto congelava de vez en cuando la pagina y paraba la simulación y el otro problema fue comprender como integrar varios sistemas sin afectarse entre si como paso con la generación del fondo de forma aleatorea que eliminaba de forma no planeada (al inicio de mi trabajo) el trazo que generaba con nois().

##### Si tuvieras que empezar la Actividad 08 de nuevo, ¿Qué harías de manera diferente basándote en lo que sabes ahora?
Lo que yo haria es primero, configurar el cambio aleatorio del fondo y luego pintar por ensima el trazo, para que esta vez sin se puedan convinar estas dos acciones, de resto el proceso lo dejaria igual.
### Actividad 10
#### Coevaluación

### Actividad 11
#### Feedback
##### Continuar: ¿Qué actividad, ejemplo o explicación de esta unidad te resultó más reveladora o útil para tu aprendizaje? ¿Qué deberíamos mantener sí o sí?
El mejor ejemplo para mi es el de la caminata, en todas sus versiones, esto debido a que se pueda explicar la diferencia de manera visual y en codigo el como cambia la aleatoridad al usar diferentes funciones de probabilidad.

##### Dejar de hacer: ¿Hubo alguna actividad o concepto que te pareció redundante, confuso o menos útil? ¿Hay algo que eliminarías o cambiarías por completo?
Yo pensaria que el más confuso fue el como programar el nois(), sin embargo luego de repetir varias veces el intento se puede llegar a entender, lo unico que se podria mirar es ver si hacer un ejemplo con el con ayuda del profesor para que sea hagan las preguntas necesarias para evitar errores que se mantienen mucho al practicar con la prueba y error.

##### Empezar a hacer: ¿Qué te faltó en esta unidad? ¿Quizás más ejemplos de artistas, más desafíos técnicos, más teoría? ¿Qué idea tienes para hacerla mejor?
reo que la unidad esta bien como esta, lo que faltaria es como agregar documenta del tipo de programación que vemos en este caso js, pero de resto todo me parecio bien.

##### Balance Teoría-Práctica: ¿Cómo sentiste el equilibrio entre analizar los ejemplos del texto guía y ponerte a programar tus propios sketches? Explica tu respuesta.
Es obvio que es más dificil salir a programar tu cuenta algo que comienzas a ver, sin embargo los ejemplos del libro son una gran base de apoyo, yo considero que como esta palnteado la mecanica de leer y entender y luego hacer esta bien diceñada, solo hay que indagar en la documentación de js para aumentar la calidad de la actividad que programamos nosotros mismos.

##### Comentario Adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad?
En general, me gusto el tema y quisiera ver como puedo seguir mejorando en esta generación de arte y me toca volver a recordar a programar en js.
