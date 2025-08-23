# Unidad 3


## 🤔 Fase: Reflect

### Actividad 11

#### Parte 1: recuperación de conocimiento (Retrieval Practice)

##### Escribe la ecuación vectorial de la segunda ley de Newton y explica cada uno de sus componentes.
###### Primera respuesta: 
Creo conocer la ecución de siempre, pero la vectorial no la recuerdo.

###### Segunda respuesta (despues de repasar más): 
F = m(a)

Siendo:

F = Fuerza neta (vector que representa la suma de todas las fuerzas que esten afectando).
m = Masa del objeto (escalar que indica la resistencia al cambio de movimiento).
a = Aceleración (vector que indica el cambio de la velocidad en el tiempo).

##### ¿Por qué es necesario multiplicar la aceleración por cero en cada frame del método update()?
###### Primera respuesta: 
Esto se hace para que cuando se saque la velocidad en un frame nuevo, esta velocidad no tome un valor acumulado en el tiempo en la aceleración, osea en el caso de tener un aceleración de dos y una velocidad de 0 en el frame 0, en el frame 1 seria velocidad 2 y en el frame 3 en vez de ser la velocidad de 4 sera 6, debido a quese esta guardando en el tiempo los valores de aceleración y se van acumulando.

###### Segunda respuesta (despues de repasar más): 
La aceleración se reinicia cada frame porque esta depende únicamente de las fuerzas aplicadas en ese instante. Si no se reinicia, se acumularían fuerzas viejas que ya no están actuando, lo que distorsionaría la simulación.

##### Explica la diferencia entre paso por valor y paso por referencia cuando aplicamos fuerzas a un objeto.
###### Primera respuesta: 
El paso por valor es para variables primitivas y este paso por valor cambia la información guardada en dicha variable en este caso puede ser la velocidad, el valor de la fricción dependiente del suelo; por el otro lado el paso por referencia es para vectores, arrays, etc, en donde no se reemplaza el valor que se guarda sino que lo modifica en un lapzo de tiempo de ejecución lo cual da como resultado que a la hora de usar un objeto podamos darle a un vector de movimiento un cambio direccional o un desenzo en su velocidad o aceleración.

###### Segunda respuesta (despues de repasar más): 
Paso por valor: Se crea una copia de la variable. Si modificamos esa copia dentro de una función, el original no cambia. Ejemplo: pasar un número que representa la fricción como parámetro.

Paso por referencia: No se copia la variable, sino que se pasa la dirección de memoria. Así, cualquier modificación afecta directamente al objeto original. Ejemplo: al pasar un vector de velocidad por referencia, la función puede modificar su dirección o magnitud y el cambio se refleja en el objeto real.

##### ¿Cuál es la diferencia conceptual entre modelar fuerzas (como fricción, gravedad) y simplemente definir algoritmos de aceleración?
###### Primera respuesta: 
La verdad no estoy seguro de como responder a esta pregunta.

###### Segunda respuesta (despues de repasar más): 
Modelar fuerzas: Significa usar las leyes físicas (como la gravedad, fricción, empuje) para calcular aceleraciones y cambios de movimiento. Osea es tratar de recrear o basarse en la física real: se suman fuerzas, se aplica 𝐹=𝑚(𝑎) y de ahí sale la aceleración.

Algoritmos de aceleración: Son reglas artificiales que definen cómo cambia la velocidad sin necesidad de una fuerza. Por ejemplo: “cada frame aumenta la velocidad en 1” no depende de una fuerza física, sino de una instrucción programada.

#### Parte 2: reflexión sobre tu proceso (Metacognición)

##### ¿Qué fue lo más desafiante en la Actividad 10 (problema de los n-cuerpos)? ¿El concepto creativo, la implementación de las fuerzas o la integración de la interactividad?
Yo diria que en esta ocación fue el concepto inspirativo ya que no soy un hombre de arte o por lo menos no de este tiepo de arte, por lo que en realidad fue muy dificil definir que me transmitia el ver esas obras y con eso poder hacer la mia, por esta razón considero que lo que más se me dificulto fue hacer el concepto creativo.

##### ¿Las fuerzas que modelaste produjeron el comportamiento que esperabas? Describe un momento “sorpresa” (esperado o inesperado) durante el desarrollo.
Cuando estaba experimentando con la atracción en los n-cuerpos estaba probando con masas no se querian atraer entre ellas, lo cual me llevo a pensar que hice mal todo el proceso y eso me dejo preocupado y despues de muschos cambios nada funcionaba, hasta que por un capricho le puse una fuerza gravitacional más grande a uno de los obejtos y en ese momento comenzo a funcionar la atracción sin embargo los cambios que efectue dañaron tanto el codigo que hizo que cuando se atrageran se lanzaron disparadas en direcciones opuestas.

##### ¿Cómo ha cambiado tu forma de pensar sobre la “física” en el arte generativo después de esta unidad?
La verdad ya de por si me gustaban las obras con sistemas fisicos realistas, pero ahora puedo apresiar mucho más el como se logra llegar a diseñar un sistema que imite al mundo real y que pueda generar mostrar un sentimiento o idea de alguien.

##### Si tuvieras una semana más, ¿Qué otras fuerzas te gustaría modelar o cómo mejorarías tu simulación del problema de los n-cuerpos?
Me gustaria modelar sistemas de coliciones con rebotes y elasticidad, ya que aunque mi obra este inspirada en el sistema solar, no significa que quiero que sea un sistema estable o realista, me gustaria que hubira cierto sentido de caos que de sorpresas al usuario.

### Actividad 12

#### Intercambia la URL de tu bitácora con un compañero.

[Bitácora](https://github.com/jfUPB/simulacion-2025-20-catflyx/blob/unidad3/apply/unidad-3/apply.md)

#### Analiza su Actividad 10 (problema de los n-cuerpos). Ejecuta su simulación, lee su concepto y revisa su código.

[Link de la actividad 10 de mi compañero](https://editor.p5js.org/catflyx/sketches/-dtaUlNS4)

#### En tu propia bitácora, escribe una retroalimentación constructiva para tu compañero, evaluando:
##### Claridad del Concepto: ¿La obra visual refleja la inspiración en las esculturas cinéticas de Calder y el problema de los n-cuerpos?
Si, los representa, segun mi apreciación su uso del color, y su forma abstracta le favorece de gran manera en la parte artistica y la parte de los n-cuerpos no vi ninguna novedad en su codigo que genere el pensar que esta mal implementado, todo funciona de buena manera y sin fallos.

##### Implementación de Fuerzas: ¿Se aplican correctamente las leyes de Newton? ¿Las fuerzas se acumulan apropiadamente?
Si, luego de ver el codigo considero que estaba bien conectado y no vi alguna reareza que me haga decir que no se aplico de manera fiel la fuerzas o la ley de Newton.

##### Creatividad en el Modelado: ¿El modelado de fuerzas es interesante y genera comportamientos únicos?
Completamente, me parece una obra visual muy llamativa y ademas me gusto como fue el desarrollo de su trabajo hasta terminar en lo que se muestra en el link que puse en la sección anterior.

##### Calidad de la Interactividad: ¿La interacción permite explorar diferentes aspectos del sistema de fuerzas?
Por lo que persibi, el sistema de seguimiento del objeto al mouse cuando se da click en la pantalla muestra un buen sistema de cambio de dirección con vectores.

### Actividad 13

#### Continuar: ¿Qué actividad o concepto de esta unidad te resultó más “revelador” para entender las fuerzas en el arte generativo?


#### Dejar de hacer: ¿Hubo alguna actividad que te pareció redundante o menos efectiva para comprender el modelado de fuerzas?
Progresión conceptual: ¿El paso de manipular aceleración directamente (unidad 2) a modelar fuerzas (unidad 3) te pareció una progresión natural y efectiva? ¿Por qué?


#### Conexión arte-física: ¿Cómo te ha ayudado esta unidad a ver la conexión entre conceptos físicos y expresión artística? ¿Te sientes más cómodo “jugando” con las leyes de la física en tus creaciones?


#### Comentario adicional: ¿Algo más que quieras compartir sobre tu experiencia explorando fuerzas en el arte generativo?
