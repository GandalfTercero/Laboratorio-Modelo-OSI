# Verificar la entrega confiable de datos
## 1. En Debian:
* Usa netcat para crear un servidor TCP:
  
      nc -l -p 1234 > recibido.txt
  - La terminal se queda en blanco, sin prompt
  - Esto indica que está escuchando correctamente
  - No verás el contenido del archivo en la pantalla (porque está siendo redirigido al archivo recibido.txt). 
  - El comando terminará automáticamente y volverás a ver el prompt
* Para solo recibir los datos y mostrarlos en pantalla sin guardarlos

      nc -l -p 1234
## 2. En Windows:
* Crea un documento de texto por medio de la línea de comandos:
  
      New-Item archivo.txt
      Set-Content archivo.txt "Tu mensaje aquí"
    - El contenido que pongas en este archivo.txt es lo que se enviará a través de netcat al servidor Debian. Puedes poner cualquier texto que quieras probar - podría ser un mensaje simple como "Hola mundo" o un texto más largo.

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/9d510966e0ff8ccc9c819072490654fd4ce93364/Capa%204/im%C3%A1genes%20capa%204/4.14.png></img>

* Envía un archivo a Debian usando powershell:
  
      $client = New-Object System.Net.Sockets.TcpClient('10.0.0.46', 1234)
      $file = [System.IO.File]::ReadAllBytes(".\archivo.txt")
      $stream = $client.GetStream()
      $stream.Write($file, 0, $file.Length)
      $stream.Close()
      $client.Close()

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/9d510966e0ff8ccc9c819072490654fd4ce93364/Capa%204/im%C3%A1genes%20capa%204/4.15.png></img>
## 3. En Wireshark:
* Observa cómo TCP asegura la entrega confiable de datos mediante confirmaciones (ACK).

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/9d510966e0ff8ccc9c819072490654fd4ce93364/Capa%204/im%C3%A1genes%20capa%204/4.16.png></img>
  Aquí se muestra una dirección distinta en Windows, una dirección IP 10.0.0.41, porque había apagado la máquina virtual, y cuando volví a iniciarla tomó esa nueva dirección IP.
* **En Debian**, para verificar que recibiste el archivo:

      cat recibido.txt

<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/9d510966e0ff8ccc9c819072490654fd4ce93364/Capa%204/im%C3%A1genes%20capa%204/4.17.png></img>
