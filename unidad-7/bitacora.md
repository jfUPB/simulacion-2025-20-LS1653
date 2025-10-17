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
Mis mayores usando Matter, fue el aprenderme los llamados de los objetos y el utilizar fisicas ya integradas de forma creativa, pues en parte el chiste de las otras unidades al crear fisicas o intentar imitar la realidad hacia que pues salieran cosas locas y divertidas, pero ahora tengo que buscar formas de hacer algo demaciado realista de forma divertida de ver.

## Actividad 3

###  Palabra elegida: 
Revolución

### ¿Cómo la animación física representa el significado de la palabra?
Lo que quiero hacer es que cada una de las letras en la palabra revolución sean ejecutadas con metodos antirevolucionarios, esto es en parte no tanto para representar la palabra sino para mostrar la consecuencia que puede traer esta misma.

#### ¿Cómo representarás la palabra? ¿Usarás cuerpos de Matter.js para formar las letras?
Etapa de ideación:
Si usare cuerpos para formar la palabra, ya que cada letra debe ser de alguna manera afectada.

Final del proceso:
Lorem

#### ¿Qué comportamiento físico (caída, flotación, colisión, elasticidad, ruptura, conexión) representará el significado?
Etapa de ideación:
Considero que tendra, caida, colisión, elasticidad, ruptura y conexión para tener una amplia varidad de ejecucuiones.

Final del proceso:
Lorem

#### ¿Cómo configurarás el mundo de Matter.js (gravedad, límites) y las propiedades de los cuerpos (masa, fricción, restitución/elasticidad) para lograr ese comportamiento?
Etapa de ideación:
El mundo tendra gravedad normal y los limites seran los propios bordes del canva. Los cuerpos tendran masa y talvez un poco de elasticidad.

Final del proceso:
Lorem


#### ¿Habrá alguna interacción del usuario (ej: click para iniciar la acción, mouse para perturbar)?
Etapa de ideación:
Pienzo que lo mejor es hacer que el usuario desida cual es la letra a la que le ocurrira la desgracia.

Final del proceso:
Lorem

###  ¿Cómo formaste las letras con Matter.js? ¿Qué propiedades físicas fueron importantes? ¿Usaste restricciones?

### Código

``` html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <title>REVOLUCIÓN - Animación Matter + p5</title>

  <!-- Librerías base -->
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.10/lib/p5.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.10/lib/addons/p5.sound.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/matter-js@0.19.0/build/matter.min.js"></script>

  <!-- Animaciones individuales -->
  <script src="animacionR.js"></script>
  <script src="animacionE.js"></script>
  <script src="animacionV.js"></script>
  <script src="animacionO.js"></script>
  <script src="animacionL.js"></script>
  <script src="animacionU.js"></script>
  <!-- (puedes agregar más animaciones aquí después) -->

  <!-- Sketch principal -->
  <script src="sketch.js"></script>

  <!-- Estilos -->
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <main></main>
</body>
</html>
```

``` js
// --- Configuración de Matter.js ---
const { Engine, World, Bodies, Constraint, Body } = Matter;
let clickedUOnce = false;
let engine, world;
let letters = [];
let curtainLeft, curtainRight;
let curtainClosing = false;
let curtainOpening = false;
let selectedLetter = null;
let showSingleLetter = false;
let isAnimating = false; // true entre primer cierre y cuando programamos la segunda cerrada
let restoring = false;   // true entre segundo cierre y la recreación de letras

// Duraciones (ms)
const T_WAIT_BEFORE_OPEN = 2000;   // espera tras primer cierre antes de abrir y mostrar letra
const T_ANIMATION = 5000;          // tiempo aproximado que dura la animación de la letra
const T_BEFORE_REOPEN = 200;       // pequeña pausa entre reset y reapertura

function setup() {
  createCanvas(900, 400);
  engine = Engine.create();
  world = engine.world;

  // suelo (estático)
  const ground = Bodies.rectangle(width / 2, height - 10, width, 20, { isStatic: true });
  World.add(world, ground);

  // preparamos cortina cerrada en inicio (mostramos apertura inicial)
  curtainLeft  = { x: 0 };         // cerrado: izquierda en 0
  curtainRight = { x: width / 2 }; // cerrado: derecha en width/2
  curtainOpening = true;           // abrimos al inicio (presentación)

  // crear letras por primera vez
  createLetters();
}

function createLetters() {
  // eliminar cuerpos previos si hubiera (seguro cuando reset)
  if (letters.length) {
    for (let b of letters) {
      try { World.remove(world, b); } catch (e) {}
    }
    letters = [];
  }

  const word = "REVOLUCIÓN";
  const startX = 120;
  const colors = [
    color(0, 0, 255), // R azul
    color(0, 0, 255), // E azul
    color(0, 0, 255), // V azul
    color(0, 0, 255), // O (mitad)
    color(255),       // L blanco
    color(255),       // U blanco
    color(255, 0, 0), // C (mitad)
    color(255, 0, 0), // I roja
    color(255, 0, 0), // Ó roja
    color(255, 0, 0)  // N roja
  ];

  let x = startX;
  for (let i = 0; i < word.length; i++) {
    const b = Bodies.rectangle(x, height / 2, 60, 60, {
      restitution: 0.4,
      friction: 0.3,
      label: word[i]
    });
    b.letter = word[i];
    b.displayColor = colors[i];
    World.add(world, b);
    letters.push(b);
    x += 75;
  }
}

function draw() {
  background(220);
  Engine.update(engine);

  // Dibujar letras (si showSingleLetter true => solo selectedLetter)
  for (let b of letters) {
    if (!showSingleLetter || b === selectedLetter) {
      const pos = b.position;
      const angle = b.angle;
      push();
      translate(pos.x, pos.y);
      rotate(angle);
      rectMode(CENTER);

      // O y C tienen mitades de color
      if (b.letter === "O") {
        noStroke();
        fill(0, 0, 255);
        rect(-15, 0, 30, 60);
        fill(255);
        rect(15, 0, 30, 60);
      } else if (b.letter === "C") {
        noStroke();
        fill(255);
        rect(-15, 0, 30, 60);
        fill(255, 0, 0);
        rect(15, 0, 30, 60);
      } else {
        fill(b.displayColor);
        stroke(0);
        rect(0, 0, 60, 60);
      }

      // Letra encima
      fill(0);
      noStroke();
      textAlign(CENTER, CENTER);
      textSize(28);
      text(b.letter, 0, 0);
      pop();
    }
  }

  // --- 🔪 actualización y dibujo de animaciones ---
  updateAnimacionE();
  drawAnimacionE();
  updateAnimacionV();
  drawAnimacionV();
  updateAnimacionO();
  drawAnimacionO();
  updateAnimacionL();
  drawAnimacionL();
  // ------------------------------------------------

  // Dibujar cortina (dos paneles)
  fill(0);
  rect(curtainLeft.x, 0, width / 2, height);
  rect(curtainRight.x, 0, width / 2, height);

  // Animar cortina: apertura / cierre
  if (curtainClosing) {
    curtainLeft.x = lerp(curtainLeft.x, 0, 0.2);
    curtainRight.x = lerp(curtainRight.x, width / 2, 0.2);

    if (abs(curtainLeft.x) < 1 && abs(curtainRight.x - width/2) < 1) {
      curtainClosing = false;
      onCurtainClosed();
    }
  }

  if (curtainOpening) {
    curtainLeft.x = lerp(curtainLeft.x, -width / 2, 0.12);
    curtainRight.x = lerp(curtainRight.x, width, 0.12);

    if (curtainLeft.x < -width/2 + 1 && curtainRight.x > width - 1) {
      curtainOpening = false;
    }
  }
  
  // --- Dibujar cuerda y anclaje de la R si existen ---
  if (cuerdaR && letraR) {
    stroke(200, 200, 255);
    strokeWeight(4);
    line(cuerdaR.pointA.x, cuerdaR.pointA.y, letraR.position.x, letraR.position.y);

    noStroke();
    fill(255, 0, 0);
    ellipse(cuerdaR.pointA.x, cuerdaR.pointA.y, 10);
  }
}

// --- mouse ---
function mousePressed() {
  // bloquea selección si estamos en animación o cortina moviéndose o restaurando
  if (curtainClosing || curtainOpening || isAnimating || restoring) return;

  let clickedU = false;

  for (let b of letters) {
    const pos = b.position;
    if (dist(mouseX, mouseY, pos.x, pos.y) < 40) {

      // Caso especial: letra U
      if (b.letter === "U") {
        console.log("La U ha sido seleccionada, desaparece sin animación.");
        try { World.remove(world, b); } catch (e) {}
        letters = letters.filter(l => l !== b); // quitarla del array
        clickedU = true;
        clickedUOnce = true; // ✅ marcamos que fue la U
        break;
      }

      // Para todas las demás letras, sigue el proceso normal
      selectedLetter = b;
      isAnimating = true;
      closeCurtain();
      break;
    }
  }

  // Si fue la U, cerramos y reabrimos sin resetear
  if (clickedU) {
    closeCurtain();
    setTimeout(openCurtain, 1500);
  }
}

function closeCurtain() {
  curtainClosing = true;
  curtainOpening = false;
}

// central: cuando la cortina termina de cerrarse
function onCurtainClosed() {
  //  Si se hizo clic en la U, solo reabrimos el telón sin resetear
  if (clickedUOnce) {
    clickedUOnce = false; // limpiamos la bandera
    setTimeout(openCurtain, 300);
    return;
  }
  // Si isAnimating true y showSingleLetter aún false => primer cierre tras selección
  if (isAnimating && !showSingleLetter) {
    showSingleLetter = true;

    // Esperamos antes de abrir (para simular el cierre completo)
    setTimeout(() => {
      openCurtain();

      // Lanzamos la animación de la letra un poco después de que empiece a abrir
      setTimeout(() => {
        triggerLetterAnimation(selectedLetter);
      }, 500);

      // Programamos el cierre final tras terminar la animación
      setTimeout(() => {
        restoring = true;
        isAnimating = false;
        closeCurtain();
      }, T_ANIMATION);

    }, T_WAIT_BEFORE_OPEN);

    return;
  }

  // Si restoring true => esta es la segunda vez que la cortina se cierra (post-animación)
  if (restoring) {
  resetLetters();
  restoring = false;
  setTimeout(() => {
    showSingleLetter = false;
    selectedLetter = null;
    openCurtain();

    // 💥 Explosión después de 1.5 segundos de abrir el telón
    setTimeout(() => explodeLastLetters(), 1500);
  }, T_BEFORE_REOPEN);
  return;
}

  // Comportamiento por defecto
  openCurtain();
}

function openCurtain() {
  curtainOpening = true;
  curtainClosing = false;
}

function resetLetters() {
  // eliminar cuerpos anteriores
  for (let b of letters) {
    try { World.remove(world, b); } catch (e) {}
  }
  letters = [];
  // recrear letras
  createLetters();
}

// --- Dispatcher de animaciones (placeholder) ---
function triggerLetterAnimation(body) {
  if (!body) return;
  switch (body.letter) {
    case "R": animateR(body); break;
    case "E": animateE(body); break;
    case "V": animateV(body); break;
    case "O": animateO(body); break;
    case "L": animateL(body); break;
    case "U": animateU(body); break;
    
    default: break;
  }
  
  if (selectedLetter === 'E') {
    animateE(body);
  }
}

// 💥 --- Explosión de las últimas letras ---
function explodeLastLetters() {
  console.log("💥 Las últimas cuatro letras explotan!");

  const count = 4;
  const total = letters.length;

  if (total < count) return; // si hay menos de 4 letras, salir

  const lastFour = letters.slice(-count);

  for (let b of lastFour) {
    // Aplicar fuerza aleatoria
    const force = Matter.Vector.create(
      (Math.random() - 0.5) * 0.2,
      (Math.random() - 0.5) * -0.3
    );
    Matter.Body.applyForce(b, b.position, force);

    // Hacer que desaparezcan luego de 1 segundo
    setTimeout(() => {
      try { World.remove(world, b); } catch (e) {}
      letters = letters.filter(l => l !== b);
    }, 1000);
  }
}

function restartSketch() {
  try { limpiarAnimacionR(); } catch (e) {}
  try { limpiarAnimacionV(); } catch (e) {}
  try { limpiarAnimacionE(); } catch (e) {}
  try { limpiarAnimacionO(); } catch (e) {}
  try { limpiarAnimacionL(); } catch (e) {}

  World.clear(world, false);
  Engine.clear(engine);

  letters = [];
  selectedLetter = null;
  showSingleLetter = false;
  isAnimating = false;
  restoring = false;
  curtainClosing = false;
  curtainOpening = true;
  curtainLeft = { x: 0 };
  curtainRight = { x: width / 2 };

  createLetters();
  Engine.run(engine);
}




// --- animacionE.js ---
// Cuchillo cae y apuñala la letra E, sin rotaciones ni cambio de fondo.

let cuchillo = null;
let cuchilloGolpeo = false;
let bodyE = null;

function animateE(body) {
  if (!body) return;
  limpiarAnimacionE();
  bodyE = body;

  // Crear el cuchillo justo arriba de la letra E
  const startX = body.position.x;
  const startY = body.position.y - 250;

  cuchillo = Matter.Bodies.rectangle(startX, startY, 20, 80, {
    restitution: 0.1,
    frictionAir: 0.002,
    label: "cuchillo",
  });

  Matter.World.add(world, cuchillo);

  // Aplicar una fuerza inicial hacia abajo
  Matter.Body.applyForce(cuchillo, cuchillo.position, { x: 0, y: 0.03 });
}

function updateAnimacionE() {
  if (!cuchillo || !bodyE || cuchilloGolpeo) return;

  // Detección simple de impacto
  const dx = cuchillo.position.x - bodyE.position.x;
  const dy = cuchillo.position.y - bodyE.position.y;
  const dist = Math.sqrt(dx * dx + dy * dy);

  // Si está lo suficientemente cerca, detener ambos
  if (dist < 60) {
    cuchilloGolpeo = true;
    Matter.Body.setStatic(cuchillo, true);
    Matter.Body.setStatic(bodyE, true);

    // Simula impacto hundiendo la E un poco
    Matter.Body.translate(bodyE, { x: 0, y: 10 });

    // Desaparece después de un momento
    setTimeout(() => {
      limpiarAnimacionE();
      if (typeof closeCurtain === "function") closeCurtain();
    }, 1000);
  }
}

function drawAnimacionE() {
  if (!cuchillo) return;
  push();
  fill(200);
  rectMode(CENTER);
  rect(cuchillo.position.x, cuchillo.position.y, 20, 80);
  pop();
}

function limpiarAnimacionE() {
  if (cuchillo) {
    try {
      Matter.World.remove(world, cuchillo);
    } catch (e) {}
    cuchillo = null;
  }
  bodyE = null;
  cuchilloGolpeo = false;
}




// === ANIMACIÓN L ===
let letraL = null;
let plataformaL = null;
let cuerdaL = null;
let animandoL = false;
let tiempoInicioL = 0;

function animateL(body) {
  if (animandoL) return; // evitar reinicio
  animandoL = true;
  letraL = body;
  tiempoInicioL = millis();

  // ⚙️ Crear cuerda y plataforma temporal
  const puntoAnclaje = { x: body.position.x, y: body.position.y + 100 };
  plataformaL = Bodies.rectangle(puntoAnclaje.x, puntoAnclaje.y + 20, 100, 10, {
    isStatic: true,
    label: "plataformaL",
    render: { fillStyle: "#999" }
  });
  World.add(world, plataformaL);

  cuerdaL = Constraint.create({
    bodyA: body,
    pointB: puntoAnclaje,
    stiffness: 0.02,
    length: 100
  });
  World.add(world, cuerdaL);

  // Simular ligera tensión inicial
  Body.applyForce(body, body.position, { x: 0, y: -0.005 });

  // ⏳ Después de 2.5 s: eliminar la plataforma y desactivar colisión
  setTimeout(() => {
    try {
      World.remove(world, plataformaL);
      plataformaL = null;
      // quitar colisión → que caiga al vacío
      body.collisionFilter.mask = 0;
      // darle impulso hacia abajo para que caiga rápido
      Body.applyForce(body, body.position, { x: 0, y: 0.05 });
    } catch (e) {}
  }, 2500);

  // ⏳ Después de 4 s: eliminar cuerda
  setTimeout(() => {
    try {
      World.remove(world, cuerdaL);
      cuerdaL = null;
    } catch (e) {}
  }, 4000);
}

function updateAnimacionL() {
  // nada físico continuo aquí por ahora
}

function drawAnimacionL() {
  if (!animandoL || !letraL) return;

  // dibujar cuerda
  if (cuerdaL) {
    stroke(180);
    strokeWeight(3);
    line(
      cuerdaL.pointB.x,
      cuerdaL.pointB.y,
      letraL.position.x,
      letraL.position.y
    );
  }

  // dibujar plataforma
  if (plataformaL) {
    push();
    fill(150);
    noStroke();
    rectMode(CENTER);
    rect(plataformaL.position.x, plataformaL.position.y, 100, 10);
    pop();
  }

  // si ya cayó muy abajo, limpiamos todo
  if (letraL.position.y > height + 100) {
    limpiarAnimacionL();
  }
}

function limpiarAnimacionL() {
  if (cuerdaL) {
    try { World.remove(world, cuerdaL); } catch (e) {}
    cuerdaL = null;
  }
  if (plataformaL) {
    try { World.remove(world, plataformaL); } catch (e) {}
    plataformaL = null;
  }
  letraL = null;
  animandoL = false;
}




// === animacionO.js ===

// Variables internas para controlar animación de la O
let animO_activa = false;
let animO_body = null;
let animO_rect = null;
let animO_inicioElevacion = 0;
let animO_fase = 0; // 0 = elevando, 1 = empalando, 2 = final
let animO_alturaMax = 80;

function animateO(body) {
  if (!body) return;
  animO_activa = true;
  animO_body = body;
  animO_inicioElevacion = millis();
  animO_fase = 0;

  // quitar gravedad momentáneamente
  Body.setStatic(body, true);
}

// Se llama en draw() desde sketch.js
function updateAnimacionO() {
  if (!animO_activa || !animO_body) return;

  if (animO_fase === 0) {
    // elevar poco a poco
    Body.translate(animO_body, { x: 0, y: -1 });
    if (millis() - animO_inicioElevacion > 1000) {
      animO_fase = 1;
      // crear rectángulo detrás de la O
      animO_rect = {
        x: animO_body.position.x,
        y: animO_body.position.y + 60,
        w: 15,
        h: 140,
        color: color(100)
      };
    }
  } else if (animO_fase === 1) {
    // empalamiento: el rectángulo sube detrás
    if (animO_rect.y > animO_body.position.y) {
      animO_rect.y -= 2;
    } else {
      animO_fase = 2;
      // dejar la O fija empalada
      Body.setStatic(animO_body, true);
    }
  }
}

function drawAnimacionO() {
  if (!animO_activa || !animO_body) return;

  // Dibujar el rectángulo (detrás de la O)
  if (animO_rect) {
    push();
    fill(animO_rect.color);
    noStroke();
    rectMode(CENTER);
    rect(animO_rect.x, animO_rect.y, animO_rect.w, animO_rect.h);
    pop();
  }
}

function limpiarAnimacionO() {
  animO_activa = false;
  animO_body = null;
  animO_rect = null;
  animO_fase = 0;
}




// --- animacionR.js ---
// Esta función se llama desde triggerLetterAnimation(selectedLetter)

let cuerdaR = null;
let anchorR = null;
let letraR = null;

function animateR(body) {
  letraR = body; // guardamos referencia global

  // Punto de anclaje inicial, un poco arriba del cuerpo
  anchorR = { x: body.position.x, y: body.position.y - 200 };

  // Crear la cuerda que lo sujeta
  cuerdaR = Matter.Constraint.create({
    pointA: anchorR,
    bodyB: body,
    length: 200,
    stiffness: 0.02
  });

  Matter.World.add(world, cuerdaR);

  // Variables locales de animación
  let tiempoSubida = 0;
  let subiendo = true;

  // Subida progresiva (la cuerda se acorta poco a poco)
  const intervaloSubida = setInterval(() => {
    if (subiendo) {
      tiempoSubida++;
      // mover el punto de anclaje hacia arriba
      cuerdaR.pointA.y -= 0.8;

      if (tiempoSubida > 200) {
        subiendo = false;
        Matter.Body.applyForce(body, body.position, { x: 0.05, y: -0.02 });
        body.frictionAir = 0.02;
      }
    }
  }, 16);

  // Al terminar la animación: limpiar y después de 1s iniciar cierre del telón
  setTimeout(() => {
    clearInterval(intervaloSubida);

    // Desaparecer la cuerda cuando termine la animación
    limpiarAnimacionR();

    // Espera 1 segundo para "respirar" y luego pedir al sketch que cierre el telón
    setTimeout(() => {
      // closeCurtain() debe existir en el scope global (sketch.js)
      if (typeof closeCurtain === "function") {
        closeCurtain();
      } else {
        console.warn("closeCurtain() no encontrada: asegúrate de que exista en tu sketch principal.");
      }
    }, 1000);

  }, 6000);
}

function limpiarAnimacionR() {
  if (cuerdaR) {
    try { Matter.World.remove(world, cuerdaR); } catch (e) {}
    cuerdaR = null;
  }
  letraR = null;
  anchorR = null;
}



// === ANIMACIÓN U ===
let letraU = null;
let animandoU = false;

function animateU(body) {
  if (animandoU) return;
  animandoU = true;
  letraU = body;

  // 🔮 "Desaparecer" la letra: se quita del mundo y no se dibuja
  try {
    World.remove(world, letraU);
  } catch (e) {}

  // la ocultamos durante toda la animación (T_ANIMATION controlado desde sketch.js)
  setTimeout(() => {
    limpiarAnimacionU();
  }, 4000); // se restaura después del cierre del telón
}

function updateAnimacionU() {
  // nada aquí
}

function drawAnimacionU() {
  // tampoco se dibuja nada, está "desaparecida"
}

function limpiarAnimacionU() {
  letraU = null;
  animandoU = false;
}




// --- animacionV.js ---
// La "V" tiembla y luego se parte en dos mitades que caen.

let vTemblando = false;
let vPartida = false;
let bodyV = null;
let mitadIzq = null;
let mitadDer = null;
let tiempoInicioTemblor = 0;
const DURACION_TEMBLOR = 1000; // 1 segundo

function animateV(body) {
  if (!body) return;
  limpiarAnimacionV();
  bodyV = body;

  // Fase 1: empezar el temblor
  vTemblando = true;
  tiempoInicioTemblor = millis();
}

function updateAnimacionV() {
  // --- Fase 1: Temblor ---
  if (vTemblando && !vPartida && bodyV) {
    const tiempo = millis() - tiempoInicioTemblor;

    // Movimiento oscilante pequeño (temblor)
    const offsetX = sin(frameCount * 20) * 3;
    const offsetY = cos(frameCount * 20) * 2;
    Matter.Body.setPosition(bodyV, {
      x: bodyV.position.x + offsetX * 0.1,
      y: bodyV.position.y + offsetY * 0.1,
    });

    // Si ya pasó el tiempo, partir la letra
    if (tiempo > DURACION_TEMBLOR) {
      partirV();
    }
  }
}

function drawAnimacionV() {
  // 🔒 Evitar dibujar si no hay animación activa o el mundo fue reiniciado
  if (!world || (!vTemblando && !vPartida)) return;

  // Si está temblando y no se ha partido
  if (vTemblando && !vPartida && bodyV) {
    const pos = bodyV.position;
    push();
    fill(0, 0, 255);
    rectMode(CENTER);
    rect(pos.x, pos.y, 60, 60);
    fill(0);
    noStroke();
    textAlign(CENTER, CENTER);
    textSize(28);
    text("V", pos.x, pos.y);
    pop();
  }

  // Si ya se partió, dibujamos las dos mitades
  if (vPartida) {
    if (mitadIzq) {
      const p = mitadIzq.position;
      push();
      fill(0, 0, 255);
      rectMode(CENTER);
      rect(p.x, p.y, 30, 60);
      pop();
    }
    if (mitadDer) {
      const p = mitadDer.position;
      push();
      fill(0, 0, 255);
      rectMode(CENTER);
      rect(p.x, p.y, 30, 60);
      pop();
    }
  }
}

// --- Función auxiliar para partir la letra ---
function partirV() {
  if (!bodyV || vPartida) return;

  vPartida = true;
  vTemblando = false;

  const x = bodyV.position.x;
  const y = bodyV.position.y;

  // Eliminar cuerpo original (desaparece la V original)
  try {
    Matter.World.remove(world, bodyV);
  } catch (e) {}
  bodyV = null;

  // Crear las dos mitades
  mitadIzq = Matter.Bodies.rectangle(x - 15, y, 30, 60, {
    restitution: 0.4,
    friction: 0.3,
  });
  mitadDer = Matter.Bodies.rectangle(x + 15, y, 30, 60, {
    restitution: 0.4,
    friction: 0.3,
  });

  // Pequeñas fuerzas hacia los lados para separarlas
  Matter.Body.applyForce(mitadIzq, mitadIzq.position, { x: -0.02, y: -0.02 });
  Matter.Body.applyForce(mitadDer, mitadDer.position, { x: 0.02, y: -0.02 });

  Matter.World.add(world, [mitadIzq, mitadDer]);
}

// --- Limpieza total ---
function limpiarAnimacionV() {
  if (bodyV) {
    try { Matter.World.remove(world, bodyV); } catch (e) {}
    bodyV = null;
  }
  if (mitadIzq) {
    try { Matter.World.remove(world, mitadIzq); } catch (e) {}
    mitadIzq = null;
  }
  if (mitadDer) {
    try { Matter.World.remove(world, mitadDer); } catch (e) {}
    mitadDer = null;
  }

  //  Reinicia todos los estados
  vTemblando = false;
  vPartida = false;
  tiempoInicioTemblor = 0;
}

// --- Reinicio cuando se cierra el telón ---
function resetAnimacionV(nuevoBody) {
  limpiarAnimacionV();
  bodyV = nuevoBody;
  vTemblando = false;
  vPartida = false;
}
```

### Captura y link
[Proyecto](https://editor.p5js.org/estebanpuerta2006/sketches/Yxk-nI_AC)

## Auto evaluación





