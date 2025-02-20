Después de haber configurado un servicio SMB en Debian, debes configurar un usuario.
1. Configura un usuario en Samba:

       sudo adduser nuevo_usuario
2. Agrega el usuario al sistema de Samba:

       sudo smbpasswd -a nuevo_usuario
3. Habilita el usuario en Samba:

       sudo smbpasswd -e nuevo_usuario
4. Modifica la sección [shared] en /etc/samba/smb.conf para incluir autenticación:

       [shared]
       path = /srv/shared
       read only = no
       browsable = yes
       valid users = nuevo_usuario
5. Guarda el archivo y reinicia el servicio Samba:

       sudo systemctl restart smbd

Ya teniendo esto, ahora sí ve a la carpeta de actividades.
