# Establecer la conexión desde Windows:
## 1. En Windows, abrir CMD o PowerShell:
Presiona Win + R, escribe cmd y presiona Enter.
## 2. Establecer la conexión con el servidor Samba:
a. Usa el comando net use para conectarse al recurso compartido en Debian:

    net use Z: \\192.168.100.10\shared /user:nuevo_usuario
    
  - ``Z:`` es la letra de unidad que asignarás al recurso compartido (puedes cambiarla si prefieres otra letra).
  - ``\\192.168.100.10\shared`` es la ruta del recurso compartido.
  - ``/user:nuevo_usuario`` especifica el nombre de usuario de Samba.
b. Si te solicita, ingresa las credenciales de usuario y contraseña configuradas en Samba.
c. Verifica la conexión:
Si la conexión es exitosa, verás un mensaje como este:

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/923435bd8a19e374612d9e6abe07ff9511a68e3b/Capa%205/im%C3%A1genes-capa-5/5.9.png>
Ahora puedes acceder al recurso compartido a través de la unidad asignada (Z:) en el Explorador de Archivos de Windows.
