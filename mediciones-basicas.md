# Mediciones básicas

[Volver al índice](README.md)

## Impedancia de entrada de un equipo/filtro

Conectar el equipo o filtro al puerto 1 y medir S11 para el rango de frecuencias de interés. Usar el formato de impedancia o el diagrama de Smith para obtener la impedancia de entrada en función de la frecuencia.

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: medición de impedancia S11" src="diagramas/rendered/s11-impedancia.svg" width="50%"/>
</p>

Recordar que esta medición es más precisa cuando el dispositivo está cerca de la impedancia característica del VNA, es decir, $Z\approx50\ \Omega$. 

También es muy importante recordar que la potencia de salida del VNA (-20 a 0 dBm dependiendo del modelo) puede llegar a modificar el comportamiento del equipo o filtro medido. En esos casos, es recomendable reducir el nivel de salida o incluir un atenuador antes del dispositivo. 

Recordar no conectar al VNA un circuito con tensiones continuas (ej, un filtro con bias tee), o algo que esté transmitiendo potencia sin las protecciones adecuadas. Internamente el VNA tiene una terminación de 50 ohms que soporta muy baja potencia.

## Inductores
### Midiendo S11 directamente
Conectar el inductor al puerto 1 usando un _fixture_ (pueden ser unas puntas tipo cocodrilo, lo más corto posible) y medir la impedancia serie en una frecuencia de interés. Por debajo de la frecuencia de autorresonancia, se puede estimar:

$$L=\frac{X}{2\pi f}$$

La mayoría de los equipos ya muestran el valor de $L$ directamente. La parte real $R$ permite estimar las pérdidas del inductor y, también aproximar $Q \approx X/R$.

### Haciéndolo resonar con un capacitor conocido
Conectar el inductor en serie con un capacitor de valor conocido y buscar la frecuencia de resonancia $f_r$ en S11. Esta se obtiene buscando el mínimo de la magnitud de S11, o el punto donde la fase cruza por cero.

Ignorando el comportamiento parásito, usando esa frecuencia se puede estimar:

$$L=\frac{1}{(2\pi f_r)^2C}$$

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: resonador LC serie medido en S11" src="diagramas/rendered/resonador-serie.svg" width="50%"/>
</p>

Se puede hacer lo mismo pero con los componentes en paralelo, y encontrar el punto de máxima magnitud de S11, o cuando cruza 180º. Medir en paralelo no es tan preciso como en serie.

## Capacitores
### Midiendo S11 directamente
Conectar el capacitor con un _fixture_ corto. En la región capacitiva, en una frecuencia de interés, calcular:

$$C=\frac{1}{2\pi fX}$$

La mayoría de los equipos ya muestran el valor de $C$ directamente. La resistencia serie equivalente puede obtenerse aproximadamente de $R$.

### Haciéndolo resonar con un inductor conocido
Al igual que el caso del inductor, se puede armar un circuito resonante con un inductor conocido y buscar la frecuencia de resonancia $f_r$ en S11. Entonces:

$$C=\frac{1}{(2\pi f_r)^2L}$$

## Stubs abiertos/cerrados
### Usando S11 
Conectar el stub al puerto 1 y barrer varias resonancias. Un abierto y un corto ideal reflejan casi toda la señal, un abierto se ve como corto de entrada cerca de $\lambda/4$, mientras que un corto se ve como abierto. El patrón se repite cada $\lambda/2$. La separación entre resonancias equivalentes es aproximadamente $\Delta f=v_p/(2l)$. De esta forma, sabiendo el largo físico del stub y midiendo $\Delta f$, se puede estimar la velocidad de propagación $v_p$.

### Insertándolo como elemento de un circuito y midiendo S21
Conectar el stub en paralelo o serie entre los puertos. De esta forma se puede medir su comportamiento como filtro, ver la frecuencia central y el ancho de banda.

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: stub en paralelo medido en S21" src="diagramas/rendered/stub-s21.svg" width="50%"/>
</p>

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: stub en serie medido en S21" src="diagramas/rendered/stub-s21-serie.svg" width="50%"/>
</p>

## Antenas
### Midiendo S11 en el punto de alimentación
Esto permite ver la impedancia de la antena a distintas frecuencias, y la ROE en la banda de interés.  

Recordar siempre realizar la medición con la antena en su posición de uso y lejos de personas, paredes y objetos conductores.

Una ROE baja no demuestra que la antena radie bien: puede haber pérdidas en la antena y la línea de alimentación, y que no se ven en S11. El cable y el entorno pueden modificar notablemente el resultado.

### Midiendo S21 contra una antena de referencia
Ubicar una antena de referencia y la antena bajo prueba en campo lejano, con distancia, polarización y orientación controladas. Medir S21 en un rango de frecuencias y repetir el ensayo reemplazando la antena bajo prueba por otra antena de referencia. Con las mismas condiciones de enlace, la diferencia entre ambas mediciones permite comparar ambas ganancias. 

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: medición S21 entre antena de referencia y antena bajo prueba" src="diagramas/rendered/antenas-s21.svg" width="50%"/>
</p>

Esta medición observa la capacidad de radiar y recibir energía, pero es difícil de realizar en la práctica. Cualquier variación de posición, orientación o polarización puede cambiar el resultado.

## Balun/Unun
### Midiendo la adaptación con S11
Conectar la entrada no balanceada al puerto 1 y terminar la salida balanceada con la impedancia para la que se diseñó el balun/unun (por ejemplo, 50 $\Omega$ para un balún 1:1 o 200 $\Omega$ para uno de relación de impedancias 1:4). Medir S11 y verificar la banda en la que la adaptación es aceptable. Esta prueba no verifica por sí sola el balance entre las dos ramas.

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: adaptación S11 de un balun o unun" src="diagramas/rendered/balun-s11.svg" width="50%"/>
</p>

### Obteniendo la relación de transformación
Conectar la entrada no balanceada al puerto 1 y colocar una resistencia variable (potenciómetro) entre los terminales de salida. Variar la resistencia y medir S11 para ver a qué resistencia se obtiene la mejor adaptación. Esto permite verificar la relación de transformación del balun/unun. Esta medición es más sencilla de realizar a baja frecuencia, donde la inductancia de los cables y la resistencia no afecta la medición.

## Transferencia de filtros pasivos
### Midiendo S21 directamente
Conectar la entrada y salida del filtro a los dos puertos, calibrados en los planos del filtro. Graficar S21 en dB para leer pérdida de inserción, frecuencias de corte (por lo general, los puntos 3 dB por debajo del nivel de la banda de paso), ancho de banda, rechazo y más.

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: medición de transferencia S21 de un filtro" src="diagramas/rendered/s21-filtro.svg" width="50%"/>
</p>

### Midiendo S11 y S22 como complemento
Medir la reflexión desde cada puerto mientras el otro está terminado en 50 $\Omega$. Una mala adaptación en la banda de paso explica parte de una S21 menor y permite ajustar las redes de adaptación de la entrada y salida.

## Cables (atenuación)
### Midiendo S21 de extremo a extremo
Calibrar hasta los planos de conexión del cable y conectar cada extremo a un puerto. La pérdida de inserción es directamente $S_{21}$ en dB; al dividirla por la longitud física se obtiene la atenuación por metro a esa frecuencia.

### Usando la reflexión de un abierto o corto
Conectar un abierto o corto conocido en el extremo remoto y medir S11. Si la carga refleja aproximadamente el 100 % y se desprecia la desadaptación, el *return loss* observado corresponde a dos recorridos del cable, por lo que la atenuación de ida es aproximadamente $RL/2$ en dB.

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: reflexión S11 de un cable terminado en abierto o corto" src="diagramas/rendered/cable-reflexion.svg" width="50%"/>
</p>

## Conectores y adaptadores
### Comparando S11 y S21 contra una referencia directa
Calibrar sin incluir el conector o adaptador a caracterizar, luego agregarlo y medir S21 a través del adaptador y S11 desde cada lado. 

<p align="center" width="100%">
<img alt="Esquema CircuitikZ: conector o adaptador medido directamente en S21" src="diagramas/rendered/conector-s21.svg" width="50%"/>
</p>

Esto permite detectar conectores gastados, falsos contactos y adaptadores que introducen reflexión o pérdida excesiva.
