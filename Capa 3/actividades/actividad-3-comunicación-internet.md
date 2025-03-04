# Comunicación con internet
Entender cómo las VMs acceden a Internet a través de NAT.
## Iniciar Wireshark:
1. Abre Wireshark en la máquina donde deseas capturar el tráfico y selecciona la interfaz de red correspondiente:
- En Debian : Selecciona enp0s3 (la interfaz NAT).
- En Windows : Selecciona Ethernet.

2. Usa el filtro ``icmp`` en Wireshark para mostrar solo los paquetes relacionados con el comando ``ping``. Esto reduce el ruido y te permite enfocarte en los paquetes relevantes.

### En Debian:
    ping 8.8.8.8  # Ping a una IP pública (Google DNS)
    ping google.com  # Requiere DNS

(imagen 3.6)

### En Windows:
    ping 8.8.8.8  # Ping a una IP pública (Google DNS)
    ping google.com  # Requiere DNS
    
(imagen 3.7)

## Análisis con Wireshark:
Aquí tienes una lista de elementos clave que debes observar en Wireshark durante el análisis:

1. Dirección IP origen
    - La dirección IP origen debe ser la de la interfaz NAT (10.0.2.x), no la de la red interna (192.168.100.x).
    - Ejemplo: Si estás en Debian, la IP origen debería ser 10.0.2.5.
    - Esto confirma que el tráfico está saliendo a través de la red NAT.
2. Dirección IP destino
    - La dirección IP destino debe ser la IP pública que estás intentando alcanzar.
    - Ejemplo: Si haces ping 8.8.8.8, la IP destino será 8.8.8.8.
3. Protocolo ICMP
    - Los paquetes deben ser de tipo ICMP, ya que ``ping`` utiliza este protocolo.
4. Traducción de direcciones (NAT)
    - VirtualBox realiza NAT (Network Address Translation) para permitir que las VMs accedan a Internet.
    - En Wireshark, observa lo siguiente:
      - Desde la perspectiva de la VM, los paquetes tienen como origen la IP privada (10.0.2.x).
      - Desde la perspectiva del host físico (si capturas tráfico en el host), los paquetes tendrán como origen la IP pública del host, es decir: desde la perspectiva de Internet, el tráfico parece provenir del host físico, no de las VMs.
5. Resolución DNS
    - Si haces ping google.com, observa cómo se resuelve el nombre de dominio a una IP pública:
    - Busca paquetes DNS (filtrando por dns en Wireshark).
        - **Debian**:
      (imagen 3.8)

        - **Windows**:
          
      (imagen 3.9)

     - Estás viendo cómo las VMs resuelven nombres de dominio (google.com, client.wns.windows.com) en direcciones IP.
     - Consultas inversas : También estás viendo cómo las VMs intentan resolver direcciones IP de vuelta a nombres de dominio.
