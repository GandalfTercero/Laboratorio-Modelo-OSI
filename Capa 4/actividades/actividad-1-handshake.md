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
  (imagen 4.7)
  
