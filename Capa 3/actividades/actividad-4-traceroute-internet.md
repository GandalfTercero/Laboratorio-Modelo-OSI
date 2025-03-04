# Traceroute/tracert a un destino en Internet:
Estos comandos permiten visualizar los **saltos intermedios** (routers o dispositivos de red) que los paquetes atraviesan para llegar a un destino en Internet. Cada "salto" representa un router por el que pasa el tráfico.

El propósito principal es:
1. Identificar la ruta que siguen los paquetes desde tu máquina hasta el destino.
2. Detectar posibles problemas en la red, como routers inalcanzables o latencias altas.

## En Debian (bash):
    traceroute 8.8.8.8
(imagen 3.10)

### Análisis en la salida:
- Primer salto : 10.0.2.1 (el gateway NAT de VirtualBox).
    - Este es el primer dispositivo que recibe el tráfico desde tu VM. Es el router virtual configurado por VirtualBox.
- Saltos siguientes (* * *) :
    - Los asteriscos indican que no se recibió respuesta desde esos routers.
    - Esto puede suceder por varias razones:
          1. **Restricciones de seguridad** : Algunos routers están configurados para ignorar las solicitudes de traceroute (ICMP o UDP).
          2. **Firewalls** : Pueden bloquear el tráfico generado por traceroute.
          3. **NAT en VirtualBox** : VirtualBox podría estar limitando la visibilidad de los saltos más allá del gateway NAT.

- **Resumen** : Solo puedes ver el primer salto (``10.0.2.1``), pero los saltos siguientes no son visibles debido a restricciones técnicas o de configuración.

## Windows (cmd):
    tracert 8.8.8.8
    
(imagen 3.11)

#### Análisis en la salida:
- **Primer salto** : ``10.0.2.1`` (el gateway NAT de VirtualBox).
    - Igual que en Debian, este es el primer dispositivo que recibe el tráfico desde tu VM.
- **Segundo salto** : ``RTK_GW.bbrouter [10.0.0.10]`` (probablemente el router del host físico o un dispositivo interno de VirtualBox).
- Saltos siguientes :
    - Estos representan los routers intermedios entre tu red local y el destino (``8.8.8.8``).
    - Por ejemplo:
        - ``100.70.141.1``: Un router en tu ISP (proveedor de servicios de Internet).
        - ``72.14.234.243``: Un router en la red de Google.
        - ``dns.google [8.8.8.8]``: El destino final (Google DNS).
- **Resumen** : En Windows, puedes ver claramente todos los saltos hasta llegar al destino. Esto te permite identificar la ruta completa que siguen los paquetes.

- ## ¿Por qué hay diferencias entre Linux y Windows?
- La diferencia clave está en cómo traceroute (Linux) y tracert (Windows) funcionan:

- traceroute (Linux) :
    - Usa UDP por defecto para enviar paquetes.
    - Algunos routers o firewalls pueden bloquear estos paquetes, lo que resulta en saltos invisibles (* * *).
- tracert (Windows) :
    - Usa ICMP (protocolo de mensajes de control de Internet) para enviar paquetes.
    - ICMP es más ampliamente aceptado, por lo que es más probable que obtengas respuestas de los routers intermedios.
Además, VirtualBox podría estar manejando el tráfico de manera diferente dependiendo del sistema operativo.

## ¿Con qué fin haces traceroute/tracert?
- **Diagnosticar problemas de red**
    - Si un salto específico muestra tiempos de respuesta muy altos o no responde (* * *), puede indicar un problema en ese router.
    - Puedes detectar si el tráfico está siendo bloqueado por firewalls o configuraciones de red.
- **Aprender sobre redes**
    - Te ayuda a entender cómo funciona el enrutamiento en Internet.
    - Observas cómo los paquetes viajan a través de múltiples redes antes de llegar al destino.
    - Aprender sobre las diferencias entre herramientas de diagnóstico en diferentes sistemas operativos.
