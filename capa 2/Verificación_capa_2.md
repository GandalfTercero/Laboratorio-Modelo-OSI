# Verificación de Capa 2
## Para ver direcciones MAC:
### En Debian

    ip link show
o

    ifconfig
Para estadísticas de tramas:

    netstat -i
### En Windows
Para ver la tabla ARP:

    arp -a
## Direcciones MAC
### En Debian
Para ver todas las interfaces:

    ip link show
Interfaces específicas:

enp0s3: 08:00:27:10:3f:b2
enp0s8: 08:00:27:ab:08:7b

Para una interfaz específica:

    ip link show enp0s8
En Windows
Para ver todas las interfaces:

    ipconfig /all
Direcciones MAC encontradas:

Ethernet (Red NAT): 08-00-27-64-63-3F
Ethernet 2 (Red Interna): 08-00-27-4B-26-EF
