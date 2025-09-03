# Unidad 4

## Actividad 1

### Artista y videos

[Memo Akten](https://www.memo.tv/)

[Simple Harmonic Motion](https://www.memo.tv/works/simple-harmonic-motion/)

[Superradiance](https://superradiance.net/)
## Actividad 2
[Angulos ejemplo](https://editor.p5js.org/juanferfranco/sketches/R1iTVQjzm)
### ¿Qué está pasando en esta simulación? ¿Cuál es la interacción?
Lo que ocurre en esta simulación es que se esta dibujando una linea que conecta dos puntos y al oprimir space esta linea junto con los dos puntos comiensan a girar en un angulo especifico sin separarce de dicha conección. 

### Nota que en cada frame se está trasladando el origen del sistema de coordenadas al centro de la pantalla. ¿Por qué crees que se hace esto?
Se traslada el origen al centro para simplificar la rotación de la figura alrededor de su propio eje central.

### Cuál es la relación entre el sistema de coordenadas y la función rotate().
rotate() siempre gira respecto al origen del sistema de coordenadas actual, y por eso casi siempre se combina con translate() para reposicionar ese origen donde queremos que ocurra la rotación.

[MOvimiento con angulos](https://editor.p5js.org/natureofcode/sketches/bZqHGYbRQ)

### ¿Qué hace la función heading()?
heading() devuelve el ángulo de un vector en radianes respecto al eje positivo X (horizontal hacia la derecha).

### ¿Qué hace la función push() y pop()? Realiza algunos experimentos para entender su funcionamiento.
push() guarda el estado actual de la transformación (traslación, rotación, escala, estilos gráficos).
pop() restaura el estado guardado.

Esto sirve para que transformaciones como translate() o rotate() no afecten a todo lo que se dibujes después.

### ¿Qué hace rectMode(CENTER)? Realiza algunos experimentos para entender su funcionamiento.
Se usa para que a la hora de girar se haga de manera natural desde el centro del objeto si se le quita el "CENTER" comienza a girar desde una esquina lo cual hace menos inmersivo el movimiento.

### ¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad? Trata de dibujar en un papel el vector de velocidad y cómo se relaciona con el ángulo de rotación y la operación de traslación y rotación.
El ángulo de rotación (angle) proviene de this.velocity.heading().
Eso significa que el rectángulo rota para “apuntar” en la dirección de su velocidad.
Matemáticamente, es el mismo ángulo que forma el vector de velocidad con el eje X.

## Actividad 3
```js
let vehicle;

function setup() {
  createCanvas(640, 240);
  vehicle = new Vehicle();
}

function draw() {
  background(255);
  vehicle.update();
  vehicle.checkEdges();
  vehicle.display();
}

class Vehicle {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.topspeed = 4;
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    // Controles con flechas
    if (keyIsDown(LEFT_ARROW)) {
      this.applyForce(createVector(-0.1, 0)); // acelera izquierda
    }
    if (keyIsDown(RIGHT_ARROW)) {
      this.applyForce(createVector(0.1, 0)); // acelera derecha
    }

    // Actualizamos movimiento
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topspeed);
    this.position.add(this.velocity);

    // Reset aceleración (importantísimo)
    this.acceleration.mult(0);
  }

  display() {
    let angle = this.velocity.heading();

    stroke(0);
    fill(127);
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);

    // Dibujar triángulo en lugar de rectángulo
    beginShape();
    vertex(20, 0);    // punta hacia adelante
    vertex(-20, 10);  // esquina izquierda
    vertex(-20, -10); // esquina derecha
    endShape(CLOSE);

    pop();
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

## Actividad 4

### Identifica motion 101. ¿Qué modificación hay que hacer al motion 101 cuando se quiere agregar fuerzas acumulativas? Trata de recordar por qué es necesario hacer esta modificación.
``` js
posición += velocidad
velocidad += aceleración

this.acceleration.mult(0);
```
Esto es necesario porque, de lo contrario, la aceleración se acumularía indefinidamente y los objetos se moverían de manera incorrecta.

### Identifica dónde está el Attractor en la simulación. Cambia el color de este.
```
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.mass = 20;
    this.G = 1;
    this.dragging = false;
    this.rollover = false; 
  }

  attract(mover) {
    // Calculate direction of force
    let force = p5.Vector.sub(this.position, mover.position);
    // Distance between objects
    let distance = force.mag();
    // Limiting the distance to eliminate "extreme" results for very close or very far objects
    distance = constrain(distance, 5, 25);

    // Calculate gravitional force magnitude
    let strength = (this.G * this.mass * mover.mass) / (distance * distance);
    // Get force vector --> magnitude * direction
    force.setMag(strength);
    return force;
  }

  // Method to display
  display() {
    ellipseMode(CENTER);
    stroke(0);
    if (this.dragging) {
      fill(50);
    } else if (this.rollover) {
      fill(100);
    } else {
      fill(175, 200);
    }
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }
}
```

Cambiar color
``` js
  display() {
  ellipseMode(CENTER);
  stroke(0);
  fill(255, 0, 0); // rojo
  ellipse(this.position.x, this.position.y, this.mass * 2);
}
```

### Observa que el Attractor tiene dos atributos this.dragging y this.rollover. Estos atributos no se modifican en el código, pero permitirían mover el attractor con el mouse y cambiar su color cuando el mouse está sobre él. ¿Cómo podrías modificar el código para que esto funcione? considera las funciones que ofrece p5.js para interactuar con el mouse.
Attractor
``` js
class Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.mass = 20;
    this.G = 1;
    this.dragging = false;
    this.rollover = false; 
    this.dragOffset = createVector(0, 0);
  }

  attract(mover) {
    let force = p5.Vector.sub(this.position, mover.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 25);

    let strength = (this.G * this.mass * mover.mass) / (distance * distance);
    force.setMag(strength);
    return force;
  }

  // Dibujo
  display() {
    ellipseMode(CENTER);
    stroke(0);
    if (this.dragging) {
      fill(50);       // cuando lo arrastro
    } else if (this.rollover) {
      fill(100);      // cuando el mouse está encima
    } else {
      fill(175, 200); // normal
    }
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }

  // Detectar si el mouse está encima
  rolloverCheck(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    this.rollover = (d < this.mass);
  }

  // Cuando presiono el mouse
  pressed(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    if (d < this.mass) {
      this.dragging = true;
      this.dragOffset.x = this.position.x - mx;
      this.dragOffset.y = this.position.y - my;
    }
  }

  // Cuando suelto el mouse
  released() {
    this.dragging = false;
  }

  // Cuando arrastro
  drag(mx, my) {
    if (this.dragging) {
      this.position.x = mx + this.dragOffset.x;
      this.position.y = my + this.dragOffset.y;
    }
  }
}
```

sketch
``` js
function draw() {
  background(255);

  attractor.rolloverCheck(mouseX, mouseY);
  attractor.drag(mouseX, mouseY);
  attractor.display();

  for (let i = 0; i < movers.length; i++) {
    let force = attractor.attract(movers[i]);
    movers[i].applyForce(force);

    movers[i].update();
    movers[i].show();
  }
}

function mousePressed() {
  attractor.pressed(mouseX, mouseY);
}

function mouseReleased() {
  attractor.released();
}
```

## Actividad 5
Observa de nuevo esta parte del código ¿Cuál es la relación entre r y theta con las posiciones x y y? Puedes repasar entonces la definición de coordenadas polares y cómo se convierten a coordenadas cartesianas.
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// PolarToCartesian
// Convert a polar coordinate (r,theta) to cartesian (x,y):
// x = r * cos(theta)
// y = r * sin(theta)

let r;
let theta;

function setup() {
  createCanvas(640, 480);
  r = height * 0.25;
  theta = 0;
}

function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  // Convert polar to cartesian
  let x = r * cos(theta);
  let y = r * sin(theta);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, x, y);
  circle(x, y, 48);
  theta += 0.02;
}

```
r = la distancia radial desde el origen (qué tan lejos está el punto del centro).
Theta = el ángulo que forma el vector respecto al eje x (en radianes en p5.js).

x = r * cos(Theta)
y = r * sen(Theta)

Multiplicar por r ajusta el tamaño de ese vector para que llegue justo a la distancia radial deseada.

### Modifica la función draw():
``` js
 function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  let v = p5.Vector.fromAngle(theta);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, x, y);
  circle(v.x, v.y, 48);
  theta += 0.02;
}
```
Este cambio genera error ya que la x y la y no estan definidas en ningun momento, pero si hacemos unos cambios:

``` js
function draw() {
  background(255);
  translate(width / 2, height / 2);

  let v = p5.Vector.fromAngle(theta);
  v.mult(r); // 👈 ajustar al radio

  fill(127);
  stroke(0);
  strokeWeight(2);

  line(0, 0, v.x, v.y);
  circle(v.x, v.y, 48);

  theta += 0.02;
}
```
El círculo vuelve a girar alrededor del centro, exactamente como antes.
La diferencia es que ahora usamos un p5.Vector en lugar de calcular manualmente con cos y sin.

### Ahora realiza esta modificación:
``` js
 function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  let v = p5.Vector.fromAngle(theta,r);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, v.x, v.y);
  circle(v.x, v.y, 48);
  theta += 0.02;
}
```
El círculo vuelve a girar alrededor del centro, exactamente como antes.
La diferencia es que ahora usamos p5.Vector.fromAngle(angle, length) el es un atajo para construir el vector, es parecido a mi solución de antes pero más simplificada (menos lineas).

## Actividad 6
