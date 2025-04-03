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


### Comando POLL de monedero.

Este comando solicita de cambio de estado de actividad, lo cual permite obtener un reporte por parte del monedero.

Si no tiene nada que reportar, retorna un ACK.

Si tiene que reportar algo, y puede retornar hasta 16 bytes. Si desea conocer el significado de esos datos, consulte la sección 5 del manual del protocolo MDB ->  [MDB protocol versión 4.3 (julio de 2019)](https://www.cable-tester.com/references/mdb-connector-pin-out/mdb-protocol-ver-4_3.pdf)




