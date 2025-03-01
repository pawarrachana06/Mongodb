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
8. bsonType

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


Note : Reference when it is duplication and changing everytime.

## Aggregate
merging the relations


``` bash 
db.books.aggregate([{$lookup:{from:"authors",localField:"authors",foreignField:"_id",as:"creator"}}])
```


author --> collection name 
localField --> field in collection 
foreignField --> _id in current table 
as  ---> alias name 

## Schema Validation

two levels:

1. validationLevel: strict /moderate
2.validationAction : error(abort)/warn(proceed)

``` bash 
db.createCollection("post",{
validator:{
$jsonSchema:{
bsonType:'object",
required:["title","text","creator","comment"],
propertiers:{
title:{ bsontype:"string",
description:"must be string",
}
}
}
}
```



``` bash

db.runCommand("collection_name",validation)
```

## Mongo server additional settings

``` bash

 --dbpath && --logpath  ## add when starting the shell
```


## Mongo compass
Visual display of db like mysql workbench


## CREATE

``` bash
insertOne(data,options)
```
if there is any duplication , it aborts and stop the furthur process.

``` bash
insertMany(data,options)
```

{ordered:false} --> to continue when fails  default is true , wjich will stop when error

## WriteConcern

default is w:1 
where we get the acknowlegdement that the opeation was perfomred successfully.

client --> MongoDb server -->Storage Engine (Memory ,Data on Disk,Journel)

Journel : Operation the enginer has to perform.

{writeConcern:{w:1, j:UNDEFINED}}   --> write on how many instances defined and be acknowlegde, j journel (todo file operation not completed)

{w:1, j:true} --> success write and stored in journel , HIGH SECURITY 

{w:1,wtimeout:200, j:true} --> to give a time for success


## What is Atomicity

transcation either successed as a whole or fails

MongoDB CRUD Operations are atomic on the document Level(Including Embedded Documents)

## Importing Data

``` bash

mongoimport filename -d databasename -c collectionname --jsonArray  --drop

```

--jsonArray : To specify there are mor than one elements

--drop : Delete the previoud collection and create new


## READ 

``` bash

db.collectionname.find({fields:value})

```



``` bash

db.collectionname.find({fields:{$operator:value}})

```

### Operators

Query operators

1.Comparision


``` bash
db.collectioname.find({runtime:{$ne:60}})
```

$ne : not equal
$lte: lower than equal to
$gt:greather than
$eq: equal to

Embedded query


``` bash
db.collectioname.find({"rating.average":{$gt:7}})
```

With Arrays


``` bash
db.collectioname.find({genres:"Drama"}}) 
```


``` bash
db.collectioname.find({genres:["Drama"]}}) # Exact match
```


``` bash
db.collectioname.find({runtime:{$in:[30,42]}}) # If the values is in the array same for $nin
```


2.Logical Operators

a.$or

``` bash
db.collectioname.find({$or:[{"rating.average:{$lt:5}},{"rating.average":{$gt:9.3}}]}) 
```

b.$and

``` bash
db.collectioname.find({$and:[{"rating.average:{$lt:5}},{"rating.average":{$gt:9.3}}]}) 
```

OR

``` bash
db.collectioname.find({"rating.average:{$lt:5}},{"rating.average":{$gt:9.3}}) # Exact match
```

default is and
if we look for same field ,we need $and

c.$nor :opposite of $or

d.$not

``` bash
db.collectioname.find({runtime:{$not:{$eg:60}}).count()
```



3.Elements

a.$exists

``` bash
db.collectioname.find({age:{$exists:true, $ne:null}}) # only exists will give the null onces also
```

b.$type


``` bash
db.collectioname.find({phone:{$type:number}})
```

4.Evaluation

a.$regex

``` bash
db.collectioname.find({summary:{$regex:/musical/}) # not efficient 
```

b.$expr

``` bash
db.collectioname.find({$expr:{$gt:["$volume","$target"]}}) # volumen is greater than target
```


## Querying Arrays

``` bash
db.collectioname.find({"hobbies.title":"Sports:})

```

a.$size


``` bash
db.collectioname.find({hobbies:{$size:3}}).pretty()

```


b.$all

when you need exactly those item but in any order


``` bash
db.collectioname.find({genre:{$all:["action","thriller"]}) # if $all is not there it will only return the exact match

```

c.$elemMatch

In embedded document if we want to get only the element that has both condition and not checking the conditions separately, we use $elemMatch

``` bash
db.collectioname.find({hobbies:{$elemMatch:{"title":{"Sport"}},{"frequency":{$gt:{3}}}}}).count()

```

These will return the document with exact match



##Cursor
Requests in Batch , limit is 20

it -->cursor shell

shell is JS

const dataCursor=db.collectionname.find()
dataCursor.next()
dataCursor.hasNext() --> return true if there is.


####sort

``` bash
db.collectioname.find().sort({"rating.average::1}).pretty() # 1 for ascending and -1 for descending

```

Multi sorting

``` bash
db.collectioname.find().sort({"rating.average::1, runtime:1}).pretty() # 1 for ascending and -1 for descending

```


Limit



``` bash
db.collectioname.find().sort({"rating.average::1}).limit(10).pretty() # 1 for ascending and -1 for descending

```


Skip


``` bash
db.collectioname.find().sort({"rating.average::1}).skip(10).pretty() # 1 for ascending and -1 for descending

```

Order doesnt matter , mongodb does the sorting if skip/limit was earlier

### Projection 

``` bash
db.collectioname.find({}, {name:1,genres:1,rating:1)).pretty() #first is  {} to return all
```

#### Projects in Array


``` bash
db.collectioname.find({genres:"Drama"),{"genres.$":1})
```

$slice

``` bash
db.collectioname.find({"rating.average":{$gt:9)},{genres:{$slice:2},name:1}).pretty()

```

return the genres with first 2 elements

``` bash
db.collectioname.find({"rating.average":{$gt:9)},{genres:{$slice:[1,2]},name:1}).pretty()

```

returns the genres with second and third element ,skipping the first name



## UPDATE

#### update


``` bash
db.collectioname.updateOne({_id:ObjectId("5d-----------")},{$set:{hobbies:[{title:"sports",frequency:5,},{title:"Cooking",frequency:3},{title:"Hiking",frequency:1}}}})
# doesnt overide the existing fields but changes/updates the matched one
```

#### updateMany

``` bash
db.collectioname.updateMany({title:"Sports"},{$set:{isSporty:true}}) # adds an extra field to matched documents

```

#### Incrementing and Decrementing values


``` bash
db.collectioname.updateOne({name:"Manuel"},{$inc:{age:1}} # -1 to decrement and 1 for increment

```

### $min , $max and $mul

``` bash
db.collectioname.updateOne({name:"Manuel"},{$max:{age:32}} # set the age to 32 if the value is less then 32 , alternatively min does the same but reverse if the value is greater than specified.mul multiplies the values

```

### Getting rid of fields

``` bash
db.collectioname.updateOne({name:"Manuel"},{$unset:{phone:''}}) # removes the  phone field

```

##Rename

``` bash
db.collectioname.updateOne({},{$rename:{age:{"totalAge"}}}) #  rename age to totalage

```

##Upsert

``` bash
db.collectioname.updateOne({name:"Maria"},{$set:{phone:"",title:"",frequency:{}}},{unpsert:true) #if the document is not present it creates one

```

## updating array

``` bash
db.collectioname.updateMany({hobbies:{$elemMatch:{title:"Sports",frequency:{$gte:3}}},{$set:{"hobbies.$.highFrequency":true}})  # hobbies returned earlier ,access it and add new values
$ updates the first matching filter
```

#### updating all array elements/embedded elements.

``` bash
db.collectioname.updateMany({totalAge:{$gt:30}},{$inc:{"hobbies.$.[].frequency":-1}}) # refering the document inside hobbies with $.[]

```

``` bash
db.collectioname.updateOne({"hobbies.frquency":{$gt:2}},{$set:{"hobbies.$[el].goodFrequency":true}}.{arrayFilters:[{"el.frequency":{$gt:2}}]})

```


$ → Updates only the first matching element in an array.
$[] → Updates all elements in an array.
$[el] with arrayFilters → Updates only specific elements that match a filter condition inside an array.

## Adding elemnents to Array


``` bash
db.collectioname.updateOne({name:"Maria",{$push:{hobbies:{$each:[{title:"Good wine",frequency:1},{title:"Hiking",frequnecy:2}]}}})

```



## Remove

``` bash
db.collectioname.updateOne({name:"Maria",{$pull:{hobbies:{title:"Good wine"}}}) # $pop 1 last ,-1 first element {$pop:{hobbies:1}} $addToSet similar to push but no duplicate values 

```


## DELETE


To delete one document

``` bash
db.collectioname.deleteOne({name:"chris"})

```

To delete multiple records

``` bash
db.collectioname.deleteMany({age:{$gt:30}})

```

Collection delete


``` bash
db.collectioname.drop()

```

Database delete


``` bash
db.collectioname.dropDatabase()

```

## Working with Indexes

- Index are better for performance , but if too many it will lower the performance during inserts. choose wisely.

``` bash
db.collectionname.explain().find({'dob.age":{$gt:60}}) # explains the execution procedure

```


``` bash
db.collectioname.createIndex({'dob.age":1}) # 1/-1 desc/asc

```

``` bash
db.collectioname.dropIndex({'dob.age':1})

```


## When to avoid indexes

1. when you are sure the query will return the full collection. Index is not essential.
2. When you are aure it will return 10%/20% of collection it will speed up performance.

#### Creating compound indexes

``` bash
db.collectioname.createIndex({'dob.age":1,gender:1}) # can work for age ,but not gender only it goes to column span. LTR

```
Creatina a compound index with two array column not work
sorting in memory 32MB


``` bash
db.collectioname.getIndexes()

```


## Partial filteres


``` bash
db.collectioname.createIndex({'dob.age":1},{partialFilterExpression:{"dob.age":{$gt:60}}) # 
#  have to specify both . difference between , compunf and partial is limited number of collection , only restricted to male
```

#### TTL (Time to Live)

to delete the collection ,which is having a date field using indexes.

``` bash
db.collectioname.createIndex({createdAt:1},{expreAfterSeconds:10})

```



``` bash
db.collectioname.explain().find() # show the query execution steps , "queryPlanner,"executionStats","allPlansExecution"

```

#### Covered queries

when the result is fully present in the index. optimization ,speed is faster.No COLUMSCAN happens.Not advised to have index for every value.

Text index

``` bash
db.collectioname.createIndex({description:"text"}) # a ,the ,is ignored

```

``` bash
db.collectioname.find({$text:{$search:"book"}}).pretty()

```
``` bash
db.collectioname.find({$text:{$search:" "}},{score:{$meta:""}}).sort({score:{$meta:""}}).pretty()

```

``` bash
db.collectioname.createIndex({description:"text"},{background:true}) 
```

## Geospatial Queries

GeoJson


``` bash
db.collectioname.insertOne({name:"california",location:{type:"Point",cordinates:[longitude,latitude]}})

```

``` bash
db.collectioname.createIndex({loaction:"2dshphere"})

```

``` bash
db.collectioname.find({location:{$near:{$geometry:{type:"Point",coordinates:[-122.47,37.77]}},$maxDistance:,$minDistance:}}

```
[Geospatial data](https://www.mongodb.com/docs/manual/geospatial-queries/#:~:text=MongoDB%20supports%20query%20operations%20on%20geospatial%20data.%20This,learn%20more%2C%20see%20Perform%20Geospatial%20Queries%20in%20Atlas.?msockid=19c3d7e25a1d6e7108cbc3475b866f2b)


### Aggregation Framework

The Aggregation Framework in MongoDB is used for processing and transforming data within a collection. It operates through a pipeline that consists of multiple stages, each performing a specific operation on the documents.


``` bash
db.collectioname.aggregate([{$match:{gender:"female"}}]).pretty()  #$match	Filters documents (like find())

```

1.$match:	Filters documents (like find())


``` bash
db.collectioname.aggregate([{$match:{gender:'female'}},{$group:{_id:{state:"$location.state"},totalPersons:{$sum:1}}}])

```

similar to 

```sql
SELECT location.state AS state, COUNT(*) AS totalPersons
FROM collectionname
WHERE gender = 'female'
GROUP BY location.state;
```



2.$group:	Groups documents by a field and performs aggregations (e.g., sum, avg)


``` bash
db.collectioname.aggregate([{$match:{gender:'female'}},{$group:{_id:{state:"$location.state"},totalPersons:{$sum:1}}},{$sort:{totalPerson:-1}}],
)

```

3.$sort: Sorts documents based on a field



``` bash
db.collectioname.aggregate([$project:{
_id:0,
name:1,
email:1,
location:{
type:"Point",
coordinate:[
'$location.coordinates.longitude',
$location.coordinates.latitude
]}}]
)

```

4.$project:	Modifies documents, includes/excludes fields, or computes new ones



``` bash
db.collectioname.aggregate([$project:{
_id:0,
name:1,
email:1,
birthdate:{
$convert:{input:'$dob.date',to"date'}}
}
]
)
```

Series of pipeline 

Pipeline Stages - The aggregation pipeline consists of multiple stages that process data sequentially.


``` bash
db.collectioname.aggregate([
{$group:{_id:{age:'$age'},allHobbies:{$push:"$hobbies"}}}
]) # returns nested hobbies
```


5. $unwind:	Deconstructs arrays into multiple documents

``` bash
db.collectioname.aggregate([
{$unwind:"$hobbies"},
{$group:{_id:{age:'$age'},allHobbies:{$push:"$hobbies"}}}
]) # returns splits the array into multiple  but duplicate
```



``` bash
db.collectioname.aggregate([
{$unwind:"$hobbies"},
{$group:{_id:{age:'$age'},allHobbies:{$addToSet:"$hobbies"}}}
]) # returns splits the array into multiple  no duplicates
```


How to get the first field from list of arrays


``` bash
db.collectioname.aggregate([
{$project:{_id:0,examScore:{$slice:["$filedname",1]}}}
]) 
```


length of array


``` bash
db.collectioname.aggregate([
{$project:{_id:0,numScore:{$size:"#examScores"}
]) 
```

Filter with project

``` bash
db.collectioname.aggregate([
{$project:{_id:0,scores:{$filter:{input:'$examScores',as:'sc',cond:{$gt:["$$sc.score",60]}}}}}
]) 
```


$bucket


``` bash
db.collectioname.aggregate([
{$bucket:{groupBy:"$dob.age",boundaries:[10,18,30,40],output:{
names:{$push:"$name.first"}
}}}
]) 
```
OR

``` bash
db.collectioname.aggregate([
{
$bucketAuto:{
groupBy:"$dob.age",
bucket:5,
output:{
numPerson:{sum:1},
avergaeAge:{$avg:'$dob.age'}
}
}
{$out:{transformedPerson}
}
]) # output into different collection.
```


$geoNear

``` bash
db.collectioname.aggregate([
{
$geoNear:{
near:{type:"Point",coordinate:[long,lat]}
},

maxDistance:10000,
num:10, #limit

}
]) #geoNear has to be the first pipeline
```



### Working with Numeric Data
1.Int 32/64 bit
2.Double 64bit/128 bit high preicision

## Security

Authentication : Identifies valid users of the database

Authorization: Identifies what these users may actually do in the database


createUser({user:"",pwd:"",roles:["userAdminAnyDatabase]) -->"Maxschwar"(Roles $ Privileges) -->Database access
db.auth(username,passsword)

db.getUser("name")

## Deployment

1.capped collection : delete the previous data , when condition meet .

``` mongodb

db.createCollection("User",{capped:true},{max:3})
```

2.Replica set (Backup/Fault tolerance)

write to primary always, read if primary is offline , new primary is elected from secondary.

[!replica set](https://github.com/user-attachments/assets/5fa240fd-110e-4cc0-a8de-c35070b7b7b8)


3.Sharding (Horizontal scaling)

more operation .

multiple servers:distrubuted data , queries ran on all.mongos(Router)

4.Deploying

mongoDb Atlas along with cloud provider.


## Transaction
success/fail


``` mongodb
const session=db.getMongo().startSesssion()
session.startTransaction()
const userC=session.getDatabase("blog").user
userC=deleteOne({_id:ObjectId("9999")} # still not deleted in todo
session.commitTransaction() #can commit/abort

```


