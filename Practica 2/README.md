
# Compass
![](/img/Compass.png)

Sensor que mide la posición relativa con el norte magnético. El nodo compass simula una brújula de 1, 2, o 3 ejes. El nodo devuelve un vector que indica la dirección norte especificada por el campo “coordinateSystem” del nodo “Worldinfo”.

## Forma de uso y configuraciones comunes en WEBOTS

* **lookupTable**: Este campo opcionalmente especifica una tabla de consulta que puede ser usada para mapear cada componente del vector (entre -1 y 1) para mostrar valores de salida específicos. Por defecto esta tabla está vacía por lo que no hay ningún mapeo aplicado.
* **xAxis, yAxis, zAxis**: Si uno de estos campos tiene el valor FALSE, no se calculará el elemento del vector correspondiente y se devolverá NaN . El valor por defecto es que los tres ejes están habilitados . La modificación de estos campos permite elegir entre una brújula digital de uno, dos o tres ejes y especificar qué ejes se utilizarán.
* **resolution**: Este campo permite definir la resolución del sensor, la resolución es el cambio más pequeño que es capaz de medir. Establecer este campo a -1 (por defecto) significa que el sensor tiene una resolución "infinita" (puede medir cualquier cambio infinitesimal). Este campo acepta cualquier valor en el intervalo (0.0, inf).

![](img/importable_externproto_Compass)

## Código

Se añade la librería math para poder calcular el arcotangente para que señale al norte.

![](/img/import_Compass)

<div class="pull-left"><img/init_Compass/></div> <div class="pull-right"><img/operation_Compass/></div>

## Diferencias con la realidad

La simulación no recibe interferencias ni genera ruido al moverse (oscilaciones de arriba abajo) y tampoco busca el norte generando una velocidad de movimiento que se tendrá que rectificar (generando ruido de otra manera). Por otro lado, el robot en la simulación al dar una vuelta completa, la brújula se “reinicia” dando una vuelta entera para volver a señalar el norte en su posición inicial (posiblemente sea un fallo del programa).

Ni que decir tiene que al simularse, este no tiene coste, mientras que en la realidad si.

---

# GPS
![](/img/GPS)

El nodo GPS se utiliza para modelar un sensor de posicionamiento global (GPS) que puede obtener información sobre su posición absoluta desde el programa del controlador.

## Forma de uso y configuraciones comunes en WEBOTS

* **type**: Este campo define el tipo de tecnología GPS utilizada como "satélite" o "láser" (actualmente se ignora).
* **accuracy**: Este campo define la precisión del GPS, es decir, la desviación estándar (expresada en metros) del ruido gaussiano añadido a la posición.
* **noiseCorrelation**: El modelo de ruido es entonces aproximado por un fenómeno gaussiano-correlacionado, que captura por ejemplo los fenómenos de deriva presentes en el GPS. El valor debe estar entre 0 y 1 y representa cuánto influye el ruido de hace 1 segundo en el ruido actual, 0 significa que no hay influencia y 1 significa que el ruido será constante. 
* **resolution**: Este campo permite definir la resolución del sensor, la resolución es el cambio más pequeño que es capaz de medir. Establecer este campo a -1 (por defecto) significa que el sensor tiene una resolución "infinita" (puede medir cualquier cambio infinitesimal). Este campo acepta cualquier valor en el intervalo (0.0, inf).
* **speedNoise**: Este campo define la desviación estándar (expresada en metros) del ruido gaussiano añadido a las medidas de velocidad del GPS.
* **speedResolution**: Este campo define la resolución de las mediciones de velocidad, la resolución es el menor cambio de velocidad que el GPS es capaz de medir. Establecer este campo a -1 (por defecto) significa que el sensor tiene una resolución "infinita" (puede medir cualquier cambio infinitesimal). Este campo acepta cualquier valor en el intervalo (0.0, inf).

![](/img/importable_externproto_GPS)

## Código

<div class="pull-left"><img/import_GPS/></div> <div class="pull-right"><img/init_GPS/></div>

![](https://img/operation_GPS)

Con el comando “format ( ‘variable’, ‘.6f’)” se consigue poner 6 decimales para que no salgan tantos por pantalla y así resulte más sencillo de ver.

![](https://img/console_GPS)

Lo que sale por la consola indicando en qué posición se encuentra el robot en grados, pasándolo luego a minutos y segundos para darlo con mayor exactitud.

## Diferencias con la realidad

No requieres de conexión a Internet para recibir los datos de los satélites, la posición es más exacta que la obtenida en el gps básico que todos utilizamos, obviamente los hay más potentes y precisos. También añadir que en la simulación, la resolución de la posición es inmediata, en la vida real (por muy rápido que funcione) tardará un tiempo (pequeño, pero existente).

Ni que decir tiene que al simularse, este no tiene coste, mientras que en la realidad si.

---

# RotationalMotor
![](https://img/Motor)

Se puede usar un nodo RotationalMotor para alimentar una HingeJoint o una Hinge2Joint para producir un movimiento de rotación alrededor del eje elegido.

![](https://img/RotationalMotor)

La forma más común de controlar un motor es el control de posición directo (control de posición). El usuario define la posición de destino utilizando la función wb_motor_set_position, luego el controlador P lleva la velocidad, la aceleración y la fuerza requerida del motor a la posición de destino.

Los motores también se pueden usar para controlar la velocidad en lugar de la posición. Esto es facilitado por dos llamadas a la función: en primer lugar se debe llamar a la función wb_motor_set_position con INFINITY (#include <math.h>, usada en python como float(‘+inf’)) ) como parámetro de posición. A continuación, se debe especificar la velocidad deseada, que puede ser positiva o negativa, llamando a la función wb_motor_set_velocity. Esto iniciará un movimiento continuo del motor con la velocidad deseada, teniendo en cuenta la aceleración y la fuerza del motor especificadas.

Si varios motores, ya sea RotationalMotor , LinearMotor o una combinación de ambos, comparten la misma estructura de nombre y pertenecen al mismo Robot, entonces se considera que están acoplados. Cuando se da una orden a un motor acoplado, por ejemplo usando las funciones wb_moto_set_position o wb_motor_set_velocity, el mismo comando se transmite a todos los demás. Aunque cada motor acoplado recibe los mismos comandos, lo que realmente imponen los motores depende de sus propios valores multiplicadores.


## Forma de uso y configuraciones comunes en WEBOTS

* El campo **name**: especifica el identificador de nombre del dispositivo motor. Este es el nombre al que wb_robot_get_device se refiere la función. Por defecto es "rotational motor".
* El campo **maxTorque**: especifica tanto el límite superior como el valor predeterminado para el par disponible del motor y se expresa en newton metro . Cuando se usa en el control de velocidad, este par máximo siempre se aplica hasta que se alcanza la velocidad objetivo. El valor de maxTorque siempre debe ser cero o positivo un pequeño maxTorque.

![](img/importable_externproto_Motor)

## Código

![](https://img/import_Motor)

<div class="pull-left"><img/init_Motor/></div> <div class="pull-right"><img/operation_Motor/></div>

## Diferencias con la realidad

Es más común que ocurran fallos de fábrica en la realidad con este componente respecto a otros, y por ello, en la simulación se trabaja en condiciones ideales. La manipulación es más sencilla en la simulación, ya que en la realidad los motores pueden ser muy grandes y pesados.

Ni que decir tiene que al simularse este no tiene coste, mientras que en la realidad si, por lo que se pueden realizar simulaciones extremas que no harías en la vida real.
