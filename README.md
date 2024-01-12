## PROBLEMA DE LA PROBABILIDAD DE ESCAPAR DEL LABERINTO

El *algoritmo de cálculo* de la probabilidad de que la rana escape del laberinto no es único, hay muchos que variarán según su nivel de profundidad y la lógica usada para hacerlo.

Para la elaboración de nuestro algoritmo hemos decidido aplicar *la regla de Laplace*, la cual nos permite calcular la probabilidad a través del número de casos de éxito. 

Hemos definido el número de intentos, fijándolo a un número elevado para tener una mayor precisión en la probabilidad. Además, se considerará que UN INTENTO HA TERMINADO si:
* Llega a una _SALIDA_, que en tal caso será un _**CASO DE ÉXITO**_
* Llega a una _MINA_, que en tal caso no se contabilizará en los casos de éxito y procederá a realizar el siguiente intento
* Realiza el número _MÁXIMO DE ITERACIONES_; que es una medida de seguridad para evitar que el programa colapse o para tratar de evitar bucles infinitos.

Para este cálculo hemos tenido que tener en cuenta lo siguiente:

- Asignar un valor aleatorio a cada movimiento (arriba, abajo, izquierda, derecha).
- Comprobar si ese movimiento elegido era un movimiento posible.
- Establecer la nueva posición de la rana.
- En dicha nueva posición, comprobar si se encontraba encima de una mina, una salida, o un túnel.
- Realizar la acción correspondiente según sea correspondiente


### ¿Dónde puede moverse?
Para comenzar, había que tener en cuenta que la rana solo puede dirigirse *hacia sus cuatro casillas adyacentes*, y que la probabilidad de que se moviera a cada una de ellas era la misma.
Sin embargo *no podrá moverse* si en la dirección en la que pretende moverse _hay un muro_ o estaba _en el borde del laberinto_.
Teniendo esto en cuenta comenzamos imaginando uno de los casos más sencillos:
"""
E-S
"""
Este laberinto tiene dimensiones 3 x 3 y la probabilidad de que llegue a la salida será del 100% ya que no existe la opción de que se encuentre con una mina que le haga perder.
### ¿Qué hacer en ese nuevo movimiento?

Una vez establecida la nueva posición de la rana, habrá que comprobar si se encuentra sobre un espacio vacío, sobre un túnel, sobre una mina, o sobre una salida.

*ESPACIO VACIO*

En caso de que sea un espacio vacío procederá a moverse a otro lugar aleatorio siempre que no exceda el número máximo de iteraciones

*TÚNEL*

En el caso de que se encuentre sobre un túnel, mirará las coordenadas de salida correspondiente.
Se establecerá la nueva posición de la rana con la correspondiente a la salida del túnel.

*MINA*

En el caso de que se encuentre sobre una mina, procederá a terminar dicho intento.
Se establecerá de nuevo la posición inicial y comenzará el siguiente intento.

*SALIDA*

En el caso de que se encuentre sobre la salida, procederá a terminar dicho intento con la peculiaridad de que se sumará en uno el número de intentos válidos, que servirá para después calcular la probabilidad

### Cálculo de Probabilidad

Para finalizar, se calculará la probabilidad de que escape haciendo el cociente entre el **número de intentos válidos** _entre_ el **número de intentos totales**
