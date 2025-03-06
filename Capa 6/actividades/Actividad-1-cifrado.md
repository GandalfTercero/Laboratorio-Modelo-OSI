# Cisfrado (SSL/TLS)
**Objetivo**: Observar el cifrado TLS en acción.

## 1. Configuración del servidor HTTPS en Debian
### a) Instalar Apache y OpenSSL
    sudo apt install apache2 openssl
- **Apache** es un servidor web que permite alojar sitios web y responder a solicitudes HTTP/HTTPS.
- **OpenSSL** es una herramienta para trabajar con certificados SSL/TLS, que son necesarios para cifrar la comunicación entre el cliente (navegador) y el servidor.
- Este comando instala ambos programas en tu sistema Debian.

### b) Generar un certificado autofirmado
    sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/apache-selfsigned.key \
    -out /etc/ssl/certs/apache-selfsigned.crt

- **¿Por qué generar un certificado?**
    - HTTPS utiliza certificados SSL/TLS para cifrar la comunicación y verificar la identidad del servidor.
    - Un certificado autofirmado es uno que no está firmado por una autoridad certificadora reconocida, pero sirve para pruebas locales.
- **Parámetros importantes:**
    - ``-x509``: Indica que estamos generando un certificado X.509 (formato estándar para certificados SSL).
    - ``-nodes``: No cifra la clave privada (para evitar tener que ingresar una contraseña cada vez que se inicie Apache).
    - ``-days 365``: El certificado será válido por 365 días.
    - ``-newkey rsa:2048``: Crea una nueva clave privada RSA de 2048 bits.
    - ``-keyout``: Guarda la clave privada en ``/etc/ssl/private/apache-selfsigned.key``.
    - ``-out``: Guarda el certificado público en ``/etc/ssl/certs/apache-selfsigned.crt``.

### c) Habilitar SSL y configurar Apache
    sudo a2enmod ssl
    sudo nano /etc/apache2/sites-available/default-ssl.conf

  - ``a2enmod ssl`` : Habilita el módulo SSL en Apache, necesario para manejar conexiones HTTPS.
    
- **Editar** ``default-ssl.conf`` :
- 
    1. Busca estas líneas en el archivo:
      - Dentro del archivo default-ssl.conf, busca las siguientes directivas:
  
      SSLCertificateFile      /etc/ssl/certs/ssl-cert-snakeoil.pem
      SSLCertificateKeyFile   /etc/ssl/private/ssl-cert-snakeoil.key

  Estas son las rutas predeterminadas que Apache usa para un certificado de prueba llamado "snakeoil". Sin embargo, como has generado tu propio certificado autofirmado, necesitas actualizar estas rutas para que apunten a los archivos que creaste.

   2. Modifica las líneas para usar tus archivos:
      - Reemplaza las rutas anteriores con las rutas de los archivos que generaste con OpenSSL:

      SSLCertificateFile      /etc/ssl/certs/apache-selfsigned.crt
      SSLCertificateKeyFile   /etc/ssl/private/apache-selfsigned.key
    - Aquí se especifican las rutas del certificado (``SSLCertificateFile``) y la clave privada (``SSLCertificateKeyFile``).
    - Estos archivos son los que generaste en el paso anterior (b).

### d) Habilitar el sitio SSL y reiniciar Apache
    sudo a2ensite default-ssl
    sudo systemctl restart apache2

- ``a2ensite default-ssl`` : Activa el sitio SSL configurado en Apache.
- **Reiniciar Apache** : Aplica los cambios realizados.

(imagen 6.1)

Si te aparece ese mensaje:

1. Recarga Apache:

       sudo systemctl reload apache2
2. Verifica el estado de Apache:

Para asegurarte que Apache está funcionando correctamente:

       sudo systemctl status apache2
Deberías ver un mensaje como este:

      ● apache2.service - The Apache HTTP Server
         Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
         Active: active (running) since ...

Si ves ``Active: active (running)``, significa que Apache está funcionando correctamente.

3. Reinicia Apache (opcional)
   
Si prefieres reiniciar Apache en lugar de recargarlo, puedes usar este comando:

        sudo systemctl restart apache2
Esto detendrá y volverá a iniciar Apache, lo que también aplicará los cambios en la configuración.

4. Verifica si el firewall está habilitado:

       sudo ufw status

   Si está habilitado, asegúrate de permitir los puertos 80 y 443:

       sudo ufw allow 80/tcp
       sudo ufw allow 443/tcp
       sudo ufw reload

## 2. Capturar tráfico en Wireshark (Debian)
### a) Configuración inicial
- **Interfaz de red** : En tu caso, usas ``enp0s8`` (red interna). Esta interfaz es la que conecta Debian y Windows en la red interna (192.168.100.x).
- **Filtros en Wireshark** :
    - ``tcp.port == 443``: Filtra el tráfico HTTPS (puerto 443).
    - ``tcp.port == 80``: Filtra el tráfico HTTP (puerto 80).
### Accede al servicio desde Windows:
Ahora, en tu máquina Windows:
#### a) Acceso HTTP
1. Abre un navegador web (por ejemplo, Chrome, Firefox o Edge).
2. Ingresa la dirección ``http://192.168.100.10`` en la barra de direcciones.
Deberías de ver lo siguiente en el navegador:

(imagen 6.2)

 
Esto generará una solicitud HTTP desde Windows hacia el servidor Debian. En Wireshark, verás los paquetes correspondientes a esta solicitud.

(imagen 6.3)

Recuerda que en esta **Capa de Presentación** se centra principalmente en el formato de los datos y cómo se presentan al navegador, entonces:

  (imagen 6.4)

#### 1. Solicitud HTTP (GET /)
   
**¿Qué significa GET /?**
- **Método HTTP** : El método ``GET`` es una solicitud que el navegador envía al servidor para **obtener un recurso** específico .
    - En este caso, ``/`` representa la página principal del sitio web (la raíz del servidor).
- **Versión HTTP** : ``HTTP/1.1`` indica que se está utilizando la versión 1.1 del protocolo HTTP.

**Encabezados importantes**
- **Host** : Indica el dominio o dirección IP del servidor al que se está conectando (en este caso, ``192.168.100.10``).
- **User-Agent** : Proporciona información sobre el navegador y el sistema operativo del cliente (por ejemplo, Chrome en Windows).
- **Accept** : Especifica los tipos de contenido que el navegador puede manejar (por ejemplo, HTML, JSON, imágenes).

**¿Por qué observar esto?**
- **Formato de la solicitud** : Entender cómo el navegador solicita recursos es fundamental para analizar el tráfico HTTP.
- **Encabezados** : Los encabezados indican **qué espera el navegador** del servidor. Por ejemplo:
      - ``Accept: text/html`` significa que el navegador espera recibir contenido HTML.
      - ``Host: 192.168.100.10`` ayuda al servidor a identificar qué sitio web debe servir (útil si hay varios sitios en el mismo servidor).

#### 2. Respuesta HTTP (200 OK)
**¿Qué significa ``200 OK``?**
- **Código de estado** : Los códigos de estado HTTP indican el resultado de la solicitud. ``200 OK`` significa que la solicitud fue exitosa y el servidor devolvió el recurso solicitado.
      - **Ejemplo**: Cuando solicitas la página principal (``GET /``), el servidor responde con ``200 OK`` y envía el contenido HTML.

**Encabezados importantes**
- **Content-Type** : Indica el tipo de contenido que el servidor está enviando.
      - En este caso, ``text/html`` significa que el contenido es HTML.
- **Content-Length** : Indica el tamaño del contenido en bytes.

**Cuerpo de la respuesta**
- El cuerpo contiene el contenido real que el servidor envía al navegador.
      - En este caso, ``<html><body><h1>It works!</h1></body></html>`` es el HTML de la página predeterminada de Apache.

**¿Por qué observar esto?**
- **Tipo de contenido** : El campo ``Content-Type`` es crucial porque le dice al navegador cómo interpretar los datos recibidos.
      - Si fuera ``image/png``, el navegador mostraría una imagen en lugar de renderizar HTML.
- **Cuerpo de la respuesta** : Observar el cuerpo te permite ver exactamente qué contenido está enviando el servidor.

#### 3. Respuesta HTTP con error (``404 Not Found``)
**¿Qué significa 404 Not Found?**
- **Código de estado** : ``404`` indica que el recurso solicitado no existe en el servidor. En este caso, el navegador solicitó /favicon.ico, pero el servidor no encontró ese archivo.

**Encabezados importantes**
- **Content-Type** : Aunque el recurso no existe, el servidor aún envía una respuesta con un tipo de contenido (por ejemplo, ``text/html``).
- **Cuerpo de la respuesta** : Contiene una página de error (en este caso, <html><body><h1>404 Not Found</h1></body></html>).

**¿Por qué observar esto?**
- **Manejo de errores** : Observar respuestas como ``404`` te ayuda a entender cómo el servidor maneja solicitudes incorrectas.
- **Tipo de contenido** : Incluso en errores, el servidor envía un tipo de contenido específico (generalmente HTML) para que el navegador pueda mostrar una página de error.

### b) Acceso HTTPS
En el mismo navegador, ingresa la dirección ``https://192.168.100.10``.

   (imagen 6.5)
   
Como estás usando un certificado autofirmado, el navegador mostrará una advertencia de seguridad. Acepta la advertencia para continuar.
Esto generará una solicitud HTTPS. En Wireshark, verás el proceso de cifrado (TLS Handshake) y el tráfico posterior cifrado.

(imagen 6.6)

#### 1. Client Hello
- **Paquete 76** :
  - El navegador envía un mensaje ``Client Hello`` al servidor.
  - Este mensaje incluye:
      - Versiones de TLS soportadas.
      - Cifrados sugeridos.
      - Datos aleatorios para generar claves.
  - En Wireshark, puedes expandir la sección TLS para ver estos detalles.
 
#### 2. Server Hello
- **Paquete 78** :
  - El servidor responde con un mensaje ``Server Hello``.
  - Incluye:
      - La versión de TLS seleccionada.
      - El cifrado seleccionado.
      - El certificado SSL/TLS (en este caso, tu certificado autofirmado).
  - También envía mensajes como ``Change Cipher Spec``, lo que indica que el cifrado está listo para comenzar.
 
  #### 3. Change Cipher Spec
- **Paquetes 79, 80, 81** :
  - Ambas partes confirman que el cifrado está activo.
  - A partir de este punto, todo el tráfico está cifrado.
 
  #### 4. Application Data
- **Paquetes 82, 83, 86, 88, etc.** :
  - Estos paquetes contienen los datos cifrados que transportan las solicitudes HTTP (``GET /``) y las respuestas HTTP (``200 OK``).
  - No puedes leer el contenido porque está protegido por cifrado.
 
  #### 5. ACK y FIN
- **Paquetes 84, 85, 92, 94** :
  - Mensajes TCP que confirman la recepción de datos (``ACK``) o cierran la conexión (``FIN``).
 
  #### ¿Por qué solo ves TCP y TLS?
Cuando aplicas el filtro ``tcp.port == 443``, Wireshark muestra solo los paquetes relacionados con el puerto 443 (el estándar para HTTPS). Aquí está la razón:

##### 1. Capa de transporte (TCP) :
- HTTPS usa TCP como protocolo de transporte.
- Por eso ves paquetes TCP que establecen la conexión (``SYN``, ``SYN-ACK``, ``ACK``) y gestionan la comunicación.
##### 2. Capa de cifrado (TLS) :
- HTTPS encapsula HTTP dentro de TLS para cifrar los datos.
- Una vez que se completa el **TLS Handshake** , todo el tráfico HTTP se cifra y aparece como **Application Data** en Wireshark.
#### 3. No hay HTTP visible :
- Como el cifrado oculta los datos HTTP, Wireshark no puede mostrarlos en texto claro.
