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



