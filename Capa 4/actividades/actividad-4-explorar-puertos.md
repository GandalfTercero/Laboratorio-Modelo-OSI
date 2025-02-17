# Explorar el uso de puertos
## 1. En Dibian:
1. Usa netstat para ver los puertos abiertos o activos en mi sistema:
  ``sudo netstat -tuln``

La salida mostrará una lista de puertos y los servicios asociados. Por ejemplo:

(imagen 4.18)

Aquí, 0.0.0.0:22 indica que el puerto 22 (SSH) está abierto y escuchando conexiones.

(imagen 4.8)

En mi caso tengo puerto 631 y puerto 55378, 5353, 50754.

2. La información me muestra:

- Los protocolos en uso (TCP/UDP)
- Las direcciones IP y puertos locales
- Las direcciones IP y puertos remotos

3. El estado de las conexiones
Tengo el puerto 631 escuchando en localhost (127.0.0.1), que típicamente es el puerto para impresión (CUPS)
4. Hay varios servicios UDP como el 5353 que es para DNS multicast

## 2. En Windows:
1. Usa netstat para ver los puertos abiertos:
   ``netstat -an``

La salida mostrará una lista de puertos y conexiones. Por ejemplo:

(imagen 4.19)

Aquí, 0.0.0.0:80 indica que el puerto 80 (HTTP) está abierto y escuchando conexiones.

(imagen 4.9)

2. Hay más conexiones activas, algunas importantes son:
  - Puerto 445: usado para compartir archivos (SMB)
  - Puerto 135: usado para RPC (Remote Procedure Call)
  - Puertos altos (49664-49670): usados por varios servicios del sistema

## 3. Relacionar los puertos con los servicios:
### 1. En Debian:
1. Usa el siguiente comando para ver los servicios asociados a los puertos:
   ``sudo lsof -i -P -n``

   (imagen 4.20)
   - El avahi-dae está usando el puerto 5353. un servicio que implementa el protocolo mDNS (Multicast DNS) . Este protocolo permite la resolución de nombres en redes locales sin necesidad de un servidor DNS centralizado.
   - cupsd está usando el puerto 631 que es para imprimir.cupsd es el demonio del sistema CUPS (Common Unix Printing System) , que gestiona las impresoras en sistemas Linux. Puerto 631 (TCP) : Es el puerto estándar para el protocolo IPP (Internet Printing Protocol), que permite configurar y gestionar impresoras en red.
   - https está usando el puerto 53, que es de DNS.Este proceso indica que el sistema está realizando una consulta DNS (puerto 53) desde la dirección IP 10.0.2.5 hacia el servidor DNS en 10.0.0.10.

 Ahora, ya que conoces los puertos y los servicios asociados que tienes en tus máquinas, relaciona los puertos con los servicios:

 2. Ejecuta el comando:
    ``cat /etc/services | grep <puerto>``

    Este archivo contiene una lista de puertos bien conocidos y sus servicios asociados. Por ejemplo:
    ``cat /etc/services | grep 5353``

    Esto te mostrará que el puerto 5353 está asociado a mdns
### 2. En Windows:
1. Usa el siguiente comando en PowerShell para ver los servicios asociados a los puertos:
   
  ``Get-Process -Id (Get-NetTCPConnection -LocalPort 80).OwningProcess``
  - Aquí especificamos el puerto 80, pero puedes utilizar otro puerto que quieras consultar.
  - Este comando busca información sobre las conexiones TCP que utilizan el puerto local 80.

La salida mostrará el proceso que está usando el puerto 80. Por ejemplo: Aquí, httpd es el proceso que está usando el puerto 80.

(imagen 4.21)

### 3. En Wireshark
* Filtra el tráfico por puertos específicos. Por ejemplo, para ver el tráfico en el puerto 80:
  
    ``tcp.port == 631``
Esto mostrará solo el tráfico TCP relacionado con el puerto 631 (CUPS).
* Si quieres filtrar UDP en lugar de TCP, usa:
  
    ``udp.port == 5353``

(imagen 4.22)
