# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

#### ¿Cómo funciona la suma dos vectores en p5.js?

Para sumar dos vectores se usa el metodo add(), lo que hace dicha función es sumar los compenetes del vector:
ej: 
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Example 1-2: Bouncing Ball, with p5.Vector!
//{!2 .bold} Instead of a bunch of floats, we now just have two variables.
let position;
let velocity;

function setup() {
  createCanvas(640, 240);
  //{!2 .bold} Note how createVector() has to be called inside of setup().
  position = createVector(100, 100);
  velocity = createVector(2.5, 2);
}

function draw() {
  background(255);
  //{!1 .bold .no-comment}
  position.add(velocity);

  //{!6 .bold .code-wide} We still sometimes need to refer to the individual components of a p5.Vector and can do so using the dot syntax: position.x, velocity.y, etc.
  if (position.x > width || position.x < 0) {
    velocity.x = velocity.x * -1;
  }
  if (position.y > height || position.y < 0) {
    velocity.y = velocity.y * -1;
  }

  stroke(0);
  fill(127);
  strokeWeight(2);
  circle(position.x, position.y, 48);
}
```

-> position.add(velocity);

Se traduciria a:
position.x += velocity.x
position.y += velocity.y

Esto significa que el vector velocity se agrega al vector position, cambiando su dirección y magnitud en cada frame del draw().

El resultado de esta suma es que el objeto (en este caso, el círculo) se mueve en la dirección indicada por el vector de velocidad.


#### ¿Por qué esta línea position = position + velocity; no funciona?
##### Respuesta sin investigar
Esta linea no funciona debido a que al ser un vector no se puede sumar de la forma norma en programación devido a que los vectores tienen dos compentes, lo que genera que al sumar de esta manera los vectores no permita su suma.

##### Respuesta luego de investigar
La línea position = position + velocity; no funciona porque position y velocity son objetos del tipo p5.Vector, no números simples.
En JavaScript no se pueden sumar objetos directamente usando +. Esa operación solo funciona con tipos primitivos como números o cadenas de texto.
Los vectores tienen componentes (x, y, z), y para sumarlos correctamente se debe usar el método .add(), que sabe cómo combinar cada componente individualmente:


### Actividad 02

#### Tome uno de los ejemplos de caminantes del Capítulo 0 y conviértalo en vectores de uso.
#### Solución:
##### ¿Qué tuviste que hacer para hacer la conversión propuesta?
Para convertir el ejemplo original al uso de vectores, primero reemplacé las variables this.x y this.y por un solo vector llamado this.position, creado con createVector(width / 2, height / 2) en el constructor. Este vector almacena tanto la posición en x como en y del caminante.

Luego, en el método show(), utilicé point(this.position.x, this.position.y) para dibujar el punto usando las coordenadas del vector.

Por último, en el método step(), modifiqué directamente los componentes x o y del vector position dependiendo del resultado aleatorio, lo cual permite que se mueva el punto.

##### Muestra el código que utilizaste para resolver el ejercicio.
``` js
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.position = createVector(width / 2, height / 2);// Usamos un vector para la posición
    
    //this.x = width / 2;
    //this.y = height / 2;
  }

  show() {
    stroke(0);
    //point(this.position.x, this.position.y);
    point(this.position);// Accedemos a x e y desde el vector
    //point(this.position*mouseX/width, this.position*mouseY/height);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      //this.x++;
      this.position.x++;
    } else if (choice == 1) {
      //this.x--;
      this.position.x--;
    } else if (choice == 2) {
      //this.y++;
      this.position.y++;
    } else {
      //this.y--;
      this.position.y--;
    }
  }
}
```
