# Crear el archivo en Windows:
1. Abre el explorador de archivos y navega al recurso compartido:

   (imagen 5.21)
2. Crea un archivo de texto llamado prueba.txt y escribe algo dentro.
3. Guarda el archivo en el recurso compartido.

  (imagen 5.22)
## Verificar el archivo en Debian:
En Debian, verifica que el archivo se haya creado correctamente:
	
       ls /srv/shared
       cat /srv/shared/prueba.txt.txt
(imagen 5.23)
# Modificar el archivo en Debian:
Edita el archivo desde Debian:

        echo "Hola desde Debian" >> /srv/shared/prueba.txt
## Verificar los cambios desde Windows:
Regresa al explorador de archivos en Windows y abre el archivo prueba.txt. Deberías ver el contenido modificado por Debian.

   (imagen 5.24)
# Eliminar el archivo desde Debian:
Elimina el archivo prueba.txt desde el explorador de archivos en Windows.
## Verificar la eliminación en Debian:
En Debian, verifica que el archivo ya no existe:

    ls /srv/shared


