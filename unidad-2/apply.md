# Unidad 2


## 🛠 Fase: Apply

### Describe el concepto de tu obra generativa:
#### Fase inicial
Mi obra consiste en un sistema de movimiento generado aleatoriamente en el que múltiples objetos orbitan alrededor del mouse. Estos objetos se desplazan dentro de una órbita definida por la posición del cursor, y su comportamiento cambia dinámicamente dependiendo de la interacción del usuario y las colisiones entre ellos.

Cuando dos objetos colisionan, se destruyen entre sí y el fondo de la pantalla cambia de color, tomando como base una mezcla de los colores aleatorios asignados a dichos objetos. Inmediatamente después, nuevos objetos son generados para mantener constante la población en pantalla.

Además, con un clic izquierdo del mouse, se invierte la dirección de la órbita, haciendo que los objetos comiencen a alejarse del cursor en lugar de acercarse. El movimiento de fondo también está animado mediante ruido Perlin (noise), el cual, de manera esporádica y con base en una aleatoriedad normalizada, pinta el fondo con nuevos colores que generan una atmósfera envolvente y fluida.

Como agregado, con la tecla "m" se podran generar más objetos y con la tecla "p" se para el traso generado con noise.

#### Resultado que salio 
Al final mi obra termino siendo un sistema de movimiento generado aleatoriamente en el que múltiples objetos orbitan alrededor del cursor del mouse. Estos objetos se desplazan siguiendo una órbita definida por la posición del cursor, y su comportamiento cambia dinámicamente según la interacción del usuario y las colisiones entre ellos.

Cuando dos círculos colisionan, se destruyen mutuamente y el fondo de la pantalla cambia de color, tomando como base una mezcla de los colores aleatorios asignados a dichos objetos. Inmediatamente después del cambio de color y la destrucción de los círculos, se generan nuevos para mantener constante la población en pantalla.

La interactividad con el espectador se logra de diversas formas:

Los círculos siempre buscan la posición del cursor.

Al presionar la tecla "p", se genera una lluvia de triángulos que simulan una lluvia de estrellas; estos triángulos caen hasta que, aleatoriamente, se detienen o se destruyen al llegar al borde inferior.

Con la tecla "m", se agregan más círculos, haciendo más caótica la órbita y el cambio de color.

Con la tecla "r", se reduce la cantidad de esferas, siendo el mínimo permitido una.

Para dar una sensación de paso del tiempo, el fondo se vuelve gradualmente más oscuro. Si este efecto no es del agrado del espectador, se puede desactivar presionando la tecla "n".

Finalmente, al hacer clic con el botón izquierdo del mouse, las órbitas cambian de dirección.
### ¿Cómo piensas aplicar el marco MOTION 101 y por qué?


### ¿Qué algoritmo de aceleración vas a utilizar? ¿Por qué?


### El contenido generado debe ser interactivo. Puedes utilizar mouse, teclado, cámara, micrófono, etc, para variar los parámetros del algoritmo en tiempo real.


### El código de la aplicación.

``` js
let orbiters = [];
let orbitDirection = 1;
let noiseOffset = 0;
let drawNoise = true;
let raining = false;
let stars = [];

function setup() {
  createCanvas(800, 600);
  for (let i = 0; i < 10; i++) {
    orbiters.push(new Orbiter());
  }
  background(255);
}

function draw() {
  if (drawNoise && random(1) < 0.01) {
    let r = noise(noiseOffset) * 255;
    let g = noise(noiseOffset + 100) * 255;
    let b = noise(noiseOffset + 200) * 255;
    background(r, g, b, 30);
    noiseOffset += 0.01;
  }

  // Orbiters
  for (let i = orbiters.length - 1; i >= 0; i--) {
    orbiters[i].update();
    orbiters[i].display();

    for (let j = i - 1; j >= 0; j--) {
      let d = dist(
        orbiters[i].pos.x,
        orbiters[i].pos.y,
        orbiters[j].pos.x,
        orbiters[j].pos.y
      );
      if (d < 20) {
        let mixColor = lerpColor(orbiters[i].col, orbiters[j].col, 0.5);
        background(mixColor);
        orbiters.splice(i, 1);
        orbiters.splice(j, 1);
        orbiters.push(new Orbiter());
        orbiters.push(new Orbiter());
        break;
      }
    }
  }

  // Lluvia de estrellas
  if (raining && frameCount % 10 === 0) {
    stars.push(new FallingStar());
  }

  for (let i = stars.length - 1; i >= 0; i--) {
    stars[i].update();
    stars[i].display();

    if (stars[i].shouldRemove) {
      stars.splice(i, 1);
    }
  }
}

function mousePressed() {
  if (mouseButton === LEFT) {
    orbitDirection *= -1;
  }
}

function keyPressed() {
  if (key === 'm') {
    orbiters.push(new Orbiter());
  }
  if (key === 'p') {
    raining = !raining;
  }
  if (key === 'n') {
    drawNoise = !drawNoise;
  }
  if (key === 'r') {
    // Elimina una órbita solo si hay más de una
    if (orbiters.length > 1) {
      orbiters.pop();
    }
  }
}

class Orbiter {
  constructor() {
    this.angle = random(TWO_PI);
    this.radius = random(50, 150);
    this.speed = random(0.01, 0.03);
    this.col = color(random(255), random(255), random(255));
    this.pos = createVector(0, 0);
  }

  update() {
    this.angle += this.speed * orbitDirection;

    let orbitX = mouseX + cos(this.angle) * this.radius;
    let orbitY = mouseY + sin(this.angle) * this.radius;

    this.pos.set(orbitX, orbitY);
  }

  display() {
    noStroke();
    fill(this.col);
    circle(this.pos.x, this.pos.y, 15);
  }
}

class FallingStar {
  constructor() {
    this.pos = createVector(random(width), 0);
    this.speed = random(2, 5);
    this.frozen = false;
    this.freezeChance = random(); // Probabilidad al inicio
    this.shouldRemove = false;
    this.color = color(random(200, 255), random(200, 255), random(100, 255));
  }

  update() {
    if (this.frozen) return;

    if (random(1) < this.freezeChance * 0.01) {
      this.frozen = true;
      return;
    }

    this.pos.y += this.speed;

    if (this.pos.y > height) {
      this.shouldRemove = true;
    }
  }

  display() {
    fill(this.color);
    noStroke();
    push();
    translate(this.pos.x, this.pos.y);
    triangle(0, -5, -5, 5, 5, 5);
    pop();
  }
}
```

### Un enlace al proyecto en el editor de p5.js.
[Mi obra orbital](https://editor.p5js.org/estebanpuerta2006/sketches/BniqhMnUc)

### Una captura de pantalla representativa de tu pieza de arte generativo.
<img width="922" height="672" alt="image" src="https://github.com/user-attachments/assets/70693cc4-7182-4fd2-8a4c-b1808b24f271" />
<img width="918" height="672" alt="image" src="https://github.com/user-attachments/assets/d87bf524-53dc-4354-8526-ecdab4ad510a" />






