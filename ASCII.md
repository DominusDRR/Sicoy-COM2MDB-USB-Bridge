# Comandos de consulta ASCII.

Ademas de las tramas de comandos MDB, el dispositivo posee los siguientes comandos que son de tipo mensajes ASCII, y permiten ralizar varias consultas al dispositivo.

## Comando FIRMWARE.

Este comando permite conocer la versión del firmware del microcontrolador del dispositivo:

![image](https://github.com/user-attachments/assets/ddf066ee-e9e1-480a-ae39-d15ecf015ab8)

## Comando HARDWARE.

Este comando permite conocer la versión del Hardware del microcontrolador del dispositivo:

![image](https://github.com/user-attachments/assets/d7cf4699-c66e-4abd-af71-55d2edb1a9d9)

## Comando UART.

Este comando permite conocer el estado de la tarea del UART que envía datos sobre el bus MDB, es para propósitos de mantenimiento por parte del desarrollador del firmware:

![image](https://github.com/user-attachments/assets/41849251-5713-4f2e-ba18-342bef0e406a)

## Comando ERROR.

Este comando permite conocer cualquier error de la tarea del UART que envía datos sobre el bus MDB, es para propósitos de mantenimiento por parte del desarrollador del firmware:

![image](https://github.com/user-attachments/assets/d4813bd8-8b52-4cf9-a20c-4fa1a96f4c3d)


## Comando LOGS.

Este comando permite conocer las tramas que han llegado desde el Host y las que ha recibido desde el bus MDB, puede almacenar hasta 256 logs.


![image](https://github.com/user-attachments/assets/c119abb8-958a-4566-90f9-1a7656630b8f)

Cada línea consta de tres partes, a la izquiera, lo que el Host envío, en el centro lo que el periférico respondió y a al derecha el log al que pertenece.

![image](https://github.com/user-attachments/assets/5605d902-ce71-4562-9c07-cd13b868522a)

En algunas ocasiones pueden indicar que el periférico respondió con datos.

![image](https://github.com/user-attachments/assets/e7d1dd1f-523a-4fa9-903d-817f7680996f)

Para conocer estos datos, se puede recurrir al comando DATOS

## Comando DATOS.

Devuelve los datos de los logs que tienen esa información.

![image](https://github.com/user-attachments/assets/eec10ca4-edb5-4aa3-88fe-2510f3a697e0)

Los DATOS constan de dos partes, los datos en si, y al log que pertenecen.

![image](https://github.com/user-attachments/assets/74dcd439-d4c0-4597-9bab-b2ca17c031f3)











