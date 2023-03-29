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
3. Para verificar si Nginx está funcionando correctamente, abra su navegador y escriba la dirección IP de su instancia de Oracle Cloud en la barra de direcciones. Si todo está configurado correctamente, debería ver la página de bienvenida de Nginx.

## Paso 5: Instalar MySQL

1. En la instancia, ejecutar los siguientes comandos:
   - `sudo yum install mysql-server`
   - `sudo systemctl start mysqld`
   - `sudo systemctl enable mysqld`
2. Ejecutar el script de seguridad de MySQL con el comando `sudo mysql_secure_installation`.
3. Verificar si MySQL está funcionando correctamente con el comando `sudo mysql -u root -p`.

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
Comentar las siguientes lineas.
```
# location ~ \.php$ {
# include snippets/fastcgi-php.conf;
# fastcgi_pass unix:/run/php/php7.4-fpm.sock;
# }
```
3. Guardar los cambios y salir del editor de texto.
4. Reiniciar Nginx con el comando `sudo systemctl restart nginx`.

## Paso 8: Verificar que LEMP esté instalado correctamente

### HTML:
1. Crear un archivo de prueba en la carpeta `/var/www/html/` con el siguiente contenido:
```
<!DOCTYPE html>
<html>
<head>
<title>Prueba de LEMP</title>
</head>
<body>
<h1>LEMP instalado correctamente!</h1>
</body>
</html>
```
2. Guardar el archivo con el nombre index.html.
3. Abrir un navegador web y navegar a la dirección IP pública de la instancia de Oracle Cloud.
4. Debería ver la página de prueba con el mensaje "LEMP instalado correctamente!".

### PHP:
1. Crear un archivo de prueba en la carpeta `/var/www/html/` con el siguiente contenido:
```
<?php
phpinfo();
?>
```
2. Guardar el archivo con el nombre info.php.
3. Abrir un navegador web y navegar a la dirección IP pública de la instancia de Oracle Cloud seguida de /info.php.
4. Debería ver una página que muestre información sobre la versión de PHP instalada en la instancia.


