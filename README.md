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



docker run -it -e MONGO_INITDB_ROOT_PASSWORD=12321 -e MONGO_INITDB_ROOT_USERNAME=root -p 8081:8081 --name MongoDB mongo



Para acceder al contenedor, abrimos una nueva terminal y ejecutamos: 

_docker exec -it mongodb /bin/bash

# Accediendo a MongoDB

Una vez dentro del contenedor con Bash abierto, podemos usar _mongosh -u root_ para acceder al cliente de MongoDB. (La contraseña a introducir es la que se introdujo previamente , al ejecutar "docker run") 

Ahora tendríamos que ver algo del estilo: 


test> ....


# Algunos comandos para familiarizarnos con MongoDB

Para entender como funciona MongoDB y los archivos .JSON, voy a usar la base de datos "Tienda".
ACLARACIÓN: No hay tablas ya que es un modelo NoSQL, hay colecciones. (busca en Wikipedia)


###### Listar Bases de datos:

 · show dbs

###### Crear Bases de datos:

 Para crear una base de datos, lo podemos hacer directamente "usando" una base de datos:
 
 · use Tienda
 
###### Crear Coleccion ( = tabla)

Al insertar datos, si la colección no está creada, se crea automaticamente:

 · db.Usuarios.insertOne({"Nombre de usuario": "Josep11", "Nombre": "Josep", "Telefono 1": "685478596","Telefono 2": "685475636", "Domicilio": "Av. Patata 25", "CP": "07658", "Fecha de nacimiento": "1990"});

###### Mostrar colecciones:

 · show collections
 
###### Mostrar contenido de las colecciones:

 · db.Usuarios.find()
 
###### Buscar un dato en concreto:

 · db.Usuarios.find ({ "Nombre de usuario": "Josep11" })

###### Insertar datos en una colección:

 · db.Usuarios.insert( [ { "Nom de usuario": "Mari", "Nombre": "Marina", "Telefono 1": "62228596", "Domicilio": "Av. Lechuga 123", "CP": "07777", "Fecha de nacimiento": "1953"}
... ])


