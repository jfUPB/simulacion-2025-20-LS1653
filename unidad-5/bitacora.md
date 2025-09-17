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

#### Constructor

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

#### run()
   ``` js
     let gravity = createVector(0, 0.05);
     this.applyForce(gravity);
     this.update();
     this.show();
   ```
   Define una fuerza constante de gravedad hacia abajo.
   Aplica esa fuerza, actualiza movimiento, y dibuja.

#### applyForce(force)
   ``` js
     this.acceleration.add(force);
   ```
   Cualquier fuerza (gravedad, viento, etc.) se suma a la aceleración.

#### update()
   ``` js
      this.velocity.add(this.acceleration);
      this.position.add(this.velocity);
      this.lifespan -= 2;
      this.acceleration.mult(0);
   ```
   Se actualiza el movimiento según física:
         vel = vel + acc
         pos = pos + vel
  La vida útil baja en 2 cada frame.
  La aceleración se resetea → para que solo afecte en el frame donde se aplica.

#### show()
   ``` js
     stroke(0, this.lifespan);
     fill(127, this.lifespan);
     circle(this.position.x, this.position.y, 8);
   ```
   Se dibuja la partícula como un círculo de radio 8.
   Usa lifespan como transparencia (alpha). -> Cuanto más cerca de morir, más transparente se vuelve.

#### isDead()
   ``` js
     return (this.lifespan < 0.0);
   ```
   Cuando la vida llega a 0, se elimina.

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas
Con: 
``` js 
particles.push(new Particle(width / 2, 20));
```
Cada frame (draw()) se crea una nueva partícula.
Esto significa que el sistema va generandocontinuamente.
El número de partículas no es fijo, sino que depende de cuántas mueren en comparación de cuántas se crean.

#### Desaparición de partículas
con:
``` js
for (let i = particles.length - 1; i >= 0; i--) {
  let particle = particles[i];
  particle.run();
  if (particle.isDead()) {
    particles.splice(i, 1);
  }
}
```
Se recorre el arreglo de atrás hacia adelante (para no desordenar índices al borrar).
Cada partícula revisa si su lifespan es menor a 0 (isDead()).
Si está muerta -> se elimina con splice(i, 1).
Así, no se acumulan partículas en la memoria.

#### Gestión de memoria en esta simulación
Creación: Las partículas se van agregando con push().
Eliminación: Se van borrando del arreglo con splice().
Con esto, el sistema mantiene solo partículas activas -> optimiza uso de RAM.

#### Experimento

### Analiza el ejemplo 4.4:
[Ejemplo 4.4](https://natureofcode.com/particles/#example-44-a-system-of-systems)

#### Analisis 

1. Creación de partículas

En cada draw() se crea una nueva partícula, esto significa que el sistema esta en constante crecimiento, pero no infinito, ya que hay un mecanismo de eliminación.


#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas

En cada ciclo (draw()):
    ``` js

    for (let emitter of emitters) {
     emitter.run();
     emitter.addParticle();
     }
   ```

Cada emisor (Emitter) genera una nueva partícula en su origin con addParticle().

Esto ocurre continuamente mientras la simulación corre → hay un flujo constante de partículas.

#### Desaparición de partículas

#### Gestión de memoria en esta simulación

#### Experimento

### Analiza el ejemplo 4.5:
[Ejemplo 4.5](https://natureofcode.com/particles/#example-45-a-particle-system-with-inheritance-and-polymorphism)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Experimento

### Analiza el ejemplo 4.6:
[Ejemplo 4.6](https://natureofcode.com/particles/#example-46-a-particle-system-with-forces)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas

#### Desaparición de partículas

#### Gestión de memoria en esta simulación

#### Experimento

### Analiza el ejemplo 4.7:
[Ejemplo 4.7](https://natureofcode.com/particles/#example-47-a-particle-system-with-a-repeller)

#### Analisis 

#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

#### Creación de partículas

#### Desaparición de partículas

#### Gestión de memoria en esta simulación

#### Experimento





