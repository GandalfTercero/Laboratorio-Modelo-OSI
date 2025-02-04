Comandos utilizados en el análisis de la Capa 1 - Debian
# Comandos básicos de verificación
## Ver todas las interfaces de red
``ip addr show``

## Ver información específica de la interfaz red NAT
``sudo ethtool enp0s3``

## Ver información específica de la interfaz de red interna
``sudo ethtool enp0s8``

## Ver estadísticas de la interfaz NAT
``sudo ethtool -S enp0s3``

## Ver estadísticas de la interfaz de red interna
``sudo ethtool -S enp0s8``
# Pruebas de tráfico en interfaz NAT
## Instalación de herramientas (si no están instaladas)
``sudo apt install wget curl``

## Prueba con ping
``ping -c 20 8.8.8.8``

## Prueba con wget
``wget www.example.com``

## Prueba con curl
``curl www.example.com``

## Ver estadísticas después de cada prueba
``sudo ethtool -S enp0s3``
# Configuración de red interna estática
``sudo ip addr add 192.168.100.10/24 dev enp0s8``

## Verificar configuración
``ip addr show enp0s8``

## Prueba de conectividad con Windows
``ping 192.168.100.20``

## Monitoreo de tráfico
``sudo tcpdump -i enp0s8``
# Pruebas de desconexión
## Verificar estado de la interfaz
``ip link show enp0s8``

## Monitorear tráfico durante la desconexión
``sudo tcpdump -i enp0s8``

## Intentar ping para confirmar desconexión
``ping 192.168.100.20``
