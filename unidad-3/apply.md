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

#### Captura una imagen representativa de tu ejemplo.





