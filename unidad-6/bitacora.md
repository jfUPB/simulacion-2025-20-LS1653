# Evidencias de la unidad 6

## Actividad 1

### Captura 1

<img width="737" height="548" alt="image" src="https://github.com/user-attachments/assets/cefde4f7-af6c-47f1-8a83-f4a807ba080f" />

Unfenced Existence, 2018

### ¿Que me inspira su trabajo?

Este trabajo me inspira a tratar de crear paisajes, esto debido a que al ver su obra me trae a la mente la sensación de apreciar mi entorno ya sea un atardecer en lo alto del cielo o un pasto alto pintado por los colores generados por las luces naturales.

### Captura 2

<img width="737" height="737" alt="image" src="https://github.com/user-attachments/assets/693e9c47-2520-4ba8-bb43-85b1891b81c7" />

pi/4

### ¿Que me inspira su trabajo?

Al ver esta obra me trae a la mente de la pelicula matrix pues la obra se muestra artificial/robotica y este tipo de diseño me inspir a tratar de crear algún tipo de cableado que tenga una forma enrevezada y llamativa que transmita la sensación de algo más haya de nuestro conocimiento tecnologico.

# Seek: Investigación

## Actividad 2

### ¿Qué es una fuerza de dirección (steering force)?
Una fuerza de dirección es un vector que ajusta el rumbo de un agente (objeto) hacia un objetivo deseado, pero lo hace de forma suave y controlada, en lugar de cambiar bruscamente su velocidad.

Se calcula como la resta entre la velocidad deseada (la dirección y magnitud a la que el agente “quisiera” moverse) y la velocidad actual del agente.

Fórmula:

steering = desired − velocity

desired es el vector hacia la meta (normalizado y escalado a la velocidad máxima).

velocity es el  vector de movimiento actual del agente.

Este steering se limita a una fuerza máxima y se aplica como una aceleración sobre el agente.
El efecto es que el agente no gira instantáneamente, sino que corrige poco a poco su dirección imitando como lo haria algo vivo.

### ¿Qué diferencia tiene este tipo de fuerza con las que ya hemos estudiado en el contexto de la simulación de agentes?
Hasta ahora, en las simulaciones con agentes y partículas hemos visto fuerzas “físicas directas”, como:

- Gravedad.

- Atracción/repulsión.

- Viento.

- Fricción.

- etc.

Estas fuerzas se aplican sobre el agente (objeto) de manera “externa” y modifican su aceleración y movimiento sin un propósito definido: simplemente obedecen a la física del entorno.

En comparación, la steering force:

Es una fuerza intencional: no busca obedecer una ley física universal, sino guiar el comportamiento del agente (objeto) hacia un objetivo (ej: seguir, huir, alinearse, evitar choques).

Actúa como una capa de control sobre las fuerzas físicas ya conocidas, introduciendo la “decisión” o el “comportamiento”.

Permite la creación de movimientos más orgánicos y naturales, que se parecen a los seres vivos.

### ¿Qué relación tiene la steering force con Craig Reynolds y su trabajo en simulación de comportamiento animal?
La relación es directa, ya que la steering force fue el concepto clave introducido por Craig Reynolds en 1987 con su modelo de [Boids](https://en.wikipedia.org/wiki/Boids) (simulación de bandadas de pájaros). 

Reynolds diseñó un sistema donde agentes simples (los boids) seguían tres reglas básicas: separación, alineamiento y cohesión. Para implementar estas reglas, necesitaba que los agentes se movieran hacia direcciones deseadas de manera realista. Allí surge la idea de la steering force.

En lugar de teletransportar o cambiar instantáneamente la velocidad de un boid, Reynolds definió que cada comportamiento genera una fuerza de dirección, y la suma de todas esas fuerzas determina el movimiento final del agente.

Este enfoque fue revolucionario ya que dio origen a la simulación realista de enjambres, bandadas y cardúmenes e influyó en animación por computadora, videojuegos, robótica y realidad virtual. Basicamente se convirtió en la base para muchos algoritmos modernos de inteligencia artificial en entornos simulados.

## Actividad 3

### Estructura del campo de flujo

El campo de flujo está representado en la clase FlowField y se usa una matriz bidimensional (this.field) de vectores (p5.Vector):

``` js
this.field = new Array(this.cols);
for (let i = 0; i < this.cols; i++) {
  this.field[i] = new Array(this.rows);
}
```
Cada celda de la matriz corresponde a una porción del canvas (un rectángulo definido por la resolución). En cada celda se almacena un vector de dirección que los agentes (vehicles) seguirán.

ej: 

<img width="1296" height="401" alt="image" src="https://github.com/user-attachments/assets/817865a4-cc87-4045-b13a-fce4c26f3b88" />

#### Inicialización de vectores:
En init(), los vectores se generan con Perlin noise para producir una textura suave de direcciones:

``` js
let angle = map(noise(xoff, yoff), 0, 1, 0, TWO_PI);
this.field[i][j] = p5.Vector.fromAngle(angle);
```

### Comportamiento del agente (Vehicle.follow(flow))
En la clase Vehicle, la función follow(flow) implementa el algoritmo de Reynolds de seguimiento de un campo:

#### a) Identificar vector en su posición actual:
El vehículo consulta el vector del campo en su ubicación:

``` js
let desired = flow.lookup(this.position);
```
lookup() convierte la posición en índices de la cuadrícula.
Esto se hace con:

``` js
let column = constrain(floor(position.x / this.resolution), 0, this.cols - 1);
let row = constrain(floor(position.y / this.resolution), 0, this.rows - 1);
return this.field[column][row].copy();
```

#### b) Calcular velocidad deseada:
Ese vector se escala a la velocidad máxima:


``` js
desired.mult(this.maxspeed);
```

#### c) Calcular steering force:
El steering es la diferencia entre velocidad deseada y actual:

``` js
let steer = p5.Vector.sub(desired, this.velocity);
steer.limit(this.maxforce);
this.applyForce(steer);
```
Con esto, el vehículo ajusta su dirección hacia el vector del campo.

### Parámetros clave

#### Resolución del campo de flujo: this.resolution en FlowField (en este caso 20).
Define el tamaño de cada celda de la cuadrícula, mientras menor la resolución, más detallado es el campo.

#### Velocidad máxima: this.maxspeed en Vehicle (dada en el constructor con random(2,5)).
Controla la rapidez máxima con la que se mueve cada agente.

#### Fuerza máxima: this.maxforce en Vehicle (constructor con random(0.1,0.5)).
Limita el giro brusco del agente, mientras menor sea el movimiento sera más suave.

### Modificación realizada
Mi modificación fue: alterar la resolución del campo de flujo para hacerlo mucho más fino

Código modificado en setup():
``` js
flowfield = new FlowField(4);
```

Efecto observado:

Con resolución 20, el campo tiene celdas grandes, los vehículos siguen vectores más generales, con trayectorias amplias y fluidas.

Con resolución 4, el campo tiene muchas más celdas pequeñas, los vectores cambian más seguido, haciendo que los agentes zigzagueen más y sus trayectorias sean mucho más intrincadas.

El movimiento colectivo se vuelve más detallado y turbulento, casi como un enjambre de insectos.
<img width="801" height="300" alt="image" src="https://github.com/user-attachments/assets/3a4808b8-87fd-449d-9523-a3388945dff8" />

## Actividad 4

### Análisis del algoritmo de Flocking

En la clase Boid, cada regla devuelve un vector de steering force. Luego, estos vectores se combinan (con pesos distintos) para obtener la dirección final de cada agente.

#### Separación:
Objetivo: evitar choques o hacinamiento, manteniendo espacio entre los boids.

Cálculo:
Se busca a los vecinos dentro de un radio de separación pequeño y para cada vecino demasiado cercano, se calcula un vector que apunte lejos de él (posición propia – posición del vecino).

Luego se promedian estos vectores y se limitan a maxforce y como resultado, los boids se “repelen” si están muy juntos.

#### Alineación 
Objetivo: moverse en la misma dirección promedio que los vecinos → comportamiento grupal coordinado.

Cálculo:
Se identifican los vecinos en un radio de percepción y se suman sus vectores de velocidad actual y se hace el promedio.

Luego se ajusta este promedio a la maxspeed.

El steering force es la diferencia entre ese vector deseado y la velocidad actual.

Y ya como resultado, los boids terminan alineando su dirección con la del grupo.

#### Cohesión
Objetivo: moverse hacia el centro de masa del grupo → mantener la bandada unida.

Cálculo:
Se encuentran los vecinos dentro del radio de cohesión y se calcula la posición promedio de estos vecinos.

Luego el boid genera una fuerza de seek hacia ese punto y como resultado: los boids tienden a reagruparse si están dispersos.

### Parámetros clave
En el código de flocking de Shiffman aparecen estas variables críticas:

#### Radio de percepción: 
Define qué tan lejos “ve” cada boid a sus vecinos (perceptionRadius). Puede ser distinto para separación, alineación y cohesión.

#### Pesos de cada regla: 
Constantes como separationWeight, alignmentWeight, cohesionWeight que escalan cada vector antes de sumarlos.

#### Velocidad máxima y fuerza máxima: 
igual que en flow fields, limitan la magnitud del movimiento y los giros.

### Modificación realizada
Aumentar drásticamente el peso de Separación y disminuir Cohesión a casi cero.

``` js
flock(boids) {
  let sep = this.separate(boids); // Separation
  let ali = this.align(boids);    // Alignment
  let coh = this.cohere(boids);   // Cohesion

  // Modificación de pesos
  sep.mult(3.0);   // Mucha más separación
  ali.mult(1.0);   // Alineación normal
  coh.mult(0.1);   // Cohesión casi nula

  // Aplicar fuerzas
  this.applyForce(sep);
  this.applyForce(ali);
  this.applyForce(coh);
}
```

Los boids evitan mucho más a sus vecinos, se dispersan y mantienen distancias grandes y como la cohesión es casi nula, no tienden a reagruparse.

Tambian, la alineación hace que no sea completamente caótico, pero aún así se vera un "enjambre" mucho más suelto y esparcido.

# Apply: Aplicación

## Actividad 5

### Diseño

#### Elecciones
Musica: [Canción](https://www.youtube.com/watch?v=IhBrB5IMTf4)

Diseños: 
  Inicio: Queria mostrar las banderas de los dos paises implicados en la canción y que se fueran intercalando.

  <img width="1458" height="277" alt="image" src="https://github.com/user-attachments/assets/b9557530-ad53-45ba-9b76-9e252fc8609f" />

  Seegunda face: Queria mostrar una mini representación de lo que se cuenta en la canción y se me ocurrio tomar parte de mi idea de la entrega anterior.

### Codigo
``` js
// === Sketch base ===
// Inglaterra vs Alemania (fondo, buques, submarinos, explosiones, flow field musical + ondas visuales)

let fondoInglaterra, fondoAlemania;
let modoFondo = "uk";
let objetos = [];

// --- Ondas visuales ---
let ondas = [];

// --- Analizador de amplitud ---
let amp;
let fft;

// --- Música ---
let musicaFondo;

// --- Flow Field ---
let flowField;
let cols, rows;
let resolution = 40;

function preload() {
  fondoInglaterra = loadImage("assets/uk.png");
  fondoAlemania = loadImage("assets/alemania.png");

  soundFormats('mp3', 'wav');
  musicaFondo = loadSound('assets/musica.mp3');
}

function setup() {
  createCanvas(800, 600);

  musicaFondo.loop();
  amp = new p5.Amplitude();
  fft = new p5.FFT();

  cols = floor(width / resolution);
  rows = floor(height / resolution);
  flowField = new Array(cols * rows);

  // Ondas de fondo (colores decorativos)
  for (let i = 100; i < height; i += 100) {
    ondas.push(new Onda(i, [0, 150, 255]));     // azul
    ondas.push(new Onda(i + 50, [255, 0, 150])); // fucsia
  }

  // Submarinos iniciales
  for (let i = 0; i < 15; i++) {
    objetos.push(new Submarino(random(width), random(height)));
  }
}

//  Nuevo: cada 3 segundos aparece un buque en una posición aleatoria
  setInterval(() => {
    objetos.push(new Buque(random(width), random(height), true));
  }, 3000);

function draw() {
  background(0);
  
  // --- FFT solo para medir intensidad ---
  let spectrum = fft.analyze();
  let energy = fft.getEnergy("bass", "treble"); // mide energía general de la música

  // Si la intensidad es alta -> cambiar fondo automáticamente
  if (energy > 205) {
    modoFondo = "de";
  } else {
    modoFondo = "uk";
  }
  
  // --- Efecto de titileo según la música ---
  let level = amp.getLevel(); 
  let brillo = map(level, 0, 0.3, 60, 150); // brillo dinámico
  brillo = constrain(brillo, 60, 150);
  
  // Fondo semitransparente con bandera que titila
  push();
  tint(255, brillo);
  if (modoFondo === "uk") image(fondoInglaterra, 0, 0, width, height);
  else image(fondoAlemania, 0, 0, width, height);
  pop();

  // --- Ondas decorativas coloridas ---
  for (let onda of ondas) {
    onda.update();
    onda.show(level);
  }

  // --- Flow Field aplicado a buques ---
  let t = millis() * 0.0005;
  for (let obj of objetos) {
    if (obj instanceof Buque) {
      let n = noise(obj.pos.x * 0.002, obj.pos.y * 0.002, t);
      let angle = n * TWO_PI * 2;
      let musicAmp = map(level, 0, 0.3, 0, 1);
      angle += musicAmp * sin(t * 5);
      let flow = p5.Vector.fromAngle(angle);
      flow.mult(0.1); 
      obj.applyForce(flow);
    }
  }

  // --- Actualizar/dibujar objetos ---
  for (let obj of objetos) {
    obj.update();
    obj.show();
  }

  // --- Explosiones afectan submarinos ---
  for (let obj of objetos) {
    if (obj instanceof Explosion) {
      for (let other of objetos) {
        if (other instanceof Submarino) {
          let d = dist(obj.pos.x, obj.pos.y, other.pos.x, other.pos.y);
          if (d < obj.r && obj.life > 0) {
            let force = p5.Vector.sub(other.pos, obj.pos);
            let intensidad = map(obj.life, 60, 0, 1, 0);
            intensidad *= map(d, 0, obj.r, 1, 0);
            force.setMag(intensidad * 2);
            other.applyForce(force);
          }
        }
      }
    }
  }

  // --- Submarinos buscan buques ---
  for (let obj of objetos) {
    if (obj instanceof Submarino) {
      let closest = null;
      let minDist = 120;
      for (let other of objetos) {
        if (other instanceof Buque) {
          let d = dist(obj.pos.x, obj.pos.y, other.pos.x, other.pos.y);
          if (d < minDist) {
            minDist = d;
            closest = other;
          }
        }
      }

      if (closest) {
        obj.seek(closest.pos);
        closest.checkSurrounded(obj);

        //  Buques huyen de submarinos
        let fleeForce = p5.Vector.sub(closest.pos, obj.pos);
        fleeForce.setMag(-1.5); 
        closest.applyForce(fleeForce);
      }
    }
  }

  // --- Eliminar explosiones muertas ---
  objetos = objetos.filter(obj => !(obj instanceof Explosion && obj.life <= 0));
}

function mousePressed() {
  if (mouseButton === LEFT) objetos.push(new Buque(mouseX, mouseY));
  if (mouseButton === RIGHT) objetos.push(new Explosion(mouseX, mouseY));
}

function keyPressed() {
  if (key === 'c' || key === 'C') {
    modoFondo = (modoFondo === "uk") ? "alemania" : "uk";
  }
  if (key === 'r' || key === 'R') {
    objetos = [];
    for (let i = 0; i < 15; i++) {
      objetos.push(new Submarino(random(width), random(height)));
    }
  }
}

// --- Clases ---
class Buque {
  constructor(x, y, spawned = false) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.maxSpeed = 1.2;
    this.maxForce = 0.05;

    this.surroundedTime = 0;
    this.spawnTime = millis();
    this.spawned = spawned;
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.y < 0) this.pos.y = height;
    if (this.pos.y > height) this.pos.y = 0;
  }

  show() {
    let alpha = 255;
    let size = 20;
    if (this.spawned) {
      let t = (millis() - this.spawnTime) / 1000;
      if (t < 2) {
        alpha = map(t, 0, 2, 0, 255);
        size = map(sin(t * PI), 0, 1, 10, 20);
      }
    }
    fill(0, 0, 200, alpha);
    ellipse(this.pos.x, this.pos.y, size, size);
  }

  checkSurrounded(sub) {
    let d = dist(this.pos.x, this.pos.y, sub.pos.x, sub.pos.y);
    if (d < 30) {
      this.surroundedTime++;
      if (this.surroundedTime > 180) {
        objetos.push(new Explosion(this.pos.x, this.pos.y));
        objetos = objetos.filter(o => o !== this);
      }
    }
  }
}

class Submarino {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector(0, 0);
    this.maxSpeed = 2;
    this.maxForce = 0.05;
  }

  applyForce(force) {
    this.acc.add(force);
  }

  seek(target) {
    let desired = p5.Vector.sub(target, this.pos);
    desired.setMag(this.maxSpeed);
    let steer = p5.Vector.sub(desired, this.vel);
    steer.limit(this.maxForce);
    this.applyForce(steer);
  }

  update() {
    let jitter = p5.Vector.random2D().mult(0.1);
    this.applyForce(jitter);

    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.y < 0) this.pos.y = height;
    if (this.pos.y > height) this.pos.y = 0;
  }

  show() {
    push();
    translate(this.pos.x, this.pos.y);
    rotate(this.vel.heading());
    fill(200, 0, 0);
    rectMode(CENTER);
    rect(0, 0, 20, 8);
    pop();
  }
}

class Explosion {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.r = 10;
    this.life = 60;
  }
  update() {
    this.r += 5;
    this.life--;
  }
  show() {
    noFill();
    stroke(255, 150, 0);
    ellipse(this.pos.x, this.pos.y, this.r);
  }
}

// --- Clase de ondas visuales decorativas ---
class Onda {
  constructor(yBase, colorOnda) {
    this.yBase = yBase;
    this.colorOnda = colorOnda;
    this.offset = random(1000);
  }

  update() {
    this.offset += 0.01;
  }

  show(level) {
    noFill();
    stroke(this.colorOnda[0], this.colorOnda[1], this.colorOnda[2], 80);
    strokeWeight(2);

    beginShape();
    for (let x = 0; x <= width; x += 20) {
      let ang = (x * 0.02) + this.offset;
      let y = this.yBase + sin(ang) * 20 * (1 + level * 5);
      vertex(x, y);
    }
    endShape();
  }
}
```

### Link

[Mi obra](https://editor.p5js.org/estebanpuerta2006/sketches/GG3j7xH2a)

### Captura

<img width="998" height="693" alt="image" src="https://github.com/user-attachments/assets/e343c097-3caa-40c1-959c-a88e9c78ae6f" />

# Auto evaluación 



