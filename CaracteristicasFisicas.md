El dispositivo está contenido en una caja plástica de material ABS, diseñada para montaje en riel DIN.

<p align="center">
  <img src="https://github.com/user-attachments/assets/91bc9894-4d6d-413f-9d7d-555d3a9f086c" alt="Dimensiones del Sicoy-COM2MDB-USB" width="100">
</p>


Las principales partes exteriores del dispositivo se muestran en la siguiente figura:


![Partes del Sicoy-COM2MDB-USB](https://github.com/user-attachments/assets/b865903a-7ac0-4a8b-9027-0a06fb17d815)

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
   



