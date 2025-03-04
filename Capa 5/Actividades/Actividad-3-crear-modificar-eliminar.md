# Crear el archivo en Windows:
1. Abre el explorador de archivos y navega al recurso compartido:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/824c00f940279a78954c06247e6aade90d7ebe6c/Capa%205/im%C3%A1genes-capa-5/5.21.png>
2. Crea un archivo de texto llamado prueba.txt y escribe algo dentro.
3. Guarda el archivo en el recurso compartido.

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/824c00f940279a78954c06247e6aade90d7ebe6c/Capa%205/im%C3%A1genes-capa-5/5.22.png>
## Verificar el archivo en Debian:
En Debian, verifica que el archivo se haya creado correctamente:
	
       ls /srv/shared
       cat /srv/shared/prueba.txt.txt
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/824c00f940279a78954c06247e6aade90d7ebe6c/Capa%205/im%C3%A1genes-capa-5/5.23.png>
# Modificar el archivo en Debian:
Edita el archivo desde Debian:

        echo "Hola desde Debian" >> /srv/shared/prueba.txt
## Verificar los cambios desde Windows:
Regresa al explorador de archivos en Windows y abre el archivo prueba.txt. Deberías ver el contenido modificado por Debian.

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/824c00f940279a78954c06247e6aade90d7ebe6c/Capa%205/im%C3%A1genes-capa-5/5.24.png>
# Eliminar el archivo desde Debian:
Elimina el archivo prueba.txt desde el explorador de archivos en Windows.
## Verificar la eliminación en Debian:
En Debian, verifica que el archivo ya no existe:

    ls /srv/shared


