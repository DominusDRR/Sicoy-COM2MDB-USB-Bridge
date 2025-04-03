El dispositivo está contenido en una caja plástica de material ABS, diseñada para montaje en riel DIN, y sus dimenciones en pulgadas o [milímetros] se aprecian en la siguiente figura

<p align="center">
  <img src="https://github.com/user-attachments/assets/91bc9894-4d6d-413f-9d7d-555d3a9f086c" alt="Dimensiones del Sicoy-COM2MDB-USB" width="700">
</p>


Las principales partes exteriores del dispositivo se muestran en la siguiente figura:

<p align="center">
  <img src="https://github.com/user-attachments/assets/b865903a-7ac0-4a8b-9027-0a06fb17d815" alt="Partes del Sicoy-COM2MDB-USB" width="300">
</p>


Descripción de las partes:

1. Conector MDB

2. Panel frontal

3. Alimentación de 24V para el bus MDB

4. Soporte de sujeción

5. Puerto USB tipo C

6. Montura para riel DIN

7. Botón de comando Break y modo de programación (Bootloader)

# Conector MDB.

El conector MDB cumple con la norma del protocolo (Master Connector) y es como se muestra en la siguiente figura:

<p align="center">
  <img src="https://github.com/user-attachments/assets/b5c3c590-43e6-4125-9fc9-5c8d204b57f8" alt="Conector MDB" width="350">
</p>

# Panel Frontal.

El panel frontal es como se muestra en la siguiente figura:

<p align="center">
  <img src="https://github.com/user-attachments/assets/86dcf4f4-8adc-49fb-8050-dd6fb48ae921" alt="Panel Frontal" width="100">
</p>


Posee 5 diodos led que forman una columna, empezando desde arriba hacia abajo, el primero indica que el microcontrolador interno está funcionando, cuando eso sucede, se enciende y apaga a un ritmo de 500 ms.

El segundo led indica que se ha transmitido una trama de bytes desde el dispositivo.

El tercer led indica cuando ha recibido una trama de bytes desde una máquina periférico

El cuarto led, indica un error de trama desde el anfitrión, desde una máquina periférico o una no respuesta desde la máquina periférico.

El quito led, se activa cuando está presente los 24V en el bus MDB

#  Alimentación de 24V para el bus MDB

Es una bornera de dos terminales para conectar 24VDC para el bus MDB, el terminal izquierdo, corresponde al terminal negativo, el terminal derecho corresponde al terminal positivo.

Internamente hay un diodo rectificador para evitar una polarizacion inversa en el bus MDB, el diodo led correspondiente en el panel indica la polaridad correcta.
   
# Soporte de sujeción

La parte posterior del dispositivo, posee una muesca que permite sujetar al dispositivo a un riel DIN.

# Puerto USB tipo C.

El puerto de conexión hacia un computador, es mediante USB de tipo 2.0, sin embargo posee un puerto C que es la norma más actual de este tipo de comunicación.

# Botón de comando Break y modo de programación (Bootloader)

Este botón permite generar un caracter break de aproximadamente 160ms en el bus MDB para provocar un reinicio en cualquier periférico conectado al bus, y esta es una caracteristca propia de este protocolo.

Este botón también permite ingresar al modo de bootloader cuando se desea actualizar el firmware del dispositivo.


