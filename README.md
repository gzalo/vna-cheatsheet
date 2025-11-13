# VNA Cheatsheet
Machete con diversas cosas que se pueden medir con un VNA (Analizador de Redes Vectorial), como el [NanoVNA](https://nanovna.com/) o sus clones.

Este documento no pretende ser una guía completa de uso del VNA, sino un resumen rápido de las mediciones más comunes que se pueden hacer con este instrumento.

Por LU6CGA (gzalo), si encontrás algún error o mejora podés crear un _pull request_ para agregarlo a la lista.

- [VNA Cheatsheet](#vna-cheatsheet)
- [Introducción](#introducción)
- [Calibración](#calibración)
- [Mediciones usando S11](#mediciones-usando-s11)
  - [Impedancia de entrada de un equipo/filtro](#impedancia-de-entrada-de-un-equipofiltro)
  - [Impedancia de salida](#impedancia-de-salida)
  - [Inductores](#inductores)
  - [Capacitores](#capacitores)
  - [Cristales / Filtros resonantes SAW / Factor Q](#cristales--filtros-resonantes-saw--factor-q)
  - [Stubs abiertos/cerrados](#stubs-abiertoscerrados)
  - [Antenas](#antenas)
  - [Balun/Unun](#balununun)
  - [Constante de propagación](#constante-de-propagación)
- [Mediciones usando S21](#mediciones-usando-s21)
  - [Transferencia de filtros pasivos](#transferencia-de-filtros-pasivos)
  - [Transferencia de filtros activos/Amplificadores](#transferencia-de-filtros-activosamplificadores)
  - [Cables (atenuación)](#cables-atenuación)
  - [Balun/Unun](#balununun-1)
  - [Cables con roturas (TDR)](#cables-con-roturas-tdr)
  - [Desadaptaciones de impedancias](#desadaptaciones-de-impedancias)

# Introducción
El VNA es un instrumento de medición que permite caracterizar [Cuadripolos](https://es.wikipedia.org/wiki/Cuadripolo) en función de la frecuencia. Mide [parámetros S (Scattering parameters)](https://es.wikipedia.org/wiki/Par%C3%A1metros_de_dispersi%C3%B3n) que describen cómo las señales se reflejan y transmiten a través de la red. Estos son números complejos que suelen ser distintos en función de la frecuencia.

# Calibración 
Es sumamente importante calibrar el VNA antes de hacer mediciones para obtener resultados precisos. Antes de calibrar hay que decidir el rango de frecuencias y el tipo de calibración a usar. 

- Calibración de 1 puerto: si solo se quiere medir S11, es necesario calibrar solo el puerto de entrada:
  - Open
  - Short
  - Load
- Calibración de 2 puertos: si se quieren medir S11 y S21 (o S22 y S12), es necesario calibrar ambos puertos:
  - Open
  - Short
  - Load
  - Through
  - Isolation (opcional)

Es necesario usar estándares de calibración de buena calidad para obtener resultados precisos. Altamente recomendado [conseguir o fabricar un kit casero con conectores SMA hembra](https://www.qsl.net/in3otd/electronics/VNA_calkit/SMA_female.html), ya que en muchos casos los nanoVNA vienen con estándares macho, lo que requiere agregar adaptadores y generan un error adicional en las mediciones.

En __todas__ las mediciones que se describen a continuación es necesario calibrar el VNA previamente, en el rango de frecuencias de interés. Si cambiamos el rango de frecuencias, es necesario recalibrar.

Cuando se usan cables o adaptadores adicionales en las mediciones, es necesario incluirlos en la calibración, de lo contrario se termina midiendo también la respuesta de esos elementos, lo que puede introducir errores significativos.

# Mediciones usando S11
## Impedancia de entrada de un equipo/filtro

1. Conectar el equipo o filtro al puerto 1 del VNA y medir S11 para el rango de frecuencias de interés.
2. Usando los distintos formatos de visualización (Smith chart, polar, etc.) se puede obtener la impedancia de entrada del equipo o filtro en función de la frecuencia.

Recordar que el VNA es más preciso cuando la impedancia está cerca de la impedancia característica del VNA, cuando $|Z| \approx 50\ \Omega$.

También es muy importante recordar que la potencia de salida del VNA (-20 a 0 dBm dependiendo del modelo, también varía en función de la frecuencia) puede llegar a modificar el comportamiento del equipo o filtro medido. En esos casos, es recomendable usar atenuadores en la entrada del equipo para reducir la potencia de la señal de entrada, o cambiar el valor de potencia de salida del VNA si es posible. Los atenuadores pueden ser incluidos en la calibración para excluirlos de las mediciones.

## Impedancia de salida

Si es un equipo activo, no es fácil de medir con un VNA, porque solo pueden medir respuestas a sus propios estímulos. [Este artículo de NXP provee más datos](https://www.nxp.com/docs/en/application-note/AN1526.pdf) de cómo realizarlo bien.

Recordar que un error pensar que la impedancia interna será de $50 \ \Omega$ si es un dispositivo pensado para conectarle una carga de $50 \ \Omega$.

En algunos amplificadores transistorizados se puede medir la potencia de salida y usar una fórmula para estimar la impedancia de salida: $Zo \approx \frac{V_{cc}-V_{CE(sat)}^2}{2 P_o}$

## Inductores 
(completar)
## Capacitores
(completar)
## Cristales / Filtros resonantes SAW / Factor Q
(completar)
## Stubs abiertos/cerrados
(completar)
## Antenas
(completar)
## Balun/Unun
(completar)
## Constante de propagación 
(completar)

# Mediciones usando S21
## Transferencia de filtros pasivos
(completar)
## Transferencia de filtros activos/Amplificadores
(completar)
## Cables (atenuación)
(completar)
## Balun/Unun
(completar)
## Cables con roturas (TDR)
(completar)
## Desadaptaciones de impedancias
(completar)

