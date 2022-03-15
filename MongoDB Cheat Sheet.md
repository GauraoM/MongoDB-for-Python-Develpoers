### Connect MongoDB Shell
mongo # connects to mongodb://127.0.0.1:27017 by default
mongo --host <host> --port <port> -u <user> -p <pwd> # omit the password if you want a prompt
mongo "mongodb://192.168.1.1:27017"
mongo "mongodb+srv://username:password@mflix.luykb.mongodb.net/<databasename>"  MongoDB Atlas

Ex:
mongo "mongodb+srv://mflixAppUser:mflixAppPwd@mflix.luykb.mongodb.net/test"  MongoDB Atlas

### Helpers

#### 1.Show Databases
  
show dbs
db // prints the current database

#### 2.Switch Database
  
use <database_name> 
Ex: use sample_training

#### 3.show collections
show collections

### CRUD

#### 1.Create
  
db.coll.insertOne({name: "Max"})
  
db.coll.insert([{name: "Max"}, {name:"Alex"}]) // ordered bulk insert
  
db.coll.insert([{name: "Max"}, {name:"Alex"}], {ordered: false}) // unordered bulk insert
  
db.coll.insert({date: ISODate()})
  
db.coll.insert({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})

#### 2.Read
  
db.coll.findOne({"cast": "Salma Hayek"}) // returns a single document
  
db.coll.find({"cast": "Salma Hayek"})    // returns a cursor - show 20 results
  
db.coll.find({"cast": "Salma Hayek"}).pretty()
  
db.coll.find({name: "Max", age: 32}) // implicit logical "AND".
  
db.coll.find({name: "Max", age: 32}).explain("executionStats") // or "queryPlanner" or "allPlansExecution"
  
db.coll.distinct("name")

##### 2.1 Count
  
db.coll.count({age: 32})
  
db.coll.estimatedDocumentCount()  

##### 2.2 Comparison
  
db.coll.find({"year": {$gt: 1970}})
  
db.coll.find({"year": {$gte: 1970}})
  
db.coll.find({"year": {$lt: 1970}})
  
db.coll.find({"year": {$lte: 1970}})
  
db.coll.find({"year": {$ne: 1970}})
  
db.coll.find({"year": {$in: [1958, 1959]}})
  
db.coll.find({"year": {$nin: [1958, 1959]}})

##### 2.3 Logical
  
db.coll.find({name:{$not: {$eq: "Max"}}})
  
db.coll.find({$or: [{"year" : 1958}, {"year" : 1959}]})
  
db.coll.find({$nor: [{price: 1.99}, {sale: true}]})
  
db.coll.find({
  $and: [
    {$or: [{qty: {$lt :10}}, {qty :{$gt: 50}}]},
    {$or: [{sale: true}, {price: {$lt: 5 }}]}
  ]
})

##### 2.4 Element
  
db.coll.find({name: {$exists: true}})
  
db.coll.find({"zipCode": {$type: 2 }})
  
db.coll.find({"zipCode": {$type: "string"}})

##### 2.5 Aggregation Pipeline
  
db.coll.aggregate([
  {$match: {status: "A"}},
  {$group: {_id: "$cust_id", total: {$sum: "$amount"}}},
  {$sort: {total: -1}}
])

##### 2.6 Text search with a "text" index
  
db.coll.find({$text: {$search: "cake"}}, {score: {$meta: "textScore"}}).sort({score: {$meta: "textScore"}})

##### 2.7 Regex
  
db.coll.find({name: /^Max/})   // regex: starts by letter "M"
  
db.coll.find({name: /^Max$/i}) // regex case insensitive

##### 2.8 Array
  
db.coll.find({tags: {$all: ["Realm", "Charts"]}})
  
db.coll.find({field: {$size: 2}})        // impossible to index - prefer storing the size of the array & update it
  
db.coll.find({results: {$elemMatch: {product: "xyz", score: {$gte: 8}}}})

##### 2.9 Projections
db.coll.find({"x": 1}, {"actors": 1})                   // actors + _id
  
db.coll.find({"x": 1}, {"actors": 1, "_id": 0})        // actors
  
db.coll.find({"x": 1}, {"actors": 0, "summary": 0})   // all but "actors" and "summary"

##### 2.10 Sort, skip, limit
  
db.coll.find({}).sort({"year": 1, "rating": -1}).skip(10).limit(3)

##### 2.11 Read Concern
  
db.coll.find().readConcern("majority")

#### 3.Update

db.coll.update({"_id": 1}, {"year": 2016})                  // Replaces the entire document
  
db.coll.update({"_id": 1}, {$set: {"year": 2016, name: "Max"}})
  
db.coll.update({"_id": 1}, {$unset: {"year": 1}})
  
db.coll.update({"_id": 1}, {$rename: {"year": "date"} })
  
db.coll.update({"_id": 1}, {$inc: {"year": 5}})
  
db.coll.update({"_id": 1}, {$mul: {price: NumberDecimal("1.25"), qty: 2}})
  
db.coll.update({"_id": 1}, {$min: {"imdb": 5}})
  
db.coll.update({"_id": 1}, {$max: {"imdb": 8}})
  
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": true}})
  
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": {$type: "timestamp"}}})

##### 3.1.Array
  
db.coll.update({"_id": 1}, {$push :{"array": 1}})
  
db.coll.update({"_id": 1}, {$pull :{"array": 1}})
  
db.coll.update({"_id": 1}, {$addToSet :{"array": 2}})
  
db.coll.update({"_id": 1}, {$pop: {"array": 1}})  // last element
  
db.coll.update({"_id": 1}, {$pop: {"array": -1}}) // first element
  
db.coll.update({"_id": 1}, {$pullAll: {"array" :[3, 4, 5]}})
  
db.coll.update({"_id": 1}, {$push: {scores: {$each: [90, 92, 85]}}})
  
db.coll.updateOne({"_id": 1, "grades": 80}, {$set: {"grades.$": 82}})
  
db.coll.updateMany({}, {$inc: {"grades.$[]": 10}})
  
db.coll.update({}, {$set: {"grades.$[element]": 100}}, {multi: true, arrayFilters: [{"element": {$gte: 100}}]})

##### 3.2.Update many
  
db.coll.update({"year": 1999}, {$set: {"decade": "90's"}}, {"multi":true})
  
db.coll.updateMany({"year": 1999}, {$set: {"decade": "90's"}})

##### 3.3 FindOneAndUpdate
  
db.coll.findOneAndUpdate({"name": "Max"}, {$inc: {"points": 5}}, {returnNewDocument: true})

##### 3.4 Upsert
  
db.coll.update({"_id": 1}, {$set: {item: "apple"}, $setOnInsert: {defaultQty: 100}}, {upsert: true})

##### 3.5.Replace
  
db.coll.replaceOne({"name": "Max"}, {"firstname": "Maxime", "surname": "Beugnet"})

##### 3.6.Save
  
db.coll.save({"item": "book", "qty": 40})

##### 3.7.Write concern
  
db.coll.update({}, {$set: {"x": 1}}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})

#### 4.Delete
  
db.coll.remove({name: "Max"})
  
db.coll.remove({name: "Max"}, {justOne: true})
  
db.coll.remove({})              // Deletes all the docs but not the collection itself and its index definitions
  
db.coll.remove({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
  
db.coll.findOneAndDelete({"name": "Max"})
  
db.deletes.find_one({'_id': 99})
  
db.deletes.delete_one({'_id': 99})
  
db.deletes.delete_many({'random_bool': False})

### Databases and Collections

#### 1. Drop
  
db.coll.drop()          // removes the collection and its index definitions
  
db.dropDatabase()       // double check that you are *NOT* on the PROD cluster... :-)

#### 2. Create Collection
  
Create collection with a $jsonschema:

db.createCollection("contacts", {
   validator: {$jsonSchema: {
      bsonType: "object",
      required: ["phone"],
      properties: {
         phone: {
            bsonType: "string",
            description: "must be a string and is required"
         },
         email: {
            bsonType: "string",
            pattern: "@mongodb\.com$",
            description: "must be a string and match the regular expression pattern"
         },
         status: {
            enum: [ "Unknown", "Incomplete" ],
            description: "can only be one of the enum values"
         }
      }
   }}
})

### Indexes

#### 1.List Indexes
  
db.coll.getIndexes()
  
db.coll.getIndexKeys()

#### 2.Create Indexes

##### 2.1 Index Types
  
db.coll.createIndex({"name": 1})                // single field index
  
db.coll.createIndex({"name": 1, "date": 1})     // compound index
  
db.coll.createIndex({foo: "text", bar: "text"}) // text index
  
db.coll.createIndex({"$**": "text"})            // wildcard text index
  
db.coll.createIndex({"userMetadata.$**": 1})    // wildcard index
  
db.coll.createIndex({"loc": "2d"})              // 2d index
  
db.coll.createIndex({"loc": "2dsphere"})        // 2dsphere index
  
db.coll.createIndex({"_id": "hashed"})          // hashed index

##### 2.2 Index Options
  
db.coll.createIndex({"lastModifiedDate": 1}, {expireAfterSeconds: 3600})      // TTL index
  
db.coll.createIndex({"name": 1}, {unique: true})
  
db.coll.createIndex({"name": 1}, {partialFilterExpression: {age: {$gt: 18}}}) // partial index
  
db.coll.createIndex({"name": 1 }, {sparse: true})

##### 2.3 Drop Indexes
  
db.coll.dropIndex("name_1")

##### 2.4 Hide/Unhide Indexes
  
db.coll.hideIndex("name_1")
  
db.coll.unhideIndex("name_1")

