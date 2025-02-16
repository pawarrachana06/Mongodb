# Mongodb Notes
![MongoDB](https://img.shields.io/badge/Database-MongoDB-green?logo=mongodb)
- MongoDB's name comes from "humongous database", emphasizing its ability to handle large amounts of data.
- Schemaless
- Mongodb server allows to create instances of databases.
- Json with key value , stored in mongodb as bson.
- In MongoDB (a NoSQL database) does not support joins like relational databases (e.g., MySQL, PostgreSQL).
  
  ![Structure](https://www.w3resource.com/w3r_images/mongodb-document-collection.png)

  ## Installation

  - [MongoDB Community Server to build solution locally](https://www.mongodb.com/try/download/community), which installs the servers(Service), client and router.
  - Service will run in the background.
    -> Search for service in start to start the Server ,look for mongodb service and stop if not need,start when needed.
    -> Alternatively through command prompt we can start/stop by following command.
 
    
    ```bash
    net stop/start MongoDB
    ```

- [Mongodb shell Installation](https://www.mongodb.com/try/download/shell)
      
 - ![image](https://github.com/user-attachments/assets/b2f59316-b890-4c5e-af64-c760bdb9ed86)
   ```bash
    show dbs # List the databases present
    ```
      
- ![image](https://github.com/user-attachments/assets/6763afa8-6d71-4f05-85ce-ba8a792c216e)

```bash
    use dbname # Create and switch to the db
```
- ![image](https://github.com/user-attachments/assets/fe9d6ade-e0b2-433d-bb8b-04b7bd772d52)

```bash
    db.collection_name.insert({key:value})
```
    
```bash
    db.collection_name.find()
```

  
```bash
   db.collection_name.find().pretty()
 ```

- [Mongo Drivers](https://www.mongodb.com/docs/drivers/?msockid=19c3d7e25a1d6e7108cbc3475b866f2b)


![image](https://github.com/user-attachments/assets/7fd3559a-b78b-40a5-a594-e16c6ba8ac19)

![image](https://github.com/user-attachments/assets/a89e073e-1f51-44d3-ba9e-edd0ff2964ae)



 

