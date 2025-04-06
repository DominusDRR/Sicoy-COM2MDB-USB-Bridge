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

Una vez que el dispositivo está en el modo de bootloader, se debe ejecutar el software denominado UnifiedHost.

![image](https://github.com/user-attachments/assets/245190b3-e495-4238-b91f-3f68e8a6ba49)

Luego seleccionamos en la opción de tipo de arquitectura a aquella que corresponde a PIC32.

![image](https://github.com/user-attachments/assets/1a8d0ad5-7650-4b36-9634-dcd0d32e6696)

A continuación, escogemos el tipo de protcolo USB:

![image](https://github.com/user-attachments/assets/c27dd808-1470-49cf-9297-3772a929745f)

En configuración, seleccionamos el tipo de dispositivo USB, que tiene que se 3C:

![image](https://github.com/user-attachments/assets/1043fa4e-a5a0-4d7b-aa33-018303c4333c)


Podemos abrir la consola para ver los pasos que se realiza la actualización del firmware, esto es en la opción Tools.

![image](https://github.com/user-attachments/assets/d85557e5-d9b6-4105-a816-67032177c7b3)

En archivo, debemos seleccionar el archivo hexadecimal, que deseamos descargar al dispositivo:

![image](https://github.com/user-attachments/assets/4baf64da-8b5b-4fac-a0be-ff42918f66b7)

Y finalmente, presionamos el botón de programación:

![image](https://github.com/user-attachments/assets/d62a08d5-8421-470d-af50-0786b87f43a0)

El software hará todo lo necesario para programar al dispositivo, dichos pasos se verán en la consola y al finalizar, el dispositivo arrancará con la nueva versión:

![image](https://github.com/user-attachments/assets/b1dfb9b2-6c57-4017-a49d-bf56e8e0c23a)








