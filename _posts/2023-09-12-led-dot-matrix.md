---
title: Led Dot Matrix (MAX7219)
author: omar
date: 2023-09-12 05:00:00 -0800
categories: [Presentación]
tags: [sensores,raspberry pi]     # TAG names should always be lowercase
img_path: /assets/img/led-matrix/
---

Una LED Dot Matrix (*Matriz de puntos LED*) es un display en forma de 
cuadricula de luces led. Es utilizado para mostrar símbolos, characteres
e incluso imagenes.


## Descripción

Un display de matriz de puntos led 8×8 suele tener 16 pines,
8 para cada fila y 8 para cada columna. Todas las filas y columnas
están conectadas entre sí para reducir la cantidad de pines. Si 
este no fuera el caso, una pantalla de matriz de puntos de 8×8
requeriría **65 pines**, uno para cada LED y otro para un ánodo común
o un conector de cátodo común. Al conectar filas y columnas, solo
se necesitan **16 pines** para controlar toda la matriz[^dot-matrix-display]. Esta técnica
de controlar una gran cantidad de LED con menos pines se conoce
como multiplexación.

![Matriz de puntos led con cables](led-matrix-img.png){: width="300" height="300"}
_Matriz de puntos led Max7219_

### Multiplexación

En esta técnica, cada columna se activa por un tiempo muy corto y,
al mismo tiempo, los LED de esa columna se encienden direccionando
la fila correspondiente. Como resultado, no se encienden más de ocho
LED al mismo tiempo. Las columnas cambian tan rápido (cientos o miles
de veces por segundo) que el ojo humano percibe la pantalla como
completamente iluminada.


## Referencias

[^dot-matrix-display]: [Interfacing MAX7219 LED Dot Matrix Display with Arduino](https://lastminuteengineers.com/max7219-dot-matrix-arduino-tutorial/)
