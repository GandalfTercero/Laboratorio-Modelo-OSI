# Terminar una Sesión
Para entender cómo se cierran las sesiones, puedes desconectar manualmente una conexión SMB.
## En Debian:
#### 1. Usa ``smbcontrol`` para cerrar una sesión específica:
Para cerrar manualmente una sesión SMB, ejecuta:

        sudo smbcontrol all close-share shared
Esto desconectará a todos los usuarios del recurso compartido shared.

#### 2. Verifica que la sesión se haya cerrado usando smbstatus.
Usa nuevamente smbstatus para confirmar que no hay sesiones activas:

        sudo smbstatus

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/9161de8d560f819a580a427066aff3ba2d13f0f9/Capa%205/im%C3%A1genes-capa-5/5.13.png>

Si la sesión se cerró correctamente, no deberías ver ninguna conexión activa relacionada con el recurso compartido shared.
## En Windows:
#### 1. Cerrar la sesión SMB:
-  Para cerrar la sesión SMB desde Windows, debes desmontar la unidad asignada (Z:) usando el siguiente comando en CMD:

       net use Z: /delete
  Esto desconectará la unidad asignada y cerrará la sesión SMB con el servidor Debian.
- Alternativamente, si no asignaste una letra de unidad (Z:) y simplemente abriste el recurso compartido en el Explorador de Archivos, puedes cerrar la sesión cerrando la ventana del Explorador donde tenías abierto el recurso compartido.
#### 2. Verificar que la sesión se haya cerrado:
- Después de cerrar la sesión, verifica que ya no hay conexiones activas al puerto SMB (445) en Windows.
- Abre una nueva terminal de CMD y ejecuta:

      netstat -an | findstr 445

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/9161de8d560f819a580a427066aff3ba2d13f0f9/Capa%205/im%C3%A1genes-capa-5/5.14.png>

Si no ves ninguna línea relacionada con la IP del servidor Debian (192.168.100.10) y el puerto 445, significa que la sesión se cerró correctamente.


