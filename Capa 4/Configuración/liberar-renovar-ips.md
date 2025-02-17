# 1. Debian.
* Libera y renueva las direcciones IP:
  ``sudo dhclient -r enp0s3``
* Renueva la dirección IP:
  ``sudo dhclient enp0s3``
* Verifica la nueva dirección IP:
  ``ip a show enp0s3``
(imagen 4.1)
# Windows.
* Abre PowerShell o CMD como administrador y libera la dirección IP actual:
  ``ipconfig /release``
  (imagen 4.2)
* Renueva la dirección IP:
  ``ipconfig /renew``
  (imagen 4.3)
* Verifica la nueva dirección IP:
  ``ipconfig``
  (imagen 4.4)
# DIRECCIÓN IP EN MODO BRIDGE:
**DEBIAN:** 10.0.0.46
**WINDOWS:** 10.0.0.45


