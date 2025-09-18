# Evidencias de la unidad 5

## Seek:

### Actividad 2

### Revisa detalladamente el ejemplo 4.2:
[Ejemplo 4.2](https://natureofcode.com/particles/#example-42-an-array-of-particles)

#### Analisis 
1. Declaración global

   ``` js
     let particles = [];
   ```
   Arreglo vacío que guardará todas las partículas activas.

2. draw()

   ``` js
     function draw() {
        background(255);
        particles.push(new Particle(width / 2, 20));
   ```
   Se limpia el fondo en cada frame.
   Cada vez que se ejecuta draw(), se genera una nueva partícula en la posición (width/2, 20), es decir, en el centro superior de la pantalla.
   Esto quiere decir que constantemente nacen partículas.

3. Bucle invertido

   ``` js
     for (let i = particles.length - 1; i >= 0; i--) {
          let particle = particles[i];
          particle.run();
          if (particle.isDead()) {
              particles.splice(i, 1);
          }
     }
   ```
   Se recorre el array de atrás hacia adelante.
   Esto se hace porque se eliminaran elementos (splice) y no queriere que se desajusten los índices al recorrerlos.
   particle.run() -> Ejecuta:
        update() -> Cambia la posición, velocidad, vida, etc.
        display() -> Dibuja la partícula en pantalla.
   particle.isDead() -> Devuelve true cuando la partícula ha "muerto". -> Si muere, se elimina del arreglo.

4. Clase Particle

#### Constructor

    ``` js
     constructor(x, y) {
       this.position = createVector(x, y);
       this.acceleration = createVector(0, 0);
       this.velocity = createVector(random(-1, 1), random(-1, 0));
       this.lifespan = 255.0;
     }
    ```
   Cada partícula tiene:
       position: dónde está.
       velocity: movimiento inicial, aleatorio en X y negativo en Y → tienden a moverse hacia arriba.
       acceleration: empieza en 0, se usa para acumular fuerzas.
       lifespan: vida útil (255 -> máximo, como alfa en colores).

#### run()
   ``` js
     let gravity = createVector(0, 0.05);
     this.applyForce(gravity);
     this.update();
     this.show();
   ```
   Define una fuerza constante de gravedad hacia abajo.
   Aplica esa fuerza, actualiza movimiento, y dibuja.

#### applyForce(force)
   ``` js
     this.acceleration.add(force);
   ```
   Cualquier fuerza (gravedad, viento, etc.) se suma a la aceleración.

#### update()
   ``` js
      this.velocity.add(this.acceleration);
      this.position.add(this.velocity);
      this.lifespan -= 2;
      this.acceleration.mult(0);
   ```
   Se actualiza el movimiento según física:
         vel = vel + acc
         pos = pos + vel
  La vida útil baja en 2 cada frame.
  La aceleración se resetea → para que solo afecte en el frame donde se aplica.

#### show()
   ``` js
     stroke(0, this.lifespan);
     fill(127, this.lifespan);
     circle(this.position.x, this.position.y, 8);
   ```
   Se dibuja la partícula como un círculo de radio 8.
   Usa lifespan como transparencia (alpha). -> Cuanto más cerca de morir, más transparente se vuelve.

#### isDead()
   ``` js
     return (this.lifespan < 0.0);
   ```
   Cuando la vida llega a 0, se elimina.

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas
Con: 
``` js 
particles.push(new Particle(width / 2, 20));
```
Cada frame (draw()) se crea una nueva partícula.
Esto significa que el sistema va generandocontinuamente.
El número de partículas no es fijo, sino que depende de cuántas mueren en comparación de cuántas se crean.

#### Desaparición de partículas
con:
``` js
for (let i = particles.length - 1; i >= 0; i--) {
  let particle = particles[i];
  particle.run();
  if (particle.isDead()) {
    particles.splice(i, 1);
  }
}
```
Se recorre el arreglo de atrás hacia adelante (para no desordenar índices al borrar).
Cada partícula revisa si su lifespan es menor a 0 (isDead()).
Si está muerta -> se elimina con splice(i, 1).
Así, no se acumulan partículas en la memoria.

#### Gestión de memoria en esta simulación
Creación: Las partículas se van agregando con push().
Eliminación: Se van borrando del arreglo con splice().
Con esto, el sistema mantiene solo partículas activas -> optimiza uso de RAM.

#### Experimento

### Analiza el ejemplo 4.4:
[Ejemplo 4.4](https://natureofcode.com/particles/#example-44-a-system-of-systems)

#### Analisis 

1)Estructura General:
Se usa un arreglo particles[] para almacenar todas las partículas activas, en donde cada frame (draw()), se añade una nueva partícula y se actualizan las existentes. Las partículas tienen un ciclo de vida definido por su atributo lifespan y cuando una partícula “muere” (lifespan ≤ 0), se elimina del arreglo.

2)Creación y control de emisores:

En mousePressed():

``` js
  emitters.push(new Emitter(mouseX, mouseY));
```
Cada vez que se hace clic, se crea un nuevo emisor en la posición del mouse.
Esto permite tener múltiples sistemas de partículas activos simultáneamente.
Todos los emisores se almacenan en el arreglo global emitters[].

3)Clase Particle

La partícula conserva la misma lógica básica:
Atributos:
 *position: posición en el espacio.
 *velocity: velocidad inicial aleatoria, le da un movimiento natural y diverso.
 *acceleration: se acumulan fuerzas externas como la gravedad.
 *lifespan: controla el tiempo de vida de la partícula.

Métodos:
 *applyForce(force): suma la fuerza a la aceleración.
 *update(): aplica física newtoniana → velocidad y posición cambian.
 *show(): la dibuja como un círculo que se desvanece al envejecer.
 *isDead(): determina si debe eliminarse. 

 4)Clase Emitter
El emisor administra un conjunto de partículas:
a)Atributo principal:
``` js
this.origin = createVector(x, y);
this.particles = [];
```
Guarda la posición de origen y un arreglo dinámico de partículas.

b)Creación de partículas:
``` js
addParticle() {
  this.particles.push(new Particle(this.origin.x, this.origin.y));
}
```
Cada ciclo, se agrega una nueva partícula en el origen del emisor.

c)Gestión de partículas:
``` js
run() {
  for (let i = this.particles.length - 1; i >= 0; i--) {
    this.particles[i].run();
    if (this.particles[i].isDead()) {
      this.particles.splice(i, 1);
    }
  }
}
```
Se recorren las partículas de atrás hacia adelante.
Se ejecuta su lógica (run()).
Si están muertas, se eliminan del arreglo -> memoria liberada por el garbage collector.

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas

En cada ciclo (draw()):

   ``` js

    for (let emitter of emitters) {
     emitter.run();
     emitter.addParticle();
     }
   ```
   Cada emisor (Emitter) genera una nueva partícula en su origen con addParticle().
   Esto ocurre continuamente mientras la simulación este activa -> hay un flujo constante de partículas.

Cuando haces click (mousePressed()):

   ``` js
     emitters.push(new Emitter(mouseX, mouseY));
   ```
   Se crea un nuevo sistema de partículas independiente en la posición del mouse. 
   Cada emisor administra sus propias partículas, así se puede tener múltiples “fuegos artificiales” simultaneamente.

#### Desaparición de partículas

En el método run() de Emitter:

   ``` js
     for (let i = this.particles.length - 1; i >= 0; i--) {
      this.particles[i].run();
      if (this.particles[i].isDead()) {
         this.particles.splice(i, 1);
      }
     }
   ```
   Cada partícula se actualiza (update()), dibuja (show()) y reduce su lifespan.
   Cuando lifespan < 0, isDead() devuelve true.
   En ese momento se elimina con splice(i, 1).
   Al recorrer el arreglo de atrás hacia adelante, no se rompen los índices al eliminar.

#### Gestión de memoria en esta simulación

*Arreglos dinámicos (this.particles):
Cada emisor mantiene un arreglo propio con solo las partículas activas.

*Liberación de objetos muertos:
Al usar splice, los objetos Particle salen del arreglo y quedan sin referencias.

*Luego, el garbage collector de JavaScript libera la memoria automáticamente.
Escalabilidad:
Como se eliminan las partículas muertas en cada frame, el sistema evita fugas de memoria y mantiene un número controlado de objetos.

#### Experimento

### Analiza el ejemplo 4.5:
[Ejemplo 4.5](https://natureofcode.com/particles/#example-45-a-particle-system-with-inheritance-and-polymorphism)

#### Analisis 

1. Estructura General:
   a)Sketch principal (setup(), draw()):
        Configura el entorno.
        Maneja un único emisor de partículas.
   
    b)Clase Particle:
        Modelo base de partícula.
        Incluye física, dibujo y ciclo de vida.

    c)Clase Emitter:  
        Contenedor que administra todas las partículas generadas.
        Cada frame crea nuevas partículas y elimina las muertas.

     d)Clase Confetti (subclase de Particle):
        Redefine la visualización de la partícula.

2. Sketch Principal:
     ``` js
        function setup() {
           createCanvas(640, 240);
           emitter = new Emitter(width / 2, 20);
        }

        function draw() {
           background(255);
           emitter.addParticle();
           emitter.run();
         }
     ```
     a)Crea un solo emisor en el centro superior del canvas.

     b)Cada frame:
         Genera una nueva partícula (addParticle).
         Actualiza y dibuja todas las partículas (run).

3. Clase Particle:
     a)Atributos:
         position: vector posición.
         velocity: velocidad aleatoria inicial (dando variación).
         acceleration: acumulación de fuerzas.
         lifespan: control de ciclo de vida.

     b)Métodos:
         applyForce(): acumula fuerzas (ej. gravedad).
         update(): actualiza velocidad y posición, reduce vida.
         show(): dibuja un círculo translúcido que se desvanece.
         isDead(): indica cuándo debe eliminarse.
         run(): aplica gravedad, actualiza y dibuja (ciclo de vida).

4. Clase Emitter:
     ``` js
        addParticle() {
           let r = random(1);
           if (r < 0.5) {
              this.particles.push(new Particle(this.origin.x, this.origin.y));
           } else {
               this.particles.push(new Confetti(this.origin.x, this.origin.y));
           }
        }
     ```
     Cada frame, el emisor genera una nueva partícula.
     Aleatoriamente crea un Particle o un Confetti.
     Esto introduce variación visual automática.

   ``` js
        run() {
           for (let i = this.particles.length - 1; i >= 0; i--) {
               let p = this.particles[i];
               p.run();
               if (p.isDead()) {
                  this.particles.splice(i, 1);
               }
           }
        }
     ```
     Recorre las partículas de atrás hacia adelante para poder borrarlas sin errores de índice.
     Llama a run() (polimórfico, puede ser Particle.run() o Confetti.run()).
     Elimina partículas muertas.

5. Clase Confetti:
     ``` js
        class Confetti extends Particle {
           show() {
               let angle = map(this.position.x, 0, width, 0, TWO_PI * 2);
               rectMode(CENTER);
               fill(127, this.lifespan);
               stroke(0, this.lifespan);
               strokeWeight(2);
               push();
               translate(this.position.x, this.position.y);
               rotate(angle);
               square(0, 0, 12);
               pop();
           }
        }
     ```
     Hereda de Particle: conserva posición, velocidad, gravedad y ciclo de vida. 
     Sobreescribe (override) el método show():
     En vez de un círculo, dibuja un cuadrado girado.
     La rotación depende de la posición en el eje X (map() -> da dinamismo).
     Mantiene el efecto de desvanecimiento usando lifespan.

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas
   En cada ciclo de draw(), se llama a emitter.addParticle().
   Ese método decide, con probabilidad 50%, crear un Particle o un Confetti (que hereda de Particle pero redefine show).
   Cada nueva partícula se construye con:
      a)Un vector de posición en el origen del emisor.
      b)Un vector de velocidad aleatoria hacia arriba.
      c)Un lifespan inicial de 255.
   Las partículas se almacenan en el array dinámico this.particles dentro de Emitter.

#### Actualización de partículas
   Cada partícula, en p.run():
     1)Recibe una fuerza de gravedad (applyForce).
     2)Se actualiza (velocidad, posición y disminución de lifespan).
     3)Se dibuja en pantalla (show).
   Esto ocurre en cada frame hasta que la partícula “muere”.

#### Desaparición de partículas
   La vida útil (lifespan) disminuye en cada actualización (this.lifespan -= 2).
   Cuando lifespan < 0, la partícula se considera muerta (isDead() devuelve true).
   En el método Emitter.run(), se recorre el array de partículas de atrás hacia adelante:
   ``` js
     for (let i = this.particles.length - 1; i >= 0; i--) {
          let p = this.particles[i];
          p.run();
          if (p.isDead()) {
               this.particles.splice(i, 1); // elimina la partícula del array
          }
     }
   ```
   Esto elimina el objeto del array, lo que significa que ya no está referenciado en el programa.
   
#### Gestión de memoria en esta simulación
   El garbage collector se encarga de liberar la memoria automáticamente. 
   Es decir, al hacer splice(i, 1), el objeto Particle eliminado deja de estar en particles, y eventualmente es liberado por el motor de JS.
   No hay fugas de memoria porque:
      a)Las partículas muertas no quedan acumuladas en el array.
      b)No se guarda ninguna referencia oculta a ellas.

#### Experimento

### Analiza el ejemplo 4.6:
[Ejemplo 4.6](https://natureofcode.com/particles/#example-46-a-particle-system-with-forces)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas

#### Desaparición de partículas

#### Gestión de memoria en esta simulación

#### Experimento

### Analiza el ejemplo 4.7:
[Ejemplo 4.7](https://natureofcode.com/particles/#example-47-a-particle-system-with-a-repeller)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas

#### Desaparición de partículas

#### Gestión de memoria en esta simulación

#### Experimento








