

GENERAR claves ssh en SO origen a conectar con cloud

comando: "ssh-keygen -t rsa -b 4096"

Aquí está la descripción de las opciones:

"-t rsa": especifica que se debe utilizar el algoritmo de cifrado RSA para la generación de claves.
"-b 4096": especifica que la longitud de la clave RSA generada debe ser de 4096 bits.

copiar la clave publica
cat ~/.ssh/id_rsa.pub

pegar clave publica antes de iniciar la instancia
(insertar jpg oracle)

_______________________
conectar desde ubuntu desktop:
ssh usuario@direccion-ip
143.47.43.162
usar passphrase si se configuró

copiar claves ssh (publica y privada) de ubuntu desktop a windows poweshell

ccp@DESKTOP-14H7LU5:~/.ssh$ cp id_rsa /mnt/c/Users/COUGAR/.ssh

ccp@DESKTOP-14H7LU5:~/.ssh$ cp id_rsa.pub /mnt/c/Users/COUGAR/.ssh

mismo procedimiento para conectar desde windows powershell

_____________________
>> TIP: crear alias para conectar sin info ip etc:
crear archivo config en directorio .ssh

en windows:
Host oracle1
  HostName 143.47.43.162
  User ubuntu
  IdentityFile C:\Users\COUGAR\.ssh\id_rsa
  
en ubuntu desktop:
Host oracle1
  HostName 143.47.43.162
  User ubuntu
  IdentityFile ~/.ssh/id_rsa

