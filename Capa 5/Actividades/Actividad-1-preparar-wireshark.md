# Usando Wireshark:
## 1. Instala Wireshark:
  - **En Debian:**

           sudo apt update
           sudo apt install wireshark
  - **En Windows:** Descarga e instala Wireshark desde su sitio oficial. Abre el navegador y búscalo.
## 2. Inicia Wireshark en Debian:
  - Abre Wireshark y selecciona la interfaz de red interna ``enp0s8``
## 3. Filtra el tráfico SMB:
  - Usa el filtro ``smb`` o ``tcp.port == 445`` para ver solo el tráfico relacionado con SMB.
## 4. Realiza operaciones en el recurso compartido:
Desde Windows, accede al recurso compartido (``\\192.168.100.10\shared``) y realiza operaciones como crear, modificar y eliminar archivos.
## 5. Inicia la captura.
Analiza el tráfico:
  - Observa cómo se establece la conexión inicial (autenticación).
  - Busca paquetes relacionados con las operaciones de archivos (por ejemplo, ``SMB2 CREATE``, ``SMB2 WRITE``, ``SMB2 CLOSE``).
  - Verifica cómo se cierra la sesión cuando terminas de interactuar con el recurso compartido.
