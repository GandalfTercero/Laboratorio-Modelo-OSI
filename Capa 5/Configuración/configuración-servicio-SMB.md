# Configurar un servicio SMB en Debian.
El protocolo SMB (Server Message Block) es un ejemplo clásico de un servicio que utiliza la capa de sesión. Vamos a configurar un servidor SMB en Debian para que Windows pueda acceder a él.
## 1. Instala el servicio **Samba**:
   
    sudo apt update
    sudo apt install samba

- El sistema instalará el software necesario para ejecutar un servidor SMB. Para sí permitir el intercambio de archivos con Windows.
## 2. Configura Samba:
a. Edita el archivo de configuración /etc/samba/smb.conf:
		
    sudo nano /etc/samba/smb.conf
b. Agrega la siguiente sección al final del archivo:
Definir un recurso compartido llamado shared que estará disponible para los clientes. Al guardar el archivo, el servidor Samba sabrá qué directorio compartir y con qué permisos.

    [shared]
    path = /srv/shared
    read only = no
    browsable = yes
c. Crea el directorio compartido:
Crear el directorio físico que será compartido y asegurarnos de que todos los usuarios tengan acceso. Un directorio vacío en /srv/shared con permisos completos. Sin este directorio, el servidor SMB no tendría nada que ofrecer a los clientes.

    sudo mkdir -p /srv/shared
    sudo chmod 777 /srv/shared
d. Reinicia el servicio Samba:
Aplicar los cambios realizados en la configuración de Samba. El servicio SMB se reiniciará y comenzará a escuchar en el puerto 445. Los cambios en la configuración solo surten efecto después de reiniciar el servicio.

    sudo systemctl restart smbd
e. Configura el firewall (si está activo):

    sudo ufw allow samba
f. Verificar que el servidor Samba está en ejecución

    sudo systemctl status smbd
  Deberías ver algo como esto:

  (imagen 5.8)


    
