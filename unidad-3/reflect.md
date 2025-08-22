# Unidad 3


## 🤔 Fase: Reflect

### Actividad 11

#### Parte 1: recuperación de conocimiento (Retrieval Practice)

##### Escribe la ecuación vectorial de la segunda ley de Newton y explica cada uno de sus componentes.
###### Primera respuesta: 
Creo conocer la ecución de siempre, pero la vectorial no la recuerdo.

###### Segunda respuesta (despues de repasar más): 
F = m(a)

Siendo:

F = Fuerza neta (vector que representa la suma de todas las fuerzas que esten afectando).
m = Masa del objeto (escalar que indica la resistencia al cambio de movimiento).
a = Aceleración (vector que indica el cambio de la velocidad en el tiempo).

##### ¿Por qué es necesario multiplicar la aceleración por cero en cada frame del método update()?
###### Primera respuesta: 
Esto se hace para que cuando se saque la velocidad en un frame nuevo, esta velocidad no tome un valor acumulado en el tiempo en la aceleración, osea en el caso de tener un aceleración de dos y una velocidad de 0 en el frame 0, en el frame 1 seria velocidad 2 y en el frame 3 en vez de ser la velocidad de 4 sera 6, debido a quese esta guardando en el tiempo los valores de aceleración y se van acumulando.

###### Segunda respuesta (despues de repasar más): 
La aceleración se reinicia cada frame porque esta depende únicamente de las fuerzas aplicadas en ese instante. Si no se reinicia, se acumularían fuerzas viejas que ya no están actuando, lo que distorsionaría la simulación.

##### Explica la diferencia entre paso por valor y paso por referencia cuando aplicamos fuerzas a un objeto.
###### Primera respuesta: 
El paso por valor es para variables primitivas y este paso por valor cambia la información guardada en dicha variable en este caso puede ser la velocidad, el valor de la fricción dependiente del suelo; por el otro lado el paso por referencia es para vectores, arrays, etc, en donde no se reemplaza el valor que se guarda sino que lo modifica en un lapzo de tiempo de ejecución lo cual da como resultado que a la hora de usar un objeto podamos darle a un vector de movimiento un cambio direccional o un desenzo en su velocidad o aceleración.

###### Segunda respuesta (despues de repasar más): 
Paso por valor: Se crea una copia de la variable. Si modificamos esa copia dentro de una función, el original no cambia. Ejemplo: pasar un número que representa la fricción como parámetro.

Paso por referencia: No se copia la variable, sino que se pasa la dirección de memoria. Así, cualquier modificación afecta directamente al objeto original. Ejemplo: al pasar un vector de velocidad por referencia, la función puede modificar su dirección o magnitud y el cambio se refleja en el objeto real.

##### ¿Cuál es la diferencia conceptual entre modelar fuerzas (como fricción, gravedad) y simplemente definir algoritmos de aceleración?
###### Primera respuesta: 
La verdad no estoy seguro de como responder a esta pregunta.

###### Segunda respuesta (despues de repasar más): 
Modelar fuerzas: Significa usar las leyes físicas (como la gravedad, fricción, empuje) para calcular aceleraciones y cambios de movimiento. Osea es tratar de recrear o basarse en la física real: se suman fuerzas, se aplica 𝐹=𝑚(𝑎) y de ahí sale la aceleración.

Algoritmos de aceleración: Son reglas artificiales que definen cómo cambia la velocidad sin necesidad de una fuerza. Por ejemplo: “cada frame aumenta la velocidad en 1” no depende de una fuerza física, sino de una instrucción programada.
#### Parte 2: reflexión sobre tu proceso (Metacognición)

##### ¿Qué fue lo más desafiante en la Actividad 10 (problema de los n-cuerpos)? ¿El concepto creativo, la implementación de las fuerzas o la integración de la interactividad?


##### ¿Las fuerzas que modelaste produjeron el comportamiento que esperabas? Describe un momento “sorpresa” (esperado o inesperado) durante el desarrollo.


##### ¿Cómo ha cambiado tu forma de pensar sobre la “física” en el arte generativo después de esta unidad?


##### Si tuvieras una semana más, ¿Qué otras fuerzas te gustaría modelar o cómo mejorarías tu simulación del problema de los n-cuerpos?

