# Mongo Commands
A list of basic Mongo commands and [Mongoose commands](#mongoose-commands) 
## Mongo Bash Commands
### Connect to local server (In bash)
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
### If you forgot to quit the Mongod Server and close to terminal
1. Open a new terminal
2. ```bash
    sudo pkill -f mongod
    ```
3. Enter you password 

### Show all database
- ```bash
  show dbs
  ```

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

## Mongoose commands
### include npm libraries in bash in your project directory
 - ```bash
    npm i mongoose
   ```
### 
