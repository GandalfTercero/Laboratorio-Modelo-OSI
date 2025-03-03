# Las direcciones MAC en la comunicación
Cuando dos dispositivos se comunican en una red local (como Ethernet o Wi-Fi), **ambos usan sus propias direcciones MAC**, pero de forma estratégica:
- **Dirección MAC origen:**  La de tu interfaz de red (tu dispositivo).
- **Dirección MAC destino:** La del dispositivo al que te estás comunicando (obtenida de la tabla ARP).

Para un laboratorio práctico donde queremos ver la comunicación entre máquinas virtuales, es mejor usar la red interna por estas razones:

**Con red interna:**

- Las máquinas virtuales se pueden comunicar directamente entre sí
- Puedes ver todo el tráfico real entre ellas
- Es un entorno aislado y controlado
- Perfecto para ver el comportamiento real de ARP y las tramas

**Con red NAT:**

- Todo el tráfico pasa por el router NAT virtual de VirtualBox.
- No verías la comunicación directa entre máquinas.
- Es más difícil observar el proceso real de las tramas.

# Capturar tráfico de red con tcdump
Usa tcpdump para observar las tramas en la red local. Necesitas usar DOS terminales al mismo tiempo para ver el proceso.
- La razón de por qué utilizas 2 terminales es:
  - Tcpdump captura el tráfico en tiempo real.
  - Si ejecutas ping después de tcpdump, no verías nada porque tcpdump ya habría terminado.
  - Al tener ambas terminales abiertas, puedes ver cómo tcpdump muestra las tramas que genera el ping

   
### Terminal 1:

    sudo tcpdump -i enp0s8 -e
- El parámetro -e muestra las direcciones MAC en las tramas Ethernet. (Déjala corriendo, este comando se queda monitoreando el tráfico)

### Terminal 2:
ping a la dirección IP de Windows.

    ping 192.168.100.20

## Deberías ver:
1. Estructura de una línea de tcpdump -e, cada línea muestra:
- Hora: 16:16:25.636401.
- MAC origen > MAC destino.
- Tipo de trama (ej: ARP, IPv4).
- Detalles del protocolo (ej: ICMP echo request).
  
2. Identificando las tramas ARP
   
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/467708eee62207c6020d3a9e367d78397daee038/capa%202/im%C3%A1genes-capa-2/2.5.png>
  a) Primera trama ARP (Request):Color azul.
  
  - MAC origen: 08:00:27:ab:08:7b (dispositivo con IP 192.168.100.10, máquina Debian).
  - MAC destino: Broadcast (envía a todos los dispositivos en la red).
  - El dispositivo 192.168.100.10 pregunta: "¿Quién tiene la IP 192.168.100.20?".
    
  b) Segunda trama ARP (Reply): Color verde.
  
  - MAC origen: 08:00:27:4b:26:ef (tu interfaz enp0s8 con IP 192.168.100.20).
  - MAC destino: 08:00:27:ab:08:7b (dispositivo que hizo la pregunta).
  - La máquina windows responde: "Yo tengo la IP 192.168.100.20, mi MAC es 08:00:27:4b:26:ef ".
    
  c) Tercera y cuarta trama ARP (Request inverso): Color amarillo.
  
  - MAC origen: 08:00:27:4b:26:ef (tu interfaz enp0s8).
  - MAC destino: 08:00:27:ab:08:7b (dispositivo 192.168.100.10).
  - Tipo: ARP Request.
  - La máquina pregunta: "¿Sigues teniendo la IP 192.168.100.10?" (esto es normal para verificar la entrada ARP en caché).
  - MAC origen: 08:00:27:ab:08:7b (dispositivo 192.168.100.10).
  - MAC destino: 08:00:27:4b:26:ef (tu interfaz).
  - Tipo: ARP Reply.
  - El dispositivo confirma: "Sí, sigo teniendo la IP 192.168.100.10".
    
3. Identificando las tramas ICMP (ping)
  - Tipo: ICMP echo request (ping enviado desde 192.168.100.10 a tu máquina).
  - Tipo: ICMP echo reply (respuesta al ping).

## Flujo completo de comunicación:
- ARP Request (192.168.100.10 pregunta por 192.168.100.20).
- ARP Reply (Tu máquina responde con su MAC).
- ICMP echo request (ping de 192.168.100.10 a tu máquina).
- ICMP echo reply (tu máquina responde al ping).
- ARP Request inverso (tu máquina verifica la MAC de 192.168.100.10).
- ARP Reply inverso (192.168.100.10 confirma su MAC).

###  ¿Por qué hay ARP si ya se conocían las MACs?
- Las entradas ARP tienen un tiempo de vida (TTL). Después de unos minutos, el sistema verifica si la MAC sigue asociada a la IP (por eso los ARP posteriores).
