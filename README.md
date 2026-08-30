# VNA Cheatsheet

Machete con diversas cosas que se pueden medir con un VNA (Analizador de Redes Vectorial), como el [NanoVNA](https://nanovna.com/) o sus clones.

Este documento no pretende ser una guía completa de uso del VNA, sino un resumen rápido de las mediciones más comunes que se pueden hacer con este instrumento.

Por LU6CGA (gzalo), si encontrás algún error o mejora podés crear un _pull request_ para arreglarlo!

- [Mediciones básicas](mediciones-basicas.md)
  - [Impedancia de entrada de equipos y filtros](mediciones-basicas.md#impedancia-de-entrada-de-un-equipofiltro)
  - [Inductores](mediciones-basicas.md#inductores) y [capacitores](mediciones-basicas.md#capacitores)
  - [Stubs abiertos y cerrados](mediciones-basicas.md#stubs-abiertoscerrados)
  - [Antenas](mediciones-basicas.md#antenas)
  - [Balun y unun](mediciones-basicas.md#balununun)
  - [Transferencia de filtros pasivos](mediciones-basicas.md#transferencia-de-filtros-pasivos)
  - [Atenuación de cables](mediciones-basicas.md#cables-atenuación)
  - [Conectores y adaptadores](mediciones-basicas.md#conectores-y-adaptadores)
- [Mediciones avanzadas](mediciones-avanzadas.md)
  - [Cristales, filtros SAW y factor Q](mediciones-avanzadas.md#cristales--filtros-resonantes-saw--factor-q)
  - [Impedancia de salida](mediciones-avanzadas.md#impedancia-de-salida)
  - [Constante de propagación](mediciones-avanzadas.md#constante-de-propagación) y [constante dieléctrica de cable o PCB](mediciones-avanzadas.md#constante-dieléctrica-de-cable-o-pcb)
  - [Choques de modo común](mediciones-avanzadas.md#choques-de-modo-común)
  - [Transferencia de filtros activos y amplificadores](mediciones-avanzadas.md#transferencia-de-filtros-activosamplificadores)
  - [Retardo de grupo](mediciones-avanzadas.md#retardo-de-grupo)
  - [Roturas y discontinuidades de cables (TDR)](mediciones-avanzadas.md#cables-con-roturas-tdr)
  - [Aislación entre puertos](mediciones-avanzadas.md#aislación-entre-puertos)
  - [Divisores y combinadores de potencia](mediciones-avanzadas.md#divisores-y-combinadores-de-potencia)
  - [Atenuadores](mediciones-avanzadas.md#atenuadores)
  - [Acopladores direccionales](mediciones-avanzadas.md#acopladores-direccionales)

## Qué se puede medir

## Introducción

El VNA es un instrumento de medición que permite caracterizar [Cuadripolos](https://es.wikipedia.org/wiki/Cuadripolo) (un nombre bastante feo para un bloque con dos puertos) en función de la frecuencia. Mide [parámetros S (Scattering parameters)](https://es.wikipedia.org/wiki/Par%C3%A1metros_de_dispersi%C3%B3n) que describen cómo las señales se reflejan y transmiten a través de la red. Estos son números complejos que suelen variar en función de la frecuencia.

_S11_ representa la relación entre la señal reflejada y la señal incidente en el puerto 1. Esto también puede ser representado como _coeficiente de reflexión_ o _pérdida de retorno_. Básicamente representa qué tan bien está adaptada la impedancia de entrada del dispositivo a la impedancia característica de la línea de transmisión (50 ohms en la mayoría de los casos).

_S21_ representa la relación entre la señal transmitida al puerto 2 y la señal incidente en el puerto 1. Esto también puede ser representado como _ganancia_ o _pérdida de inserción_. Básicamente representa qué tan bien se transmite la señal a través del dispositivo, cómo cambia la amplitud y la fase de la señal al pasar por el mismo.

La forma visual de representar estos parámetros es mediante un diagrama de Smith, que permite ver el coeficiente de reflexión (y la impedancia) en función de la frecuencia. Para entender un poco más cómo funciona dicho diagrama, se puede experimentar con el [Online Smith Chart](https://onlinesmithchart.com/).

_En el NanoVNA, los dos puertos del equipo se llaman **CH0 y CH1**, pero en la mayoría de los equipos profesionales se llaman puerto 1 y puerto 2. En este documento se usarán los términos **puerto 1** y **puerto 2**._

## Calibración

Es sumamente importante calibrar el VNA antes de hacer mediciones para obtener resultados precisos. Antes de calibrar hay que decidir el rango de frecuencias y el tipo de calibración a usar.

- Calibración de 1 puerto: si solo se quiere medir S11, es necesario calibrar solo el puerto de entrada:
  - Open
  - Short
  - Load
- Calibración de 2 puertos: si se quieren medir S11 y S21 (o S22 y S12 en equipos profesionales), es necesario calibrar ambos puertos:
  - Open
  - Short
  - Load
  - Through
  - Isolation (opcional - disminuye el efecto de _crosstalk_ entre ambos puertos)

Es necesario usar estándares de calibración de buena calidad para obtener resultados precisos. Es altamente recomendado [conseguir o fabricar un kit casero con conectores SMA hembra](https://www.qsl.net/in3otd/electronics/VNA_calkit/SMA_female.html), ya que en muchos casos los nanoVNA vienen con estándares macho, lo que requiere agregar adaptadores y generan un error adicional en las mediciones.

**Si cambiamos el rango de frecuencias, es necesario recalibrar.** En la mayoría de los casos tiene más sentido recalibrar que guardar la calibración anterior y usarla en otro momento, ya que la calibración podría variar con la temperatura y otros factores. 

Cuando se usan cables o adaptadores adicionales en las mediciones, es necesario incluirlos en la calibración. De lo contrario se termina midiendo también la respuesta incluyendo a dichos elementos, lo que puede introducir errores no desados. En los diagramas se muestra el mejor "plano/planos de referencia" para realizar la calibración.

### Offset delay

En algunos casos no podemos calibrar el VNA en el punto exacto de medición. En estos casos es posible usar la función de _offset delay_ para compensar la diferencia de fase introducida por estos elementos. Una forma de elegir el valor de _offset delay_ es realizar la calibración normalmente y luego dejando la punta abierta o en cortocircuito, medir la fase de S11 y elegir un valor de _offset delay_ que haga que la fase medida sea cero o 180 grados, según corresponda. 
