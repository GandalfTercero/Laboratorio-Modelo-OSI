# Capa 5, Capa de sesión.
Este laboratorio tiene como objetivo ayudarte a entender cómo funciona la capa de sesión (Capa 5) del modelo OSI en la práctica. A través de ejemplos concretos, explorarás cómo se establecen, gestionan y terminan las sesiones entre aplicaciones en diferentes sistemas. Utilizaremos protocolos como SMB (Server Message Block) y RPC (Remote Procedure Call) para observar cómo la capa de sesión gestiona las interacciones entre aplicaciones distribuidas.

## ¿Qué vamos a entender?
1. El papel de la capa de sesión:
  - Cómo se diferencia de las capas inferiores (como la capa de transporte).
  - Cómo gestiona las conexiones entre aplicaciones específicas mientras estas intercambian datos.
2. Cómo funcionan los protocolos SMB y RPC:
  - SMB: Observarás cómo se comparten archivos entre sistemas (Windows y Debian) y cómo se mantienen las sesiones mientras realizas operaciones como crear, modificar y eliminar archivos.
  - RPC: Verás cómo una aplicación en un sistema puede invocar funciones remotas en otro sistema, utilizando llamadas RPC.
3. Monitoreo y análisis del tráfico:
  - Usando herramientas como Wireshark, podrás capturar y analizar el tráfico de red para observar cómo se gestionan las sesiones a nivel de paquetes.

## ¿Con qué trabajamos?
**1. Entorno de trabajo:**
  - Dos máquinas virtuales configuradas en VirtualBox:
    
    - **Debian (Linux):** Actúa como servidor.
      
    - **Windows 10:** Actúa como cliente.
  - Dos redes configuradas:
    
    - **Red NAT:** Para conectividad básica.
      
    - **Red interna:** Para simular un entorno de red local. En este caso vas a trabajar con esta.
  
#### 2. Herramientas y protocolos utilizados:

  - **Samba:** Configuramos un servidor SMB en Debian para compartir archivos con Windows.
  
  - **rpcbind:** Configuramos un servicio RPC básico para realizar llamadas remotas.
  
  - **Wireshark:** Capturamos y analizamos el tráfico de red para observar cómo funcionan SMB y RPC a nivel de paquetes.

#### 3. Comandos de monitoreo:

  - **smbstatus:** Para ver sesiones SMB activas.
  
  - **netstat:** Para verificar conexiones en puertos específicos.
    
  - **Test-NetConnection (PowerShell):** Para probar conectividad desde Windows.

#### 4. Operaciones prácticas:

  - **SMB:** Crear, modificar y eliminar archivos en un recurso compartido para observar cómo la capa de sesión gestiona las conexiones.
    
  - **RPC:** Realizar una llamada remota desde Windows al servidor Debian para entender cómo funciona este protocolo.
    
## ¿Qué logras con este laboratorio?
Al finalizar este laboratorio, habrás:

**1. Comprendido el papel de la capa de sesión:** Sabrás cómo esta capa gestiona las interacciones entre aplicaciones, diferenciándola claramente de la capa de transporte.

**2. Experimentado con protocolos reales:** Habrás trabajado con SMB y RPC, dos protocolos clave que operan en la capa de sesión.

**3. Analizado el tráfico de red:** Habrás usado Wireshark para observar cómo se gestionan las sesiones a nivel de paquetes, profundizando en el funcionamiento interno de estos protocolos.
