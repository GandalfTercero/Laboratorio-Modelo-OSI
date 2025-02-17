**1. Elimina o desactiva la red NAT personalizada (OSI-Lab).**
Como inicialmente tenemos una red NAT personalizada:
(aquí va la imagen 4.0)

**Toca eliminarla**
En VirtualBox:
  - Ve a "Herramientas" > "redes NAT".
  - Selecciona la red OSI-Lab y haz clic en "Eliminar".
**Verifica la configuración de las máquinas virtuales:**
  - Asegúrate de que el Adaptador 1 de ambas máquinas virtuales (Debian y Windows) esté configurado como Bridge.
  - Si el Adaptador 1 está asignado a la red OSI-Lab, cámbialo a Bridge.
