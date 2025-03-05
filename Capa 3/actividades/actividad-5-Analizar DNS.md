# Analizar DNS (Capa 7 + Capa 3)
Ver cómo se resuelven nombres de dominio a IPs.
### 1. Abrir wireshark:
- Selecciona la interfaz de la red nat en windows o Debian (donde vas a trabajar).
- Aplica el filtro ``dns``.
### 2. Ejecutar ``nslookup``
- En Windows/Debian:

      nslookup google.com

Lo hice con windows:
  
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/217a572e171837800756a00c8ed1a9aa95be49e2/Capa%203/im%C3%A1genes-capa-3/3.13.png>

**Explicación:**
- **Servidor** : ``RTK_GW.bbrouter`` es el nombre del servidor DNS que respondió a tu consulta.
    - Su dirección IP es ``10.0.0.10``.
- **Respuesta no autoritativa** :
    - Esto significa que el servidor DNS (10.0.0.10) no es la fuente oficial (autoritativa) para el dominio google.com. En cambio, obtuvo la información de otro servidor DNS en la jerarquía DNS.
- **Direcciones resueltas** :
    - google.com tiene dos direcciones:
        - Una dirección IPv6: ``2800:3f0:4005:40c::200e``.
        - Una dirección IPv4: ``142.250.218.78``.

### 3. Captura de Wireshark durante ``nslookup``

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/217a572e171837800756a00c8ed1a9aa95be49e2/Capa%203/im%C3%A1genes-capa-3/3.12%20(2).png>

- Líneas 7-10: Consultas correctas
  - Consulta A :
      - Tu máquina pregunta: "¿Cuál es la dirección IPv4 de ``google.com``?"
      - El servidor DNS responde: "``google.com`` tiene la dirección IPv4 ``142.250.218.78``."
  - Consulta AAAA :
      - Tu máquina pregunta: "¿Cuál es la dirección IPv6 de ``google.com``?"
      - El servidor DNS responde: "``google.com`` tiene la dirección IPv6 ``2800:3f0:4005:40c::200e``."

## salida del comando ping:
Antes de enviar el ping, tu máquina necesita saber la dirección IP de google.com.
  - Si la dirección IP ya está en la caché DNS de tu máquina, no se realiza una nueva consulta DNS.
  - Si no está en caché, tu máquina vuelve a consultar al servidor DNS para obtener la dirección IP.
En este caso, hay una nueva consulta DNS (``A google.com``) justo antes del ``ping``. Esto significa que la dirección IP no estaba en caché o que el sistema decidió volver a resolver el nombre por seguridad.

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/217a572e171837800756a00c8ed1a9aa95be49e2/Capa%203/im%C3%A1genes-capa-3/3.12.png>

### Después de obtener la dirección IP, tu máquina le envía un ping a Google
Una vez que tu máquina tiene la dirección IP de google.com (por ejemplo, 142.250.78.174), envía un paquete ICMP (ping) hacia esa dirección.
Google responde con un paquete ICMP, indicando que está disponible.

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/217a572e171837800756a00c8ed1a9aa95be49e2/Capa%203/im%C3%A1genes-capa-3/3.14.png>

## Resumen del flujo completo
1. ``nslookup google.com`` :
    - Tu máquina consulta al servidor DNS para obtener la dirección IP de ``google.com``.
    - El servidor DNS responde con las direcciones IPv4 e IPv6.
2. ``ping google.com`` :
    - Antes de enviar el ``ping``, tu máquina verifica si la dirección IP de ``google.com`` está en caché.
    - Si no está en caché (o si el sistema decide verificar nuevamente), tu máquina consulta al servidor DNS otra vez.
    - Una vez que tiene la dirección IP, envía un paquete ICMP (``ping``) hacia esa dirección.
3. **Wireshark** :
    - Capturas todas las consultas DNS y el tráfico ICMP generado por el ``ping``.
    - También ves consultas adicionales (como ``wpad.bbrouter``), que son irrelevantes para este caso.
