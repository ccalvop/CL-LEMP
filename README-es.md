

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
  
  __________________________configurar LAMP

**Paso 1: Instalar Apache

1. Conéctate a la instancia de Oracle Cloud utilizando un cliente SSH.

2. Actualiza los repositorios de paquetes disponibles ejecutando el siguiente comando:
sudo apt update

3. Instala el servidor web Apache con el siguiente comando:
sudo apt install apache2

4. Verifica que Apache esté instalado y en ejecución ingresando el siguiente comando:
sudo systemctl status apache2

**Paso 2: Instalar MySQL

1. Instala el servidor de base de datos MySQL con el siguiente comando:
sudo apt install mysql-server

2. Cuando se complete la instalación, ejecuta el siguiente comando para asegurar la instalación:
sudo mysql_secure_installation
Este comando te guiará a través de una serie de preguntas para mejorar la seguridad del servidor MySQL. Sigue las instrucciones para completar la configuración

```
las preguntas de seguridad para configurar adecuadamente MySQL usando el comando mysql_secure_installation:

Al ejecutar sudo mysql_secure_installation, se te pedirá que ingreses la contraseña del usuario root de MySQL. Si acabas de instalar MySQL, es posible que aún no hayas establecido una contraseña para el usuario root. En ese caso, simplemente presiona Enter para dejar la contraseña en blanco y continuar.

La primera pregunta que se te hará es si deseas cambiar la contraseña del usuario root. Si no has establecido una contraseña aún, puedes elegir "N" para dejar la contraseña en blanco.

La siguiente pregunta te preguntará si deseas desactivar el inicio de sesión remoto del usuario root. Es una buena práctica de seguridad desactivar el inicio de sesión remoto del usuario `root, por lo que puedes elegir "Y" para desactivarlo.

La siguiente pregunta te preguntará si deseas eliminar los usuarios anónimos. Es una buena práctica de seguridad eliminar los usuarios anónimos para evitar posibles brechas de seguridad, por lo que puedes elegir "Y" para eliminarlos.

La siguiente pregunta te preguntará si deseas desactivar el inicio de sesión del usuario root en el servidor de base de datos. Es una buena práctica de seguridad desactivar el inicio de sesión del usuario root en el servidor de base de datos, por lo que puedes elegir "Y" para desactivarlo.

La siguiente pregunta te preguntará si deseas eliminar la base de datos de prueba. La base de datos de prueba es una base de datos que se crea automáticamente en MySQL para realizar pruebas y no es necesaria para un servidor de producción. Por lo tanto, es recomendable eliminarla, por lo que puedes elegir "Y" para eliminarla.

Finalmente, se te preguntará si deseas recargar los privilegios de la tabla de permisos para que los cambios surtan efecto. Elije "Y" para recargar los privilegios.
```

3. Verifica que MySQL esté instalado y en ejecución ingresando el siguiente comando:
sudo systemctl status mysql

