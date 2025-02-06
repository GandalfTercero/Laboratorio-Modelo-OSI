Verificación de Capa 2
En Debian
Para ver direcciones MAC:
``ip link show``
o
``ifconfig``
Para estadísticas de tramas:
``netstat -i``
En Windows
Para ver la tabla ARP:
``arp -a``
Direcciones MAC
En Debian
Para ver todas las interfaces:
``ip link show``
Interfaces específicas:

enp0s3: 08:00:27:10:3f:b2
enp0s8: 08:00:27:ab:08:7b

Para una interfaz específica:
``ip link show enp0s8``
En Windows
Para ver todas las interfaces:
``ipconfig /all``
Direcciones MAC encontradas:

Ethernet (Red NAT): 08-00-27-64-63-3F
Ethernet 2 (Red Interna): 08-00-27-4B-26-EF

Estructura de una Dirección MAC

Primeros 3 pares (00:1A:2B): OUI (Organizationally Unique Identifier)

Identifica al fabricante
Asignado por IEEE


Últimos 3 pares (3C:4D:5E): Identificador único del dispositivo

Asignado por el fabricante
No debe repetirse



Comunicación en Red
Comunicación Local

Verificación de destino en red local
Proceso ARP para mapear IP a MAC
Construcción de trama Ethernet:

MAC origen
MAC destino
Datos a transmitir



Comunicación Externa
Proceso de comunicación fuera de la red local:

Router identifica necesidad de envío externo
Construcción de trama:

MAC origen: Dispositivo emisor
MAC destino: MAC del router/gateway
IP origen: Dispositivo emisor
IP destino: Dispositivo final
