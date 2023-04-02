

GENERAR claves ssh en SO origen a conectar con cloud
comando: "ssh-keygen -t rsa -b 4096"
Aquí está la descripción de las opciones:
"-t rsa": especifica que se debe utilizar el algoritmo de cifrado RSA para la generación de claves.
"-b 4096": especifica que la longitud de la clave RSA generada debe ser de 4096 bits.

copiar la clave publica
cat ~/.ssh/id_rsa.pub

pegar clave publica antes de iniciar la instancia
(insertar jpg oracle)

conectar
ssh usuario@direccion-ip
