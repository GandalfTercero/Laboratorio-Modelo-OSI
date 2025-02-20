# Analizar el handshake de TCP
## 1. En Debian.
* Abre Wireshark y selecciona la interfaz de red en modo Bridge (enp0s3).
* Aplica un filtro para capturar solo tráfico TCP:
  ``tcp``
## 2. En Windows.
* Abre el navegador, si tienes una página ya configurada verás inmediatamente en wireshark el handshake. Caso contrario, busca cualquier página web.
## 3. En Wireshark.
* Observa los paquetes SYN, SYN-ACK y ACK del handshake de TCP.
* También verás las solicitudes HTTP (GET) y las respuestas (HTTP/1.1 200 OK).
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/69531bff58a4f52413e0646c787fc5d4d1ffc3c6/Capa%204/im%C3%A1genes%20capa%204/4.7.png></img>
Esto sucede porque muchos protocolos modernos utilizan HTTP como base para iniciar la conexión antes de pasar a un protocolo más especializado.
