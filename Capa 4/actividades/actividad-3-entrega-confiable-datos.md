# Verificar la entrega confiable de datos
## 1. En Debian:
* Usa netcat para crear un servidor TCP:
  
  ``nc -l -p 1234 > recibido.txt``
  - La terminal se queda en blanco, sin prompt
  - Esto indica que está escuchando correctamente
  - No verás el contenido del archivo en la pantalla (porque está siendo redirigido al archivo recibido.txt). 
  - El comando terminará automáticamente y volverás a ver el prompt
* Para solo recibir los datos y mostrarlos en pantalla sin guardarlos

  ``nc -l -p 1234``
## 2. En Windows:
* Crea un documento de texto por medio de la línea de comandos:
  
  ``New-Item archivo.txt``

  ``Set-Content archivo.txt "Tu mensaje aquí"``
    - El contenido que pongas en este archivo.txt es lo que se enviará a través de netcat al servidor Debian. Puedes poner cualquier texto que quieras probar - podría ser un mensaje simple como "Hola mundo" o un texto más largo.

  (imagen 4.14)

* Envía un archivo a Debian usando powershell:
  
  ``$client = New-Object System.Net.Sockets.TcpClient('10.0.0.46', 1234)``
  
  ``$file = [System.IO.File]::ReadAllBytes(".\archivo.txt")``
  
  ``$stream = $client.GetStream()``

  ``$stream.Write($file, 0, $file.Length)``

  ``$stream.Close()``
  
  ``$client.Close()``

  (imagen 4.15)

## 3. En Wireshark:
* Observa cómo TCP asegura la entrega confiable de datos mediante confirmaciones (ACK).

  (imagen 4.16)

  Aquí se muestra una dirección distinta en Windows, una dirección IP 10.0.0.41, porque había apagado la máquina virtual, y cuando volví a iniciarla tomó esa nueva dirección IP.
* **En Debian**, para verificar que recibiste el archivo:
    ``cat recibido.txt``

  (imagen 4.17)

