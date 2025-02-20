# 1. Debian.
* Libera y renueva las direcciones IP:

      sudo dhclient -r enp0s3
* Renueva la dirección IP:

      sudo dhclient enp0s3
* Verifica la nueva dirección IP:

      ip a show enp0s3
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/c5fa1de4afa18d280717393052965596ad3232f9/Capa%204/im%C3%A1genes%20capa%204/4.1.png></img>
# 2. Windows.
* Abre PowerShell o CMD como administrador y libera la dirección IP actual:

      ipconfig /release
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/c5fa1de4afa18d280717393052965596ad3232f9/Capa%204/im%C3%A1genes%20capa%204/4.2.png></img>
* Renueva la dirección IP:

      ipconfig /renew
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/c5fa1de4afa18d280717393052965596ad3232f9/Capa%204/im%C3%A1genes%20capa%204/4.3.png></img>
* Verifica la nueva dirección IP:

      ipconfig
<img src=https://github.com/GandalfTercero/Laboratorio-Modelo-OSI/blob/c5fa1de4afa18d280717393052965596ad3232f9/Capa%204/im%C3%A1genes%20capa%204/4.4.png></img>
# DIRECCIÓN IP EN MODO BRIDGE:
- **DEBIAN:** 10.0.0.46
- **WINDOWS:** 10.0.0.45


