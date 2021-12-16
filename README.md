# MongoDB

Podemos instalar MongoDB de dos formas, la primera, es desde la pagina principal, siguiendo la siguiente guía: 

_https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/ ( Ubuntu )
_https://fastdl.mongodb.org/windows/mongodb-windows-x86_64-5.0.5.zip ( Windows )

La segunda forma, es atravez de Docker, la cuál se explica en esta guía.

# Instalando MongoDB con Docker

Lo primero que haremos es montar un contenedor con la imagen oficial de MongoDB. Debemos tener en cuenta las siguientes variables:


 · MONGO_INITDB_ROOT_PASSWORD= contraseña
 
 · MONGO_INITDB_ROOT_USERNAME= root
 
 · -p para asignar el puerto

El comando completo para montar el contenedor es la siguiente:

#_docker run -it -e MONGO_INITDB_ROOT_PASSWORD=12321 -e MONGO_INITDB_ROOT_USERNAME=root -p 8081:8081 --name MongoDB mongo

Para acceder al contenedor, abrimos una nueva terminal y ejecutamos: 

_docker exec -it mongodb /bin/bash

# Accediendo a MongoDB

Una vez dentro del contenedor con Bash abierto, podemos usar _mongosh -u root_ para acceder al cliente de MongoDB. (La contraseña a introducir es la que se introdujo previamente , al ejecutar "docker run") 
