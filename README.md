# MongoDB

Podemos instalar MongoDB de dos formas, la primera, es desde la pagina principal, siguiendo la siguiente guía: 

_https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/ ( Ubuntu )
_https://fastdl.mongodb.org/windows/mongodb-windows-x86_64-5.0.5.zip ( Windows )

La segunda forma, es atravez de Docker, la cuál se explica en esta guía.

# Instalando MongoDB con Docker

Lo primero que haremos es montar un contenedor con la imagen oficial de MongoDB. Debemos tener en cuenta las siguientes variables:


     MONGO_INITDB_ROOT_PASSWORD= contraseña
     MONGO_INITDB_ROOT_USERNAME= root
     -p para asignar el puerto


El comando completo para montar el contenedor es la siguiente:

      docker run -it -e MONGO_INITDB_ROOT_PASSWORD=12321 -e MONGO_INITDB_ROOT_USERNAME=root -p 8081:8081 --name MongoDB mongo


Para acceder al contenedor, abrimos una nueva terminal y ejecutamos: 

     docker exec -it mongodb /bin/bash
     
     ![imagen](https://user-images.githubusercontent.com/80277545/146464397-f0e7c35f-5dd8-4830-8ae5-48a9561bef43.png)

     

# Accediendo a MongoDB

Una vez dentro del contenedor con Bash abierto, podemos usar _mongosh -u root_ para acceder al cliente de MongoDB. (La contraseña a introducir es la que se introdujo previamente , al ejecutar "docker run") 

Ahora tendríamos que ver algo del estilo: 

     mongosh -u root
     test> ....
     ![imagen](https://user-images.githubusercontent.com/80277545/146464477-bc5d297f-f476-4446-ae7f-a54b3f253f52.png)


# Algunos comandos para familiarizarnos con MongoDB

Para entender como funciona MongoDB y los archivos .JSON, voy a usar la base de datos "Tienda".
ACLARACIÓN: No hay tablas ya que es un modelo NoSQL, hay colecciones. (busca en Wikipedia)


###### Listar Bases de datos:

      show dbs
      ![imagen](https://user-images.githubusercontent.com/80277545/146464531-5e4b1465-4809-4ab8-bc53-7e3f0370b563.png)

     

###### Crear Bases de datos:

 Para crear una base de datos, lo podemos hacer directamente "usando" una base de datos:
 
      use Tienda
      ![imagen](https://user-images.githubusercontent.com/80277545/146464575-ba3572fe-7678-4cc5-98ef-0a521d32a91e.png)

 
###### Crear Coleccion ( = tabla)

Al insertar datos, si la colección no está creada, se crea automaticamente:

     db.Usuarios.insertOne({"Nombre de usuario": "Josep11", "Nombre": "Josep", "Telefono 1": "685478596","Telefono 2": "685475636", "Domicilio": "Av. Patata 25", "CP": "07658", "Fecha de nacimiento": "1990"});
     ![imagen](https://user-images.githubusercontent.com/80277545/146464646-1a0e57ff-b775-4604-99d0-6ba726783f57.png)


###### Mostrar colecciones:

     show collections
     ![imagen](https://user-images.githubusercontent.com/80277545/146464711-b88ae14a-e169-43a7-a209-07f6506c625a.png)

     
 
###### Mostrar contenido de las colecciones:

     db.Usuarios.find()
     ![imagen](https://user-images.githubusercontent.com/80277545/146464758-b8b9c126-d0aa-4a80-aaa2-9f528e122e3c.png)

 
###### Buscar un dato en concreto:

     db.Usuarios.find ({ "Nombre de usuario": "Josep11" })
     ![imagen](https://user-images.githubusercontent.com/80277545/146464813-964bf6a6-12b0-4eb0-ad9c-9921c206871f.png)

     

###### Insertar datos en una colección:

     db.Usuarios.insert( [ { "Nom de usuario": "Mari", "Nombre": "Marina", "Telefono 1": "62228596", "Domicilio": "Av.          Lechuga 123", "CP": "07777", "Fecha de nacimiento": "1953"}
     ... ])
     
     


