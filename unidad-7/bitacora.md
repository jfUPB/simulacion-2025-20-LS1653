# Evidencias de la unidad 7

## Actividad 1
### Punto a
Ejemplo 1: Exit

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/2da29fe0-d29d-475b-a16e-88dbb847d2e2" />


Con el movimiento de la X y la forma de puerta de la I, logran traer a la mente la tipica señal de salida que aparece en todas partes.

<img width="267" height="189" alt="image" src="https://github.com/user-attachments/assets/e0787681-4507-4322-a589-a354694920ff" />

Y por esta misma razón lograr tener una conexión imagen palabra, ya que nos hace recordar un elemnto que vemos de forma un poco incosiente casi todos los días.

Ejemplo 2: Tunel

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/8a29b093-bacb-41b6-8003-ddb55e52e172" />


Con la forma de la n y el como las otras a su lado van en escala de forma de que entre más serca de la n es más pequeña la letra lo cual me hace pensar que las letras estan entrando por el "tunel" y por esa misma razón considero que lo que se ve refuerza lo que dice la palabra.

Ejemplo 3: Mirror

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/771d27dc-03ff-4b40-9e80-5c7e92fa16d0" />

Literalmente cumple la función del espejo, mostrando de forma invertida la palabra que se refleja sobre el "espejo" en este caso la O, basicamente actua como el reflejo que veriamos en ciertos angulos con el un espejo cualquiera, lo que refuerza la sensación que genera la palabra sobre el objeto que representa.

Ejemplo 4: Smile 

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/7657e658-1a12-42bb-a03b-75ef0022141e" />

Esta es un poco simple de explicar, ya que se juega con el tamaño del palo de la "i" y tambien con su punto dando la sensación de un ojo abierto y otro guiñando, por otro lado se curba la "l" en busca de dar la sensación de una sonrisa lo cual al final logra. Por esa razón da el sentido de lo que dice la palabra con lo que muestra el diseño implisito en la misma.

### Punto b
Idea 1: Puente

Esta palabra se puede usar de forma que si se escribe en mayusculas hacer que la "P" y la ultima "E" mantengan su tamaño mientras que las demás letras se hacen más pequeñas y se van subiendo un poco dando la forma de un arco, para dar la sensación de un puente, como en la siguiente imagen:

<img width="225" height="225" alt="image" src="https://github.com/user-attachments/assets/0534bb25-6494-473d-8fbe-c07670ca38ac" />

Idea 2: mouse

Con esta palbra abria que diseñar mucho, pero la idea seria hacer que la "o" de un moemnto a otro le aparescan tres puntos dentro de ella haciendo referencia a los ojos y naris del ratón, al ladode dicha naris 3 palitos lado a lado representando los bigotes y despues que le aparesacan dos oregitas y una cola a la misma "o".

Ejemplo visual:

<img width="827" height="287" alt="image" src="https://github.com/user-attachments/assets/adaa8567-0964-4e76-b9b4-8c811057bb0e" />

## Actividad 2:

### Experimentos:

Experimento 1: (con el video de Patt Vira)
``` js
const {Engine, Body, Bodies, Composite, Render, Runner} = Matter;

let engine;
let boxes = []; let circle; let polygon;
let ground;

function setup() {
  createCanvas(400, 400);
  engine = Engine.create() ;
 
    
    
  //box = new Rect(100,100 ,50 ,50);
  ground = new Ground(200,300 ,400 ,10);
  
  
  //ground = Bodies.rectangle(200, 300, 400, 10, {isStatic: true} );
  
  
}

function draw() {
  background(220);
  Engine.update(engine);
  //box.display();
  for(let i = 0; i<boxes.length; i++){
    boxes[i].display();
  }
  ground.display();
  
  
  //push();
  //rectMode(CENTER);
  //let x = box.position.x;
  //let y = box.position.y;
  //let angle = box.angle;
  
  //translate(x, y);
  //rotate(angle);
  //rect(0, 0 , 50, 50);
  //pop();
  
  //let gp1 = ground.bounds.min.x;
  //let gp2 = ground.bounds.min.y;
  //let gp3 = ground.bounds.max.x;
  //let gp4 = ground.bounds.max.y;
  
  //rectMode(CORNERS);
  //rect(gp1,gp2,gp3,gp4);
}

function mousePressed(){
  boxes.push(new Rect(mouseX,mouseY ,20 ,20));
}

class Rect{
  constructor(x, y, w, h){
    this.w = w;
    this.h = h;
    
    this.body = Bodies.rectangle(x, y, this.w, this.h);
    Body.setAngularVelocity(this.body,3);
    Composite.add(engine.world, this.body);
  }
  
  display(){
    push();
  rectMode(CENTER);
  let x = this.body.position.x;
  let y = this.body.position.y;
  let angle = this.body.angle;
  
  translate(x, y);
  rotate(angle);
  rect(0, 0 , this.w, this.h);
  pop();
  }
}


class Ground{
   constructor(x, y, w, h){
     this.w = w;
    this.h = h;
     
     this.ground = Bodies.rectangle(x, y, this.w, this.h, {isStatic: true} );
     Composite.add(engine.world, this.ground);  
   }
  
  display(){
    push();
  rectMode(CENTER);
  let x = this.ground.position.x;
  let y = this.ground.position.y;
  
  
  translate(x, y);
  
  rect(0, 0 , this.w, this.h);
  pop();
  }
}
```

Experimento 2: (colisiones y lanzamiento)
``` js
// Alias de Matter.js
const { Engine, Bodies, Body, Composite, Constraint } = Matter;

let engine;
let base;
let plank;
let pivot;
let smallBox;
let heavyBoxes = [];
let walls = [];

function setup() {
  createCanvas(600, 400);
  engine = Engine.create();

  //  Base triangular
  base = Bodies.polygon(300, 300, 3, 50, { isStatic: true });

  //  Tabla (catapulta)
  plank = Bodies.rectangle(300, 260, 180, 20, {
    restitution: 0.2,
    density: 0.002
  });

  // 🔗 Pivote central
  pivot = Constraint.create({
    pointA: { x: 300, y: 260 },
    bodyB: plank,
    pointB: { x: 0, y: 0 },
    stiffness: 1
  });

  //  Primer cuadrado liviano
  smallBox = Bodies.rectangle(370, 220, 30, 30, {
    restitution: 0.6,
    density: 0.001
  });

  //  Agregamos todo al mundo
  Composite.add(engine.world, [base, plank, smallBox, pivot]);

  //  Bordes del canvas (muros sólidos)
  let thickness = 40;
  let options = { isStatic: true };

  let floor = Bodies.rectangle(width / 2, height + thickness / 2, width, thickness, options);
  let ceiling = Bodies.rectangle(width / 2, -thickness / 2, width, thickness, options);
  let leftWall = Bodies.rectangle(-thickness / 2, height / 2, thickness, height, options);
  let rightWall = Bodies.rectangle(width + thickness / 2, height / 2, thickness, height, options);

  walls = [floor, ceiling, leftWall, rightWall];
  Composite.add(engine.world, walls);
}

function draw() {
  background(230);
  Engine.update(engine);

  // Dibujar todo
  drawBody(base);
  drawBody(plank);
  drawBody(smallBox);
  for (let box of heavyBoxes) drawBody(box);
  for (let wall of walls) drawBody(wall);

  fill(0);
  textAlign(CENTER);
  text("Haz clic para reiniciar la catapulta", width / 2, 30);
}

function mousePressed() {
  //  Reiniciar la catapulta
  // Reposicionamos el plank al centro
  Body.setPosition(plank, { x: 300, y: 260 });
  Body.setAngle(plank, 0);
  Body.setAngularVelocity(plank, 0);
  Body.setVelocity(plank, { x: 0, y: 0 });

  //  Nuevo cuadrado liviano (el proyectil)
  smallBox = Bodies.rectangle(370, 220, 30, 30, {
    restitution: 0.6,
    density: 0.001
  });
  Composite.add(engine.world, smallBox);

  //  Nuevo cuadrado pesado que cae en el otro extremo
  let heavyBox = Bodies.rectangle(230, 150, 40, 40, {
    restitution: 0.2,
    density: 0.01
  });
  heavyBoxes.push(heavyBox);
  Composite.add(engine.world, heavyBox);
}

//  Dibuja cualquier cuerpo de Matter.js
function drawBody(body) {
  const vertices = body.vertices;
  beginShape();
  for (let i = 0; i < vertices.length; i++) {
    vertex(vertices[i].x, vertices[i].y);
  }
  endShape(CLOSE);
}
```

Experimento 3: (Fusión y división de cuerpos)

``` js
// --- Configuración de Matter.js ---
const { Engine, World, Bodies, Body, Events } = Matter;

let engine, world;
let squares = [];
let walls = [];

// --- Clase Square ---
class Square {
  constructor(x, y, size, fusionCount = 0) {
    this.size = size;
    this.fusionCount = fusionCount;
    this.lastCollision = millis();
    this.isRed = false;
    this.redSince = null;

    // Color inicial: más fusiones => más azul
    const blueValue = map(this.fusionCount, 0, 10, 200, 255, true);
    const whiteValue = map(this.fusionCount, 0, 10, 255, 100, true);
    this.color = color(whiteValue - 30, whiteValue - 30, blueValue);

    this.body = Bodies.rectangle(x, y, size, size, {
      restitution: 0.4,
      friction: 0.3,
      label: "square"
    });

    World.add(world, this.body);
  }

  show() {
    const pos = this.body.position;
    const angle = this.body.angle;
    push();
    translate(pos.x, pos.y);
    rotate(angle);
    rectMode(CENTER);
    fill(this.color);
    stroke(255);
    rect(0, 0, this.size, this.size);
    pop();
  }

  update() {
    // Si pasaron más de 3 s sin colisiones => se parte
    if (millis() - this.lastCollision > 3000 && this.size > 15) {
      this.split();
    }

    // Si el cuadrado está rojo y han pasado 3 s desde que se volvió rojo => explota
    if (this.isRed && this.redSince && millis() - this.redSince > 3000) {
      explodeSquare(this);
    }
  }

  split() {
    const pos = this.body.position;
    World.remove(world, this.body);
    squares = squares.filter(s => s !== this);

    const newSize = this.size / 1.4;
    const s1 = new Square(pos.x - newSize / 2, pos.y, newSize);
    const s2 = new Square(pos.x + newSize / 2, pos.y, newSize);
    squares.push(s1, s2);
  }

  markCollision() {
    this.lastCollision = millis();
  }
}

// --- Función de fusión ---
function mergeSquares(s1, s2) {
  const p1 = s1.body.position;
  const p2 = s2.body.position;

  // Nuevo tamaño (crece moderadamente)
  const newSize = sqrt(sq(s1.size) + sq(s2.size)) * 0.9;
  const newX = (p1.x + p2.x) / 2;
  const newY = (p1.y + p2.y) / 2;

  // Eliminar los viejos
  World.remove(world, [s1.body, s2.body]);
  squares = squares.filter(s => s !== s1 && s !== s2);

  // Nueva cantidad de fusiones acumuladas
  const newFusionCount = s1.fusionCount + s2.fusionCount + 1;

  // Crear nuevo cuadrado fusionado
  const merged = new Square(newX, newY, newSize, newFusionCount);

  // --- Lógica de color ---
  const blueValue = map(newFusionCount, 0, 10, 200, 255, true);

  if (blueValue >= 255) {
    merged.color = color(255, 0, 0);
    merged.isRed = true;
    merged.redSince = millis(); // inicia el temporizador de explosión
  } else {
    const whiteValue = map(newFusionCount, 0, 10, 255, 100, true);
    merged.color = color(whiteValue - 30, whiteValue - 30, blueValue);
  }

  squares.push(merged);
}

// --- Explosión ---
function explodeSquare(sq) {
  const pos = sq.body.position;
  World.remove(world, sq.body);
  squares = squares.filter(s => s !== sq);

  // --- Muchísimos fragmentos ---
  const numFragments = int(random(20, 40)); // entre 20 y 40 pedazos

  for (let i = 0; i < numFragments; i++) {
    const size = random(5, 15); // fragmentos pequeños
    const s = new Square(pos.x, pos.y, size);
    squares.push(s);

    // --- Impulso aleatorio ---
    const angle = random(TWO_PI);
    const force = random(0.02, 0.08); // más fuerza para dispersarse más
    Body.applyForce(s.body, s.body.position, {
      x: cos(angle) * force,
      y: sin(angle) * force * -1 // un poco más de impulso hacia arriba
    });
  }

  // --- Efecto visual de explosión ---
  push();
  noStroke();
  for (let i = 0; i < 10; i++) {
    fill(255, random(100, 200), 0, random(80, 180));
    ellipse(pos.x, pos.y, sq.size * random(1.5, 3));
  }
  pop();
}

// --- Setup ---
function setup() {
  createCanvas(800, 600);
  engine = Engine.create();
  world = engine.world;

  // Muros del canvas
  const options = { isStatic: true };
  walls = [
    Bodies.rectangle(width / 2, height + 25, width, 50, options),
    Bodies.rectangle(width / 2, -25, width, 50, options),
    Bodies.rectangle(-25, height / 2, 50, height, options),
    Bodies.rectangle(width + 25, height / 2, 50, height, options)
  ];
  World.add(world, walls);

  // Cuadrados iniciales
  for (let i = 0; i < 6; i++) {
    squares.push(new Square(random(200, 600), random(50, 250), random(30, 50)));
  }

  // Detectar colisiones
  Events.on(engine, "collisionStart", event => {
    for (let pair of event.pairs) {
      const a = pair.bodyA;
      const b = pair.bodyB;

      if (a.label === "square" && b.label === "square") {
        const s1 = squares.find(s => s.body === a);
        const s2 = squares.find(s => s.body === b);
        if (s1 && s2) {
          s1.markCollision();
          s2.markCollision();

          // Fusionar si aún existen ambos
          mergeSquares(s1, s2);
        }
      }
    }
  });
}

// --- Draw ---
function draw() {
  background(20);
  Engine.update(engine);

  for (let s of squares) {
    s.update();
    s.show();
  }

  fill(200);
  noStroke();
  textAlign(CENTER);
  text("Haz clic para crear un cuadrado nuevo", width / 2, 30);
}

// --- Clic: agrega un nuevo cuadrado ---
function mousePressed() {
  const s = new Square(mouseX, mouseY, random(25, 45));
  squares.push(s);
}



// square.js
// Definimos la clase Square. Usamos Matter.* explícitamente para evitar dependencias de scope.
(function () {
  const Bodies = Matter.Bodies;
  const World = Matter.World;

  class Square {
    constructor(x, y, size, col) {
      this.size = size;
      this.color = col || color(255); // usa p5 color()
      this.lastCollision = millis();
      this.fusionCount = 0;
      this.merged = false;
      this.isRed = false;
      this.baseRedSize = null;
      this.isRed = false;
      this.redSince = null; // tiempo en que se volvió rojo

      // Cuerpo de Matter
      this.body = Bodies.rectangle(x, y, this.size, this.size, {
        restitution: 0.6,
        friction: 0.3,
        label: "square"
      });

      // Añadir al mundo (world debe existir en el momento de instanciar)
      World.add(window.world || Matter.world || /*fallback*/ Matter.Composite.create(), this.body);
      // Nota: en tu sketch, 'world' será definido como window.world = engine.world; (ver sketch.js)
    }

    show() {
      fill(this.color);
      stroke(255);
      strokeWeight(1);
      let pos = this.body.position;
      let angle = this.body.angle;

      push();
      translate(pos.x, pos.y);
      rotate(angle);
      rectMode(CENTER);
      rect(0, 0, this.size, this.size);
      pop();
    }

    update() {
      // placeholder para futuros comportamientos
      // Si el cuadrado es rojo y han pasado 3 s desde que cambió de color => explota
if (this.isRed && this.redSince && millis() - this.redSince > 3000) {
  explodeSquare(this);
}
    }

    touch() {
      this.lastCollision = millis();
    }

    checkSplit() {
      if (millis() - this.lastCollision > 3000 && this.size > 20) {
        // divide en dos cuadrados más pequeños
        let newSize = this.size / 1.4;
        let pos = this.body.position;

        // eliminar actual
        Matter.World.remove(window.world, this.body);

        // buscar y quitar de array 'squares' (sketch.js se encargará de esto si corresponde)
        // Para evitar acoplamiento fuerte, el sketch.js hará la limpieza después de detectar el split.
        // Pero aquí podemos crear dos nuevos cuerpos y devolverlos como sugerencia.
        let a = new Square(pos.x - newSize / 2, pos.y, newSize);
        let b = new Square(pos.x + newSize / 2, pos.y, newSize);
        // Marcamos el actual para que el sketch lo reemplace (o el sketch puede filtrar por size/estado)
        this._toRemove = true; // bandera que el sketch puede leer
        // Añadimos los nuevos al arreglo global en sketch.js (si se desea)
        if (window.squares && Array.isArray(window.squares)) {
          window.squares.push(a, b);
        }
      }
    }
  }

  // Exponer Square al scope global para que sketch.js pueda instanciarla
  window.Square = Square;
})();
```

### Capturas:

Experimento 1: (con el video de Patt Vira)

<img width="473" height="306" alt="image" src="https://github.com/user-attachments/assets/8439aa9b-12d8-479a-a933-afb277ccae71" />

Experimento 2: (colisiones y lanzamiento)

<img width="748" height="492" alt="image" src="https://github.com/user-attachments/assets/20f3d609-1dc8-4e9d-8654-1186a2f82f61" />

Experimento 3: (Fusión y división de cuerpos)

<img width="832" height="556" alt="image" src="https://github.com/user-attachments/assets/df9eb7b6-0234-4de1-b37a-5f51e24f7c7b" />


<img width="838" height="245" alt="image" src="https://github.com/user-attachments/assets/6e82f694-1bcb-4c21-9e8d-067fc8e8d320" />

<img width="826" height="272" alt="image" src="https://github.com/user-attachments/assets/89a0d96b-415e-4ba1-af96-fc36b240043e" />

### Explicación:
Capturas para mi repaso rapido:

<img width="1080" height="550" alt="image" src="https://github.com/user-attachments/assets/d710e4b5-ff1d-4333-8f46-f69a77a8254d" />

<img width="1080" height="550" alt="image" src="https://github.com/user-attachments/assets/c81e5fc0-0388-489b-80ed-ead37df861dc" />

Engine: Diria que es la parte más esencial de matter ya que su trabajo es calcular la fisica, posiciones, velocidades, colisiones, gravedad, etc.
Se puede resumir en que este decide el como se mueven y reaccionan los cuerpos.

World: Es literalmente el mundo en el que se encuentran los objetos que creamos.

Bodies: Son objetos que tienen forma, masa y comportamiento, estos mismos pueden tomar cualquier forma y se les puede dar caracteristicas, como color y propiedades, como que rebote mas o se quede inmovil en el mundo.

Constraint: Es algo que conecta dos cuerpos la cual limita o convina el movimiento de dischos cuerpos.

MouseConstraint: Este permite la interacción de los objetos con el mouse.

### Dificultades: 




