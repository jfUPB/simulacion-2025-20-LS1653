# Evidencias de la unidad 4

## Explicación conceptual de la obra

* ¿Qué concepto de la unidad 4 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> El concepto fue ondas. Lo apliqué creando una onda circular de círculos que se expande hacia afuera. La onda tiene picos de colores aleatorios y entre ellos se hace una interpolación de color, lo que genera un efecto dinámico y rítmico en la composición.

* ¿Qué concepto de la unidad 3 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> El concepto fue el de n-cuerpos y atracción gravitacional. Implementé varios cuerpos que interactúan entre sí con fuerzas de atracción y además influyen de manera aleatoria sobre los círculos de la onda, generando distorsiones y un movimiento orgánico.

* ¿Qué concepto de la unidad 2 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> El concepto fue Motion 101 e interpolación de colores. Apliqué Motion 101 en el comportamiento de los cuerpos al actualizar sus posiciones y velocidades siguiendo las fuerzas de atracción. También utilicé la interpolación de colores para los espacios entre los picos de la onda, creando una transición visual suave.

* ¿Qué concepto de la unidad 1 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Los conceptos fueron aleatoriedad con ruido Perlin y salto de Lévy. El ruido Perlin lo usé para generar variaciones suaves y naturales en los colores de la onda, mientras que el salto de Lévy lo empleé para determinar la aparición de los cuerpos, lo que aporta un carácter impredecible y orgánico a la obra.

## ¿Cómo resolviste la interacción?
> Tu respuesta aquí:
> La interacción la resolví de forma sencilla: El espectador puede modificar el patrón de la onda a su gusto, lo que le da control creativo sobre la obra. Además, implementé navegación con el mouse: con el botón derecho se puede mover por el canva y con las teclas + y - se controla el zoom para acercar o alejar la vista. Finalmente, con la tecla r es posible eliminar uno de los cuerpos para reducir el caos en la dinámica, y con la tecla m se puede añadir un nuevo cuerpo, generando así un comportamiento más caótico y complejo.

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra]((https://editor.p5js.org/estebanpuerta2006/sketches/aD9mw1VIp))

## Código de la obra 

``` js
// --- Obra generativa: Onda circular + N-cuerpos + Lévy + Perlin ---
// Unidades:
// U1: Perlin noise (atracción ondulada) + Lévy flights (cuerpos)
// U2: Motion 101 (pos/vel/acc) + interpolación de color
// U3: N-cuerpos (gravitación)
// U4: Onda (sinusoide) con control de amplitud/frecuencia/fase

let waves = [];
let bodies = [];
let sliders = {};
let t = 0;

// Pan y zoom
let viewX = 0, viewY = 0;
let isPanning = false;
let lastMouse;
let zoom = 1;

let bgEvents = []; // lista de colores activos en el fondo
let shapeMode = "circle"; // figura actual para ondas

let central;
let centralActive = false;
let lastToggle = 0;
let toggleInterval = 4000;

function setup() {
  createCanvas(1000, 1000);
  central = new CentralBody();
  colorMode(RGB, 255, 255, 255, 255);
  noStroke();

  // Sliders UI
  createP('Amplitud').style('margin:8px 0 0 0');
  sliders.amp = createSlider(10, 200, 80, 1);
  createP('Frecuencia (ciclos alrededor)').style('margin:8px 0 0 0');
  sliders.freq = createSlider(1, 24, 8, 1);
  createP('Velocidad radial (expansión)').style('margin:8px 0 0 0');
  sliders.radSpeed = createSlider(0, 6, 1.8, 0.1);
  createP('Fase').style('margin:8px 0 0 0');
  sliders.phase = createSlider(0, TWO_PI, 0, 0.01);

  waves.push(new WaveRing({
  numPoints: 240,
  peakEvery: 12,
  baseR0: 60
}));

  // algunos cuerpos iniciales
  for (let i = 0; i < 8; i++) bodies.push(new Body());
}

function draw() {
  // toggle on/off del central cada 4s
if (millis() - lastToggle > toggleInterval) {
  centralActive = !centralActive;
  lastToggle = millis();
}

// dibujar central
central.show(centralActive);
  
  // --- Fondo dinámico con degradado ---
  let blended = color(0, 0, 0);
  let totalWeight = 0;
  for (let i = bgEvents.length - 1; i >= 0; i--) {
    let e = bgEvents[i];
    let elapsed = millis() - e.time;
    let alpha = map(elapsed, 0, 2000, 1, 0); // dura 2s
    if (alpha <= 0) {
      bgEvents.splice(i, 1);
    } else {
      blended = lerpColor(blended, e.col, alpha / (1 + totalWeight));
      totalWeight++;
    }
  }
  
  background(blended);

  translate(width/2, height/2);
  scale(zoom);
  translate(viewX, viewY);

  // --- Actualizar cuerpos (n-cuerpos) y dibujar ---
  // --- Actualizar cuerpos ---
  for (let i = bodies.length - 1; i >= 0; i--) {
  let b = bodies[i];
  b.update(bodies);

  if (centralActive) {
    central.attract(b);
  }

  // si salió de ±500: efecto + regeneración
  if (abs(b.pos.x) > 500 || abs(b.pos.y) > 500) {
    bgEvents.push({col: b.c, time: millis()});
    let shapes = ["circle", "rect", "triangle", "pentagon"];
    shapeMode = random(shapes);

    bodies.splice(i, 1);
    bodies.push(new Body());
  }
}

  // Dibujar cuerpos
  for (let i = 0; i < bodies.length; i++) {
    bodies[i].show();
  }

  // --- Generar nuevas ondas periódicamente ---
  if (frameCount % 50 === 0) {
    waves.push(new WaveRing({
      numPoints: 240,
      peakEvery: 12,
      baseR0: 60
    }));
  }

  // --- Actualizar y dibujar todas las ondas ---
  for (let i = waves.length - 1; i >= 0; i--) {
    let w = waves[i];
    w.amp = sliders.amp.value();
    w.freq = sliders.freq.value();
    w.radialSpeed = sliders.radSpeed.value();
    w.phase = sliders.phase.value();
    w.update(bodies, t);
    w.show();

    // Eliminar las ondas que se fueron demasiado lejos
    if (w.baseR > max(width, height) * 1.5) {
      waves.splice(i, 1);
    }
  }

  t += 0.01;
}

// Click: recolorea SOLO los picos (los puntos intermedios conservan su color)
function mousePressed() {
  // Convertir a coords centradas
  const mx = mouseX - width/2;
  const my = mouseY - height/2;
  // Si hiciste click en la zona central (para evitar cambios accidentales sobre los sliders)
  if (mouseY > 0 && mouseY < height && mouseX > 0 && mouseX < width) {
    wave.recolorPeaks();
  }
}

// Teclas: m agrega, r quita
function keyPressed() {
  if (key === 'm' || key === 'M') bodies.push(new Body());
  if (key === 'r' || key === 'R') bodies.pop();
}

// ---------------------- WaveRing ----------------------
class WaveRing {
  constructor({numPoints=180, peakEvery=10, baseR0=80}) {
    this.numPoints = numPoints;
    this.peakEvery = peakEvery;
    this.baseR = baseR0;
    this.radialSpeed = 2.0;
    this.amp = 80;
    this.freq = 8;
    this.phase = 0;

    this.isPeak = new Array(numPoints).fill(false);
    for (let i = 0; i < numPoints; i++) {
      if (i % peakEvery === 0) this.isPeak[i] = true;
    }

    // colores persistentes por punto
    this.col = new Array(numPoints);
    // colores de pico actuales
    this.peakCol = new Array(numPoints);

    // Inicializar colores
    for (let i = 0; i < numPoints; i++) {
      if (this.isPeak[i]) {
        this.peakCol[i] = randomColor();
        this.col[i] = this.peakCol[i];
      } else {
        // interpolación inicial entre picos vecinos
        this.col[i] = this.interpolateBetweenPeaks(i);
      }
    }
  }

  // Busca los picos anterior y siguiente y hace una interpolación angular
  interpolateBetweenPeaks(idx) {
    const n = this.numPoints;
    // hallar pico anterior
    let prev = idx;
    while (!this.isPeak[prev]) prev = (prev - 1 + n) % n;
    // hallar pico siguiente
    let next = idx;
    while (!this.isPeak[next]) next = (next + 1) % n;

    // distancia fraccional de prev->idx respecto a prev->next
    let total = (next - prev + n) % n;
    if (total === 0) total = n;
    let along = (idx - prev + n) % n;
    let t = along / total;

    return lerpColorSafe(this.peakCol[prev], this.peakCol[next], t);
  }

  // Solo recolorea picos; NO re-interpola los intermedios -> conservan su color original
  recolorPeaks() {
    for (let i = 0; i < this.numPoints; i++) {
      if (this.isPeak[i]) {
        this.peakCol[i] = randomColor();
        this.col[i] = this.peakCol[i];
      }
    }
  }

  update(bodies, time) {
    // expansión
    this.baseR += this.radialSpeed;
    if (this.baseR > max(width, height)) this.baseR = 60;

    // Precalculo de ángulos
    this.angles = [];
    this.points = [];

    for (let i = 0; i < this.numPoints; i++) {
      const a = map(i, 0, this.numPoints, 0, TWO_PI);
      this.angles[i] = a;

      // radio sinusoide
      const r = this.baseR + this.amp * sin(this.freq * a + this.phase + time);

      // posición base
      let x = r * cos(a);
      let y = r * sin(a);

      // Atracción débil de los cuerpos (modulada por ruido)
      // (Los puntos de la onda NO interactúan entre sí)
      let off = createVector(0, 0);
      for (let b = 0; b < bodies.length; b++) {
        const bp = bodies[b].pos;
        const dvec = createVector(bp.x - x, bp.y - y);
        const d = max(8, dvec.mag());
        dvec.normalize();

        // fuerza muy débil, 1/r^2, modulada por Perlin y aleatoriedad suave
        const per = noise(0.1 * i, 0.1 * b, time) * 0.8 + 0.2;
        const strength = per * (bodies[b].mass) / (d * d) * 12; // coef pequeño
        off.add(p5.Vector.mult(dvec, strength));
      }

      this.points[i] = createVector(x + off.x, y + off.y);
    }
  }

  show() {
    // dibujar pequeñas circunferencias en cada punto
    for (let i = 0; i < this.numPoints; i++) {
      fill(this.col[i]);
      const p = this.points[i];
      circle(p.x, p.y, this.isPeak[i] ? 10 : 6);
    }
  }
}

// ---------------------- Bodies (N-cuerpos + Lévy) ----------------------
class Body {
  constructor() {
    // posición inicial distribuida alrededor
    this.pos = createVector(random(-width/3, width/3), random(-height/3, height/3));
    this.vel = p5.Vector.random2D().mult(random(0.5, 2));
    this.acc = createVector(0, 0);
    this.mass = abs(randomGaussian(1.8, 0.6)) + 0.4;
    this.c = randomColor();
  }

  applyForce(f) {
    // Motion 101
    this.acc.add(p5.Vector.div(f, this.mass));
  }

  // Gravedad desde otros cuerpos (clásico N-body, simplificado)
  gravitate(others) {
    const G = 0.4;
    for (let o of others) {
      if (o === this) continue;
      let dir = p5.Vector.sub(o.pos, this.pos);
      let d = constrain(dir.mag(), 12, 260);
      let strength = (G * this.mass * o.mass) / (d * d);
      dir.setMag(strength);
      this.applyForce(dir);
    }
  }

  // Salto Lévy ocasional
  levyKick(prob = 0.02, alpha = 1.5, scale = 1.2) {
    if (random() < prob) {
      const step = levy(alpha) * scale;
      this.vel.add(p5.Vector.random2D().mult(step));
    }
  }

  update(others) {
  this.gravitate(others);
  this.levyKick();

  this.vel.add(this.acc);
  this.pos.add(this.vel);
  this.acc.mult(0);

  // ---- Detectar estallido (cuando pasa ±400) ----
  if (abs(this.pos.x) > 400 || abs(this.pos.y) > 400) {
    // evento de color en el fondo
    bgEvents.push({col: this.c, time: millis()});
    let shapes = ["circle", "rect", "triangle", "pentagon"];
    shapeMode = random(shapes);

    // eliminar este cuerpo y crear otro nuevo
    let idx = bodies.indexOf(this);
    if (idx !== -1) {
      bodies.splice(idx, 1);   // quita el cuerpo actual
      bodies.push(new Body()); // añade un nuevo cuerpo fresco
      return; // salir de update() para evitar seguir con un body eliminado
    }
  }

  // ya no hay wrap de bordes (se elimina esa parte)
  
  // fricción suave
  this.vel.mult(0.995);
}

  show() {
  push();
  noStroke();
  fill(this.c);
  circle(this.pos.x, this.pos.y, this.mass * 10); // tamaño proporcional a la masa
  pop();
}
}

// ---------------------- Función auxiliar para figuras ----------------------
function drawShape(mode, s) {
  if (mode === "circle") {
    circle(0, 0, s);
  } else if (mode === "rect") {
    rectMode(CENTER);
    rect(0, 0, s, s);
  } else if (mode === "triangle") {
    triangle(-s/2, s/2, 0, -s/2, s/2, s/2);
  } else if (mode === "pentagon") {
    beginShape();
    for (let a = 0; a < TWO_PI; a += TWO_PI/5) {
      vertex(cos(a) * s/1.2, sin(a) * s/1.2);
    }
    endShape(CLOSE);
  }
}

// ---------------------- Helpers ----------------------
function randomColor() {
  return color(random(40,255), random(40,255), random(40,255), 230);
}

// Interpolación segura incluso si c1/c2 son undefined (no debería ocurrir)
function lerpColorSafe(c1, c2, t) {
  if (!c1) c1 = color(255,0,0);
  if (!c2) c2 = color(0,0,255);
  return lerpColor(c1, c2, constrain(t, 0, 1));
}

// Generador de paso Lévy (cola pesada)
function levy(alpha = 1.5) {
  // Método: muestrear u~Uniform(-pi/2,pi/2), v~Exp(1); Mantegna-like simplificado
  const u = random(-PI/2, PI/2);
  const v = -log(1 - random()); // exponencial(1)
  const s = sin(alpha * u) / pow(cos(u), 1/alpha);
  const t = pow( cos((1 - alpha) * u) / v, (1 - alpha) / alpha );
  const step = s * t;
  return step;
}

function mousePressed() {
  if (mouseButton === LEFT) {
    // recolorea todos los picos de todas las ondas
    for (let w of waves) w.recolorPeaks();
  }
  if (mouseButton === RIGHT) {
    isPanning = true;
    lastMouse = createVector(mouseX, mouseY);
  }
}

function mouseDragged() {
  if (isPanning && mouseButton === RIGHT) {
    let dx = (mouseX - lastMouse.x) / zoom;
    let dy = (mouseY - lastMouse.y) / zoom;
    viewX += dx;
    viewY += dy;
    lastMouse.set(mouseX, mouseY);
  }
}

function mouseReleased() {
  if (mouseButton === RIGHT) {
    isPanning = false;
  }
  if (mouseButton === CENTER) {
    zoom *= 0.8; // zoom out
  }
}

function keyPressed() {
  if (key === 'm' || key === 'M') bodies.push(new Body());
  if (key === 'r' || key === 'R') bodies.pop();
  if (key === '+') zoom *= 1.2;
  if (key === '-') zoom *= 0.8;
}

// ---------------------- CentralBody ----------------------
class CentralBody {
  constructor() {
    this.pos = createVector(0, 0);
    this.mass = 5000; // masa muy grande
    this.r = 60;      // radio visual
  }

  attract(body) {
    let force = p5.Vector.sub(this.pos, body.pos);
    let d = constrain(force.mag(), 40, 300); // distancias seguras
    let G = 4; // gravedad central más fuerte
    let strength = (G * this.mass * body.mass) / (d * d);
    force.setMag(strength);
    body.applyForce(force);
  }

  show(active) {
    push();
    noStroke();
    if (active) {
      fill(255, 80, 50); // rojo brillante
    } else {
      fill(120); // gris cuando está "apagado"
    }
    circle(this.pos.x, this.pos.y, this.r*2);
    pop();
  }
}
```

## Captura de pantalla representativa
<img width="892" height="673" alt="image" src="https://github.com/user-attachments/assets/de407a28-4498-4867-8bd9-7d1c89987c8d" />

<img width="892" height="666" alt="image" src="https://github.com/user-attachments/assets/1e9a41b4-dc70-4148-bb87-3344e962c6d1" />










