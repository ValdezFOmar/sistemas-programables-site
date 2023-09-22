---
title: ¿Qué sensonres tiene mi smartphone?
author: omar
date: 2023-09-20 05:00:00 -0800
categories: [Presentación]
tags: [sensores,smartphone,app]     # TAG names should always be lowercase
img_path: /assets/img/sensores-smartphone/
---

## Detección de sensores

Para realizar la detección de sensores en un telefono Android, se utilizó la aplicación
Sensor Box[^app-sensores], con esta aplicación es posible detectar y probar los distintos
sensores de fabrica de los que dispone el dispositivo.

### Tabla de Sensores

A continuación se presenta una tabla con los distintos sensores que Sensor Box permite
interactuar, así como información detallada de cada sensor.

> Haz clic en las capturas para hacer zoom.
{: .prompt-tip }

| Sensor       | Icono | Detecta     | ¿Detectado? | Captura       |
| :----------: | :---: | ----------- | :---------: | :-----------: |
| Acelerometro | ![](icons/acelerometro.jpg) | Dirección del dispositivo, para autorotar<br>la pantalla verticalmente. | Sí | ![](acelerometro.jpg) |
| Luz          | ![](icons/luz.jpg) | Intensidad de la luz en el ambiente<br>para ajustar el brillo de la pantalla. | Sí | ![](sensor-luz-alta.jpg) |
| Orientación  | ![](icons/orientacion.jpg) | Estado de la dirección del dispositivo, para<br>autorotar la pantalla horizontalmente. | Sí | ![](orientacion.jpg) |
| Proximidad   | ![](icons/proximidad.jpg) | Distancia del dispositivo a la cara/manos<br>para apagar la pantalla durante una llamada. | Sí | ![](proximidad-lejos.jpg) |
| Temperatura  | ![](icons/temperatura.jpg) | No detectado. | No | No detectado. |
| Giroscopio   | ![](icons/giroscopio.jpg) | Mide 6 direcciones al mismo tiempo (Posición 3D),<br> se utiliza para desarrollo de videojuegos. | Sí | ![](giroscopio.jpg) |
| Sonido       | ![](icons/sonido.jpg) | Intensidad de sonido alrededor del dispositivo. | Sí | ![](volumen-alto.jpg) |
| Magnetico    | ![](icons/magnetico.jpg) | Campos magneticos, util para la detección<br>de metales y simular una brujula. | Sí | ![](magnetico-alto.jpg) |
| Presión      | ![](icons/presion.jpg) | No detectado. | No | No detectado. |

## Referencias

[^app-sensores]: [Sensor Box for Android - Senso](https://play.google.com/store/apps/details?id=com.nirmallabs.sensorbox)

