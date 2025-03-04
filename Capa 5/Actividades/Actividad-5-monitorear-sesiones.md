# Monitorear Sesiones Activas:
Para observar cómo se manejan las sesiones en la capa 5, usaremos herramientas como netstat y smbstatus.
## En Debian:
#### 1. Usa smbstatus para ver las conexiones SMB activas:
	sudo smbstatus
Esto mostrará información detallada sobre:
- Sesiones activas : Usuarios conectados y sus direcciones IP.
- Conexiones abiertas : Recursos compartidos (shared) en uso.
- Bloqueos de archivos : Archivos bloqueados por usuarios.
Ejemplo de salida:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/d30c72816b3cbdb4bf15e13fc2eb5d8ec2a732e8/Capa%205/im%C3%A1genes-capa-5/5.10.png>

Aquí puedes ver que el usuario “nuevo_usuario” está conectado desde la IP 192.168.100.20.
#### 2. Usa netstat para ver las conexiones de red:
    netstat -tuln | grep 445

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/e0af98d317c63934dcd0ef6d622e45670a4c57fd/Capa%205/im%C3%A1genes-capa-5/5.11.png>

Esto confirma que el servicio SMB está escuchando en el puerto 445.
## En Windows:
#### 1. Usa netstat para ver las conexiones activas:
    netstat -an | findstr 445
  Esto mostrará las conexiones SMB establecidas con Debian.

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/e0af98d317c63934dcd0ef6d622e45670a4c57fd/Capa%205/im%C3%A1genes-capa-5/5.12.png>

Aquí puedes ver que la máquina Windows (192.168.100.20) está conectada al servidor Debian (192.168.100.10) a través del puerto 445.
