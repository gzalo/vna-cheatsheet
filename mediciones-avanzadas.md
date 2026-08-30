# Mediciones avanzadas

[Volver al índice](README.md)

Estas mediciones requieren _fixtures_, una calibración más cuidadosa o análisis adicionales.

## Impedancia de salida

### Mirando el puerto de salida en S11
Para un _dispositivo pasivo_, o un activo **apagado**, conectar a su entrada una impedancia típica, y medir S11 conectando el puerto 1 a la salida. El Smith chart muestra la impedancia que presenta ese puerto.

Tener en cuenta que esto no representa necesariamente la impedancia de salida de un equipo activo funcionando.

### Con el equipo activo mediante un puente
La impedancia de salida de un equipo activo se mide aplicando una pequeña señal de prueba en su salida mientras funciona, y separando la señal de prueba de su propia salida mediante un puente, acoplador o fixture adecuado. [Este artículo de NXP](https://www.nxp.com/docs/en/application-note/AN1526.pdf) describe técnicas de medición más completas.

## Cristales / Filtros resonantes SAW / Factor Q
### Midiendo S21 a través del dispositivo
Conectar el cristal o filtro entre los dos puertos, usando la red de adaptación indicada por el fabricante si corresponde. Buscar la frecuencia de máxima transmisión $f_0$, la pérdida de inserción y los puntos $f_1$ y $f_2$ que estén 3 dB por debajo de la misma. 

$$Q\approx\frac{f_0}{f_2-f_1}$$

Recordar que el acoplamiento y las terminaciones pueden cambiar el ancho de banda y, por tanto, el $Q$ medido. 

### Midiendo S11
Conectar el resonador/cristal al puerto 1 y buscar los cambios de impedancia: la resonancia serie suele verse como un mínimo de impedancia y la antirresonancia como un máximo. 

## Constante de propagación
### Midiendo la periodicidad de S11
(completar)

### Midiendo fase de S21
(completar)

## Choques de modo común
### Midiendo la impedancia de modo común en S11
En un _choke_, conectar ambos devanados en serie de modo que las corrientes creen flujo magnético en el mismo sentido (conexión de modo común), y medir S11 con un fixture corto. Para un _choke_ con conectores coaxiales se necesita un fixture que fuerce la corriente de prueba por la parte exterior de la malla.

Esto permite ver para qué rango de frecuencias la impedancia es alta (lo que implica un mejor rechazo a las corrientes de modo común) y comparar núcleos, cantidad de vueltas y materiales.

## Constante dieléctrica de cable o PCB
### Calculándola a partir de la velocidad de propagación
(completar)

## Transferencia de filtros activos/Amplificadores
### Midiendo S21 a pequeña señal
Alimentar el circuito según su especificación, bloquear la continua hacia ambos puertos con capacitores o y medir S21 con potencia suficientemente baja para mantener operación lineal. Usar atenuadores si hace falta proteger el receptor del VNA o el circuito a medir.

### Repitiendo S21 para distintos niveles
Hacer varios barridos aumentando la potencia de salida del VNA (o retirando atenuadores) y comparar la ganancia. La caída respecto de la ganancia de pequeña señal permite estimar el inicio de compresión (no linealidad).

## Retardo de grupo
### Derivándolo de la fase de S21
Medir la fase de S21 y derivarla respecto de la frecuencia. Muchos VNA muestran directamente el retardo de grupo en el formato _Delay_. Lo típico es medirlo en la banda de paso de filtros, donde la fase debería ser aproximadamente lineal y el retardo de grupo constante. 

## Cables con roturas (TDR)
### Transformando S11 al dominio del tiempo
Calibrar en el extremo del cable, medir S11 con el rango de frecuencias más amplio posible y usar la función de transformación temporal/IFFT del VNA o exportar los datos. El nanovna-saver también permite hacer una transformación similar. 

Una rotura se comporta como una reflexión positiva (tendiendo a abierto); un corto, como una negativa.

### Observando el rizado periódico en frecuencia
Una discontinuidad a distancia $d$ produce ondulaciones en S11 cuya periodicidad se relaciona aproximadamente con $\Delta f=v_p/(2d)$. Medir esa separación y despejar $d$.

## Aislación entre puertos
### Midiendo la transferencia no deseada en S21
Conectar el puerto excitado y el puerto que debería estar aislado al VNA, y terminar todos los demás puertos del dispositivo en cargas de 50 $\Omega$. Medir S21 en dB: cuanto más negativo sea, mayor es la aislación. Esto se puede usar en relés, _switches_, duplexores, combinadores y más.

## Divisores y combinadores de potencia
### Midiendo pérdida, balance y aislación
Conectar la entrada al puerto 1 del VNA y una salida al puerto 2; terminar las demás salidas en 50 $\Omega$. Repetir para cada salida y comparar S21, S11 y S22 (si el equipo lo soporta). Para medir la aislación entre salidas, terminar la entrada y medir S21 entre el par de salidas.

## Atenuadores
### Midiendo S21 y las reflexiones de ambos lados
Calibrar en los dos conectores del atenuador y medir S21 para obtener la atenuación y su planitud en frecuencia. Medir S11 y S22 (si equipo lo soporta) para comprobar la adaptación.

## Acopladores direccionales y _RF taps_
### Midiendo acoplamiento, pérdida de paso y directividad
En un acoplador de cuatro puertos, realizar cada medición terminando en $50\ \Omega$ los puertos no utilizados.

- Medir S21 entre entrada y puerto de paso para calcular pérdida de paso.
- Medir S21 entre entrada y puerto acoplado (o tap) para calcular el acoplamiento.
- Medir S21 entre puerto de paso y puerto acoplado para determinar el aislamiento. La directividad se obtiene como la diferencia entre el aislamiento y el acoplamiento, en dB.
- Medir S11 en cada puerto para comprobar la adaptación.
