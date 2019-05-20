## Lecture ✍️

### What is Mongo DB
Mongo DB is what we will use for persistence in our MERN full-stack development exercise. Mongo is the 'M' of 'MERN'. Persistence is storing the data in some manner, so that the data is accessible even if the application is shutdown and restarted or across multiple instances of applications. You may recollect from the previous API exercises that the Pokemons we created through POST request don't exist when we restarted the web server. This is because, they were not persisted or stored. The storage of data electronically is called *Database*. Mongo will now serve as our data or persistence layer. Mongo DB is a document database or NoSQL database. Rather than storing the data across tables in a relational database, all the data will be stored in documents which are just text files with data represented as JSON.

#### Prerequisites
* Install (Mongo DB)[https://docs.mongodb.com/manual/administration/install-community/]
* You should be comfortable with CLI and JSON.

### Accessing Mongo DB
We will now create an instance of Mongo DB in our system and access it through a CLI. To access Mongo DB, we will need to run two terminals; one will run the Mongo DB server and the other for us to run the Mongo CLI.
The Mongo CLI is the client which will send requests to Mongo DB server, which will respond with a JSON file. It is very similar to the client-server architecture we saw in the case of Web server and Web API. 

## A comparison of Relational DBMS and Mongo DB
<table>
    <tr>
        <th>Relational Database</th>
        <th>Mongo DB</th>
    </tr>
    <tr>
        <td>Database</td>
        <td>Database</td>
    </tr>
        <td>Tables</td>
        <td>Collection</td>
    <tr>
        <td>Rows/Records</td>
        <td>Documents</td>
    </tr>
    <tr>
        <td>Columns</td>
        <td>Fields</td>
    </tr>
</table>

As mentioned in the table above, a record in a relational Database, is represented as a document in Mongo DB. Documents in MongoDB are BSON, which is a binary data format that is like JSON, but includes additional type data.

We will start Mongo DB as a service from one terminal and connect to the DB from another terminal. The instructions here are for Mac OS. If you are using windows or other OS, please visit the Mondo DB site given above and follow the instructions specific to your OS.

### Run Mongo DB
From a terminal issue the following command to start the Mongo DB service

```
brew services start mongodb-community@4.0
```

### Connect and use Mongo DB
To connect to the Mongo DB, as mentioned we will open a new shell and issue the following command. 

```
mongo
```

You will now see the prompt, where we can start issuing commands. We will issue the following command to list all the default databases that are present.

```
show dbs
```

This should list 3 databases namely *admin, config and local*.
We will now create a new database for keeping all the pokemon data. Let's name it *pokedex*.

```
use pokedex
```

This will create a DB name Pokedex, if it doesn't exist and switch to that DB. But the DB will not be listed in the *show dbs* until the database has some data because, as mentioned before, in Mongo the database is in the form of a file. The file is not created until the collections are created. 

Let us create a collection called **pokemon** in our database. The current database is referred to as **db**. Since *use pokedex* switched to the pokedex database, **db** will now refer to **pokedex** in our CLI's context.

```
db.createCollection('pokemon')
```

Now that we have created our collection, the *show dbs* should list our database. Check to see if that's the case. To see all the collections in your database we can use the following command.

```
show collections
```

This should list *pokemon* the collection we created in our database earlier. Once you see it, you are all set to explore CRUD with Mongo DB.


## CRUD Operations

### Create
To add data to our collection, we use the insert command. We start inserting the data using the following command. 

```
db.pokemon.insert({
```

You will see that pressing *enter* after issuing the command takes you to the next line preceded with **...** . This means that the CLI is waiting for data to be entered. Like in Javascript, the end of a command is assumed when there are closing brackets matching the opening ones. Let type the data we want to insert and finish it with the appropriate brackets.

```
    id:1,
    name:'bulbsaur',
    height:'6 cm'
})
```

You should get *WriteResult({ "nInserted" : 1 })*, which indicates that the data was successfully inserted. 0 would indicate failure in inserting the data. 

### Retrieve
Let's now retrieve all the data in the pokemon collection. 

```
db.pokemon.find()
```

In this case, we inserted just one pokemon data. What if we want to enter more than one. We can either run the above command multiple times or pass the data as an array. 

```
db.pokemon.insert([{id:2,name:'ivusaur',height:'99.1 cm'},{id:3,name:'venusaur',height:'2.01 m'}])
```

The array is indicated in the above command with square brackets; each unit of data is within curly brackets, {*data here*} and comma separated from each other. The output will indicate that there was a bulk insert attempted and will also tell the user how many units of data were added.

Now when you do a *db.pokemon.find()* you should see all the three pokemons listed.


#### Task 
Insert 5 more pokemons with their respective ids using single insert or bulk insert and retrieve them all with the find command.

In all of the above cases, we have retrieved all the data in the pokemon collection. We will now look at how to retrieve just one record or document from the collection based on conditions. Let's retrieve the pokemon whose id is 3.

```
db.pokemon.find({id:3})
```

We can retrieve the data based on any of the fields in the document. 

```
db.pokemon.find({name:'ivysaur'})
db.pokemon.find({height:'2.01 m'})
```

We can also retrieve multiple documents based on a condition. Let's retrieve all the documents where the name of the pokemon contains "saur" (which is all the pokemons. Try any string you want :smile:)

```
db.pokemon.find({name: /saur/})
```
Or if you want to retrieve the first one which matches the condition amongst many such documents which match, we use *findOne*.

```
db.pokemon.findOne({name: /saur/})
```

We can also use $eq,$gt,$lt to search numeric values based on conditions. 

### Tasks

Can you find out what each of these commands do? What will they return?

```
db.pokemon.find( { id: { $eq: 5 } } )

db.pokemon.find( { id: { $lt: 4 } } )

db.pokemon.find( { id: { $gt: 2 } } )

```
### Update
Now that we are familiar with C and R of the **CRUD**, let's look at U. To update a document, we need to finrst identify a document based on a condition and then update the document. So update in Mongo DB takes two parameters; first one to identify the document to be updated and the second one which has the changes. 
Let's change the document which has id as 1 to have a different name. 

```
db.pokemon.update({id:1},{$set:{name:'diffsaur'}})
```

This command identifies the document with id 1 and changes the name to diffsaur. Let's do a *db.pokemon.find()* to see the records in the collection to ensure our changes have happened. Update will by default only update the first document that is matched. If you want to update multiple documents at once, we have to specify the third and fourth boolean parameters which are for 
* **upsert** - This is a combination of update and insert (true/false - if this should be an “upsert” operation; that is, if the record(s) do not exist, insert one. Upsert by default is true and only inserts a single document) and 
* **multiple** (true/false - indicates if all documents matching criteria should be updated rather than just one.)


Now what if we decide to have an additional field for imageURL for all the pokemon? We can add a column to the existing documents with the following command.

```
db.pokemon.update({},{$set:{"imageUrl":''}},false,true)
```
Here the '{}' implies there is not conditions or restrictions and all the documents need to be updated. 

### Delete

Now that we know how to retrieve all documents and also selective documents based on a criteria, deleted the documents is very simple. The parameters for deletion are the same as find.

```
db.pokemon.remove({name: /diff/})
```

This will retrieve all records where the name contains the word 'diff' and delete them. Remove has to be handled diligently. *db.pokemon.remove({})* will remove all the records in the collection and  *db.pokemon.remove()* without any parameters will delete the entire collection. 


