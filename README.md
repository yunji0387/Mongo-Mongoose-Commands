# Mongo/Mongoose Commands
A list of basic Mongo commands and [Mongoose commands](#mongoose-commands) 
## Mongo Bash Commands
### Connect to local server (In bash)
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

1. activate local server port
  - ```bash
    mongod
    ```
  - activate success when we see "Waiting for connection" and port number
    ![Image](Images/mongodConnection.png)
2. connect with mongo shell
  - ```bash
    mongosh
    ```

<!-- /MarkdownTOC -->
</details>

### If you forgot to quit the Mongod Server and close to terminal
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

1. Open a new terminal
2. ```bash
    sudo pkill -f mongod
    ```
3. Enter you password 

<!-- /MarkdownTOC -->
</details>

### Show all database
<details close>
<summary><b>(click to expand/hide)</b></summary>
<!-- MarkdownTOC -->

- ```bash
  show dbs
  ```

<!-- /MarkdownTOC -->
</details>

## Create Operation

### Create a new database
- ```bash
  use <database name>
  ```

### Insert a data to database
- ```bash
  db.<database name>.insertOne(
    {
      name: "tim",
      age: 26
    }
  )
  ```   
- if database does not exist, it will create one.

### Insert a data with many subData (one to many relationship)
- ```bash
  db.<database name>.insertOne(
    {
      name: "tim",
      age: 26,
      achievement:[
        {
          title: "cap",
          year: 2021
        },
        {
          title: "gold",
          year: 2023
        }
      ]
    }
  )
  ```   

## Read Operation
### Find specific data
- ```bash
  db.<database name>.find(
    {
      name: "tim",
      age: 26
    }
  )
  ```  
### Find data in specific bound
- find data in database that has age > 10
- ```bash
  db.<database name>.find(
    {
      age: {$gt: 10}
    }
  )
  ```
### Find data with specific return
- find data in database that has age > 10 and return with name and id
- 0 = do not show, 1 = show
- ```bash
  db.<database name>.find(
    {
      age: {$gt: 10}
    },
    {
      _id: 0,
      name: 1
    }
  )
  ```
 
 ## Update Operation
 ### update a specific data
 - ```bash
    db.<database name>.updateOne(
      {
        _id: 1
      },
      {
        $set: {title: 15}
      }
    )
   ```
   
## Delete Operation
### delete a database
1. switch to the database
- ```bash
    use <database name>
   ```
2. delete the database
- ```bash
    db.dropDatabase()
   ```
### delete a specific data
 - ```bash
    db.<database name>.deleteOne(
      {
        _id: 1
      }
    )
   ```
- delete successful if return acknowledged: true, and deletedCount: 1

## [Mongoose commands](https://mongoosejs.com/docs/index.html)
### include npm libraries in bash in your project directory
 - ```bash
    npm i mongoose
   ```
### Connect to mongoDB database in nodejs
1. require package  
   - ```javascript
      const mongoose = require("mongoose"); 
     ```
2. connect to mongoDB database
   - connect to database with local host
    - ```javascript
        mongoose.connect("mongodb://localhost:27017/<database name>", { useNewUrlParser: true });
      ```
### Disconnect to mongoDB database in nodejs
- ```javascript
    mongoose.connection.close();
  ```
### [Data validation](https://mongoosejs.com/docs/validation.html)
- ```javascript
    const <schema name> = new mongoose.Schema({
          name: {
            type: String,
            required: [true, "Please check your data entry, no name specified!"]
          },
          rating: {
            type: Number,
            min: 1,
            max: 10
          },
          review: String
        });
  ```
### Establishing Relationships and Embedding Documents
- ```javascript
    const schema1 = new mongoose.Schema({
          name: {
            type: String,
            required: [true, "Please check your data entry, no name specified!"]
          },
          rating: {
            type: Number,
            min: 1,
            max: 10
          },
          review: String
        });
        
   const schema2 = new mongoose.Schema({
        name: String,
        age: Number,
        FavouriteBook: schema1
   }); 
  ```
## Create Operation
### create New Schema and Model(collection)
  1.  ```javascript
        const <schema name> = new mongoose.Schema({
          name: String,
          rating: Number,
          review: String
        });
      ```
  2.  ```javascript
        const <Model name> = mongoose.model("<Database name> without s", <schema name>);
      ``` 
   - model name's first letter usually written in Capital letter
### insert new object(document) to databse
- ```javascript
    const obj = new <Model name>({
      <key>: <value>,
      <key>: <value>,
      <key>: <value>
    });
    
    const obj.save();
  ```
### insert many objects(documents) to database
- ```javascript
    const obj1 = new <Model name>({
      <key>: <value>,
      <key>: <value>,
      <key>: <value>
    });
    
    <Model name>.insertMany([obj1, obj2, obj3])
       .then(function(){
           console.log("Successfully add item list to database.");
       })
       .catch(function(err){
           console.log(err);
       });
    
    // Alternate version
    /*
    <Model name>.insertMany([obj1, obj2, obj3])
       .then(() => {
           console.log("Successfully add item list to database.");
       })
       .catch((err) => {
           console.log(err);
       });
    */
  ```
## Read operation
### read all objects(documents) in database
- ```javascript
    <Model name>.find({})
       .then(function(<result name>){
           console.log("Successfully add item list to database.");
       })
       .catch(function(err){
           console.log(err);
       });
  ```
## Update operation
### update an object(document) in database
- ```javascript
    <Model name>.updateOne({_id: "123123"} , {name: "newName"}, function(err){
      if(err){
        console.log(err);
      }else{
        console.log("Successfully updated the document.");
      });
  ```
## Delete operation
### delete an object(document) in database
- ```javascript
    <Model name>.deleteOne({_id: "123123"})
      .then(function(){
            console.log("Successfully deleted item");
        })
        .catch(function(err){
            console.log(err);
        });
  ```
### delete multiple objects(documents) in database
- ```javascript
    <Model name>.deleteMany({name: "John"})
      .then(function(){
            console.log("Successfully deleted items");
        })
        .catch(function(err){
            console.log(err);
        });
  ```
