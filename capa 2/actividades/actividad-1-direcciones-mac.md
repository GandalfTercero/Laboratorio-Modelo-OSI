# Verificación de Capa 2
### En Debian

    ip link show
o

    ifconfig

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/171272e3aff19f42ad52ed24cdde5407628b7895/capa%202/im%C3%A1genes-capa-2/2.1.png>

- La dirección MAC de enp0s3(red nat): 08:00:27:10:3f:b2
- La dirección MAC de enp0s8(red interna): 08:00:27:ab:08:7b

### En Windows
En powershell, ejecuta el siguiente comando que me muestra todas las interfaces que hay, busca la línea que contiene ``dirección física``.

    ipconfig /all
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/171272e3aff19f42ad52ed24cdde5407628b7895/capa%202/im%C3%A1genes-capa-2/2.2.png>
- La dirección MAC De ethernet(red nat): 08-00-27-64-63-3F
- La dirección MAC de ethernet 2 (red interna): 08-00-27-4B-26-EF
  
## 2. Para revisar la tabla de ARP

### En Debian
Para ver la tabla ARP, muestra las entradas ARP activas o en caché:

    ip neigh show

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/171272e3aff19f42ad52ed24cdde5407628b7895/capa%202/im%C3%A1genes-capa-2/2.3.png>

#### Explicación del escenario:
- Interfaz enp0s3 (Red Nat):
  - MAC local: 08:00:27:10:3f:b2 (la dirección física de tu tarjeta de red en Debian).
  - MAC en la tabla ARP (52:54:00:12:35:00): Es la dirección MAC del dispositivo al que está conectado (en este caso, el router de la red NAT, probablemente VirtualBox.
- Interfaz enp0s8(Red Interna): No se muestra alguna entrada porque:
  - No ha habido tráfico reciente en esa red que requiera resolver direcciones MAC.
  - Las entradas ARP son temporales (se borran después de un tiempo si no hay actividad).
  - Si las máquinas de la red interna están configuradas con IPs estáticas o no han interactuado, la tabla ARP estará vacía.
 
### En Windows:

    arp -a

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/171272e3aff19f42ad52ed24cdde5407628b7895/capa%202/im%C3%A1genes-capa-2/2.4.png>

#### Explicación del escenario:

#### Interfaz NAT (10.0.2.6):                       

| Dirección IP   | Dirección MAC     |     Tipo  |
|----------------|-------------------|-----------|
| 10.0.2.1       | 52-54-00-12-35-00 |	Dinámico |
| 10.0.2.3       | 08-00-27-c4-07-0b |	Dinámico |
| 10.0.2.255     | ff-ff-ff-ff-ff-ff |	Estático |
| ... (multicast)|	...	             |  Estático |

- 10.0.2.1: Es el router de la red NAT (VirtualBox o similar). Su MAC (52:54:00:12:35:00) corresponde al servicio de NAT, no a tu interfaz.
- 10.0.2.3: Es otra máquina en la red NAT (posiblemente otra VM o dispositivo).

#### Interfaz interna (192.168.100.20):

|Dirección IP	    | Dirección MAC	    | Tipo     |
|-------------------|-------------------|----------|
| 192.168.100.255	| ff-ff-ff-ff-ff-ff	| Estático |
| ... (multicast)	| ...	            | Estático |

- No hay entradas dinámicas: Esto indica que no ha habido comunicación reciente con otros dispositivos en la red interna (192.168.100.0/24).
- Las direcciones estáticas (como 192.168.100.255) son direcciones de broadcast o multicast, no dispositivos reales.
  
## ¿Por qué no coincide con tu MAC local la tabla ARP?
- La tabla ARP no muestra tu propia MAC, sino las direcciones MAC de otros dispositivos en la red con los que te has comunicado.
- En redes NAT (como en VirtualBox), el router (10.0.2.1) tiene su propia MAC, que es la que aparece en la tabla ARP.

