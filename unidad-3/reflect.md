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

### Actividad 07

``` js
mover.applyForce(wind);
mover.applyForce(gravity);

applyForce(force) {
    // Asume que la masa es 10
    force.div(10);
    this.acceleration.add(force);
}
```

#### ¿Qué ves raro?

Lo raro es que se esta dividiendo el vector "force" directamente, pero "force" es un objeto y los objetos se pasan por referencia en js.p5.

Lo cual hace que se modifique el mismo vector force.

Entonces, pj:
``` js
let wind = createVector(1, 0);
let gravity = createVector(0, 0.5);

mover.applyForce(wind);
mover.applyForce(gravity);
```

Después de la primera llamada:

wind ya no es (1, 0), ahora quedó dividido entre 10 → (0.1, 0).

Después de la segunda llamada:

gravity tampoco es (0, 0.5), ahora quedó en (0, 0.05).

Es decir, se estan alterando las fuerzas originales, cuando en realidad las fuerzas deberían permanecer intactas, porque son propiedades del "mundo" y no del objeto que recibe la fuerza.

La solución correcta es hacer una copia del vector antes de modificarlo:
``` js
applyForce(force) {
    let f = force.copy();   // 👈 hacemos una copia
    f.div(10);              // dividimos la copia por la masa
    this.acceleration.add(f);
}
```

De esta forma:

wind sigue siendo (1, 0)

gravity sigue siendo (0, 0.5)

Lo que se modifica es solo la copia, que se acumula en la aceleración.

### Actividad 08
``` js
let friction = this.velocity.copy();
let friction = this.velocity;
```

#### ¿Cuál es la diferencia entre las dos líneas?
##### Línea 1: let friction = this.velocity.copy();

.copy() crea un nuevo objeto p5.Vector con los mismos valores que this.velocity.

Esto significa que friction es independiente de this.velocity.

Si después modificas friction, no afecta a this.velocity.

##### Línea 2: let friction = this.velocity;

Aquí no hay copia: friction y this.velocity son dos referencias al mismo objeto en memoria.

Si cambias algo en friction, también cambia en this.velocity, porque ambos apuntan al mismo vector.

#### ¿Qué podría salir mal con let friction = this.velocity;

Lo que puede salir mal es que por ejemplo al querer calcular la fricción basada en la velocidad actual, pero al normalizar o escalar friction, también se termina modificando this.velocity sin querer. Eso rompe la lógica, porque la velocidad debería mantenerse intacta hasta el momento en que sumas todas las fuerzas.

#### En el fragmento de código ¿Cuándo es por VALOR y cuándo por REFERENCIA.

this.velocity.copy() → nuevo objeto (VALOR).

this.velocity → misma referencia (REFERENCIA).

### Actividad 09
#### 1. Fricción → El cuadrado deslizándose

##### Cómo modelé la fuerza:

La fricción se modeló como una fuerza que se opone al movimiento del objeto.
Cada vez que se hace clic aparece un cuadrado en el borde izquierdo que se desplaza horizontalmente con una velocidad inicial.
La fricción se resta a la velocidad en cada frame, hasta que el cuadrado se detiene.
Con la tecla "v" aumentamos la velocidad inicial de los nuevos cuadrados.
Con la tecla "f" aumentamos la magnitud de la fricción.

##### Relación conceptual:

La fricción representa cómo los objetos en el mundo real pierden energía al deslizarse, y aquí los cuadrados se van deteniendo con el tiempo.
La interactividad simboliza cómo nuestras acciones (clic, teclas) pueden cambiar las condiciones de un sistema físico.


``` js
let cuadrados = [];
let velocidadInicial = 5; // velocidad inicial de nuevos cuadrados
let friccionBase = 0.05; // fricción global

function setup() {
  createCanvas(800, 400);
}

function draw() {
  background(220);
  
  // Mostrar e actualizar todos los cuadrados
  for (let c of cuadrados) {
    c.update();
    c.display();
  }
  
  // Mostrar info en pantalla
  fill(0);
  textSize(14);
  text("Click: generar cuadrado | 'v': aumentar velocidad (" + velocidadInicial + ") | 'f': aumentar fricción (" + friccionBase.toFixed(2) + ")", 10, height - 10);
}

function mousePressed() {
  cuadrados.push(new Cuadrado(velocidadInicial));
}

function keyPressed() {
  if (key === 'v' || key === 'V') {
    velocidadInicial += 1;
  }
  if (key === 'f' || key === 'F') {
    friccionBase += 0.01;
  }
}

// Clase Cuadrado
class Cuadrado {
  constructor(vel) {
    this.x = 0;
    this.y = random(height - 40);
    this.size = 40;
    this.vel = vel;
  }
  
  update() {
    if (this.vel > 0) {
      // aplicar fricción
      let friccion = friccionBase;
      this.vel -= friccion;
      this.vel = max(this.vel, 0); // evitar negativos
      this.x += this.vel;
    }
  }
  
  display() {
    fill(100, 150, 255);
    rect(this.x, this.y, this.size, this.size);
  }
}
```

[Enlace del ejemplo](https://editor.p5js.org/estebanpuerta2006/sketches/CAxZodIk7)

<img width="942" height="496" alt="image" src="https://github.com/user-attachments/assets/3f17789b-dcef-4339-8bb3-fff0706e740d" />


#### 2. Resistencia del aire y de fluidos → Caida libre del cialo al agua

##### Cómo modelé la fuerza:

Cada clic genera un círculo en la parte superior que cae en caída libre.
El canvas está dividido en dos mitades:
Parte superior (aire): resistencia baja.
Parte inferior (agua): resistencia alta.
La tecla "p" cambia el paso de integración (afecta cómo se siente la caída en el agua).

##### Relación conceptual:

Muestra cómo los fluidos afectan la caída de los objetos.
Simboliza el contraste entre el movimiento libre y el movimiento resistido.

``` js
let particles = [];
let gravity;
let airResistance = 0.01;   // Resistencia del aire
let waterResistance = 0.1;  // Resistencia del agua (se puede modificar con "p")

function setup() {
  createCanvas(600, 600);
  gravity = createVector(0, 0.2); // fuerza de gravedad
}

function draw() {
  background(220);

  // Divisiones: aire (arriba) y agua (abajo)
  stroke(0);
  line(0, height/2, width, height/2);
  noStroke();
  fill(180, 220, 255, 100);
  rect(0, 0, width, height/2);  // cielo
  fill(0, 100, 255, 120);
  rect(0, height/2, width, height/2); // agua

  // Actualizar partículas
  for (let p of particles) {
    // Gravedad
    p.applyForce(gravity);

    // Determinar si está en aire o agua
    if (p.pos.y < height/2) {
      // Aire
      let drag = p.vel.copy();
      drag.mult(-1);
      drag.setMag(airResistance * p.vel.magSq());
      p.applyForce(drag);
    } else {
      // Agua
      let drag = p.vel.copy();
      drag.mult(-1);
      drag.setMag(waterResistance * p.vel.magSq());
      p.applyForce(drag);
    }

    p.update();
    p.display();
  }
}

function mousePressed() {
  particles.push(new Particle(mouseX, 20));
}

function keyPressed() {
  if (key === 'p' || key === 'P') {
    waterResistance += 0.05; // Aumentar resistencia del agua
    print("Nueva resistencia del agua: " + waterResistance);
  }
}

// Clase Partícula
class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.r = 16;
  }

  applyForce(force) {
    let f = force.copy();
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  display() {
    fill(255, 100, 100);
    ellipse(this.pos.x, this.pos.y, this.r*2);
  }
}
```

[Enlace del ejemplo](https://editor.p5js.org/estebanpuerta2006/sketches/QToKZP1l6)

<img width="750" height="692" alt="image" src="https://github.com/user-attachments/assets/6f048faa-1f72-4b7e-b366-e636473e0084" />

#### 3. Atracción gravitacional → orbitas

##### Cómo modelé la fuerza:

Se generan varias esferas en pantalla.
Todas son atraídas hacia un punto central (la “estrella”).
La gravedad es una fuerza proporcional a la distancia.
Con la tecla "f" se aumenta la intensidad de la gravedad.
No hay colisión entre objetos, y el fondo no cambia de color.

##### Relación conceptual:

Representa el comportamiento de los cuerpos celestes bajo la gravedad.
Simboliza cómo todo tiende a atraerse hacia un centro común.

``` js
let estrellas = [];
let gravedad = 1500; // fuerza gravitacional inicial
let centro;

function setup() {
  createCanvas(800, 600);
  centro = createVector(width/2, height/2); // "orbita" central que atrae
}

function draw() {
  background(0);

  // Dibujar el centro (la "órbita A")
  fill(255, 200, 0);
  noStroke();
  ellipse(centro.x, centro.y, 30, 30);

  // Dibujar y actualizar las estrellas
  for (let estrella of estrellas) {
    // Vector de dirección hacia el centro
    let dir = p5.Vector.sub(centro, estrella.pos);
    let distSq = constrain(dir.magSq(), 100, 10000); 
    let fuerza = gravedad / distSq; // Ley de gravitación simplificada

    dir.setMag(fuerza);
    estrella.vel.add(dir); // Aplicar fuerza
    estrella.pos.add(estrella.vel);

    // Dibujar la estrella
    fill(150, 200, 255);
    ellipse(estrella.pos.x, estrella.pos.y, 10, 10);
  }

  // Texto de info
  fill(255);
  textSize(16);
  text("Click = Crear estrella | f = aumentar gravedad (" + nf(gravedad, 1, 2) + ")", 10, 20);
}

function mousePressed() {
  // Crear estrella en posición aleatoria
  let nueva = {
    pos: createVector(mouseX, mouseY),
    vel: p5.Vector.random2D().mult(random(2, 4))
  };
  estrellas.push(nueva);
}

function keyPressed() {
  if (key === 'f' || key === 'F') {
    gravedad += 100; // aumentar la fuerza de atracción
  }
}
```

[Enlace del ejemplo](https://editor.p5js.org/estebanpuerta2006/sketches/xU8XVmbYbX)

<img width="918" height="672" alt="image" src="https://github.com/user-attachments/assets/16b02be1-3139-4595-b3a8-e4c2107c4a83" />
