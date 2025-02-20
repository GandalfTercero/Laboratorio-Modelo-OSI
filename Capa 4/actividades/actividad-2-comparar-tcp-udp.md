## 1. En Debian:
* Usa netcat para crear un servidor UDP:

      nc -u -l -v -p 1234
* En otra terminal, usa netcat para crear un servidor TCP:

      nc -l -v -p 1234

Los servidores UDP y TCP en Debian no muestran salida inmediata porque están en modo de escucha.
## 2. En Windows:
* Conéctate al servidor UDP en Debian:
  
      $udpClient = New-Object System.Net.Sockets.UdpClient
  
      $udpClient.Connect("10.0.0.46", 1234)
  
      $mensaje = "MENSAJE DE PRUEBA - SI VES ESTO, LA CONEXIÓN UDP FUNCIONA"
  
      $bytes = [Text.Encoding]::ASCII.GetBytes($mensaje)
  
      $enviados = $udpClient.Send($bytes, $bytes.Length)

* Conéctate al servidor TCP en Debian:

      Test-NetConnection -ComputerName 10.0.0.46 -Port 1234
## 3. Em Wireshark:
* Abre Wireshark en Windows
* Selecciona tu interfaz de red
* Usa este filtro para ver solo el tráfico relevante:

      tcp.port == 1234
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/865826e70ed7fc1eaea2032e69720e33056e0b4e/Capa%204/im%C3%A1genes%20capa%204/4.10.png></img>
  
  o
      
      udp.port == 1234
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/865826e70ed7fc1eaea2032e69720e33056e0b4e/Capa%204/im%C3%A1genes%20capa%204/4.11.png></img>
## 4. Servidor UDP:
**En Windows:**
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/865826e70ed7fc1eaea2032e69720e33056e0b4e/Capa%204/im%C3%A1genes%20capa%204/4.12.png></img>
Una vez ejecutado sale bytes enviados: 40.
**En Debian**
Debes ver el mensaje
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/865826e70ed7fc1eaea2032e69720e33056e0b4e/Capa%204/im%C3%A1genes%20capa%204/4.13.png></img>



