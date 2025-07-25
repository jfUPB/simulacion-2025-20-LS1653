# Unidad 1

## 🛠 Fase: Apply

### Actividad 8 

#### Creación de obra generativa

##### Vas a crear una obra generativa interactiva en tiempo real utilizando los conceptos de aleatoriedad que has aprendido en esta unidad. Tu obra debe:

*Usar al menos tres conceptos estudiados en esta unidad COMBINADOS de manera creativa y coherente.

*Tu obra de ser interactiva y generativa en tiempo real. Puedes usar el mouse, el teclado o cualquier otro sensor de entrada para interactuar con la obra.

#### Un texto donde expliques el concepto de obra generativa.

##### Forma inicial
Mi obra sera diceñada a base de circulos continuos imitando el traso de un lapiz este movimiento lo generare con el ruido Perlin, estos circulos cambiaran de tamaño al ser oprimida la letra "f" el tamaño lo definire con una distribución normal, el tamaño sera variable por un tiempo definido por un número aleatorio generado por la función random(), ahora tambien le pondre la opción de que cambie la figura dibujada, esto lo hare con el click, las formas seran el cuadrado, el circulo original y el triangulo, ya por ultimo hare que aleatoriamente cambien de color algunas figuras, las figuras que cambiaran de color seran definidas por el Lévy fligth y por ultimo con la distribución normal se borraran partes del arte generado en zonas especificas estas zonas se elimiran cada vez que el usuario oprecione la letra "b".

##### Forma final
Se mantuvo la estructura inicial en su mayoria solo que ahora la figura mantiene el tamaño asignado al undir la letra "f" osea no cambia con el tiempo, tambien agregue una segunda linea que se activa con la letra "d" y por ultimo agregado puse que con la letra "g" aparesaca un fondo predefinido que a su vez tiene una pequeña probabilidad de salir por su cuenta.

#### Copia el código en tu bitácora.
```` js
// Esteban

let walker;
let walker2;
let bgShape;
let shapeSize = 100;
let shapeTypes = ["circle", "square", "triangle"];
let currentShape = 0;
let shapeTimer = 0;
let drawSecondLine = false;
let shouldUpdateBackground = false; // ← NUEVO
let r = 4;

function setup() {
  createCanvas(640, 240);
  walker = new Walker("circle");
  walker2 = new Walker("circle");
  bgShape = new BackgroundShape();
  background(255);
  textSize(20);
  textAlign(CENTER, CENTER);
  fill(255);
}

function draw() {
  // Pintar fondo SÓLO si se pidió
  if (shouldUpdateBackground || random(1) < 0.001) { // ← con baja probabilidad
    bgShape.update();
    bgShape.display();
    shouldUpdateBackground = false; // ← se apaga después de pintar
  }

  walker.step();
  walker.show();

  if (drawSecondLine) {
    walker2.step();
    walker2.show();
  }
}

function keyPressed() {
  if (key === 'f') {
    r = int(randomGaussian(6, 3));
  }

  if (key === 'b') {
    let eraseX = int(randomGaussian(width / 2, width / 6));
    let eraseY = int(randomGaussian(height / 2, height / 6));
    noStroke();
    fill(255);
    rectMode(CENTER);
    rect(eraseX, eraseY, 60, 60);
  }

  if (key === 'r') {
    background(255);
    walker = new Walker("circle");
    r = 6;
    drawSecondLine = false;
    bgShape = new BackgroundShape();
  }

  if (key === 'd') {
    drawSecondLine = true;
  }

  if (key === 'g') { // ← NUEVA tecla para actualizar fondo manualmente
    shouldUpdateBackground = true;
  }
}

function mousePressed() {
  walker.toggleShape();
  walker2.toggleShape();
}

// Walker Class (igual que antes)
class Walker {
  constructor(_drawType) {
    this.x = width / 2;
    this.y = height / 2;
    this.tx = random(1000);
    this.ty = random(1000);
    this.drawType = _drawType;
    this.color = color(245);
  }

  show() {
    fill(this.color);
    noStroke();
    if (this.drawType === "circle") {
      circle(this.x, this.y, r);
    } else if (this.drawType === "square") {
      rectMode(CENTER);
      square(this.x, this.y, r);
    } else if (this.drawType === "triangle") {
      triangle(
        this.x, this.y - r / 2,
        this.x - r / 2, this.y + r / 2,
        this.x + r / 2, this.y + r / 2
      );
    }
  }

  toggleShape() {
    if (this.drawType === "circle") {
      this.drawType = "square";
    } else if (this.drawType === "square") {
      this.drawType = "triangle";
    } else {
      this.drawType = "circle";
    }
  }

  step() {
    this.x = map(noise(this.tx), 0, 1, 0, width);
    this.y = map(noise(this.ty), 0, 1, 0, height);
    this.tx += 0.01;
    this.ty += 0.01;

    if (random(1) < 0.01) {
      this.color = color(random(230), random(230), random(230));
    }
  }
}

// BackgroundShape class (sin cambios)
class BackgroundShape {
  constructor() {
    this.size = 100;
    this.shape = shapeTypes[currentShape];
    this.colorOffset = 0;
  }

  update() {
    this.size = 80 + sin(frameCount * 0.05) * 40;
    shapeTimer++;
    if (shapeTimer > 180) {
      currentShape = (currentShape + 1) % shapeTypes.length;
      this.shape = shapeTypes[currentShape];
      shapeTimer = 0;
    }
    this.colorOffset += 0.01;
  }

  display() {
    noStroke();
    for (let y = 0; y < height; y++) {
      let inter = map(y, 0, height, 0, 1);
      let c1 = color(255, 100, 150);
      let c2 = color(100, 150, 255);
      let c = lerpColor(c1, c2, (inter + this.colorOffset) % 1);
      stroke(c);
      line(0, y, width, y);
    }

    fill(255, 240);
    stroke(0, 30);
    strokeWeight(1);
    push();
    translate(width / 2, height / 2);
    if (this.shape === "circle") {
      ellipse(0, 0, this.size);
    } else if (this.shape === "square") {
      rectMode(CENTER);
      rect(0, 0, this.size, this.size);
    } else if (this.shape === "triangle") {
      let h = this.size;
      triangle(
        0, -h / 2,
        -h / 2, h / 2,
        h / 2, h / 2
      );
    }
    pop();
  }
}
````

#### Coloca en enlace a tu sketch en p5.js en tu bitácora
[Mi primer arte :)](https://editor.p5js.org/estebanpuerta2006/sketches/vw-82ntv4)

#### Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora
<img width="798" height="296" alt="image" src="https://github.com/user-attachments/assets/e5ed7bd2-0cce-4114-ae92-23a4909ad744" />
