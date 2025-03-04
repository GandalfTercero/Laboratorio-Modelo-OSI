# Experimentar con RPC (Remote Procedure Call)
## En Debian:
#### 1.Instala un servidor RPC simple:
El paquete rpcbind es necesario para manejar llamadas RPC. Instálalo con el siguiente comando:

    sudo apt install rpcbind
#### 2. Inicia el servicio:
Una vez instalado, inicia el servicio rpcbind:

    sudo systemctl start rpcbind
#### 3. Habilita el servicio para que se inicie automáticamente al arrancar el sistema (opcional):
Si deseas que el servicio RPC esté disponible siempre que enciendas tu servidor Debian, habilita el servicio:

    sudo systemctl enable rpcbind
#### 4. Verifica que el servicio esté activo:
Usa el siguiente comando para confirmar que el servicio rpcbind está funcionando correctamente:

    sudo systemctl status rpcbind
Deberías ver algo como esto:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/dd0a5379607fd4c5823327f1deb4e2500608951c/Capa%205/im%C3%A1genes-capa-5/5.15.png>

#### 5. Verifica que el puerto RPC (111) esté en uso:
El puerto predeterminado para RPC es el 111 . Usa netstat para confirmar que el puerto está escuchando conexiones:

    netstat -tuln | grep 111
Deberías ver algo como esto:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/dd0a5379607fd4c5823327f1deb4e2500608951c/Capa%205/im%C3%A1genes-capa-5/5.16.png>

Esto indica que el servicio RPC está listo para recibir llamadas remotas.
#### 6. Verifica el firewall en Debian
Un firewall podría estar bloqueando el tráfico al puerto 111. Si estás usando ufw, asegúrate de permitir el tráfico RPC.
Permite el puerto 111:

    sudo ufw allow 111
Verifica el estado del firewall

    sudo ufw status
Deberías ver algo como esto:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/dd0a5379607fd4c5823327f1deb4e2500608951c/Capa%205/im%C3%A1genes-capa-5/5.19.png>

## En Windows:
#### 1. Usa PowerShell para probar una llamada RPC:
Abre PowerShell y ejecuta el siguiente comando para verificar la conectividad al puerto RPC (111):

    Test-NetConnection -ComputerName 192.168.100.10 -Port 111
Si la conexión es exitosa, verás algo como esto:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/dd0a5379607fd4c5823327f1deb4e2500608951c/Capa%205/im%C3%A1genes-capa-5/5.17.png>

Esto confirma que el puerto RPC está accesible desde Windows.
#### 2. Interpretación del resultado:
  - Si TcpTestSucceeded es **True**, significa que el servicio RPC en Debian está funcionando correctamente y es accesible desde Windows.
  - Si TcpTestSucceeded es **False**, revisa:
      - Que el servicio rpcbind esté activo en Debian (sudo systemctl status rpcbind).
      - Que no haya un firewall bloqueando el puerto 111 en Debian o Windows.
En mi máquina, salió que era falso:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/dd0a5379607fd4c5823327f1deb4e2500608951c/Capa%205/im%C3%A1genes-capa-5/5.18.png>

En este caso yo no tenía habilitado el firewall para el puerto de RPC, después de habilitarlo ya me salía **True.**

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/dd0a5379607fd4c5823327f1deb4e2500608951c/Capa%205/im%C3%A1genes-capa-5/5.20.png>

