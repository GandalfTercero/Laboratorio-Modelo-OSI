# 1. Ver la negociación inicial de la conexión:
- Usa el filtro:
    
      smb2.cmd == 0
(imagen 5.25)
# 2. Ver la creación del archivo:
- Usa el filtro:

      smb2.create_action == 0x00000001
- Esto muestra los paquetes donde se crea el archivo.

(imagen 5.26)
# 3. Ver la escritura en el archivo (modificación):
- Usa el filtro:

      smb2.cmd == 9
  (imagen 5.27)
- Esto muestra los paquetes de escritura (SMB2 Write Request/Response).
# 4. Ver la eliminación del archivo:
- Usa el filtro:

      smb2.cmd == 6
  (imagen 5.28)
- Esto muestra los paquetes de eliminación (SMB2 Close Request/Response).
# 5. Buscar un archivo específico:
- Usa la función de búsqueda (Ctrl + F) en Wireshark.
- Busca el nombre del archivo (prueba.txt) en los paquetes.


