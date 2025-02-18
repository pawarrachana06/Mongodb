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



![image](https://th.bing.com/th/id/OIP.3YXF1z_XDug112LJVPbwnQHaDB?w=292&h=142&c=7&r=0&o=5&dpr=1.3&pid=1.7)
![image](https://www.quickprogrammingtips.com/wp-content/uploads/2020/08/mongodb-architecture.jpg)


## Database, collection , Document
- Mongodb has the following structure:
 -> Database 
 -> Database can have many Collection ,similar to Tables in sql.
 -> Document is the object or data to be stored.

## JSON VS BSON

![Difference](https://miro.medium.com/v2/resize:fit:875/1*3oKrtK8VhuVetGnCHTTbeg.png)

![image](https://github.com/user-attachments/assets/630f8405-90a9-4f14-b2b9-6d6106907c32)

## CRUD operation in mongodb

- Application : The code can use Mongodb Driver and (CRUD) on MongoDb server .
- Analystic/BI tools : BI/connector/shell -->Mongodb server (read)
- Admin : Shell -->Mongodb server (CRUD)

CREATE

``` bash
insertOne(data,options)
```



``` bash
insertMany(data,options)
```

READ

```bash
find(filter,options)
 ```

```bash
filterOne(filter,options)
```

UPDATE

```bash
updateOne(filter,data,options)
 ```

```bash
updateMany(filter,data,options)
```

```bash
replaceOne(filter,data,options)
 ```

DELETE

```bash
deleteOne(filter,options)
```

```bash
deletMany(filter,options)
```

``` bash

deleteMany({}) # delete all

```


![image](https://github.com/user-attachments/assets/8e1d2a30-c775-4620-aeb9-b36de999eedb)
![image](https://github.com/user-attachments/assets/54e00b75-f275-4f6d-aabb-d98ded26dd74)


## update vs updateMany()

```bash
updateMany(filter,data,options) # $set is important 
```

```bash
update(filter,data,options) # $ set is not important , and will replace the object with the update value instead of adding a new field to existing.
```

eg : Write a query to update the age of a student named Alice to 26 in the “students” collection.

``` bash
db.students.updateOne(
   { name: "Alice" },
   { $set: { age: 26 } }
)
```

## Replace

```bash
replaceOne(filter,data,options) # Is best to replace the fields with new fields instead of update
```

## Find
```bash
 find() # gives a cursor , use it to get more
```
```bash
 find().forEach()/toArray() # to get all at onces
```

## To drop a db or collection

``` bash
db.dropDatabase()
```

``` bash
db.myCollection.drop()
```

## Projection
- To only get the data needed .rather then filtering in backend code

```bash
 db.collection_name.find({},{name:1,_is:0}) # only return name {}-> return all , 0 is to exclude
```

## Embedded Document

- 100 level of nesting
- 16 MB size document

```bash
 db.collection_name.updateOne({name:"Max"},{status:{description:"Writer"}})
```

## Schemas and Relations

### Data types

1. Text : string , with "" on right side
2. Boolean :true/false
3. Number : NumberInt(),Integer (int 32) eg 55 , NumberLong (int 64) eg .100000, NumberDecimal eg.12.99
4. objectId : unqiue id
5. date:ISODate("2018-09-09") new Date()
6. Timestamp : Timestamp() new Timestamp()
7. Array :List of all above eg . []

--> NumberInt creates a int32 value => NumberInt(55)

--> NumberLong creates a int64 value => NumberLong(7489729384792)

--> If you just use a number (e.g. insertOne({a: 1}), this will get added as a normal double into the database. The reason for this is that the shell is based on JS which only knows float/ double values and doesn't differ between integers and floats.

--> NumberDecimal creates a high-precision double value => NumberDecimal("12.99") => This can be helpful for

## One to one relations

Embedded document eg.patient and summary 

## One to Many relation

--> reference method (city citizen eg)
--> Embedded document (question answer eg)

## Many to Many

--> Reference and emebedded (eg. customer  order eg)

- Reference when it is duplication and changing everytime.








  


 

