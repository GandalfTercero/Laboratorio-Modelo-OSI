# Usar el modo BRIDGE (OSI-Lab).
Si configuras el Adaptador 1 en modo Bridge, ambas máquinas virtuales estarán en la misma red que el host.
En este caso, podrías capturar el tráfico de Windows mientras visita una página web cualquiera, ya que el tráfico pasaría por la interfaz de red de Debian.
## 1. En VitualBox:
* Ve a "Herramientas" > "redes NAT".
  (imagen 4-0)
* Selecciona la red OSI-Lab y haz clic en "Eliminar".
## 2. Verifica la configuración de las máquinas virtuales:
* Asegúrate de que el Adaptador 1 de ambas máquinas virtuales (Debian y Windows) esté configurado como Bridge.
* Si el Adaptador 1 está asignado a la red OSI-Lab, cámbialo a Bridge.

