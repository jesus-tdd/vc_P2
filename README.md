## Práctica 2. Funciones básicas de OpenCV


### Tarea 1

> Realiza la cuenta de píxeles blancos por filas (en lugar de por columnas).
> Determina el valor máximo de píxeles blancos para filas, maxfil, mostrando el número de filas y sus respectivas posiciones, con un número de píxeles blancos mayor o igual que 0.90*maxfil.
> Resalta con alguna primitiva gráfica en la imagen de Canny las filas que cumplen dicha condición.

Los píxeles por fila se han obtenido normalizando la suma de los píxeles de cada fila,
tal como se demostraba en el ejemplo de clase.

Se han usado funciones de *numpy* para encontrar la fila con más píxeles blancos,
así como las filas cuya cantidad de píxeles blancos era >=90% con respecto al máximo.

Dichas filas se han representado gráficamente en la imagen resultado de Canny mediante líneas rojas.
Para esto ha sido necesario convertir la imagen de escala de grises a RGB.


### Tarea 2

> Aplica umbralizado a la imagen resultante de Sobel (convertida a 8 bits), y posteriormente realiza el conteo por filas y columnas similar al realizado en el ejemplo con la salida de Canny de píxeles no nulos.
> Calcula el valor máximo de la cuenta por filas y columnas, y determina las filas y columnas por encima del 0.90*máximo.
> Remarca con alguna primitiva gráfica dichas filas y columnas sobre la imagen del mandril. 
> Visualiza los resultados obtenidos para la imagen (o una de tu elección) con Canny y Sobel tras umbralizar.
> ¿Cómo se comparan los resultados obtenidos a partir de Sobel y Canny?

Esta tarea se ha realizado de manera homónima a la anterior, pero cambiando la imagen inicial por el resultado de Sobel.

La conversión a 8 bits de la imagen se ha realizado con *cv2.convertScaleAbs()*.
Por su parte, el umbral se le ha aplicado con *cv2.threshold()*.
El umbralizado ha sido binario, quedando en blanco los píxeles superiores a 128 y el resto en negro.

En el código se ha incluido el análisis de las columnas del resultado de Canny.


### Tarea 3.

> Tras ver los vídeos
> [My little piece of privacy](https://www.niklasroy.com/project/88/my-little-piece-of-privacy),
> [Messa di voce](https://youtu.be/GfoqiyB1ndE?feature=shared)
> y
> [Virtual air guitar](https://youtu.be/FIAmyoEpV5c?feature=shared)
> proponer un demostrador reinterpretando la parte de procesamiento de la imagen, 
> tomando como punto de partida alguna de dichas instalaciones.


#### Versión 1

Se trata de una implementación sencilla del vídeo 
"[My little piece of privacy](https://www.niklasroy.com/project/88/my-little-piece-of-privacy)".

El movimiento se detecta mediante la diferencia de los fotogramas captados en la webcam.

Las columnas que deben ser tapadas por la cortina se calculan de forma homónima al procedimiento de los apartados anteriores,
pero usando el valor máximo (más a la derecha) y mínimo (más a la izquierda) en lugar de todos los valores encontrados.
Esta vez, la cantidad de blanco en la columna debe ser mayor o igual al 20% del máximo, frente al 90% usado en las tareas 1 y 2.

Se trabaja sobre cada fotograma en espejo.

#### Versión 2

Versión más divertida de lo implementado anteriormente.
Se calcula el punto medio del movimiento y se mapea la posición al fotograma correspondiente de un gif.