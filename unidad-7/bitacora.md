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

### Capturas:

Experimento 1: (con el video de Patt Vira)

<img width="473" height="306" alt="image" src="https://github.com/user-attachments/assets/8439aa9b-12d8-479a-a933-afb277ccae71" />

Experimento 2: (colisiones y lanzamiento)

<img width="748" height="492" alt="image" src="https://github.com/user-attachments/assets/20f3d609-1dc8-4e9d-8654-1186a2f82f61" />


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



