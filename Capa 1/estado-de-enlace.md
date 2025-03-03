El estado de enlace es como verificar si un cable está bien conectado y funcionando. Necesitamos saber esto porque:
- Si el enlace físico no funciona, nada más funcionará.
- Un enlace puede estar "conectado" pero funcionando mal.
- Nos ayuda a diagnosticar problemas básicos de red
### Debian:
#### 1. Identifica las interfaces.
``ip link show``
#### 2. Verifica el estado de cada interfaz.
La información importante:
- Link detected: yes (Hay conexión física).
- Speed: 1000 Mb/s (Velocidad actual de conexión).
- Duplex: Full (El modo de transmisión).
En este caso las condiciones son ideales.

**En VirtualBox se puede simular la desconexión sin tocar cables físicos.** Es decir, se tienen 2 tipos de redes:
- Red Nat (Para salir a Internet).
- Red Interna (Para comunicación entre máquinas virtuales).

### Simular la desconexión:
1. Desde **Debian**, ve a la ventana superior de VirtualBox.
2. En Dispositivos ---> Red

<img src="https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/ea25546cd64f1702919cc3ff4e38d5fb9dbd8681/Capa%201/Capturas/1.3.png"></img>

Actualmente VirtualBox te está mostrando, cómo hay una conexión física para cada interfaz. **Si se desmarca, la interfaz del adaptador 2 (Red Interna)**, ya no aparecerá conectado, y ya no habrá una conexión entre las máquinas virtuales.

- Verificar ejecutando ``sudo ethtool enpos8`` que ya no haya conexión física.
- Probar que ya no hay conexión interna entre las máquinas.
  ``ip link show enp0s8``

<img src="https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/ea25546cd64f1702919cc3ff4e38d5fb9dbd8681/Capa%201/Capturas/1.4.png"></img>
  
  La interfaz aparece en estado DOWN, significa que no está activa.
- Probar conexión por medio de ping:
  ``ping 192.168.100.20``

  <img src="https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/ea25546cd64f1702919cc3ff4e38d5fb9dbd8681/Capa%201/Capturas/1.5.png"></img>

- Desde **Windows**, revisa el estado de conexión:
     Panel de control> Red e Internet> Centro de redes y recursos compartidos > cambiar configuración del adaptador.
  
   <img src="https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/ea25546cd64f1702919cc3ff4e38d5fb9dbd8681/Capa%201/Capturas/1.6.png"></img> 
     
 - Probar conectividad:
   ``ping 192.168.100.10``
   
  <img src="https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/ea25546cd64f1702919cc3ff4e38d5fb9dbd8681/Capa%201/Capturas/1.7.png"></img> 
   
Cuando ejecutas ``ethtool`` estás verificando el estado del enlace físico (Capa 1) y también obtienes información de la Capa 2 (Enlace de Datos). Es una herramienta que te muestra información de ambas capas.
