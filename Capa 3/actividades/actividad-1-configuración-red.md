# Verificar configuración de red
## En Debian:
    ip a # ver interfacez y direcciones ip

(imagen 3.1)
#### Asegúrate de que ambas VMs tengan las IPs configuradas correctamente en ambas redes (NAT e Interna).
  
    ip r # Mostrar tabla de enrutamiento

(imagen 3.2)

#### Resumen general de la tabla de enrutamiento:

|  Destino  |  Interfaz  |  Gateway  |  Propósito  |
|-----------|------------|-----------|-------------|
|``default``|``enp0s3``  |``10.0.2.1``| Enviar tráfico a redes externas, (por ejemplo, internet)|
|``10.0.2.0/24``|``enp0s3``|  -    | Comunicación directa con dispositivos en la red NAT (``10.0.2.x``).|
|``169.254.0.0/16``|``enp0s3``|  -  | Comunicación en caso de fallo de DHCP (no usada en la configuración).|
|``192.168.100.0/24``|``enp0s8``|  -  | Comunicación directa con dispositivos en la red interna (``192.168.100.x``).|

La tabla de enrutamiento te muestra cómo tu sistema decide qué hacer con los paquetes de red dependiendo de su destino:
- La interfaz enp0s3 (NAT) maneja el acceso a Internet y la comunicación en la red 10.0.2.x.
- La interfaz enp0s8 (red interna) maneja la comunicación en la red 192.168.100.x.

## En Windows:
    ipconfig /all  # Ver interfaces y direcciones IP
    route print  # Mostrar tabla de enrutamiento

(imagen 3.3)

#### Resumen general de la tabla de enrutamiento:

|  Destino  |  Interfaz  |  Gateway  |  Propósito  |
|-----------|------------|-----------|-------------|
|``0.0.0.0``|``10.0.2.6``|``10.0.2.1``| Acceso a Internet a través de la red NAT.|
|``10.0.2.0/24``|``10.0.2.6``|  -  | Comunicación directa con dispositivos en la red NAT (``10.0.2.x``).|
|``127.0.0.0/8``|``127.0.0.1``|  -  | Comunicación local dentro del sistema (loopback).|
|``192.168.100.0/24``|``192.168.100.20``|  -  | Comunicación directa con dispositivos en la red interna (``192.168.100.x``).|

La tabla de enrutamiento en Windows refleja la configuración de mis dos redes en VirtualBox:
- La red NAT (10.0.2.x) proporciona acceso a Internet.
- La red interna (192.168.100.x) permite la comunicación entre máquinas virtuales.
