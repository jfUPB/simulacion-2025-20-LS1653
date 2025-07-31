# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

#### ¿Cómo funciona la suma dos vectores en p5.js?
Para convertir el ejemplo original al uso de vectores, primero reemplacé las variables this.x y this.y por un solo vector llamado this.position, creado con createVector(width / 2, height / 2) en el constructor. Este vector almacena tanto la posición en x como en y del caminante.

Luego, en el método show(), utilicé point(this.position.x, this.position.y) para dibujar el punto usando las coordenadas del vector.

Por último, en el método step(), modifiqué directamente los componentes x o y del vector position dependiendo del resultado aleatorio, lo cual permite mover el punto

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

### Actividad 03
#### Experimenta
#### Dale una mirada a este código:
```js
let position;

function setup() {
    createCanvas(400, 400);
    position = createVector(6,9);
    console.log(position.toString());
    playingVector(position);
    console.log(position.toString());
    noLoop();
}

function playingVector(v){
    v.x = 20;
    v.y = 30;
}

function draw() {
    background(220);
    console.log("Only once");
}
```

#### ¿Qué resultado esperas obtener en el programa anterior?
Despues de desglosar en menor o mayor medida el codigo puedo llegar a deducir que lo que tendre como resultado es:
Que en la consola se imprimira el vector posición, como no se que hace el metodo noLoop(), voy a considerar que para el programa, lo que a su vez hace que solo se imprima dos veces el vectoe posición en la consola.

#### ¿Qué resultado obtuviste?
Como dije al final solo se imprime dos veces el valor del vector posición, sin embargo no fue por la razón que dije, si o si en el programa se imprimira dos veces el valor del vector posición, lo que hace realmente el metodo noloop() es hacer que el programa se detenga luego de imprimir el mensaje en la función draw().

#### Recuerda los conceptos de paso por valor y paso por referencia en programación. Muestra ejemplos de este concepto en javascript.
##### Paso por valor: 
significa que se copia el valor original. Si se modifica el valor dentro de una función, el original no cambia. Esto ocurre con tipos primitivos como números o strings.

ej:
``` js
function cambiaValor(x) {
  x = 100;
}

let a = 5;
cambiaValor(a);
console.log(a); // Imprime 5, no fue modificado
```

##### Paso por referencia: 
significa que se pasa la referencia al mismo objeto o estructura. Si se modifica dentro de una función, el original también cambia. Esto ocurre con objetos y arrays.

ej:
``` js
function modificaObjeto(obj) {
  obj.nombre = "Nuevo";
}

let persona = { nombre: "Original" };
modificaObjeto(persona);
console.log(persona.nombre); // Imprime "Nuevo"
```

#### ¿Qué tipo de paso se está realizando en el código?
En el código se está realizando paso por referencia, ya que se está pasando el vector posición (el cual es un objeto) a la función playingVector(v). Como los objetos en JavaScript se pasan por referencia, cualquier cambio hecho a la variable v dentro de la función también afecta directamente a position.

Esto se puede ver y corroborar al ver que después de ejecutar playingVector(position), los valores de position han cambiado de (6, 9) a (20, 30).

#### ¿Qué aprendiste?
Aprendi dos cosas la primera que no tiene tanto que ver con lo explicado en este ejercicio es que el metodo noloop() detiene el ciclo interno del codigo generando que solo se ejecuten las funciones una vez y no continuamente en el tiempo.
