# Unidad 2


## 🤔 Fase: Reflect

### Actividad 09

#### Parte 1: recuperación de conocimiento (Retrieval Practice)

##### Escribe la “receta” del marco MOTION 101.
1) Se declara un objeto.
   ``` js
       let objmove;
   ```
2) Se crea el objeto en setup.
   ``` js
       
      function setup() {
         createCanvas(640, 240);
          objmove = new Objmove();          
      }   
   ```
3) Se llama a los metodos que necesita el objeto.
   ``` js
      function draw() {
          background(255);
         mover.update();
         mover.checkEdges();
         mover.show();
      }
   ```
4) El objeto tiene dos o tres vectores: posición, velocidad y aceleración.
   position: dónde está el objeto.
   velocity: hacia dónde y qué tan rápido se mueve.
   acceleration: cómo cambia la velocidad.
   ``` js
      class Objmove {
        constructor() {
          this.position = createVector(width / 2, height / 2);
          this.velocity = createVector(0, 0);
          this.acceleration = createVector(0, 0);
        }
        ...
      }
   ```
5) Se generan los cambios de posició y velocidad
   ``` js
      class Objmove {
        constructor() {
          ...
        }

        update() {
          this.velocity.add(this.acceleration);
          this.position.add(this.velocity);
        }
        show() {
          ...
        }
        checkEdges() {
          ...
        }
      }
   ```
##### ¿Cómo se relaciona el marco MOTION 101 con los conceptos de position, velocidad y aceleración?
El marco MOTION 101 se basa en representar posición, velocidad y aceleración como vectores, lo que permite modificar de forma dinámica el comportamiento de un objeto. Si estos conceptos no se aplican, el movimiento del objeto dependerá únicamente de valores predefinidos, sin responder a variaciones de fuerzas externas, resultando en desplazamientos repetitivos y aburridos.

##### Si tuvieras que explicar el concepto de motion 101 de manera geométrica, ¿Cómo lo harías?
Si tuviera que explicarlo de alguna manera, diria que la interpretación geometrica de motion 101 seria como un triangulo, en el cual cada uno de sus lados representa alguano de los vectores de velocidad, aceleración y posición los cuales por si mismos se pueden describir como el lugar en el que esta el objeto, su cambio de posición y el cambio de velocidad, los cuales nos darian como resultado el desplazamiento dinamico de algún objeto como explique en la pregunta anterior.

#### Parte 2: reflexión sobre tu proceso (Metacognición)

##### ¿Qué fue lo más desafiante en la Actividad 08? ¿El concepto creativo, la implementación del algoritmo de aceleración o la integración de la interactividad?
Diria que lo más complicado fue la implementación de la aceleración debido a querer generar una orbita en la cual los objetos chocacen, tenia que encontrar un valor maximo de la velocidad en el cual no se viera afectado el rendimiento ni la parte visual del trabajo.

##### ¿Tu algoritmo de aceleración produjo el efecto que esperabas? Describe un momento “sorpresa” (esperado o inesperado) durante su desarrollo.
Lo más inespera que me pudo pasar fue que algunos objetos se movian a velocidades estrepitosas generando que colicionaran inmediatamente entre ellas, lo cual a su vez generaba un cambio de color demaciado abrupto en el fondo llegandome a marear.

##### ¿Cómo ha cambiado tu forma de pensar sobre el “movimiento” en una pantalla después de esta unidad?
He descubierto un sin fin de posibilidades que puedo utilizar para generar movimientos más dinamicos los cuales le puedan dar más vida a mis obras.

##### Si tuvieras una semana más, ¿qué mejorarías o qué otro algoritmo de aceleración te gustaría experimentar?
Lo que yo le agregaria seria seguramente más interacciones, como otros objetos que se generen en la pantalla además de los triangulos que caen, talvez dar algún boton que cambie el color de los circulos que orbitan para que no se tenga que esperar a que estas colicionen para que cambien de color y por ultimo dejar que el usuario escoja si quiere que los circulos colisionen o si mejor simplemente dejar que estos dibujen sin interrupción.

### Actividad 10
Compañero:
Simara Paola Villasmil Jiménez

#### URL:
https://github.com/jfUPB/simulacion-2025-20-catflyx/blob/unidad1/reflect/unidad-1/reflect.md

#### Comentario:
##### Claridad del Concepto: La descripción en su mayoria ayuda a visualizar lo que se quiere lograr, sin embargo igual queda muy ambiguo debido a que no se especifican formas, objetos o colores; sin embargo esto se debe a que estas descripciones no fueron colocadas en el concepto sino despues, en la parte del codigo, ya con esa parte leida el concepto queda completamente entendida y representa fielmente el resultado.

##### Creatividad del Algoritmo: El resultado me parecio muy vacano debido a las interacciones de movimiento en la orbita y a los objetos que chocan por la pantalla genera un efecto visual unico y llamativo que siempre cambia.

##### Calidad de la Interactividad: El impacto que genera la interactividad es puramente en la parte visual osea color y forma lo cual le favorece al diseño, ya en la parte de intuitividad, no puedo decir que algo fuera intuitivo ya que las teclas no parecen la inicial de la acción que se hace, tipo z y x cambian de color los objetos que orbitan y r y t los objetos que chocan con el borde de la pantalla y eso no me dice nada.
#### Conversación:
Lo estuvimos conversando durante la clase.

### Actividad 11
#### Continuar: ¿Qué actividad o concepto de esta unidad te resultó más “iluminador” o útil?
El concepto más util fue la aceleración en el motion 101 debido a que con esta puedo tratar de integrar sistemás fisicos semirealistas o inventarme los mios para hacer proyectos más llamativos.

#### Dejar de hacer: ¿Hubo alguna actividad que te pareció redundante o menos efectiva?
Por lo que experimente no creo que en este caso hubiera una actividad que fuera util.

#### Empezar a hacer: ¿Qué te gustaría explorar a continuación? ¿Más fuerzas físicas (fricción, resortes), sistemas de partículas, o algo más?
Justamente me gustaria ver como implementar sistemas fiscos semirealistas para ver que nuevos resultados obtendria.

#### Método de aprendizaje: ¿El paso de los experimentos guiados (Seek) a la aplicación libre (Apply) te pareció una transición natural y efectiva? ¿Por qué?
Considero que si y no al mismo tiempo, debido a que considero que debimos tener por lo menos otra guia del Seek desbelando utilidades del motion 101, ya que nuestra unica ilustración fue "trate de hacer tres tipos de movimientos" en ves de darnos un repertorio más grande, ya que lo más efectivo a mi gusto es mostrar ejemplos y luego pedir que se haga algo.

#### Comentario adicional: ¿Algo más que quieras compartir sobre tu experiencia en esta unidad?
Nada en particular, simplemente que me gusto este nuevo tema y voy a probar a hacer algunas cosas nuevas con elasticidad o fricción a ver como interactuan con un sistema como js.
