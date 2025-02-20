## 1. Detén el servicio Samba
Antes de desinstalar Samba, detén los servicios relacionados (smbd y nmbd):
		
    sudo systemctl stop smbd
    sudo systemctl stop nmbd
## 2. Desinstala los paquetes de Samba
Para desinstalar completamente Samba, usa el siguiente comando:
		
    sudo apt remove --purge samba samba-common samba-common-bin
El uso de la opción --purge asegura que no solo se eliminen los paquetes, sino también los archivos de configuración asociados (como /etc/samba/smb.conf).
## 3. Elimina los archivos residuales
Samba puede haber dejado algunos archivos o directorios en tu sistema. Elimínalos manualmente si es necesario:
		
    sudo rm -rf /etc/samba
    sudo rm -rf /var/lib/samba
    sudo rm -rf /var/log/samba
    sudo rm -rf /var/cache/samba
  Esto eliminará:

    /etc/samba: Archivos de configuración.
    /var/lib/samba: Datos de Samba (como secrets.tdb).
    /var/log/samba: Logs generados por Samba.
    /var/cache/samba: Cachés temporales.
## 4. Limpia los residuos del sistema
Después de desinstalar Samba, limpia los paquetes innecesarios y libera espacio en el sistema:
		
    sudo apt autoremove
    sudo apt clean
## 5. Verifica que Samba ha sido eliminado:
Para confirmar que Samba ya no está instalado, ejecuta:
		
    dpkg -l | grep samba
Si no ves ninguna salida relacionada con Samba, significa que ha sido eliminado correctamente.

**Si ves salida:**
### a. Verifica las dependencias:
Para verificar si otros paquetes dependen de libldb2 o samba-libs, usa el siguiente comando:
		
    apt-cache rdepends libldb2 samba-libs

Esto mostrará una lista de paquetes que dependen de estas bibliotecas. Si ves otros programas importantes en la lista, es posible que no quieras eliminar estos paquetes para evitar romper dichos programas.
### b. Elimina los paquetes relacionados con Samba
Si decides que ya no necesitas estos paquetes, puedes eliminarlos con el siguiente comando:
		
    sudo apt remove --purge libldb2 samba-libs
Esto eliminará las bibliotecas y cualquier archivo asociado.
### c. Limpia los residuos
Después de eliminar los paquetes, limpia los residuos del sistema:
		
    sudo apt autoremove
    sudo apt clean
### d. Verifica que todo ha sido eliminado
Vuelve a ejecutar el siguiente comando para confirmar que no quedan paquetes relacionados con Samba:

    dpkg -l | grep samba
Si no ves ninguna salida, significa que todos los paquetes relacionados con Samba han sido eliminados.
