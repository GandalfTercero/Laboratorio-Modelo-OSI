# Capa 6 - Prensentación.

**Entorno de pruebas:**
- **VirtualBox 7.1.4** con dos máquinas virtuales:
    - **Debian** (IPs: ``10.0.2.5`` [NAT], ``192.168.100.10`` [Red Interna]).
    - **Windows 10** (IPs: ``10.0.2.6`` [NAT], ``192.168.100.20`` [Red Interna]).
- **Herramientas:** Wireshark, Apache, OpenSSL, netcat, PowerShell.

## 🎯 Objetivos
1. Observar el cifrado TLS/SSL (seguridad).
2. Analizar compresión de datos (eficiencia).
3. Verificar codificación de caracteres (compatibilidad).

   
La capa de presentación (OSI Layer 6) actúa como **traductora** entre los datos de la aplicación (Capa 7) y el formato requerido para su transmisión en la red. Sus funciones clave son:
1. Cifrado/Descifrado : Protege la confidencialidad (ej. TLS/SSL).
2. Compresión : Reduce el tamaño de los datos para mayor eficiencia.
3. Codificación : Asegura que los datos sean legibles en ambos extremos (ej. UTF-8, ASCII).

## ¿Por qué este laboratorio es útil?
El laboratorio simula escenarios reales donde la Capa 6 resuelve problemas críticos:

### 1. Cifrado (SSL/TLS)
- **Problema** : Datos sensibles viajan en texto claro (HTTP).
- **Solución** : TLS cifra los datos (HTTPS).
- **En el lab** :
    - Configuras un servidor HTTPS y observas el handshake TLS en Wireshark.
    - Comparas tráfico HTTP (texto claro) vs HTTPS (datos cifrados).
    - Aprendizaje : La Capa 6 gestiona el cifrado antes de que los datos salgan de la máquina.

### 2. Compresión
- **Problema** : Datos grandes consumen ancho de banda.
- **Solución** : Compresión (ej. gzip).
- **En el lab** :
    - Envías archivos comprimidos y sin comprimir via ``netcat``.
    - En Wireshark, ves cómo los datos comprimidos ocupan menos paquetes.
    - **Aprendizaje** : La Capa 6 optimiza la transmisión sin afectar el contenido original.

### 3. Codificación de caracteres
- **Problema** : Símbolos especiales (ej. "Café") se corrompen si no hay acuerdo en la codificación.
- **Solución** : Usar estándares como UTF-8.
- **En el lab** :
    - Creas un archivo con caracteres UTF-8 y lo abres en Windows con editores que no lo soportan (ej. Bloc de notas).
    - Corriges el error usando herramientas que especifican la codificación.
    - **Aprendizaje** : La Capa 6 garantiza que los datos se interpreten correctamente en destino.

## Conclusión
Este laboratorio te permite **ver en acción** cómo la Capa 6 resuelve problemas prácticos:

- **Cifrado** → Protege datos sensibles.
- **Compresión** → Ahorra recursos.
- **Codificación** → Evita corrupción de datos.

Al usar herramientas reales (OpenSSL, Wireshark, gzip) y analizar paquetes, entiendes cómo la teoría OSI se aplica en sistemas reales. ¡Es como ver "bajo el capó" de las comunicaciones seguras y eficientes! 🔍💻
