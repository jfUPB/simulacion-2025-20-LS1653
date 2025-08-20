# Unidad 3


## 🤔 Fase: Reflect

### Actividad 01

Video hacerca de [Video](https://youtu.be/FUchd9wwBoI?si=b-s6SZWgt_EEdrOP)

### Actividad 02

Observa el proyecto [Data Structure](https://www.sosolimited.com/work/data-structure/).

### Actividad 03

Fuerzas [Capitulo del libro](https://natureofcode.com/forces/)

### Actividad 04

Motion 101

``` js
// Declare the Mover object.
let mover;

function setup() {
  createCanvas(640, 240);
  // Create the Mover object.
  mover = new Mover();
}

function draw() {
  background(255);
  // Call methods on the Mover object.
  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    // The object has two vectors: position and velocity.
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-2, 2), random(-2, 2));
  }

  update() {
    // Motion 101: position changes by velocity.
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 48);
  }

  checkEdges() {
    if (this.position.x > width) {
      this.position.x = 0;
    } else if (this.position.x < 0) {
      this.position.x = width;
    }

    if (this.position.y > height) {
      this.position.y = 0;
    } else if (this.position.y < 0) {
      this.position.y = height;
    }
  }
}
```

### Actividad 05

``` js
class Mover {
  constructor() {
    this.position = createVector();
    this.velocity = createVector();
    this.acceleration = createVector();
  }
}

//Ahora, considera que en un frame actúan sobre este elemento dos fuerzas: viento y gravedad. Por tanto, en ese frame aplicarás las dos fuerzas:

mover.applyForce(wind);

//y luego:

mover.applyForce(gravity);

//Finalmente, en el método applyForce de la clase Mover tendrás algo como:

applyForce(force) {
  this.acceleration = force;
}
```
#### ¿Qué problema le ves a este planteamiento?
El problema que detecto es que estamos cambiando la aceleración cada vez que se llama en vez de que se sumen entre ellas, osea la estamos modificando.

#### ¿Qué solución propones?
Mi solución seria usar la función add() para sumar las fuerzas y asi tener la verdadera aceleración.
``` js
applyForce(force) {
  let f = p5.Vector.div(force, this.mass); // por si luego usamos masas distintas
  this.acceleration.add(f); 
}
```
#### ¿Cómo lo implementarías en p5.js?
La implementación quedaria de esta manera:
``` js
let mover; // 👈 declaramos fuera para que lo reconozcan setup y draw

class Mover {
  constructor(x, y, m) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = m; // masa del objeto
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass); 
    this.acceleration.add(f); // acumulamos la fuerza/m
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); // reseteamos la aceleración
  }

  display() {
    ellipse(this.position.x, this.position.y, this.mass * 16);
  }
}

function setup() {
  createCanvas(400, 400);
  mover = new Mover(200, 200, 1);
}

function draw() {
  background(220);

  let wind = createVector(0.1, 0);    // fuerza hacia la derecha
  let gravity = createVector(0, 0.2); // fuerza hacia abajo

  mover.applyForce(wind);
  mover.applyForce(gravity);

  mover.update();
  mover.display();
}
```

### Actividad 06
``` js
//Ya te diste cuenta entonces que la fuerza neta es la sumatoria de todas las fuerzas que actúan sobre un objeto. Ahora, ¿Qué pasa si en un frame actúan sobre un objeto dos fuerzas? ¿Cómo calculas la aceleración resultante?

mover.applyForce(wind);
mover.applyForce(gravity);
.
.
.

applyForce(force) {
  // Segunda ley de Newton, pero con acumulación de fuerza, sumando todas las fuerzas de entrada a la aceleración
  this.acceleration.add(force);
}

⚠️

//Te diste cuenta qué pasó aquí con respecto a la actividad anterior? Vuelve a mirar.

//Entonces en cada frame, la aceleración se calcula como la sumatoria de todas las fuerzas que actúan sobre un objeto:

mover.applyForce(wind);
mover.applyForce(gravity);
mover.update();

//Y en el método update() se actualiza la velocidad y la posición del objeto:

update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
}
``` 

#### ¿Por qué es necesario multiplicar la aceleración por cero en cada frame?

Porque la aceleración debe reflejar únicamente las fuerzas del frame actual, no arrastrar fuerzas viejas.

#### ¿Por qué se multiplica por cero justo al final de update()?

Porque es justo después de haber usado la aceleración acumulada para modificar la velocidad y la posición.
