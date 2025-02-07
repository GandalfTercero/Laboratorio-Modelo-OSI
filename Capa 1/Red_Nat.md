# ¿Por qué es importante empezar con la red nat?
1. Garantizar que hay conexión a internet de los sistemas.
2. Suele tener más tráfico y actividad, lo que te permite ver más tipos de paquetes y estadísticas.
3. Puedes ver cómo funciona la capa física con tráfico real.

# Debian
1. Utilizarás un comando de diagnóstico que muestra información detallada sobre la configuración y el estado de una interfaz:
  ``sudo ethtool enp0s3`` 
#### Enfócate en:
<img src="https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/70b3e7f94d5737bef285716b36a122c62bef50cf/Capa%201/Capturas/1.1.png"></img>

2. Ahora, ejecutas el siguiente comando que muestra las estadísticas detalladas del historial de red (Es como ver el historial de actividad).
``sudo ethtool -S enp0s3``
#### Enfócate en:
<img src="https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/70b3e7f94d5737bef285716b36a122c62bef50cf/Capa%201/Capturas/1.2.png"></img>

Estas estadísticas son útiles para: Diagnosticar problemas de red, Monitorear el rendimiento, Detectar errores de transmisión, Ver cuánto tráfico ha pasado por la interfaz.
#### Lo importante a considerar:
Tu interfaz está funcionando perfectamente (no hay errores)
Hay más tráfico de entrada que de salida (normal en una conexión NAT)
La conexión está configurada para el mejor rendimiento posible (1000baseT/Full)

### Pruebas de conectividad
Para instalar los comando ``wget``y ``curl``, ejecuta:
``sudo apt install wget curl``

1. Como ya tienes las estadísticas anteriores, haz solo 20 pings a Google:
   ``ping -c 20 8.8.8.8``
   
3. Vuelve a ver las estadísticas:
   ``sudo ethtool -S enp0s3``

4. Para descargar algo:
   ``wget www.example.com``

5. Vuelve a ver las estadísticas:
   ``sudo ethtool -S enp0s3``

6. Ejecuta cel "curl" para hacer una petición:
   ``curl www.example.com``

7. Vuelve a ver las estadísticas:
   ``sudo ethtool -S enp0s3``

Al hacer los comandos con curl y wget, el número de bytes recibidos y transmitidos como los paquetes recibidos y transmitidos aumentaron a medida que ejecutaba un nuevo comando, sin embargo no se presentó ningún error de recepción y de transmisión.

#### 1. Aumento de bytes y paquetes:
Esto demuestra que la capa física está transmitiendo y recibiendo datos correctamente.
Cada comando genera tráfico de red que se refleja en los contadores.
El incremento en las estadísticas confirma que los datos están fluyendo por el medio físico (en este caso virtual)

#### 2. Ausencia de errores:
rx_errors: 0 y tx_errors: 0 indican que:
La señal es clara y estable.
No hay problemas en la transmisión física.
La interfaz está funcionando de manera óptima.

#### 3. No hay paquetes descartados, lo que significa que no hay problemas de capacidad

# Windows
1. Abre el símbolo del sistema (CMD) como administrador:

    Presiona Windows + X
   
Selecciona "Windows PowerShell (Admin)"

2. Para ver estadísticas detalladas de la conexión, puedes usar estos comandos:
``ipconfig /all``
#### Enfócate prinicpalmente en:

- Tipo de adaptador de red: El nombre de las interfaces de red.
- Velocidad de la conexión: indica la velocidad de conexión en Mbps
- Dirección física (MAC): Tu dirección MAC única.
- Estado de DHCP: Si está habilitado o desabilidato.
- Sufijo DNS específico para la conexión: importante para la resolución de nombres

#### Para ver estadísticas de rendimiento:
``netstat -e``

- Muestra estadísticas acumuladas de TODAS tus interfaces de red activas
- "Bytes" muestra el tráfico total enviado y recibido
- "Errors" indica errores de transmisión

