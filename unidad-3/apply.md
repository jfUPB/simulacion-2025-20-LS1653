# Unidad 3


## 🛠 Fase: Apply

### Actividad 10

#### Diseña e implementa tu obra generativa interactiva en tiempo real.
    - Debe ser interactiva.
      m: agrega una nueva esfera.
      r: elimina la última esfera.
      p: pausa/reanuda el sistema.
      t: activa/desactiva manualmente la “esfera ancla” (la masa central).
      Arrastrar con el mouse: rotar cámara (usando orbitControl en WEBGL).
      
    - Debes usar al menos dos algoritmos diferentes de la unidad 1, además de random.
      Ruido Perlin (noise): Usado para la posición inicial de cada esfera, esto para que su aparción sea sercana y a su vez no se genere literalmente ensima de otra esfera.
      Distribución normal (randomGaussian): Usado para colocar el radio y la masa de cada esfera, con valores mayormente cercanos a un promedio, pero permitiendo la aparición de masas atípicas o mejor dicho fuera de la media.
      
#### Explica cómo modelaste el problema de los n-cuerpos en tu obra.
Cada esfera es un cuerpo definido por (posición, velocidad, aceleración, masa).
En cada actualización del sistema, cada cuerpo experimenta la fuerza gravitacional que ejercen todos los demás cuerpos, siguiendo la ley de gravitación de Newton:

<img width="165" height="63" alt="image" src="https://github.com/user-attachments/assets/f61566aa-a5f1-49b6-a337-d085e01a82b7" />

Donde m1 y m2 son las masas de las esferas.
r es la distancia entre los cuerpos.
G es la constante gravitacional ajustada para la simulación.

La fuerza resultante se acumula en la aceleración de cada esfera, modificando su velocidad y trayectoria.
De esta manera se modela un sistema de n-cuerpos interactivos, donde la dinámica no es predecible y siempre está cambiando con la intervención del usuario.

#### Copia el enlace a tu simulación en p5.js.
[Link de mi obra](https://editor.p5js.org/estebanpuerta2006/sketches/VLkRH0AOz) 

#### Copia el código.
``` js
let bodies = [];
let paused = false;

// colores del fondo
let bgColor;
let targetBg;

// esfera central (el "Sol")
let central;
let centralActive = false;
let lastToggle = 0;
let toggleInterval = 4000; // cada 4 segundos cambia estado

function setup() {
  createCanvas(800, 600, WEBGL); 
  bgColor = color(20);
  targetBg = color(20);

  // crear la esfera central
  central = new CentralBody();
}

function draw() {
  // transición de color del fondo hacia targetBg
  bgColor = lerpColor(bgColor, targetBg, 0.02);
  background(bgColor);

  // Luz para dar efecto 3D
  directionalLight(255, 255, 255, 0.25, 0.25, -1);
  ambientLight(100);

  // Cámara sencilla para ver mejor
  orbitControl();

  // actualizar estado del central (encendido / apagado)
  if (millis() - lastToggle > toggleInterval) {
    centralActive = !centralActive;
    lastToggle = millis();
  }

  // dibujar central
  central.show(centralActive);

  // Dibujar cuerpos
  for (let i = bodies.length - 1; i >= 0; i--) {
    let body = bodies[i];
    body.show();
    if (!paused) {
      body.update(bodies);

      // si el central está activo, atraer con fuerza extra
      if (centralActive) {
        central.attract(body);
      }
    }

    // chequeamos si salió de los límites
    if (
      abs(body.pos.x) > 1200 ||
      abs(body.pos.y) > 1200 ||
      abs(body.pos.z) > 1200
    ) {
      // color del cuerpo se convierte en color de fondo
      bgColor = body.c;
      targetBg = color(20); // luego regresa a negro
      bodies.splice(i, 1); // eliminar cuerpo
    }
  }
}

function keyPressed() {
  if (key === 'm' || key === 'M') {
    bodies.push(new Body());
  }
  if (key === 'r' || key === 'R') {
    bodies.pop();
  }
  if (key === 'p' || key === 'P') {
    paused = !paused;
  }
}

class Body {
  constructor() {
    // Posición inicial usando ruido Perlin
    this.xoff = random(1000);
    this.yoff = random(1000);
    this.zoff = random(1000);

    this.pos = createVector(
      map(noise(this.xoff), 0, 1, -width / 2, width / 2),
      map(noise(this.yoff), 0, 1, -height / 2, height / 2),
      map(noise(this.zoff), 0, 1, -300, 300)
    );

    // Velocidad con random hasta 80
    this.vel = createVector(random(-80, 80), random(-80, 80), random(-80, 80)).mult(0.01);

    // Tamaño y "masa" con gaussiana
    this.r = abs(randomGaussian(20, 15)); 
    this.mass = abs(randomGaussian(20, 15));

    // Color random
    this.c = color(random(255), random(255), random(255));
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.vel.add(f);
  }

  attract(others) {
    for (let other of others) {
      if (other !== this) {
        let force = p5.Vector.sub(other.pos, this.pos);
        let d = constrain(force.mag(), 5, 25);
        let G = 1;
        let strength = (G * this.mass * other.mass) / (d * d);
        force.setMag(strength);
        this.applyForce(force);
      }
    }
  }

  update(others) {
    this.attract(others);
    this.pos.add(this.vel);
  }

  show() {
    push();
    translate(this.pos.x, this.pos.y, this.pos.z);
    noStroke();
    ambientMaterial(this.c);
    sphere(this.r);
    pop();
  }
}

class CentralBody {
  constructor() {
    this.pos = createVector(0, 0, 0);
    this.mass = 5000; // masa muy grande
    this.r = 60; // radio del sol
  }

  attract(body) {
    let force = p5.Vector.sub(this.pos, body.pos);
    let d = constrain(force.mag(), 50, 500); // distancia segura
    let G = 5; // más fuerte que las normales
    let strength = (G * this.mass * body.mass) / (d * d);
    force.setMag(strength);
    body.applyForce(force);
  }

  show(active) {
    push();
    translate(this.pos.x, this.pos.y, this.pos.z);
    noStroke();
    if (active) {
      ambientMaterial(255, 80, 50); // rojo brillante cuando atrae
    } else {
      ambientMaterial(100); // gris cuando apagado
    }
    sphere(this.r);
    pop();
  }
}
```

#### Captura una imagen representativa de tu ejemplo.

<img width="917" height="673" alt="image" src="https://github.com/user-attachments/assets/dddc6b0e-14a2-471b-844b-8ad72f2d9f77" />
<img width="917" height="673" alt="image" src="https://github.com/user-attachments/assets/8e7d99e6-a408-456d-9763-57477b5112cd" />

#### Usa tu creatividad para crear algo diferente basado en ese concepto y en las esculturas cinéticas de Alexander Calder.

Luego de ver muchas obras de el, siento que sus obras siempre muestran la conección entre los elementos más pequeños conectados a elementos más grandes, decidi hacer una obra que






