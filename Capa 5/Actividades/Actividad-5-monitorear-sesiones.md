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

(imagen 5.10)
Aquí puedes ver que el usuario “nuevo_usuario” está conectado desde la IP 192.168.100.20.
#### 2. Usa netstat para ver las conexiones de red:
    netstat -tuln | grep 445
(imagen 5.11)
Esto confirma que el servicio SMB está escuchando en el puerto 445.
## En Windows:
#### 1. Usa netstat para ver las conexiones activas:
    netstat -an | findstr 445
  Esto mostrará las conexiones SMB establecidas con Debian.

  (imagen 5.12)

Aquí puedes ver que la máquina Windows (192.168.100.20) está conectada al servidor Debian (192.168.100.10) a través del puerto 445.
