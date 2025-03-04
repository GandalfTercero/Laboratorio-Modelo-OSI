# Capa 3 - Capa de enlace de datos.
## Objetivo
Este laboratorio práctico permite explorar la Capa 3 (Red) del modelo OSI, enfocándose en direccionamiento IP, enrutamiento y análisis de paquetes. Aprenderás:
- Cómo las direcciones IP permiten la comunicación lógica entre redes.
- El rol de las tablas de enrutamiento y gateways.
- La diferencia entre Capa 2 (Enlace de datos) y Capa 3 (Red).

## Configuración del Entorno
- Máquinas Virtuales (VMs):
  - Debian:
    - Red NAT: 10.0.2.5
    - Red Interna: 192.168.100.10

  - Windows 10:
    - Red NAT: 10.0.2.6
    - Red Interna: 192.168.100.20

- Herramientas:
  - Wireshark (instalado en ambas VMs).
  - Comandos CLI: ``ping``, ``route``, ``traceroute``, ``arp``.

## Preguntas para Entender la Diferencia entre Capa 2 y Capa 3
**1. Direccionamiento:**

  - ¿Por qué las direcciones MAC (Capa 2) no se usan para comunicaciones en Internet, pero las IPs (Capa 3) sí?

**2. Alcance:**

  - Si dos dispositivos están en la misma red, ¿es necesario un router (Capa 3) para que se comuniquen?

**3. Encapsulación:**

  - En Wireshark, ¿por qué un paquete ICMP muestra tanto direcciones IP como MAC?

**4. Tablas:**

  - ¿Qué ocurriría si eliminas la entrada de la red 192.168.100.0/24 en la tabla de enrutamiento de Debian?

**5. Caso Práctico:**

  - Si haces ping desde Debian (10.0.2.5) a Windows (10.0.2.6) en la red NAT:
    - ¿Se usa ARP? ¿Por qué?
    - ¿Qué diferencia hay frente a un ping en la red interna?

## Conclusiones Clave
- **Capa 2 (MAC):** Gestiona la comunicación física en una red local (misma subred).
- **Capa 3 (IP):** Permite el enrutamiento lógico entre redes diferentes.
- **Sinergia:** Ambas capas trabajan juntas: las IPs definen el destino final, las MACs el próximo salto físico.

## Notas para el Usuario:
- Asegúrate de que las VMs tengan ambas interfaces de red activas.
- Si los pings fallan, verifica firewalls.
