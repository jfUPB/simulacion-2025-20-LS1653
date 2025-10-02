# Evidencias de la unidad 6

## Actividad 1

### Captura 1

<img width="737" height="548" alt="image" src="https://github.com/user-attachments/assets/cefde4f7-af6c-47f1-8a83-f4a807ba080f" />

Unfenced Existence, 2018

### ¿Que me inspira su trabajo?

Este trabajo me inspira a tratar de crear paisajes, esto debido a que al ver su obra me trae a la mente la sensación de apreciar mi entorno ya sea un atardecer en lo alto del cielo o un pasto alto pintado por los colores generados por las luces naturales.

### Captura 2

<img width="737" height="737" alt="image" src="https://github.com/user-attachments/assets/693e9c47-2520-4ba8-bb43-85b1891b81c7" />

pi/4

### ¿Que me inspira su trabajo?

Al ver esta obra me trae a la mente de la pelicula matrix pues la obra se muestra artificial/robotica y este tipo de diseño me inspir a tratar de crear algún tipo de cableado que tenga una forma enrevezada y llamativa que transmita la sensación de algo más haya de nuestro conocimiento tecnologico.

# Seek: Investigación

## Actividad 2

### ¿Qué es una fuerza de dirección (steering force)?
Una fuerza de dirección es un vector que ajusta el rumbo de un agente (objeto) hacia un objetivo deseado, pero lo hace de forma suave y controlada, en lugar de cambiar bruscamente su velocidad.

Se calcula como la resta entre la velocidad deseada (la dirección y magnitud a la que el agente “quisiera” moverse) y la velocidad actual del agente.

Fórmula:

steering = desired − velocity

desired es el vector hacia la meta (normalizado y escalado a la velocidad máxima).

velocity es el  vector de movimiento actual del agente.

Este steering se limita a una fuerza máxima y se aplica como una aceleración sobre el agente.
El efecto es que el agente no gira instantáneamente, sino que corrige poco a poco su dirección imitando como lo haria algo vivo.

### ¿Qué diferencia tiene este tipo de fuerza con las que ya hemos estudiado en el contexto de la simulación de agentes?
Hasta ahora, en las simulaciones con agentes y partículas hemos visto fuerzas “físicas directas”, como:

- Gravedad.

- Atracción/repulsión.

- Viento.

- Fricción.

- etc.

Estas fuerzas se aplican sobre el agente (objeto) de manera “externa” y modifican su aceleración y movimiento sin un propósito definido: simplemente obedecen a la física del entorno.

En comparación, la steering force:

Es una fuerza intencional: no busca obedecer una ley física universal, sino guiar el comportamiento del agente (objeto) hacia un objetivo (ej: seguir, huir, alinearse, evitar choques).

Actúa como una capa de control sobre las fuerzas físicas ya conocidas, introduciendo la “decisión” o el “comportamiento”.

Permite la creación de movimientos más orgánicos y naturales, que se parecen a los seres vivos.

### ¿Qué relación tiene la steering force con Craig Reynolds y su trabajo en simulación de comportamiento animal?
La relación es directa, ya que la steering force fue el concepto clave introducido por Craig Reynolds en 1987 con su modelo de [Boids](https://en.wikipedia.org/wiki/Boids) (simulación de bandadas de pájaros). 

Reynolds diseñó un sistema donde agentes simples (los boids) seguían tres reglas básicas: separación, alineamiento y cohesión. Para implementar estas reglas, necesitaba que los agentes se movieran hacia direcciones deseadas de manera realista. Allí surge la idea de la steering force.

En lugar de teletransportar o cambiar instantáneamente la velocidad de un boid, Reynolds definió que cada comportamiento genera una fuerza de dirección, y la suma de todas esas fuerzas determina el movimiento final del agente.

Este enfoque fue revolucionario ya que dio origen a la simulación realista de enjambres, bandadas y cardúmenes e influyó en animación por computadora, videojuegos, robótica y realidad virtual. Basicamente se convirtió en la base para muchos algoritmos modernos de inteligencia artificial en entornos simulados.

## Actividad 3

### Estructura del campo de flujo

El campo de flujo está representado en la clase FlowField y se usa una matriz bidimensional (this.field) de vectores (p5.Vector):

``` js
this.field = new Array(this.cols);
for (let i = 0; i < this.cols; i++) {
  this.field[i] = new Array(this.rows);
}
```
Cada celda de la matriz corresponde a una porción del canvas (un rectángulo definido por la resolución). En cada celda se almacena un vector de dirección que los agentes (vehicles) seguirán.

ej: 

<img width="1296" height="401" alt="image" src="https://github.com/user-attachments/assets/817865a4-cc87-4045-b13a-fce4c26f3b88" />

#### Inicialización de vectores:
En init(), los vectores se generan con Perlin noise para producir una textura suave de direcciones:

``` js
let angle = map(noise(xoff, yoff), 0, 1, 0, TWO_PI);
this.field[i][j] = p5.Vector.fromAngle(angle);
```

### Comportamiento del agente (Vehicle.follow(flow))
En la clase Vehicle, la función follow(flow) implementa el algoritmo de Reynolds de seguimiento de un campo:

#### a) Identificar vector en su posición actual:
El vehículo consulta el vector del campo en su ubicación:

``` js
let desired = flow.lookup(this.position);
```
lookup() convierte la posición en índices de la cuadrícula.
Esto se hace con:

``` js
let column = constrain(floor(position.x / this.resolution), 0, this.cols - 1);
let row = constrain(floor(position.y / this.resolution), 0, this.rows - 1);
return this.field[column][row].copy();
```

#### b) Calcular velocidad deseada:
Ese vector se escala a la velocidad máxima:


``` js
desired.mult(this.maxspeed);
```

#### c) Calcular steering force:
El steering es la diferencia entre velocidad deseada y actual:

``` js
let steer = p5.Vector.sub(desired, this.velocity);
steer.limit(this.maxforce);
this.applyForce(steer);
```
Con esto, el vehículo ajusta su dirección hacia el vector del campo.

### Parámetros clave

#### Resolución del campo de flujo: this.resolution en FlowField (en este caso 20).
Define el tamaño de cada celda de la cuadrícula, mientras menor la resolución, más detallado es el campo.

#### Velocidad máxima: this.maxspeed en Vehicle (dada en el constructor con random(2,5)).
Controla la rapidez máxima con la que se mueve cada agente.

#### Fuerza máxima: this.maxforce en Vehicle (constructor con random(0.1,0.5)).
Limita el giro brusco del agente, mientras menor sea el movimiento sera más suave.

### Modificación realizada
Mi modificación fue: alterar la resolución del campo de flujo para hacerlo mucho más fino

Código modificado en setup():
``` js
flowfield = new FlowField(4);
```

Efecto observado:

Con resolución 20, el campo tiene celdas grandes, los vehículos siguen vectores más generales, con trayectorias amplias y fluidas.

Con resolución 4, el campo tiene muchas más celdas pequeñas, los vectores cambian más seguido, haciendo que los agentes zigzagueen más y sus trayectorias sean mucho más intrincadas.

El movimiento colectivo se vuelve más detallado y turbulento, casi como un enjambre de insectos.
<img width="801" height="300" alt="image" src="https://github.com/user-attachments/assets/3a4808b8-87fd-449d-9523-a3388945dff8" />

## Actividad 4



## Actividad 5




