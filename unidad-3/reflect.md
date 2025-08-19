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
