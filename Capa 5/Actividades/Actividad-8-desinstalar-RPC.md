# En Debian:
## 1. Detén el servicio rpcbind:
	  
    sudo systemctl stop rpcbind
    sudo systemctl disable rpcbind
## 2. Elimina el paquete rpcbind:
	
    sudo apt remove --purge rpcbi
## 3. Limpia los residuos del sistema:

    sudo apt autoremove
    sudo apt clean
