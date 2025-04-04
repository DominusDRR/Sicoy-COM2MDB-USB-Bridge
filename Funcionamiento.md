## Conexión al PC mediante cable USB.

El dispositivo se alimenta directamente del voltaje proporcionado por el puerto USB. Por otro lado, la conexión de 24V en la bornera inferior es exclusivamente para suministrar energía al bus MDB y no forma parte del funcionamiento interno del dispositivo.

Para conectar el dispositivo, utilice un cable USB según se muestra en la siguiente figura.

Al conectar el dispositivo al puerto USB, el sistema operativo asignará automáticamente un número de puerto COM virtual.

Cuando el dispositivo se energiza, emite una breve tonada musical, indicando que está listo para operar.

Una vez identificado el puerto COM asignado, el usuario podrá enviar y recibir tramas utilizando cualquier aplicación compatible con comunicación serie.

## Ejemplos de Comandos MDB.

### Comando reinicio de monedero.

Este comando reinicia al monedero conectado al bus MDB, y su trama es así:

0xFE 0x08 0x01 0xFE 0x08 0x00

La respuesta a este comando es un ACK, que significa que el comando ha sido procesado correctamente, el cual es 0x00

![image](https://github.com/user-attachments/assets/dbfcb8dc-6237-4c76-a8ac-ce769a4bfc61)


### Comando POLL de monedero.

Este comando solicita de cambio de estado de actividad, lo cual permite obtener un reporte por parte del monedero.

Si no tiene nada que reportar, retorna un ACK.

Si tiene que reportar algo, y puede retornar hasta 16 bytes. Si desea conocer el significado de esos datos, consulte la sección 5 del manual del protocolo MDB ->  [MDB protocol versión 4.3 (julio de 2019)](https://www.cable-tester.com/references/mdb-connector-pin-out/mdb-protocol-ver-4_3.pdf)

Su trama sera:

0xFE 0x0B 0x01 0xFE 0x0N 0x00


### Comando habilitación de monedas en el monedero.

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



 
### Habilitación de caracteristicas especiales con subcomando igual a 0x01.

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






