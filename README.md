# MongoDB

Podemos instalar MongoDB de dos formas, la primera, es desde la página principal, siguiendo la siguiente guía: 

_https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/ ( Ubuntu )
_https://fastdl.mongodb.org/windows/mongodb-windows-x86_64-5.0.5.zip ( Windows )

La segunda forma, es atrevés de Docker, la cual se explica en esta guía.

### En caso de usar el archivo .yaml de este repositorio:

En el directorio donde montemos el fichero .yaml (recuerda que es con "docker compose up" en linux y "docker-compose up" desde Powershell), se nos creará una carpeta "home", esta estará bindeada (conectada) con el directorio /home del contenedor. 

( Siempre podemos recurrir a ussar comandos propios de Docker para pasar datos de un lugar a otro "docker cp", etc)


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
ACLARACIÓN: No hay tablas, ya que es un modelo NoSQL, hay colecciones. (busca en Wikipedia)


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

###### Insertar varias coleccions:

     Usuaris> db.Usuarios.insertMany([{"Nombre de usuario": "Manolo", "Nombre": "Manolin", "Telefono 1": "6658465", "Telefono 2" : "65848651", "Domicilio" : " Av. Patata 23", "CP" : "07004", "Fecha de nacimiento": "2001"}, {"Nombre de usuario" : "Perxita", "Nombre" : "Federico", "Telefono 1": "6548123", "Telefono 2" : "49841238", "Domicilio" : "Av. Tomate 2", "CP":"989845", "Fecha de nacimiento":"2002"}])
     {
     acknowledged: true,
     insertedIds: {
    '0': ObjectId("61def5dde5f14e2c56e01496"),
    '1': ObjectId("61def5dde5f14e2c56e01497")
     }
     }
     

###### Insertar varios datos en una columna: 

      db.Usuarios.insert({ 'Nombre de usuario' : "Zoser77", Nombre :  "Raul", 'Telefono 1' : "6425884", 'Telefono 2' : "887451478", Domicilio : "Av. Cebolla 23" , CP : "87414", 'Fecha de nacimiento' : "1999" , "Juegos favoritos": { "De pley": " Spiderman", "De Nintendo" : "Zelda"}})

![imagen](https://user-images.githubusercontent.com/80277545/149176036-10d3ce6b-7c49-4ead-9b63-9f6bc5632f5f.png)


####### Actualizar colecciones:

En el siguiente caso, tenemos dos entradas, donde queremos que tengan el mismo nombre , "Pablito". Si queremos que "Pablito", sea el nombre de los usuarios "Zoser77", ejecutaremos lo siguiente:

![imagen](https://user-images.githubusercontent.com/80277545/149177991-2507c45c-1f60-45aa-9cc7-c3419f77f656.png)

Ejecutariamos lo siguiente:

          db.Usuarios.update({ "Nombre de usuario": "Zoser77"},{ $set: {"Nombre":"Pablito"}},{multi:true})
          
Esto en SQL sería:

          UPDATE Usuarios
          SET nombre=Pablito
          where "Nombre de usuario" = Zoser77
          
Resultado:

![imagen](https://user-images.githubusercontent.com/80277545/149178641-12be74d8-6225-4227-8b53-284f1cc2cd15.png)


### Operadores Logicos en MongoDB
