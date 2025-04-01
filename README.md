# Sicoy-COM2MDB-USB-Bridge
Este repositorio contiene el manual del dispositivo Sicoy COM2MDB USB Bridge  y el firmware actualizado. Se publicarán mejoras y correcciones de manera continua.

## Descripción  
- Este dispositivo permite enviar comandos a un periférico MDB (Multi-Drop Bus) desde una computadora a través de USB.
- Funciona como un puerto serial COM virtual, interpretando los comandos recibidos y generando tramas compatibles con el protocolo MDB.
- Si desea conocer más información del protocolo MDB, puede descargarlo en [MDB protocol versión 4.3 (julio de 2019)](https://www.cable-tester.com/references/mdb-connector-pin-out/mdb-protocol-ver-4_3.pdf)

### Formato de la trama a enviar desde el anfitrión (Computador)
- El protocolo MDB utiliza una comunicación RS232 de 9 bits, lo que no puede realizarse directamente desde un PC. Para solucionar esto, el dispositivo convierte la comunicación estándar en una trama compatible con MDB, con el siguiente formato:

Cada mensaje consta de:
Inicio → Indica el comienzo de un byte.
Comando → Byte de instrucción.
Noveno bit → Bit adicional requerido por MDB.
Datos → Uno o más bytes de datos.
CHK → Byte de comprobación.

| Inicio | Comando | 9º Bit | Inicio | Dato 0 | 9º Bit | Inicio | Dato 1 | 9º Bit | ... | Inicio | Dato N | 9º Bit | Inicio | CHK | 9º Bit |

El byte denominado Inicio siempre tiene el valor 0xFE en hexadecimal.
Solo el Comando tiene su noveno bit en 1, mientras que los Datos y el CHK siempre tienen el noveno bit en 0, un ejmplo de esta trama puede ser:

0xFE 0x37 0x01 0xFE 0x01 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0xFF 0x00 0xFE 0x34 0x00

El bit de comprobación CHK es la suma de los comandos y todos los datos (Checksum como suma directa), de esta suma sólo se toma la parte baja o los 8 primeros bits

0x37 + 0x01 + 0xFF + 0xFF + 0xFF + 0xFF = 0x0434

La parte baja de 0x0434 es 0x34.

**No todos los comandos envían datos, es decir, son sólo un comando y su byte CHK**, por ejemplo, para reiniciar, a un monedero, la trama es así:

0xFE 0x08 0x01 0xFE 0x08 0x00.

Nótese que aquí, el byte CHK es el mismo, ya que no hay más bytes que se consideren datos, luego del comando.



### Comandos del sistema
Los comandos soportados en la versión 1.00 del firmware son los siguientes:
#### Monedero

Reinicio → 0x08

POLL → 0x0B

Tipo de moneda → 0x0C

Comando de expansión → 0x0F (Subcomando 0x01 para habilitación de características)

#### Billetera

Reinicio → 0x30

Calibración → 0x31

Seguridad → 0x32

POLL → 0x33

Tipo de billetera → 0x34

Depósito → 0x35

Comando de expansión → 0x37 (Subcomando 0x01 para habilitación de características)

### Reglas de operación para el envío y recepción de comandos y datos
El dispositivo sigue las siguientes reglas para la transmisión y recepción de bytes de manera automática, esto significa que el usuario, no debe preocuparse en cumplire esas reglas, el dispositivo lo hace por si sólo.

#### a. Comando sin datos
Si se envía un comando que no necesita datos, solo el comando y su byte de CHK, la máquina responde con un ACK:

Host: CMD* + CHK

Periférico: ACK*

#### b. Comando con datos de respuesta
Si se envía un comando que requiere datos de respuesta, el periférico enviará uno o más bytes de datos, seguidos por su byte CHK. Finalmente, el periférico enviará un ACK:

Host: CMD* + CHK

Periférico: Dato0, Dato1, ..., DatoN, CHK*

Host: ACK [Este ACK lo genera el dispositivo automáticamente]

#### c. Comando con datos adicionales
Si se envía un comando con datos adicionales y su byte CHK, el periférico responderá con un ACK:

Host: CMD* + Dato0 + Dato1 + ... + DatoN + CHK

Periférico: ACK* 

#### d. Comando con datos adicionales

No hay respuesta desde la máquina periférico, o ésta, responde con un NACK (no comprende la trama) o un RET (repetir ultima trama)

**En este caso, el usuario no debe preocuparse de reintentar enviar la trama inciial, el dispositivo, lo hace de manera automática hasta 5 veces ante de abortar e informar con uan señal audible**

Nota: El asterisco (*) denota que el noveno bit está en 1.


## Características físicas  
- Especificaciones y dimensiones con gráficos.  

