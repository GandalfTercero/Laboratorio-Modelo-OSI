# Pruebas de Conectividad en la Red Interna
Ahora que sabemos que las IPs están configuradas correctamente, podemos verificar si las máquinas pueden comunicarse entre sí y acceder a Internet.
## Iniciar wireshark:
- Abre Wireshark en la máquina donde deseas capturar el tráfico.
- Selecciona la interfaz de red correspondiente:
    - En Debian : Selecciona enp0s8 (la interfaz de red interna).
    - En Windows : Selecciona la interfaz ethernet 2.
- Usa el filtro ``icmp`` en Wireshark para mostrar solo los paquetes relacionados con el comando ``ping`` (Esto reduce el ruido y te permite enfocarte en los paquetes relevantes).
  
### En Debian:
    ping 192.168.100.20  # Ping a Windows (Red Interna)

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/2e4ca815c0116cb90a8d6e7373ccb396849e3c87/Capa%203/im%C3%A1genes-capa-3/3.4.png>

### En Windows (cmd):
    ping 192.168.100.10  # Ping a Debian (Red Interna)}
    
## Analizar los paquetes
Mientras ejecutas los comandos ``ping``, observa los paquetes capturados en Wireshark:
  - Verifica que las direcciones IP origen y destino coincidan con las IPs de la red interna:
    - Origen: ``192.168.100.10`` (Debian) → Destino: ``192.168.100.20`` (Windows).
    - Origen: ``192.168.100.20`` (Windows) → Destino: ``192.168.100.10`` (Debian).
  - Asegúrate de que los paquetes sean de tipo ICMP (protocolo usado por ``ping``).

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/2e4ca815c0116cb90a8d6e7373ccb396849e3c87/Capa%203/im%C3%A1genes-capa-3/3.5.png>

#### 1. Paquetes ICMP de solicitud y respuesta :
- Cuando haces ``ping``, se envían paquetes ICMP de tipo "Echo Request" desde la máquina origen.
- La máquina destino responde con paquetes ICMP de tipo "Echo Reply".
#### 2. Direcciones IP correctas :
- Las direcciones IP origen y destino deben coincidir con las IPs de la red interna (192.168.100.x).
- Como estás trabajando en la red interna, no debería haber traducción de direcciones (NAT). Las IPs deben ser las mismas tanto en origen como en destino.

Entonces, esto confirma que:
- El tráfico fluye directamente entre las dos máquinas en la red interna.
- No hay NAT ni intermediarios involucrados.
