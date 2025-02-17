## 1. En Debian:
* Usa netcat para crear un servidor UDP:
  ``nc -u -l -v -p 1234``
* En otra terminal, usa netcat para crear un servidor TCP:
  ``nc -l -v -p 1234``

Los servidores UDP y TCP en Debian no muestran salida inmediata porque están en modo de escucha.
## 2. En Windows:
* Conéctate al servidor UDP en Debian:
  
    ``$udpClient = New-Object System.Net.Sockets.UdpClient``
  
    ``$udpClient.Connect("10.0.0.46", 1234)``
  
    ``$mensaje = "MENSAJE DE PRUEBA - SI VES ESTO, LA CONEXIÓN UDP FUNCIONA"``
  
    ``$bytes = [Text.Encoding]::ASCII.GetBytes($mensaje)``
  
    ``$enviados = $udpClient.Send($bytes, $bytes.Length)``

(imagen 4.23)
* Conéctate al servidor TCP en Debian:
  ``Test-NetConnection -ComputerName 10.0.0.46 -Port 1234``
## 3. Em Wireshark:
* Abre Wireshark en Windows
* Selecciona tu interfaz de red
* Usa este filtro para ver solo el tráfico relevante:
  ``tcp.port == 1234 ``
  (imagen 4.10)
  
  o
  
  ``udp.port == 1234``
  (imagen 4.11)
## 4. Servidor UDP:
**En Windows:**
(imagen 4.12)
Una vez ejecutado sale bytes enviados: 40.
**En Debian**
Debes ver el mensaje
(imagen 4.13)



