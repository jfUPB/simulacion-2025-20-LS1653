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

1.Modificación
Unidad 1: Aleatoriedad
Se añadió aleatoriedad en el tamaño (random(5,15)) y el color (random(100,255)).

2.Gestión
Cada partícula se guarda en el array particles.
En cada frame se revisa si su vida (lifespan) es menor que 0, y si lo es, se elimina con splice().
De esta manera se evita acumular partículas muertas en memoria

3.Explicación
Unidad 1: Aleatoriedad
   Se añadió aleatoriedad en el tamaño (random(5,15)) y el color (random(100,255)).
   Esto se aplicó en el constructor de cada partícula.

Por qué:
   La aleatoriedad da diversidad visual y naturalidad al sistema, evitando que todas las partículas se vean idénticas.

4.Enlace
[Enlace](https://editor.p5js.org/estebanpuerta2006/sketches/pyemkROqv)

5.Codigo
``` js
  let particles = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  particles.push(new Particle(width / 2, 20));

  // Looping through backwards to delete
  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    if (particle.isDead()) {
      //remove the particle
      particles.splice(i, 1);
    }
  }
}


class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;

    // ---- Unidad 1: Aleatoriedad ----
    this.size = random(5, 15); // tamaño aleatorio
    this.color = color(random(100, 255), random(100, 255), random(100, 255), this.lifespan);
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity); // Unidad 3: Gravedad
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    noStroke();
    fill(this.color);
    circle(this.position.x, this.position.y, this.size);
  }

  isDead() {
    return (this.lifespan < 0.0);
  }
}
```

6.Captura

<img width="458" height="300" alt="image" src="https://github.com/user-attachments/assets/c2f1c31c-f7a8-4ed8-900b-ec89d37c6b53" />


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

1.Modificación
Unidad 2: Motion 101, suma de fuerzas
Además de la gravedad, añadí otra fuerza constante: el viento.

2.Gestión
Cada Emitter crea partículas en su origen (addParticle()).
Estas se almacenan en un array dentro del objeto Emitter.
En cada frame, se recorre el array en reversa y se eliminan con splice() aquellas que han muerto (lifespan < 0).
Esto garantiza que la memoria no se llene con partículas innecesarias.

3.Explicación
Unidad 2: Motion 101, suma de fuerzas
Además de la gravedad, añadí otra fuerza constante: el viento.
En cada frame, la partícula recibe dos fuerzas:
   gravity = (0, 0.05)
   wind = (0.02, 0)
Estas fuerzas se suman en la aceleración (this.acceleration.add(force)).
Luego, la aceleración modifica la velocidad, y la velocidad la posición (modelo clásico de Motion 101).

Por qué:
Esto ilustra cómo varias fuerzas simultáneas afectan el movimiento de un objeto y el como con esto se puede lograr un concepto más atractivo visualmente.


4.Enlace
[Enlace](https://editor.p5js.org/estebanpuerta2006/sketches/stdxSBDu2)

5.Codigo
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Particles are generated each cycle through draw(),
// fall with gravity and fade out over time
// A ParticleSystem object manages a variable size
// list of particles.

// an array of ParticleSystems
let emitters = [];

function setup() {
  createCanvas(640, 240);
  let text = createP("click to add particle systems");
}

function draw() {
  background(255);
  for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();
  }
}

function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
  }

  run() {
    // Unidad 3: Gravedad
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);

    // ---- Unidad 2: Motion 101 (suma de fuerzas) ----
    let wind = createVector(0.06, 0); // viento hacia la derecha
    this.applyForce(wind);

    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0); // reset acumulador
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  run() {
    // Looping through backwards to delete
    for (let i = this.particles.length - 1; i >= 0; i--) {
      this.particles[i].run();
      if (this.particles[i].isDead()) {
        // Remove the particle
        this.particles.splice(i, 1);
      }
    }

    // Run every particle
    // ES6 for..of loop
    // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of
    // https://www.youtube.com/watch?v=Y8sMnRQYr3c
    // for (let particle of this.particles) {
    //   particle.run();
    // }

    // Filter removes any elements of the array that do not pass the test
    // I am also using ES6 arrow snytax
    // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions
    // https://www.youtube.com/watch?v=mrYMzpbFz18
    // this.particles = this.particles.filter(particle => !particle.isDead());

    // Without ES6 arrow code would look like:
    // this.particles = this.particles.filter(function(particle) {
    //   return !particle.isDead();
    // });
  }
}
```

6.Captura

<img width="797" height="298" alt="image" src="https://github.com/user-attachments/assets/432bb30c-4416-4c2b-b9ff-2812cc049b3f" />


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

1.Modificación
Unidad 4: Ondas / sinusoides
Se añadió un movimiento horizontal ondulatorio a cada partícula.

2.Gestión
Cada Emitter guarda sus partículas en un array.
Se crean nuevas en cada frame y se eliminan las muertas con splice().
Esto mantiene el sistema eficiente y evita fugas de memoria.

3.Explicación
Unidad 4: Ondas / sinusoides
Se añadió un movimiento horizontal ondulatorio a cada partícula.
Usamos la función sin(frameCount * frecuencia + desfase) * amplitud para modificar su posición en X.
Esto hace que las partículas se balanceen mientras caen.

Por qué:
En vez de caer en línea recta, las partículas parecen “flotar” o mecerse en el aire, logrando que se sienta cómo un confeti real.

4.Enlace
[Enlace](https://editor.p5js.org/estebanpuerta2006/sketches/qcXwoAlZL)

5.Codigo
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Particles are generated each cycle through draw(),
// fall with gravity and fade out over time
// A ParticleSystem object manages a variable size
// list of particles.


let emitter;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 20);
}

function draw() {
  background(255);
  emitter.addParticle();
  emitter.run();
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;

    // Unidad 4: Ondas / Sinusoides
    this.amplitude = random(10, 30); // amplitud de la onda
    this.frequency = random(0.05, 0.1); // frecuencia de la onda
    this.offset = random(TWO_PI); // desfase
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);

    // Movimiento ondulatorio agregado (Unidad 4)
    this.position.x += sin(frameCount * this.frequency + this.offset) * 2;

    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    let r = random(1);
    if (r < 0.5) {
      this.particles.push(new Particle(this.origin.x, this.origin.y));
    } else {
      this.particles.push(new Confetti(this.origin.x, this.origin.y));
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Child class constructor
class Confetti extends Particle {
  // Override the show method
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

6.Captura

<img width="415" height="302" alt="image" src="https://github.com/user-attachments/assets/46c858a3-a859-40ed-bf9d-eebf29569cc7" />

<img width="382" height="300" alt="image" src="https://github.com/user-attachments/assets/026cb8c4-7cd3-4ac8-9666-4a50202b09a3" />


### Analiza el ejemplo 4.6:
[Ejemplo 4.6](https://natureofcode.com/particles/#example-46-a-particle-system-with-forces)

#### Analisis 

1)Estructura general:

   Programa principal (setup y draw) -> Inicializa el lienzo, crea un emisor y controla el bucle de animación.
   Clase Particle → Define cómo se comporta una partícula individual: su movimiento, cómo recibe fuerzas, cómo se dibuja y cómo “muere”.
   Clase Emitter → Gestiona un conjunto dinámico de partículas: las crea, les aplica fuerzas y elimina las que mueren.

2)Programa principal:
   ``` js
     function setup() {
       createCanvas(1280, 480);
       emitter = new Emitter(width / 2, 50);
     }

     function draw() {
       background(255,30);

       let gravity = createVector(0, 0.1);
       emitter.applyForce(gravity);

       emitter.addParticle();
       emitter.run();
     }
   ```
   Se crea un emisor de partículas en el centro horizontal y a 50 px de la parte superior.
   Cada frame:
      Se dibuja un fondo blanco con transparencia (30) -> crea un efecto de “estela” al mover partículas.
      Se crea un vector gravedad que empuja a todas las partículas hacia abajo.
      El emisor:
         Crea una nueva partícula en cada frame (addParticle).
         Actualiza todas las partículas activas (run).

3)Clase Particle:
   ``` js
     class Particle {
        constructor(x, y) {
        this.position = createVector(x, y);
        this.acceleration = createVector(0, 0.0);
        this.velocity = createVector(random(-1, 1), random(-2, 0));
        this.lifespan = 255.0;
        this.mass = 1;
     }
   ```
   Cada partícula tiene:
     Posición inicial en el emisor.
     Aceleración (se acumula con fuerzas aplicadas).
     Velocidad inicial aleatoria hacia arriba/los lados.
     Tiempo de vida (lifespan): empieza en 255 (transparencia máxima).
     Masa (se usa para calcular cómo afecta una fuerza).

4)Clase Emitter:
   ``` js
     class Emitter {
       constructor(x, y) {
       this.origin = createVector(x, y);
       this.particles = [];
     }
   ```
   El emisor tiene:
     Un origen (posición fija donde nacen las partículas).
     Una lista dinámica de partículas (this.particles).

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas
  Cada frame se llama a emitter.addParticle().
  Si la simulación corre a 60 fps -> se crean ~60 partículas por segundo.

#### Desaparición de partículas
  Una vez muerta (lifespan < 0), el Emitter la elimina del array.
   
#### Gestión de memoria en esta simulación
  Cuando el Emitter hace splice(i, 1), elimina la referencia a la partícula muerta.
  Como ya no hay referencias, el recolector de basura libera esa memoria automáticamente.
  Resultado:
     No se acumulan partículas muertas.
     El array mantiene un tamaño estable (dependiendo de cuántas estén vivas en un momento dado).
     No hay fugas de memoria.

#### Experimento

1.Modificación
Unidad 1: Aleatoriedad, variante Perlin noise
En lugar de usar random(), utilicé noise() para controlar un movimiento horizontal suave.

2.Gestión
El Emitter crea partículas en cada frame con addParticle().
Todas las partículas se guardan en un array.
En cada iteración (run()), si una partícula muere (lifespan < 0), se elimina con splice().
Esto asegura que el array solo guarde partículas vivas y evita fugas de memoria.

3.Explicación
En lugar de usar random(), utilicé noise() para controlar un movimiento horizontal suave.
Cada partícula tiene un noiseOffset diferente, por lo que no se mueven todas igual.
Esto hace que las trayectorias sean orgánicas, más parecidas a fenómenos naturales como humo o polvo.

Por qué:
Le da un aspecto más suave gracias al ruido Perlin y lo hace más bonito a la vista del espectador ya que parece algo ordenado entre lo aleatorio.

4.Enlace
[Enlace](https://editor.p5js.org/estebanpuerta2006/sketches/BbvOOv-Hc)

5.Codigo
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let emitter;

function setup() {
  createCanvas(1280, 480);
  emitter = new Emitter(width / 2, 50);
}

function draw() {
  background(255,30);

  // Apply gravity force to all Particles
  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  emitter.addParticle();
  emitter.run();
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0.0);
    this.velocity = createVector(random(-1, 1), random(-2, 0));
    this.lifespan = 255.0;
    this.mass = 1;

    // ---- Unidad 1 (variante): Perlin noise ----
    this.noiseOffset = random(1000); // punto de partida diferente para cada partícula
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);

    // Movimiento horizontal suave con Perlin noise
    let n = noise(this.noiseOffset + frameCount * 0.01);
    let offset = map(n, 0, 1, -2, 2); 
    this.position.x += offset;

    this.acceleration.mult(0);
    this.lifespan -= 2.0;
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Emitter {

  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    //{!3} Using a for of loop to apply the force to all particles
    for (let particle of this.particles) {
      particle.applyForce(force);
    }
  }

  run() {
    //{!7} Can’t use the enhanced loop because checking for particles to delete.
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```

6.Captura

<img width="517" height="600" alt="image" src="https://github.com/user-attachments/assets/824f43e1-c910-42e1-8762-20f57f5fc2c3" />


### Analiza el ejemplo 4.7:
[Ejemplo 4.7](https://natureofcode.com/particles/#example-47-a-particle-system-with-a-repeller)

#### Analisis 

1)Estructura general del programa:
   El código simula un sistema de partículas que:
     Se emiten desde un punto fijo en la pantalla (un Emitter).
     Son afectadas por gravedad universal.
     Son repelidas por un objeto invisible (Repeller).
     Desaparecen gradualmente con el tiempo para evitar acumulación infinita.

2)Clase Particle:
   Atributos: posición, velocidad, aceleración, vida útil.
   Métodos:
      applyForce(f): acumula fuerzas en la aceleración.
      update(): integra aceleración y velocidad → movimiento realista.
      show(): dibuja un círculo semitransparente que se desvanece al morir.
      isDead(): indica cuándo la partícula debe eliminarse.

3)Clase Emitter:
    Atributos: origen de emisión, arreglo de partículas.
    Métodos:
      addParticle(): genera nuevas partículas en el origen.
      applyForce(force): aplica una fuerza (como la gravedad) a todas las partículas.
      applyRepeller(repeller): calcula una fuerza de repulsión entre cada partícula y el repulsor.
      run(): actualiza, dibuja y elimina partículas muertas.

4)Clase Repeller:
    Atributos: posición fija y fuerza de repulsión (power).
    Métodos:
      repel(particle): calcula la fuerza de repulsión basada en la distancia (inspirada en la ley de gravitación, pero invertida).
      show(): dibuja un círculo representando el repulsor.
      
#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas
   ``` js
     this.particles.push(new Particle(this.origin.x, this.origin.y));
   ```
   En cada ciclo de draw() se ejecuta emitter.addParticle().
   Este método hace:

#### Desaparición de partículas

   Cada partícula tiene un atributo lifespan, que comienza en 255.0 y disminuye en update():
   ``` js
      this.lifespan -= 2;
   ```
   Cuando lifespan llega a 0, el método isDead() devuelve true.
   En el método run() del Emitter, se recorre el arreglo de partículas de atrás hacia adelante y si alguna está muerta, se elimina con:
   ``` js
      this.particles.splice(i, 1);
   ```

#### Gestión de memoria en esta simulación
   Creación dinámica: cada frame aparecen nuevas partículas, ocupando memoria en el heap.
   Eliminación temprana: al morir, se eliminan del arreglo con splice().
   Garbage Collector: al no haber referencias a las partículas muertas, el motor de JS (V8 en p5.js) recicla esa memoria.

#### Experimento

1.Modificación
Unidad 4
Apliqué el modelo de Hooke: F = -k * distancia.

2.Gestión
El sistema de partículas sigue manejando la vida útil con lifespan, y cuando una partícula está muerta (isDead()), se elimina con splice. Esto evita que se acumulen partículas en memoria.
-> Así se gestiona de manera eficiente la creación/destrucción dinámica.

3.Explicación
Unidad 4
Apliqué el modelo de Hooke: F = -k * distancia.
El emisor ahora oscila alrededor de un ancla, produciendo un movimiento elástico.
Esto se aplicó directamente a la posición del emitter en cada frame.

Por qué:
Los resortes añaden momentos menos predecibles y tambien queria utilizarlo ya que es el que menos tengo repasado.

4.Enlace
[Enlace](https://editor.p5js.org/estebanpuerta2006/sketches/1_V73Zi5w)

5.Codigo
``` js
let emitter;
let repeller;
let anchor; // punto de anclaje del resorte

function setup() {
  createCanvas(640, 240);
  anchor = createVector(width / 2, 60);
  emitter = new Emitter(width / 2, 60);
  repeller = new Repeller(width / 2, 200);
}

function draw() {
  background(255);

  // El emisor ahora está conectado al anchor con un resorte
  let springForce = p5.Vector.sub(anchor, emitter.origin);
  let k = 0.05; // constante de elasticidad
  springForce.mult(k);
  emitter.origin.add(springForce); // aplicamos fuerza hacia el anchor

  emitter.addParticle();

  // Gravedad universal
  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  // Repulsión
  emitter.applyRepeller(repeller);

  emitter.run();
  repeller.show();

  // Dibujar el resorte como línea para visualizarlo
  stroke(0, 100);
  line(anchor.x, anchor.y, emitter.origin.x, emitter.origin.y);
  fill(0);
  circle(anchor.x, anchor.y, 8); // punto de anclaje
}

// Repeller igual que antes
class Repeller {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.power = 150;
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 32);
  }

  repel(particle) {
    let force = p5.Vector.sub(this.position, particle.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 50);
    let strength = (-1 * this.power) / (distance * distance);
    force.setMag(strength);
    return force;
  }
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.acceleration = createVector(0, 0);
    this.lifespan = 255.0;
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(f) {
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
    }
  }

  applyRepeller(repeller) {
    for (let particle of this.particles) {
      let force = repeller.repel(particle);
      particle.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```

6.Captura

<img width="511" height="293" alt="image" src="https://github.com/user-attachments/assets/31eac5c3-099c-4f85-a83a-0ec27a690d0b" />

## Apply

### Actividad 3


## Mi nota propuesta

Tu mismo vas a propoer una nota basada en la rúbrica y justificarás cada criterio de la rúbrica indicando qué evidencias presentes en la bitácora justifican la nota que propones.

Si tu bitácora no incluye la nota propuesta y la justificación tendrás una nota de 0.










