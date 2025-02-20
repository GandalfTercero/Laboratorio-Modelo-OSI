# Usar el modo BRIDGE (OSI-Lab).
Si configuras el Adaptador 1 en modo Bridge, ambas máquinas virtuales estarán en la misma red que el host.
En este caso, podrías capturar el tráfico de Windows mientras visita una página web cualquiera, ya que el tráfico pasaría por la interfaz de red de Debian.
## 1. En VitualBox:
* Ve a "Herramientas" > "redes NAT".
  <img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/1f1cc972b45e404ebea8df33bc00ab2fb1640fdf/Capa%204/im%C3%A1genes%20capa%204/4.0.png></img>
* Selecciona la red OSI-Lab y haz clic en "Eliminar".
### ¿Por qué hay que eliminarlo?
* Si tienes una red NAT personalizada configurada, VirtualBox la usará incluso si el Adaptador 1 está configurado como Bridge.
* Esto hace que las máquinas virtuales obtengan direcciones IP de la red NAT personalizada en lugar de la red física.
### El modo Bridge no funciona correctamente:
* Cuando hay una red NAT personalizada activa, el modo Bridge no puede obtener direcciones IP de la red física.

## 2. Verifica la configuración de las máquinas virtuales:
* Asegúrate de que el Adaptador 1 de ambas máquinas virtuales (Debian y Windows) esté configurado como Bridge.
* Si el Adaptador 1 está asignado a la red OSI-Lab, cámbialo a Bridge.
  
