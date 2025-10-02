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



Reynolds diseñó un sistema donde agentes simples (los boids) seguían tres reglas básicas: separación, alineamiento y cohesión.

Para implementar estas reglas, necesitaba que los agentes se movieran hacia direcciones deseadas de manera realista. Allí surge la idea de la steering force.

En lugar de teletransportar o cambiar instantáneamente la velocidad de un boid, Reynolds definió que cada comportamiento (seguir, huir, evitar obstáculos) genera una fuerza de dirección, y la suma de todas esas fuerzas determina el movimiento final del agente.

Este enfoque fue revolucionario porque:

Dio origen a la simulación realista de enjambres, bandadas y cardúmenes.

Influyó en animación por computadora, videojuegos, robótica y realidad virtual.

Se convirtió en la base para muchos algoritmos modernos de inteligencia artificial en entornos simulados.
## Actividad 3

## Actividad 4

## Actividad 5



