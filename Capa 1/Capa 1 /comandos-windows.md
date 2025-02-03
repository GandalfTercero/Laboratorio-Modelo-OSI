Configuraciones y Comandos en Windows - Capa 1
Comandos de Verificación de Red
powershellCopy# Ver configuración completa de red
ipconfig /all

# Ver estadísticas de red
netstat -e
netstat -s
Configuración de Red Interna
Pasos para Configuración Manual

Panel de Control > Centro de redes y recursos compartidos
Cambiar configuración del adaptador
Clic derecho en adaptador de RED INTERNA
Seleccionar "Propiedades"
Seleccionar "Protocolo de Internet versión 4 (TCP/IPv4)"

Configuración IP

Dirección IP: 192.168.100.20
Máscara de subred: 255.255.255.0
Puerta de enlace: Vacía
Servidores DNS: Vacíos

Pruebas de Conectividad
powershellCopy# Ping a máquina Debian
ping 192.168.100.10 -n 10

# Ver estadísticas después de ping
netstat -e
Verificación de Estado de Red
powershellCopy# Verificar estado de conexiones
netstat -an
