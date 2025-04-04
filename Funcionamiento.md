## Conexión al PC mediante cable USB.

El dispositivo se alimenta directamente del voltaje proporcionado por el puerto USB. Por otro lado, la conexión de 24V en la bornera inferior es exclusivamente para suministrar energía al bus MDB y no forma parte del funcionamiento interno del dispositivo.

Para conectar el dispositivo, utilice un cable USB según se muestra en la siguiente figura.

<p align="center">
  <img src="https://github.com/user-attachments/assets/82a74a87-e02f-4d33-a936-c04b554bd524" alt="Riel DIN" width="200">
</p>

Al conectar el dispositivo al puerto USB, el sistema operativo asignará automáticamente un número de puerto COM virtual.

Cuando el dispositivo se energiza, emite una breve tonada musical, indicando que está listo para operar.

Una vez identificado el puerto COM asignado, el usuario podrá enviar y recibir tramas utilizando cualquier aplicación compatible con comunicación serie.

## Ejemplos de Comandos MDB.

### Comandos para monedero

#### Comando reinicio de monedero.

Este comando reinicia al monedero conectado al bus MDB, y su trama es así:

0xFE 0x08 0x01 0xFE 0x08 0x00

La respuesta a este comando es un ACK, que significa que el comando ha sido procesado correctamente, el cual es 0x00

![image](https://github.com/user-attachments/assets/dbfcb8dc-6237-4c76-a8ac-ce769a4bfc61)


#### Comando POLL de monedero.

Este comando solicita de cambio de estado de actividad, lo cual permite obtener un reporte por parte del monedero.

Si no tiene nada que reportar, retorna un ACK.

Si tiene que reportar algo, y puede retornar hasta 16 bytes. Si desea conocer el significado de esos datos, consulte la sección 5 del manual del protocolo MDB ->  [MDB protocol versión 4.3 (julio de 2019)](https://www.cable-tester.com/references/mdb-connector-pin-out/mdb-protocol-ver-4_3.pdf)

Su trama sera:

0xFE 0x0B 0x01 0xFE 0x0B 0x00

![image](https://github.com/user-attachments/assets/67378733-1b20-4848-871d-3e489481a27a)


#### Comando habilitación de monedas en el monedero.

Este comando consiste en 4 bytes, los dos primeros consisten en el tipo de monedas que el monedero aceptará.

Cada bit representa un tipo de moneda en particular, lo que significa hasta 16 tipos diferentes de monedas, poniendo en 1 lógico significa que acpetará esa moneda, caso contrario, significa que no lo acepta.

Los dos siguientes bytes significan las monedas que dispensará, de igual manera, cada bit corresponde a una moneda particular, y su despacho es habilitado en 1 lógico, y su bloqueo es con cero lógico.

De igual manera, si el monedero acepta este comando con sus datos, responde un ACK.

Una trama ejemplo de este comando es:

0xFE 0x0C 0x01 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0x08 0x00

Este comando podemos explicar cada parte así:

0xFE 0x0C 0x01 // Comando y el noveno bit en 1L

0xFE 0xFF 0x00 
0xFE 0xFF 0x00 // Todas las 16 opciones de monedas que acepta son habilitadas, 

0xFE 0xFF 0x00 
0xFE 0xFF 0x00  // Todas las 16 opciones de monedas que devuelve o entrega de cambio son habilitadas

0xFE 0x08 0x00  // Checksum, suma de 0x0C + 0xFF + 0xFF + 0xFF + 0xFF = 0x08

![image](https://github.com/user-attachments/assets/9d42a8ec-cd37-4686-8834-e7a19c4673d1)

 
#### Habilitación de caracteristicas especiales con subcomando igual a 0x01.

Este comando se utiliza para habilitar cada una de las funciones opcionales definidas en los puntos del sub comando 0x00 (Aun no implementado) Z30 a Z33 anteriores correpondiente al comando . Para habilitar una función, se establece un bit en 1 ógico cada bite de los datos.

A parte del subcomando, son necesarios 4 bytes que corresponden a las 32 opciones que poseen los campos Z30 a Z33.

Un ejemplo de la trama de este comando es:

0xFE 0x0F 0x01 0xFE 0x01 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0x0C 0x00

De igual manera, si lo analizamos detenidamente, es así:

0xFE 0x0F 0x01 // Comando con su noveno bit en 1
0xFE 0x01 0x00 // Subcomando en 0x01

0xFE 0xFF 0x00 
0xFE 0xFF 0x00 
0xFE 0xFF 0x00 
0xFE 0xFF 0x00 // Habilitando todos los bits de Z30 a Z33

0xFE 0x0C 0x00 // CHK = 0x0C = 0x0F + 0x01 + 0xFF + 0xFF + 0xFF + 0xFF

![image](https://github.com/user-attachments/assets/8489f8f4-0071-4ac0-a511-dfb7ef7c82e7)

#### Habilitación de caracteristicas especiales con subcomando igual a 0x02 (Pago o entrega de monedas).

Este comando tiene como primer dato el subcmando igual a uno, y el segundo dato es el valor de monedas que se desea entregar o pagar al usaurio del monedero.

Un ejemplo de esta trama es:

0xFE 0x0F 0x01 0xFE 0x02 0x00 0xFE 0x0A 0x00 0xFE 0x1B 0x00

Esta trama analizada es:

0xFE 0x0F 0x01 // Comando con noveno bit en 1
0xFE 0x02 0x00 // Subcamndo igual a 2 (noveno bit en 0) 
0xFE 0x0A 0x00 // Valor monedas a pagar
0xFE 0x1B 0x00 // CHK, que es 0x0F + 0x02 + 0x0A = 0x1B

![image](https://github.com/user-attachments/assets/531348ca-9f0f-4a38-9307-6180cfae28a5)

### Comandos para billetera.

#### Comando reinicio de billetera.

Este comando reinicia la billetera conectado al bus MDB, y su trama es así:

0xFE 0x30 0x01 0xFE 0x30 0x00

La respuesta a este comando es un ACK, que significa que el comando ha sido procesado correctamente, el cual es 0x00.

![image](https://github.com/user-attachments/assets/e9aa2214-f710-454a-a007-0c2648f35a07)

#### Comando de Calibración de Billetera.

Este comando retorna la calibración de la billetera, para más detalles, vease el manual del protocolo MDB.

La trama de este comenado es:

0xFE 0x31 0x01 0xFE 0x31 0x00

![image](https://github.com/user-attachments/assets/aba20f04-6fd6-45f9-a32e-c6c5318dbaf1)


#### Comando de Seguridad de Billetera.

Al emitir este comando, se debe incluir 2 bytes de datos. Cada bit de esos dos bytes indican el tipo de billete(s) con un nivel de seguridad "alto". Tenga en cuenta que los validadores que no admiten niveles de seguridad duales deben informar un nivel de seguridad "alto" en los bytes de respuesta Z9-Z10 al comando STATUS (31H). 

La respuesta a este comando es un ACK

Por favor refiérase al manual del protocolo MDB para más detalles.

Un ejemplo de esta trama es:

0xFE 0x32 0x01 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0x30 0x00

Cada parte de este comando es:

0xFE 0x32 0x01 // Comando con su noveno bit en 1 lógico

0xFE 0xFF 0x00 
0xFE 0xFF 0x00 //  Estado de los bytes Z9-Z10

0xFE 0x30 0x00 // CHK = 0x32 + 0xFF + 0xFF = 0x30

![image](https://github.com/user-attachments/assets/a9282c5c-fa97-403e-8671-310092d2df33)

## Comando POLL de Billetera.

Este comando solicita de cambio de estado de actividad, lo cual permite obtener un reporte por parte de la billetera.

Si no tiene nada que reportar, retorna un ACK.

Su trama sera:

0xFE 0x33 0x01 0xFE 0x33 0x00.


![image](https://github.com/user-attachments/assets/d0a09ae2-da79-430b-aadd-b4769f046cde)

#### Comando habilitación de billetes de la billetera

Este comando consiste en 4 bytes, los dos primeros consisten en el tipo de monedas que el monedero aceptará.

Cada bit representa un tipo de billete en particular, lo que significa hasta 16 tipos diferentes de billetes, poniendo en 1 lógico significa que acpetará esa billete, caso contrario, significa que no lo acepta.

Los dos siguientes bytes significan los billetes que dispensará, de igual manera, cada bit corresponde a una moneda particular, y su despacho es habilitado en 1 lógico, y su bloqueo es con cero lógico.

De igual manera, si la billetera acepta este comando con sus datos, responde un ACK.

Una trama ejemplo de este comando es:

0xFE 0x34 0x01 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0x30 0x00

Este comando podemos explicar cada parte así:

0xFE 0x34 0x01 // Comando y el noveno bit en 1L

0xFE 0xFF 0x00 
0xFE 0xFF 0x00 // Todas las 16 opciones de monedas que acepta son habilitadas, 

0xFE 0xFF 0x00 
0xFE 0xFF 0x00  // Todas las 16 opciones de monedas que devuelve o entrega de cambio son habilitadas

0xFE 0x30 0x00  // Checksum, suma de 0x34 + 0xFF + 0xFF + 0xFF + 0xFF = 0x30

![image](https://github.com/user-attachments/assets/39addac5-5e7a-4280-93bf-bce019e6a8ca)

#### Comando de depósito de billetera.

Este comando sirve para indicar la acción correspondiente a un billete en depósito.

El monedero envía un byte de datos, denominado Y1, donde:

Si Y1 = 0; rechazar el billete
Si Y1 = xxxxxxx1; Guardar el billete («x» significa cualquier valor)

Un ejemplo de este comando es:

0xFE 0x35 0x01 0xFE 0x36 0x00.

Este comando tiene por respuesta un ACK.

![image](https://github.com/user-attachments/assets/44c08e2f-f58b-41e2-846b-637ba5abd2a7)


#### Habilitación de caracteristicas especiales de billetera con subcomando igual a 0x01.

Este comando se utiliza para habilitar cada una de las funciones opcionales definidas en los puntos del sub comando 0x00 (Aun no implementado) Z30 a Z33 anteriores correpondiente al comando . Para habilitar una función, se establece un bit en 1 ógico cada bite de los datos.

A parte del subcomando, son necesarios 4 bytes que corresponden a las 32 opciones que poseen los campos Z30 a Z33.

Un ejemplo de la trama de este comando es:

0xFE 0x37 0x01 0xFE 0x01 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0x34 0x00

De igual manera, si lo analizamos detenidamente, es así:

0xFE 0x37 0x01 // Comando con su noveno bit en 1
0xFE 0x01 0x00 // Subcomando en 0x01

0xFE 0xFF 0x00 
0xFE 0xFF 0x00 
0xFE 0xFF 0x00 
0xFE 0xFF 0x00 // Habilitando todos los bits de Z30 a Z33

0xFE 0x37 0x00 // CHK = 0x37 = 0x0F + 0x01 + 0xFF + 0xFF + 0xFF + 0xFF

![image](https://github.com/user-attachments/assets/0e0989ee-1b8c-4e06-95f7-36b987d5a39f)
