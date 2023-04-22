![underconstruction](https://user-images.githubusercontent.com/126183973/233772689-0592fd0b-cd89-4eb0-8fdb-ddb60c827302.jpg)


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
143.47.43.xxx

usar passphrase si se configuró

copiar claves ssh (publica y privada) de ubuntu desktop a windows poweshell

ccp@XXX:~/.ssh$ cp id_rsa /mnt/c/Users/XXX/.ssh

ccp@XXX:~/.ssh$ cp id_rsa.pub /mnt/c/Users/XXX/.ssh

mismo procedimiento para conectar desde windows powershell

_____________________
>> TIP: crear alias para conectar sin info ip etc:
crear archivo config en directorio .ssh

en windows:

Host oracle1
  HostName 143.47.43.xxx
  User ubuntu
  IdentityFile C:\Users\XXX\.ssh\id_rsa
  
en ubuntu desktop:

Host oracle1
  HostName 143.47.43.xxx
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

La siguiente pregunta te preguntará si deseas eliminar los usuarios anónimos. Es una buena práctica de seguridad eliminar los usuarios anónimos para evitar posibles brechas de seguridad, por lo que puedes elegir "Y" para eliminarlos.

La siguiente pregunta te preguntará si deseas desactivar el inicio de sesión remoto del usuario root. Es una buena práctica de seguridad desactivar el inicio de sesión remoto del usuario `root, por lo que puedes elegir "Y" para desactivarlo.

La siguiente pregunta te preguntará si deseas desactivar el inicio de sesión del usuario root en el servidor de base de datos. Es una buena práctica de seguridad desactivar el inicio de sesión del usuario root en el servidor de base de datos, por lo que puedes elegir "Y" para desactivarlo.

Finalmente, se te preguntará si deseas recargar los privilegios de la tabla de permisos para que los cambios surtan efecto. Elije "Y" para recargar los privilegios.
```

```
Si error 
el método de autenticación que se está utilizando para el usuario root en MySQL no almacena datos de autenticación en el servidor MySQL. Debido a esto, no puedes usar el comando SET PASSWORD para establecer una contraseña para el usuario root. En su lugar, deberás usar el comando ALTER USER para establecer la contraseña del usuario root.

Para establecer la contraseña del usuario root en MySQL utilizando el comando ALTER USER, sigue estos pasos:

Inicia sesión en MySQL como usuario root ejecutando el siguiente comando:
sudo mysql -u root

Una vez que hayas iniciado sesión en MySQL, utiliza el siguiente comando para establecer la contraseña del usuario root:
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'tu_contraseña';

Después de ejecutar el comando ALTER USER, utiliza el siguiente comando para actualizar los cambios en la tabla de permisos:
FLUSH PRIVILEGES;

volver a ejecutar sudo mysql_secure_installation
```

3. Verifica que MySQL esté instalado y en ejecución ingresando el siguiente comando:
sudo systemctl status mysql

**Paso 3: Instalar PHP

1. Instala PHP y sus módulos con el siguiente comando:
sudo apt install php libapache2-mod-php php-mysql

2. Verifica que PHP esté instalado ingresando el siguiente comando:
php -v

**Paso 4: Publicar una página web

1. Crea una carpeta llamada public_html en la raíz de tu directorio de inicio con el siguiente comando:
mkdir ~/public_html

2. Crea un archivo index.php en la carpeta public_html con el siguiente comando:
echo "<?php phpinfo(); ?>" > ~/public_html/index.php

3. Reinicia Apache para que tome los cambios realizados con el siguiente comando:
sudo systemctl restart apache2

4. Verifica que Apache esté en ejecución y no haya errores con el siguiente comando:
sudo systemctl status apache2

-----
poner pagina de prueba en ubicacion predeterminada /var/www/html
cambiar permisos a /var/www/html
sudo chown -R www-data:www-data /var/www/html

