# 1. Ver la negociación inicial de la conexión:
- Usa el filtro:
    
      smb2.cmd == 0
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/860ff47fdff03adf470a2d68a35d86ae767c6e2c/Capa%205/im%C3%A1genes-capa-5/5.25.png>

# 2. Ver la creación del archivo:
- Usa el filtro:

      smb2.create_action == 0x00000001
- Esto muestra los paquetes donde se crea el archivo.

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/860ff47fdff03adf470a2d68a35d86ae767c6e2c/Capa%205/im%C3%A1genes-capa-5/5.26.png>

# 3. Ver la escritura en el archivo (modificación):
- Usa el filtro:

      smb2.cmd == 9
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/860ff47fdff03adf470a2d68a35d86ae767c6e2c/Capa%205/im%C3%A1genes-capa-5/5.27.png>
Esto muestra los paquetes de escritura (SMB2 Write Request/Response).

# 4. Ver la eliminación del archivo:
- Usa el filtro:

      smb2.cmd == 6
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/7a4b337e93807780c64b2c1752da0468f50eaa96/Capa%205/im%C3%A1genes-capa-5/5.28.png>
 Esto muestra los paquetes de eliminación (SMB2 Close Request/Response).
# 5. Buscar un archivo específico:
- Usa la función de búsqueda (Ctrl + F) en Wireshark.
- Busca el nombre del archivo (prueba.txt) en los paquetes.


