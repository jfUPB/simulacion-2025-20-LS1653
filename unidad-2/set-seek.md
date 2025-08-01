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

Lo segundo fue que comprendí mejor cómo funcionan los tipos de datos cuando se pasan a funciones. En este caso, al pasar un objeto, este se pasa por referencia, lo que significa que cualquier cambio dentro de la función afecta directamente al objeto original. Considero que este concepto sera muy util para manipular datos complejos, y me abre la posibilidad de experimentar con estructuras más dinámicas, como listas de objetos que pueden modificarse según ciertas condiciones o entradas aleatorias.

### Actividad 04
#### Explora posibilidades
##### ¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?
El metodo mag() sirve para medir la magnitud de un vector o lo que es lo mismo encontrar cual es el tamaño de dicho vector, lo cual sirve para facilitarnos hacer operaciones  como normalización, comparación de velocidades o distancias.

Ahora la diferencia entre mag() y magSq() es que magSq() calcula tambien el tamaño del vector pero al cuadrado, lo cual visualmente se ve de esta manera:


<img width="828" height="172" alt="image" src="https://github.com/user-attachments/assets/7027b841-1b04-4f22-ab87-a38acf590d3d" />

Y como se ve en la imagen dedido a que magSq() cancela la raiz, hace que calcular su resultado sea más sencillo lo cual la hace más eficiente.

##### ¿Para qué sirve el método normalize()?
El método normalize() sirve para convertir un vector en uno de la misma dirección pero con una longitud (magnitud) igual a 1, hay que tener en cuenta que el vector que devuelve con magnitud 1 no reemplaza o cambia al vector original.

##### Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?
El método dot() sirve para calcular cuánto apuntan dos vectores en la misma dirección; osea nos devuelve un número que nos dice si van en la misma dirección, en direcciones opuestas o si son perpendiculares.

##### El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?
###### Versión de instancia
``` js
let v1 = createVector(1, 2);
let v2 = createVector(3, 4);

let resultado = v1.dot(v2);
```
Se llama desde un objeto vector (en este caso v1).

Hace el producto punto entre v1 y v2.

Es como decir:
"Desde el punto de vista de v1, dime cuál es su producto punto con v2".

Versión estática
``` js
let v1 = createVector(1, 2);
let v2 = createVector(3, 4);

let resultado = p5.Vector.dot(v1, v2);
```
Se llama desde la clase Vector directamente, sin necesidad de tener un objeto que llame el método.

También hace el producto punto entre v1 y v2.

Es como decir:
"Dado dos vectores, dame su producto punto" — sin estar "parado" en ninguno en particular.

##### Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.
El producto cruz de dos vectores genera un nuevo vector perpendicular (es decir, en ángulo recto) al plano que forman esos dos vectores.

La dirección de ese nuevo vector se determina con la regla de la mano derecha (si apuntas el índice en la dirección del primer vector y el medio hacia el segundo, el pulgar apunta en la dirección del producto cruz).

La magnitud (o tamaño) del vector resultante equivale al área del paralelogramo formado por los dos vectores originales.

Si los dos vectores son paralelos, el resultado es el vector cero porque no hay “plano” entre ellos.

##### ¿Para que te puede servir el método dist()?
El método dist() sirve para calcular la distancia entre dos puntos definidos por sus coordenadas, usando el teorema de Pitágoras. Es útil para saber qué tan lejos están objetos o entidades en una escena ya sea en 2D o 3D.

##### ¿Para qué sirven los métodos normalize() y limit()?
###### normalize()
Como ya se habia respondido el método normalize() sirve para convertir un vector a un vector unitario, es decir, mantiene la misma dirección pero su magnitud pasa a ser 1.

Su utilidad basicamente es que se puede utilizar para conservar la dirección de un vector sin que su tamaño influya y además es útil cuando solo te importa la dirección de un objeto, no qué tan rápido.

###### limit()
El método limit(max) sirve para restringir la magnitud (tamaño) de un vector a un valor máximo. Si el vector ya tiene menor magnitud, no lo cambia.

Su utilidad basicamente es que se puede utilizar para evitar y regular valores como la velocidad.

### Actividad 05
#### Interpolamos?
#### Vas a tomar como inspiración este ejemplo de la referencia de p5.js:

``` js
function setup() {
    createCanvas(100, 100);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(30, 0);
    let v2 = createVector(0, 30);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```

#### Mi resultado
``` js
let l = 0;
let arriba;

function setup() {
    createCanvas(400, 400);
}

function draw() {
    background(200);
    
    let v0 = createVector(50, 50);
    let v1 = createVector(200, 0);
    let v2 = createVector(0, 200);
    let v3 = p5.Vector.lerp(v1, v2, l);
    let origen = p5.Vector.add(v0, v1);
    let destino = p5.Vector.add(v0, v2);
    let dir = p5.Vector.sub(destino, origen);
    
    // Interpolación de color
    let c1 = color(255, 0, 0);    // rojo
    let c2 = color(0, 0, 255);    // azul
    let interpolado = lerpColor(c1, c2, l);  // color interpolado

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, interpolado);  // color cambia dinámicamente
    drawArrow(origen, dir, 'green');
  
    if(l <= 0){
        arriba = true;
    }
    if(l >= 1){
        arriba = false;
    }
    
    if(arriba){
        l = l + 0.01;
    } else {
        l = l - 0.01;
    }
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```

#### Analiza cómo funciona el método lerp().
lerp() se puede tomar como la forma de calcular las compoenetes de un vector teniendo en cuenta otrod dos vectores, esto lo que hace es que la posición de este nuevo vector sea definido como una interpolación de las posiciones de esos dos vectores, dependiendo de cual sea el tercer parametro que uno le coloque entre 1 y 0, este nuevo vector se asemejara más a uno de los vectores, pj: darle 1 como parametro hara que se paresca más al segundo vector, darle como parametro 1 hara que se paresca al primero y si se le da 0.5 hara que ese nuevo vector sea la parte media de los dos.

#### Nota que además de la interpolación lineal de vectores, también puedes hacer interpolación lineal de colores con el método lerpColor().
