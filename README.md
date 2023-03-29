# Cloud-LEMP

Este proyecto tiene como objetivo crear una instancia en Oracle Cloud y configurar un servidor LEMP (Linux, Nginx, MySQL y PHP).

## Introducción

En este proyecto, crearemos una instancia en Oracle Cloud y configuraremos un servidor LEMP que alojará una página web de prueba. Esta página web mostrará información sobre el sistema operativo y la versión de PHP instalada.

## Paso 1: Crear instancia en Oracle Cloud

1. Crear una cuenta en Oracle Cloud.
2. Crear una instancia con las siguientes especificaciones:
   - SO: Oracle Linux 7.9
   - Forma de pago: Pagar según el uso
   - Tipo de máquina: VM.Standard.E2.1.Micro
   - VPC: VPC con al menos una subnet pública
   - SSH Public Key: Utilizar la clave pública generada en el paso 2
3. Conectarse a la instancia utilizando SSH.

## Paso 2: Generar claves SSH

1. Abrir una terminal.
2. Ejecutar el comando `ssh-keygen -t rsa -b 4096 -C "correo@ejemplo.com"`.
3. Guardar las claves generadas en una carpeta segura.

## Paso 3: Conectar a la instancia de Oracle Cloud utilizando SSH

1. En la terminal, ejecutar el comando `ssh -i <ruta de la clave privada> opc@<IP de la instancia>`.
2. Ingresar la contraseña asignada durante la creación de la instancia.

## Paso 4: Instalar Nginx

1. En la instancia, ejecutar los siguientes comandos:
   - `sudo yum update`
   - `sudo yum install epel-release`
   - `sudo yum install nginx`
2. Verificar que Nginx esté instalado correctamente ejecutando el comando `nginx -v`.

## Paso 5: Instalar MySQL

1. En la instancia, ejecutar los siguientes comandos:
   - `sudo yum install mysql-server`
   - `sudo systemctl start mysqld`
   - `sudo systemctl enable mysqld`
2. Ejecutar el script de seguridad de MySQL con el comando `sudo mysql_secure_installation`.

## Paso 6: Instalar PHP

1. En la instancia, ejecutar los siguientes comandos:
   - `sudo yum install php php-fpm php-mysqlnd`
   - `sudo systemctl start php-fpm`
   - `sudo systemctl enable php-fpm`

## Paso 7: Configurar Nginx para usar PHP

1. En la instancia, modificar el archivo de configuración de Nginx ejecutando el comando `sudo nano /etc/nginx/sites-available/default`.
2. Modificar la sección `location ~ \.php$` para que se vea como sigue:
```
location ~ .php$ {
include snippets/fastcgi-php.conf;
fastcgi_pass unix:/run/php/php-fpm.sock;
}
```
3. Guardar los cambios y salir del editor de texto.
4. Reiniciar Nginx con el comando `sudo systemctl restart nginx`.

## Paso 8: Verificar que LEMP esté instalado correctamente

1. Crear un archivo de prueba en la carpeta `/var/www/html/` con el siguiente contenido:
```
<!DOCTYPE html>
   <html>
   <body>
   <?php
   phpinfo();
   ?>
   </body>
   </html>
   ```
