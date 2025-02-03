# Laboratorio Modelo OSI - Capa 1 (Física)
## Descripción General
Este laboratorio explora la Capa 1 (Física) del modelo OSI utilizando VirtualBox como plataforma de virtualización. Se analizan dos tipos de interfaces de red en máquinas virtuales con Debian y Windows.
Entorno de Laboratorio
Máquinas Virtuales

# Debian

Interfaz enp0s3 (RED NAT)
Interfaz enp0s8 (RED INTERNA)


# Windows

Adaptador Ethernet (RED NAT)
Adaptador Ethernet 2 (RED INTERNA)



Comandos Básicos de Verificación
Debian
bashCopy# Ver interfaces de red
ip addr show

# Ver información específica de una interfaz
sudo ethtool enp0s3
sudo ethtool enp0s8

# Ver estadísticas de una interfaz
sudo ethtool -S enp0s3
Windows
powershellCopy# Ver configuración de red
ipconfig /all

# Ver estadísticas
netstat -e
netstat -s
Análisis de Interfaces
1. Interfaz NAT (enp0s3/Adaptador Ethernet)
Configuración y Análisis

Razones para analizar primero:

Asegura conectividad a Internet
Mayor variedad de tráfico
Permite ver funcionamiento con tráfico real



Parámetros Importantes
bashCopy# Ejemplo de salida de ethtool
Link detected: yes
Speed: 1000Mb/s
Duplex: Full
Supported ports: [ TP ]
Supported link modes: 
  - 10baseT/Half
  - 10baseT/Full
  - 100baseT/Half
  - 100baseT/Full
  - 1000baseT/Full
Pruebas Realizadas

Prueba de Ping
bashCopyping -c 20 8.8.8.8

Prueba de Descarga
bashCopywget www.example.com

Prueba con CURL
bashCopycurl www.example.com


2. Interfaz RED INTERNA (enp0s8/Adaptador Ethernet 2)
Configuración IP
Debian
bashCopysudo ip addr add 192.168.100.10/24 dev enp0s8
Windows

IP: 192.168.100.20
Máscara: 255.255.255.0
Sin puerta de enlace

Pruebas de Conectividad
bashCopy# Desde Debian
ping 192.168.100.20

# Desde Windows
ping 192.168.100.10
Simulación de Desconexión
Procedimiento

Acceder a VirtualBox con la VM en ejecución
Menú "Dispositivos" → "Configuración de red"
Desmarcar "Conectar" para la interfaz deseada

Verificaciones
Debian
bashCopy# Verificar estado de interfaz
ip link show enp0s8

# Monitorear tráfico
sudo tcpdump -i enp0s8

# Probar conectividad
ping 192.168.100.20
Observaciones Importantes

Estadísticas de Red

Ausencia de errores indica funcionamiento óptimo
Incremento en bytes tx/rx confirma comunicación efectiva
No hay paquetes descartados


Direccionamiento IP

APIPA (169.254.x.x) indica falta de configuración
IPs estáticas necesarias para red interna
Separación de rangos (.10 y .20) para mejor administración



Conclusiones

La capa física muestra funcionamiento óptimo en ambiente virtualizado
Las interfaces mantienen conexión estable a 1000Mb/s Full Duplex
La virtualización permite simular escenarios de desconexión física
Las herramientas de diagnóstico muestran claramente el estado del enlace

Referencias

Documentación de VirtualBox
Manual de ethtool
Documentación de Windows Network Commands
