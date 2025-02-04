Configuraciones y Comandos en Windows - Capa 1
# Comandos de Verificación de Red
## Ver configuración completa de red
``ipconfig /all``

# Ver estadísticas de red
``netstat -e``
``netstat -s``
# Configuración de Red Interna
## Pasos para Configuración Manual
1. Panel de Control.
2. Centro de redes y recursos compartidos.
3. Cambiar configuración del adaptador.
4. Clic derecho en adaptador de RED INTERNA.
5. Seleccionar "Propiedades".
6. Seleccionar "Protocolo de Internet versión 4 (TCP/IPv4)".
7. Seleccionar "Propiedades".

## Configuración IP
1. Dirección IP: 192.168.100.20
2. Máscara de subred: 255.255.255.0
3. Puerta de enlace: Vacía
4. Servidores DNS: Vacíos

# Pruebas de Conectividad
## Ping a máquina Debian
``ping 192.168.100.10 -n 10``

## Ver estadísticas después de ping
``netstat -e``
# Verificación de Estado de Red
## Verificar estado de conexiones
``netstat -an``
