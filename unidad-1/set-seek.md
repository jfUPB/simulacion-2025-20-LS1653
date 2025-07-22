# Unidad 1

## 🔎 Fase: Set + Seek

### ACTIVIDAD 01

#### Piensa y describe en una sola frase y en tus propias palabras cómo la aleatoriedad influye en el arte generativo.

Al ver los diferentes videos y explicaciones, pude llegar a una conclusión que el efecto de la aleatoriedad en el arte generativo hace que en el caso del arte abstracto se consiga una imagen viva y en movimiento simulando un efecto que se puede considerar organico pues no sigue una linea ni patron sino que se desarrolla según conveniencia y pura suerte, lo caul da como resultado figuras completamente nuevas a cada momento que mantienen el interes del contemplador debido a la pregunta ¿en que se convertira? o ¿como cambiara?. Por otra parte en el caso del arte realista, siento que la aleatoridad daña de gran manera estas obras, no por que no sean creativas o interesantes, si no debido a sus errores y su falta de congruencia al ir cambiando en el tiempo, pienso que si estos errores pudiesen ser eliminados a futuro, el arte generativo podria llegar incluso más lejos ya que podriamos tener, un personaje cambiante que se mantega congruente en el tiempo.

Pero en si el como influye la aleatoridad en el arte generativo es en como podemos nostros ver en una imagen que siempre a sido inerte en el tiempo y estatica, ahora se puede ver con vida, cambiando infinitamente y que se mantenga interesante para el espectador. 

### ACTIVIDAD 02

#### Luego de ver el trabajo de Sofía piensa y escribe en TUS PROPIAS palabras:

##### Cuál es el papel de la aleatoriedad en su obra?
El papel de la aleatoridad en este trabajo es en resumidas cuentas generar la persepción de crecimiento, como si los elementos que se muestran frueran ramas de un árbol que estan creciendo, haciendo referencia a la misma canción que se escucha, en si lo que busca la aleatoridad es darle vida de manera visual al sonido que las personas escuchan, es como darle un rostro a lo que no vemos y un color a las emociones que nos transmite.

##### Según tu perfil profesional, cómo se aplica el concepto de aleatoriedad en el tipo de proyectos que desarrollas. Ilustra tu respuesta con ejemplos concretos.
La aleatoridad en mi futuro profecional se aplicara en la construcción de mapas o niveles de maneara procedural, en dónde yo comensare generando cierto numero de elementos, colores y personajes, pero estos elementos, colores y personajes se podran convinar de maneras infinitas de forma que cada espacio en el mundo dentro del juego paresca nuevo o por lo menos diferente.

Tambien la aleatoridad me puede ayudar de mejor manera en darle un movimiento más organico a los npc, puesto que lo normal es darle movimientos definidos, pero estos movimientos no solo son monotonos sino que tambien aburridos, al darle aleatoridad con algunos limitantes, se puede hacer que los npc puedan tener un desplazamiento más novedoso.

Ya lo ultimo que se me ocurre en el uso de la aleatoridad, es en la generación de recompensas como en un rpg en donde, nunca hay un resultado concreto sino que todo depende de tu suerte en obtener ciertos items con estadisticas variables.

### ACTIVIDAD 03

#### Realiza el siguiente experimento y reporta los resultados en tu bitácora:

##### Modifica el código del ejemplo Example 0.1: A Traditional Random Walk.

##### Codigo original
/*
//Esteban

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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
*/

##### Codigo cambiado

/*
//Esteban

let walker;
let walker2;

function setup() {
  createCanvas(640, 240);
  walker = new Walker("point");
  walker2 = new Walker("circle");
  background('red');
}

function draw() {  
  //background('blue');
  walker.step();
  walker.show();  
  
  walker2.step();
  walker2.show();  
}

class Walker {
  constructor(_drawType) {
    this.x = width / 2;
    this.y = height / 2;
    this.drawType = _drawType;
  }

  show() {
    stroke('green');    
    if(this.drawType === 'point'){
       point(this.x, this.y);
    }    
    else if(this.drawType === 'circle'){
      circle(this.x, this.y, 20);
    }
    
  }

  step() {
    const choice = floor(random(7));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else if (choice == 3){
      this.y--;
    } else if (choice == 4) {
      this.y++; this.x++;
    } else if (choice == 5) {
      this.y++; this.x--;
    } else if (choice == 6) {
      this.y--; this.x--;
    } else{
      this.y--; this.x++;
    }
  }
}

*/

##### Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.
lo principal que yo cambie fue 

/*
  function setup() { 
   background('red');
 }

 function draw() {  
  background('blue');  
}

show() {
    stroke('green');      
  }

 step() {
    const choice = floor(random(7));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else if (choice == 3){
      this.y--;
    } else if (choice == 4) {
      this.y++; this.x++;
    } else if (choice == 5) {
      this.y++; this.x--;
    } else if (choice == 6) {
      this.y--; this.x--;
    } else{
      this.y--; this.x++;
    }
  }
*/

Esos cambios combinados con el codigo original, lo que haran según lo que creo es:

El fondo de la pantalla primero se volvera rojo, el color de la linea que deja el punto y el circulo sera verde, pero esta no se podra ver debido a que puse en la función draw que background('blue');, lo que hace que no se vea el stroke('green'); pero si se vean tanto el punto, como el circulo.

Ya por ultimo el mayor cambio es que en step(), genere más opciones de movimiento lo cual le permite al punto y el circulo moverse de más maneras en este caso de manera diagonal.

##### Ejecuta el código y escribe en tu bitácora qué sucedió realmente.
En si los cambios que yo hice dieron el resultado que mensione antes, sin embargo, esto es debido a que no me arriesgue tanto al modificar el codigo, si ubiera intentado modificar el codigo de manera más compleja seguramente ubiera fallado más rapido.

##### Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?
Si fue lo que espere, ya que como mencione no me arriesgue mucho a modificar el codigo de mil maneras solo hice cambios pequeños y calculados.

### Actividad 4

#### En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.
La diferencia entre estas dos radica en que una distribución uniforme de un resultado es cuando todos los posibles resultados tienen la misma posibilidad de salir, como al tirar un dado que no este modificado, en si tiene un chande de 1/6 de que caiga cualquiera de sus 6 caras, en cambio una distribución no uniforme lo que hace es veneficiar un resultado, por lo que un resultado es más probable que otros, un ejemplo de esto es el dado cargado antes mencionado, este lo que hace es que al aumentar el peso de una cara del dado hace que sea más probable que salga una cara que otra.

#### Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.
Logre hacer que el lado derecho se viera veneficiado, sin embargo lo hice de manera diferente, aqui lo muestro:

/*
// Esteban

let walker;
let counts = [0, 0, 0, 0]; // [x++, x--, y++, y--]
let labels = ["x++", "x--", "y++", "y--"];

function setup() {
  createCanvas(640, 240);
  walker = new Walker("point");
  background('red');
  textSize(20);
  textAlign(CENTER, CENTER);
  fill(255);
}

function draw() {
  walker.step();
  walker.show();

  // Dibujar tabla
  drawTable();
}

function drawTable() {
  noStroke();
  fill(0, 150); // fondo semitransparente
  rect(440, 0, 200, height);

  fill(255);
  for (let i = 0; i < counts.length; i++) {
    text(labels[i], 540, 30 + i * 50);
    text(counts[i], 600, 30 + i * 50);
  }
}

class Walker {
  constructor(_drawType) {
    this.x = width / 2;
    this.y = height / 2;
    this.drawType = _drawType;
  }

  show() {
    stroke('green');
    if (this.drawType === 'point') {
      point(this.x, this.y);
    }
  }
  
  step() {
    let choice;
    let r = random(); // entre 0 y 1
  if (r < 0.4) {
    this.x++; // 40% de las veces: derecha
    choice = 0;
  } else if (r < 0.55) {
    this.x--; // 15% de las veces: izquierda
    choice = 1;
  } else if (r < 0.75) {
    this.y++; // 20%: abajo
    choice = 2;
  } else {
    this.y--; // 25%: arriba
    choice = 3;
  }

    counts[choice]++; // actualiza conteo
  }
}
*/

Luego de varios intentos logre hacer que funcionara con la funación randomGaussian().

/*
// Esteban

let walker;
let counts = [0, 0, 0, 0]; // [x++, x--, y++, y--]
let labels = ["x++", "x--", "y++", "y--"];

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
  textSize(16);
  textAlign(LEFT, CENTER);
}

function draw() {
  walker.step();
  walker.show();
  drawTable();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    let g = randomGaussian(0, 1); // valores centrados en 0
    let choice;

    if (g < -0.4) {
    this.x++; 
    choice = 0;
  } else if (g < 0  && g >= -0.4) {
    this.x--; 
    choice = 1;
  } else if (g < 0.5 && g >= 0) {
    this.y++; 
    choice = 2;
  } else {
    this.y--; 
    choice = 3;
  }
    print(choice);

    if (choice == 0) this.x++;
    else if (choice == 1) this.x--;
    else if (choice == 2) this.y++;
    else if (choice == 3) this.y--;

    counts[choice]++;
  }
}

function drawTable() {
  fill(255);
  noStroke();
  rect(450, 0, 190, height); // fondo para tabla

  fill(0);
  for (let i = 0; i < labels.length; i++) {
    text(labels[i] + ": " + counts[i], 460, 40 + i * 30);
  }
}
*/

### ACTIVIDAD 05

#### Una vez has entendido el concepto de distribución normal, vas a pensar en una nueva manera de visualizarlo.

#### Crea un nuevo sketch en p5.js que represente una distribución normal.
#### Copia el código en tu bitácora.
/*
let frequencies = [];

function setup() {
  createCanvas(1000, 100);
  background(255);

  for (let i = 0; i < width; i++) {
    frequencies[i] = 0;
  }
}

function draw() {
  // Generar valor con distribución normal
  let x = int(randomGaussian(width / 2, 60));

  // Aumentar frecuencia si está en el canvas
  if (x >= 0 && x < width) {
    frequencies[x]++;
  }

  background(255);

  // Encontrar la frecuencia máxima
  let maxFreq = max(frequencies);

  noStroke();

  // Dibujar puntos con color según su frecuencia
  for (let i = 0; i < width; i++) {
    let freq = frequencies[i];

    // Mapear frecuencia a color:
    // 0 -> azul
    // maxFreq/2 -> amarillo/naranja
    // maxFreq -> rojo
    let inter = map(freq, 0, maxFreq, 0, 1);
    let col = color(0, 0, 255); // azul por defecto

    if (inter < 0.5) {
      // Interpolar entre azul y amarillo
      col = lerpColor(color(0, 0, 255), color(255, 204, 0), inter * 2);
    } else {
      // Interpolar entre amarillo y rojo
      col = lerpColor(color(255, 204, 0), color(255, 0, 0), (inter - 0.5) * 2);
    }

    fill(col);
    ellipse(i, height - freq, 4, 4);
  }
}
*/
![imagen](<img width="712" height="210" alt="image" src="https://github.com/user-attachments/assets/80eb7d3e-7ecc-4372-b014-45a0166ce5fa" />
)
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
