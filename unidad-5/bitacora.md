# Evidencias de la unidad 5

## Seek:

### Actividad 2

### Revisa detalladamente el ejemplo 4.2:
[Ejemplo 4.2](https://natureofcode.com/particles/#example-42-an-array-of-particles)

#### Analisis 
1. Declaración global

   ``` js
     let particles = [];
   ```
   Arreglo vacío que guardará todas las partículas activas.

2. draw()

   ``` js
     function draw() {
        background(255);
        particles.push(new Particle(width / 2, 20));
   ```
   Se limpia el fondo en cada frame.
   Cada vez que se ejecuta draw(), se genera una nueva partícula en la posición (width/2, 20), es decir, en el centro superior de la pantalla.
   Esto quiere decir que constantemente nacen partículas.

3. Bucle invertido

   ``` js
     for (let i = particles.length - 1; i >= 0; i--) {
          let particle = particles[i];
          particle.run();
          if (particle.isDead()) {
              particles.splice(i, 1);
          }
     }
   ```
   Se recorre el array de atrás hacia adelante.
   Esto se hace porque se eliminaran elementos (splice) y no queriere que se desajusten los índices al recorrerlos.
   particle.run() -> Ejecuta:
        update() -> Cambia la posición, velocidad, vida, etc.
        display() -> Dibuja la partícula en pantalla.
   particle.isDead() -> Devuelve true cuando la partícula ha "muerto". -> Si muere, se elimina del arreglo.

4. Clase Particle

Constructor
    ``` js
     constructor(x, y) {
       this.position = createVector(x, y);
       this.acceleration = createVector(0, 0);
       this.velocity = createVector(random(-1, 1), random(-1, 0));
       this.lifespan = 255.0;
    }
   ```
    Cada partícula tiene:
       position: dónde está.
       velocity: movimiento inicial, aleatorio en X y negativo en Y → tienden a moverse hacia arriba.
       acceleration: empieza en 0, se usa para acumular fuerzas.
       lifespan: vida útil (255 -> máximo, como alfa en colores).

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

### Analiza el ejemplo 4.4:
[Ejemplo 4.4](https://natureofcode.com/particles/#example-44-a-system-of-systems)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

### Analiza el ejemplo 4.5:
[Ejemplo 4.5](https://natureofcode.com/particles/#example-45-a-particle-system-with-inheritance-and-polymorphism)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

### Analiza el ejemplo 4.6:
[Ejemplo 4.6](https://natureofcode.com/particles/#example-46-a-particle-system-with-forces)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

### Analiza el ejemplo 4.7:
[Ejemplo 4.7](https://natureofcode.com/particles/#example-47-a-particle-system-with-a-repeller)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?


