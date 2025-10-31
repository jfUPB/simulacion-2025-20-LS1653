# Evidencias de la unidad 8
## Actividad 01
### a) conecxión imagen-sonido
En Dimension N, la relación entre el sonido y la imagen se siente profundamente integrada. Los visuales parecen reaccionar a las frecuencias más graves mediante pulsaciones lentas y expansiones de color, mientras que los sonidos agudos producen líneas finas, fractales o destellos de luz que vibran en la pantalla. No se trata solo de la sincronía rítmica, sino de una conexión con el sonido: cuando la música se vuelve más densa o caótica, los visuales se saturan, se fragmentan y se expanden como si el sonido los estuviera impulsando desde dentro.


En Sónar+D CCCB 2020, la conexión es más atmosférica. Aquí la música de Carles Viarnès, más pianística y etérea, se traduce en paisajes digitales que fluyen suavemente. Los colores cambian con la armonía, las transiciones visuales responden a la intensidad del sonido, y se perciben movimientos ondulantes que siguen los crescendos y los silencios. En lugar de reaccionar al ritmo, los visuales acompañan la estructura emocional de la música.

### b) Explica qué elementos te parecieron generativos y por qué crees que cada visualización sería única.
En ambos casos, los visuales de Alba G. Corral presentan características claramente generativas:

Uso de formas orgánicas que evolucionan de manera continua y no repetitiva.

Patrones que se deforman y transforman con el tiempo, probablemente guiados por algoritmos que responden a la amplitud o las frecuencias del sonido.

Texturas vivas, que emergen, desaparecen y mutan, creando la sensación de que el sistema tiene cierta autonomía.

En Dimension N, las figuras abstractas parecen tener comportamiento propio: crecen, colisionan, se disuelven, como si cada ejecución fuera irrepetible.

En Sónar+D, el flujo visual recuerda a un “pintar con código”, donde el azar y el cálculo coexisten: las variaciones no son totalmente predecibles, lo que sugiere un sistema sensible y adaptativo.

Por estas razones, es evidente que cada performance sería única, incluso si la música fuera la misma. Las visuales generativas dependen de valores aleatorios, del entorno sonoro en vivo, y de la interpretación manual de la artista en tiempo real.


### c)Reflexión sobre la sensación de “liveness”.
La sensación de liveness en los trabajos de Alba G. Corral es muy fuerte. Los visuales están siendo generados en tiempo real provoca una conexión directa entre el público, la música y la imagen.
No se siente como un video pregrabado, sino como una improvisación audiovisual, donde el sonido guía a la imagen y la imagen reinterpreta al sonido. Esta interacción crea un diálogo vivo entre disciplinas, en el que el código se convierte en un instrumento expresivo más.

En ambos casos, la experiencia transmite presencia y reacción inmediata: los visuales respiran con la música, se emocionan con ella y se transforman en sincronía. Esa cualidad viva y efímera es lo que convierte a las obras generativas de Alba G. Corral en performances irrepetibles.


## Actividad 02
### Pieza musical elegida

Título: La Hija de las Estrellas
Artista: SAUROM
Enlace: https://youtu.be/tuArrB6YfGE?si=Gk_SPp8rmr40a1te

Elegí esta canción debido a su dinámica narrativa y estructura cambiante, que combina momentos suaves y melódicos con secciones intensas llenas de energía. Esto permite traducir visualmente las transiciones musicales a través de diferentes comportamientos de las formas, colores y partículas en pantalla.
Su naturaleza épica y fantástica también inspira un mundo visual místico, donde la música guía el movimiento del color y la forma.

### Concepto visual
El concepto sera en base en el viaje de una estrella que nace, brilla, explota y renace.
A través de la visualización, busco representar la energía y emociones contenidas en la canción:

Momentos suaves: La cámara recorre un espacio lleno de luz tenue y ondas que fluyen lentamente, como un cosmos en calma.

Momentos intensos: Explosiones de color, formaciones que se expanden como supernovas, y figuras que se transforman según el ritmo.

Transiciones: Los cambios de frecuencia harán que el entorno se mueva y deforme, como si el espacio mismo respirara con la música.

Visualmente será tratara de hacer una mezcla de ondas, partículas y campos de flujo (flow fields), combinados para generar movimientos orgánicos y sincronizado con la música.

### Inputs
Los inputs que se usare para interpretar la música en tiempo real serán:

``` markdown
| **Input**                              | **Descripción**                                    | **Efecto visual asociado**                                         |
|----------------------------------------|----------------------------------------------------|--------------------------------------------------------------------|
| Amplitud general (nivel de volumen)    | Captura la energía global de la canción.           | Cambia el brillo y saturación del fondo, genera pulsaciones de luz.|
| Frecuencias graves (bajos)             | Detectadas con FFT.                                | Aumentan el tamaño o explosividad de las partículas; simulan las ondas de impacto.|
| Frecuencias medias-altas (instrumentos y voz) | Responden a los detalles melódicos.         | Activan deformaciones de malla, colores cambiantes y movimientos de los “rayos” visuales.|
| Intensidad rítmica (beat o picos)      | Picos detectados por variaciones rápidas de energía.| Cambia la imagen o tono de fondo automáticamente, simulando cambios de atmósfera.|
```

### Algoritmos y técnicas 
Se utilizara una combinación de técnicas generativas vistas durante el curso:

Flow Fields:
Para mover los objetos (buques, partículas, ondas) con trayectorias fluidas que se deforman según la música.
Cada frecuencia influirá en la dirección y fuerza de los vectores del campo.

Flocking Behavior (comportamiento de enjambre):
Para simular cómo las partículas o elementos luminosos se agrupan y separan con el ritmo.

Partículas con física simple:
Usadas para representar explosiones estelares y expansión energética.

Interacción con FFT (Fast Fourier Transform):
Para vincular frecuencias específicas con transformaciones visuales (color, tamaño, posición, rotación, etc.).

Transición dinámica de fondos:
Cuando la intensidad de la música aumenta, cambia el fondo de forma automática, representando un cambio de “atmósfera” o capítulo visual.

### Boceto conceptual

Imagino la escena como un universo vivo:

En el fondo, una malla ondulante que se distorsiona con la música, como si el espacio vibrara.
En primer plano, formas y partículas que representan energía estelar, flotando y girando con el ritmo.
En momentos de calma, el color se enfría (azules, violetas, blancos suaves).
En los clímax, el color se calienta (rojos, dorados, naranjas brillantes) y todo se acelera.
Cada vez que la música alcanza un punto máximo, una supernova visual inunda la pantalla, marcando el impacto sonoro.

### Boceto

<img width="550" height="375" alt="image" src="https://github.com/user-attachments/assets/e01d73d3-c8f2-4495-8dc9-cd65c78a1618" />

### Boceto inspiracional generado a mi petición por chatgpt

<img width="246" height="207" alt="image" src="https://github.com/user-attachments/assets/a7c02eec-0ef4-421d-a226-4ac1553dc357" />


## Actividad 03
``` js
let musicaFondo, amplitude, fft;
let fondos = [];
let fondoActual;
let cambioFondoTimer = 0;

let ondas = [];
let particulas = [];
let orbes = [];
let explosiones = [];
let ondasExpansivas = [];
let estrellas = [];
let pinceles = [];

const N_ONDAS = 8;
const N_START_PARTICLES = 40;
const N_ESTRELLAS = 60;
const N_PINCELES = 5;
const CAMBIO_FONDO_INTERVALO = 5000;

// --- PRELOAD ---
function preload() {
  soundFormats('mp3', 'wav');
  musicaFondo = loadSound('assets/hija.mp3');
  for (let i = 1; i <= 4; i++) fondos.push(loadImage(`assets/fondo${i}.jpg`));
}

// --- SETUP ---
function setup() {
  createCanvas(1000, 700);
  noStroke();
  musicaFondo.loop();

  amplitude = new p5.Amplitude();
  fft = new p5.FFT(0.8, 64);
  fondoActual = random(fondos);

  for (let i = 0; i < N_ONDAS; i++) ondas.push(new Onda(random(height), random(0.5, 2)));
  for (let i = 0; i < N_START_PARTICLES; i++) particulas.push(new Particula(random(width), random(height)));
  for (let i = 0; i < N_ESTRELLAS; i++) estrellas.push(new Estrella());
  for (let i = 0; i < N_PINCELES; i++) pinceles.push(new PincelNoise());
}

// --- DRAW ---
function draw() {
  let nivel = amplitude.getLevel();

  // Fondo con leve transparencia (permite fundido de los trazos)
  fill(0, 30);
  rect(0, 0, width, height);

  // Fondo musical cada 5s
  if (millis() - cambioFondoTimer > CAMBIO_FONDO_INTERVALO) {
    fondoActual = random(fondos);
    cambioFondoTimer = millis();
  }

  // Imagen de fondo atenuada
  tint(255, 80);
  image(fondoActual, 0, 0, width, height);
  noTint();

  // Ondas
  for (let onda of ondas) {
    onda.actualizar(nivel);
    onda.mostrar();
  }

  // Partículas
  for (let p of particulas) {
    p.actualizar(nivel);
    p.mostrar();
  }

  // Estrellas tipo flocking
  for (let e of estrellas) {
    e.actualizar(nivel);
    e.mostrar();
  }

  // Orbes
  for (let o of orbes) {
    o.actualizar(nivel);
    o.mostrar();
  }

  // Explosiones
  for (let e of explosiones) {
    e.actualizar();
    e.mostrar();
  }

  // Ondas expansivas
  for (let o of ondasExpansivas) {
    o.actualizar(nivel);
    o.mostrar();
  }

  // Pinceles “vivos”
  for (let p of pinceles) {
    p.actualizar(nivel);
    p.mostrar();
  }

  explosiones = explosiones.filter(e => !e.fin);
  ondasExpansivas = ondasExpansivas.filter(o => !o.fin);

  // Click genera un orbe
  if (mouseIsPressed) {
    let c = color(random(100,255), random(100,255), random(255));
    orbes.push(new Orbe(mouseX, mouseY, c));
  }
}

// --- CLASES ---

class Onda {
  constructor(y, v) {
    this.y = y;
    this.velocidad = v;
    this.offset = random(1000);
    this.colorBase = color(random(100,255), random(100,255), random(255));
  }
  actualizar(n) { this.offset += 0.02; this.n = n; }
  mostrar() {
    noFill();
    strokeWeight(2);
    let c = lerpColor(this.colorBase, color(255), this.n * 3);
    stroke(c);
    beginShape();
    for (let x = 0; x < width; x += 10) {
      let y = this.y + sin(x * 0.02 + this.offset) * (this.n * 400);
      vertex(x, y);
    }
    endShape();
  }
}

class Particula {
  constructor(x, y) {
    this.base = createVector(x, y);
    this.pos = this.base.copy();
    this.angulo = random(TWO_PI);
    this.radio = random(50, 250);
    this.velAngulo = random(0.001, 0.005);
    this.colorBase = color(random(180, 255), random(180, 255), random(255), 180);
  }
  actualizar(n) {
    this.angulo += this.velAngulo;
    let exp = map(n, 0, 0.4, 0.8, 2.5);
    this.pos.x = this.base.x + cos(this.angulo) * this.radio * exp;
    this.pos.y = this.base.y + sin(this.angulo) * this.radio * exp;
  }
  mostrar() { noStroke(); fill(this.colorBase); ellipse(this.pos.x, this.pos.y, 2.5); }
}

class Orbe {
  constructor(x, y, c) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(1, 3));
    this.tam = random(10, 25);
    this.c = c;
    this.explotado = false;
    this.tiempoVida = random(300, 600);
  }
  actualizar(n) {
    if (this.explotado) return;
    this.pos.add(this.vel);
    this.vel.add(p5.Vector.random2D().mult(0.05));
    this.tam += sin(frameCount * 0.05) * 0.5;
    this.tiempoVida--;
    if ((n > 0.4 && random() < 0.05) || this.tiempoVida < 0) this.explotar(n);
  }
  explotar(n) {
    this.explotado = true;
    for (let i = 0; i < 15; i++) explosiones.push(new Explosion(this.pos.x, this.pos.y, this.c));
    ondasExpansivas.push(new OndaExpansiva(this.pos.x, this.pos.y, this.c, n));
  }
  mostrar() {
    if (!this.explotado) {
      noStroke();
      fill(this.c);
      ellipse(this.pos.x, this.pos.y, this.tam);
    }
  }
}

class Explosion {
  constructor(x, y, c) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(2, 6));
    this.tam = random(2, 6);
    this.c = c;
    this.vida = 255;
    this.fin = false;
  }
  actualizar() {
    this.pos.add(this.vel);
    this.vel.mult(0.95);
    this.vida -= 5;
    if (this.vida <= 0) this.fin = true;
  }
  mostrar() {
    noStroke();
    fill(red(this.c), green(this.c), blue(this.c), this.vida);
    ellipse(this.pos.x, this.pos.y, this.tam);
  }
}

class OndaExpansiva {
  constructor(x, y, c, n) {
    this.x = x;
    this.y = y;
    this.c = c;
    this.t = 0;
    this.maxT = 300;
    this.vel = map(n, 0, 0.5, 2, 8);
    this.fin = false;
  }
  actualizar(n) {
    this.t += this.vel + n * 10;
    if (this.t > this.maxT) this.fin = true;
  }
  mostrar() {
    noFill();
    stroke(red(this.c), green(this.c), blue(this.c), map(this.t, 0, this.maxT, 255, 0));
    strokeWeight(2);
    ellipse(this.x, this.y, this.t);
  }
}

class Estrella {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = p5.Vector.random2D();
    this.c = color(random(150,255), random(150,255), random(255));
  }
  actualizar(n) {
    this.pos.add(this.vel);
    if (random() < 0.02 + n * 0.5) this.vel = p5.Vector.random2D().mult(random(1, 3 + n * 10));
    this.pos.x = (this.pos.x + width) % width;
    this.pos.y = (this.pos.y + height) % height;
  }
  mostrar() {
    noStroke();
    fill(this.c);
    ellipse(this.pos.x, this.pos.y, 3);
  }
}

// --- NUEVA CLASE: PINCEL NOISE ---
class PincelNoise {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.angulo = random(TWO_PI);
    this.c = color(random(100,255), random(100,255), random(255));
    this.paso = random(1,3);
  }
  actualizar(n) {
    // Movimiento basado en ruido y nivel de sonido
    let ruido = noise(this.pos.x * 0.005, this.pos.y * 0.005, frameCount * 0.005);
    this.angulo += map(ruido, 0, 1, -0.3, 0.3) + n * 2;
    let dir = p5.Vector.fromAngle(this.angulo);
    this.pos.add(dir.mult(this.paso + n * 20));

    // Reaparece si sale de pantalla
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.y < 0) this.pos.y = height;
    if (this.pos.y > height) this.pos.y = 0;
  }
  mostrar() {
    strokeWeight(random(1, 3));
    let alpha = random(80, 150);
    stroke(red(this.c), green(this.c), blue(this.c), alpha);
    point(this.pos.x, this.pos.y);
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

[Mi obra](https://editor.p5js.org/estebanpuerta2006/sketches/rpFwA0Byp)

### Capturas

<img width="1262" height="695" alt="image" src="https://github.com/user-attachments/assets/8344f0e6-0849-4e62-b3af-934dd83e8fcc" />

<img width="1255" height="692" alt="image" src="https://github.com/user-attachments/assets/98247c89-12c4-4ce5-abaa-572eca7b4a8c" />


## Auto evaluación
### Mi nota: 5.0

### Mi defensa:
Luego de todo un semestre haciendo trabajos considero que este ultimo demuestra mi dominio en todos los temas anteriores, a su vez considero que mi trabajo refleja el proceso que estube haciendo durante este semestre pues cada uno de mis trabajos fue inspirado de un trabajo de una unidad anterior escepto el de la unidad 1 ya que no habia unidad del cual apalancarme. Tambien resolvi cada parte de esta unidad y puedo decir que quede satisfecho con mi resultado.

