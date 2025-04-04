# Actualización del firmware.

La actualización del firmware permite descargar una nueva versión del firmware sin la necesidad de recurir a un programador externos.

Hay básicamente 2 maneras de entrar en ese modo

## Ingreso por software.

Este método es utilizando el comando ASCII denominado BOOT y se puede hacer cuando el dispositivo está funcionado correctamente

![image](https://github.com/user-attachments/assets/7cda08ef-e66b-4d8b-b60e-57d1d0784946

## Ingreso por Hardware.

Este método se utiliza cuando se descarga un firmware no útil, esta condición puede suceder por las siguientes razones.

1. Interrupción de la energía cuando se estaba programando al dispositivo. 
2. Desconexión del cable USB mientras se estaba programando al dispositivo.
3. Descarga de un archivo hexadecimal corrupto o erroneo.

En esto tres caso, el dispositivo se comporta como si tuviera un daño permanente.

La forma que el dispositivo regrese al modo bootloader para descargar un archivo correcto con siste en los siguiente pasos.

1. Desconetar el cable USB del dispositivo.
2. Presionar el botón que envía un comando break al bus MDB.
3. No dejar de presionar el botón.
4. Conectar el cable USB.
5. En el momento que suene una tonada musical (que es diferente a aquella cuando empieza a funcionar en modo normal), se debe soltar el botón

En ese momento el dispositivo entra al modo bootlader y está listo para que se descargue un archivo correcto

## Caracteristicas del Modo Bootloader

En este modo, los diodos leds del panel frontal, se encienden de manera alternada, y una señal acústica de corta duración suena de manera periódica.

## Software de actualización.

Una vez que el dispositivo está en el modo de bootloader, se debe ejecutar el software denominado UnifiedHost

