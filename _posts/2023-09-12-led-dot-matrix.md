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

Para activar un LED específico, solo se necesita aplicar un voltaje
positivo a la fila respectiva de ese punto y negativo o tierra a la
columna respectiva de ese punto. Si la fila obtiene un voltaje positivo
y la columna se vuelve negativa, entonces solo se iluminará un LED en particular.


## Integrar con Raspberry Pi Pico

### Conexiones

Para poder utilizar la MAX7219 con una raspberr pi pico, será necesario realizar
las siguientes conexiones entre los puertos de los dispositivos:

| Matriz LED MAX7219 | Raspberry Pi Pico
| ------------------ | ------------------
| VCC	               | VBUS (5V)
| GND	               | GND
| DIN	               | GP3 (SPI0_TX)
| CS	               | GP5 (SPI0_CSn)
| CLK	               | GP2 (SPI0_SCK)

![Demostración de las conexiones entre los dispositivos](connection-diagram.png)
_Demostración de las conexiones entre **raspeberry pi pico** y **MAX7219**[^dot-matrix-pico]_

### Libreria

Para poder controlar la MAX7219 será necesario hacer uso de la libreria
**micropython-max7219**[^max7219-library]. Al obtener la libreria, esta se podrá
importar de la siguiente manera:

```python
import max7219
```

Además, se necesitá importar algunas librerias mas y realizar 
ciertas configuraciones para poder controlar la matriz correctamente.
El siguiente codigo muestra como realizar una configuración basica:

```python
from machine import Pin, SPI
import max7219

spi = SPI(0,sck=Pin(2),mosi=Pin(3))
cs = Pin(5, Pin.OUT)

# Ajustar por el numero de matrices conectadas
num_matrices = 1
display = max7219.Matrix8x8(spi, cs, num_matrices)

display.brightness(10)
```

Este codigo realiza lo siguiente:

1. Importa las librerias y clases necesarias para trabajar.
2. Inicializa la conexión entre los puertos/pines del respberry pi pico y de la MAX7219 para que se puedan comunicar.
3. La varible `num_matrices` establece el numero de matrices que se han conectado (en este caso, se asume que se ha conectado 1 matriz).
4. La variable `display` será la interfaz por la cual será posible interactuar (a travéz de metodos) con la matriz LED.
5. Se ajusta el nivel de brillo de los LEDs.


## Ejemplo

El siguientes script es un ejemplo funcional que dibuja una cara:

```python
import max7219
from machine import SPI, Pin

spi = SPI(0, sck=Pin(2), mosi=Pin(3))
cs = Pin(5, Pin.OUT)

num_matrices = 1
display = max7219.Matrix8x8(spi, cs, num_matrices)

display.brightness(10)

face = [
    (1, 1),
    (1, 2),
    (1, 5),
    (1, 6),
    (2, 1),
    (2, 2),
    (2, 5),
    (2, 6),
    (3, 3),
    (3, 4),
    (4, 2),
    (4, 3),
    (4, 4),
    (4, 5),
    (5, 2),
    (5, 3),
    (5, 4),
    (5, 5),
    (6, 2),
    (6, 5),
]

while True:
    for y, x in face:
        display.pixel(x, y, 1)
    display.show()
```

El codigo anterior genera el siguiente resultado:

![Matris LED mostrando una cara](led-matrix-face.png){: width="300" height="300"}

> Ejemplo disponible en [Wokwi](https://wokwi.com/projects/375825934873346049).
{: .prompt-tip}


## Referencias

[^dot-matrix-display]: [Interfacing MAX7219 LED Dot Matrix Display with Arduino](https://lastminuteengineers.com/max7219-dot-matrix-arduino-tutorial/)
[^dot-matrix-pico]: [MAX7219 LED Dot Matrix Display with Raspberry Pi Pico](https://microcontrollerslab.com/max7219-led-dot-matrix-display-raspberry-pi-pico/)
[^max7219-library]: [MicroPython Library for MAX7219 8x8 LED Matrix](https://github.com/mcauser/micropython-max7219)

