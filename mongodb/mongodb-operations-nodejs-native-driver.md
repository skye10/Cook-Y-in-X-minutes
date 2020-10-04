### MongoDB insert, delete, modify operations using the Node.js native driver

#### Problem

You want to add, delete, modify records in MongoDB from Node.js using the native driver.

#### Assumptions
* You have [Node.js](https://nodejs.org/en/) and [MongoDB](https://www.mongodb.com/try/download/community) installed on your system
* Assumes version 3.6 of the MongoDB Node.js driver
* [Start MongoDB](https://github.com/skye10/Cook-Y-in-X-minutes/wiki/Start-and-stop-MongoDB-on-OSX) on your machine. We will assume it is serving on `localhost:27017`, the default port. 

#### References
* Visit the excellent [guide](https://mongodb.github.io/node-mongodb-native/) by MongoDB itself


***

#### Recipes

##### Sample data

Here's some data (on movies) that we will play with. 

```javascript
let records = [
    {"name": "Episode IV-A New Hope", "release": "May 25, 1977", "director": "George Lucas"},
    {"name": "Episode V-The Empire Strikes Back", "release": "May 21, 1980", "director": "Irvin Kershner"},
    {"name": "Episode VI-A New Hope", "release": "May 25, 1983", "director": "Richard Marquand"}
];
```



##### Insert many records

Create a file called `app.js` with the following code:

```javascript
// File app.js

const MongoClient = require('mongodb').MongoClient;
const url = 'mongodb://localhost:27017';
const testdb = 'testdb';
const client = new MongoClient(url, { useUnifiedTopology: true });

let records = [] // See above
 
client.connect(function(err) {
		if (err) throw err;
    const db = client.db(testdb); // 1
    const movieColl = db.collection('movies'); // 2
    movieColl.insertMany(records); // 3
    // client.close(); // 4 
    // console.log("Closed connection to MongoDB");
});
```
Run it as follows:
```bash
$ node app.js
```
This results in the records being inserted into the database — but the client connection will still remain open! We will fix this in the next section using callbacks.

> ###### Notes
>
> 1. Handler for the database `'testdb` 
> 2. Movie collection called `movies` on `testdb`
> 3. Command `insertMany()` used to insert and array of records `[{}, {}, …]` into the `movies` collection
> 4. Note that if we try to close the client here, it will error out with `MongoError: Cannot use a session that has ended`.  To close the connection gracefully, we need to use callbacks. 
>



##### Insert many records, and gracefully close connection

The strategy is to define a function to insert records, which provides a callback. The called-back function closes the connection once record insertion is complete. The full `app.js` looks like this now:

```javascript
const MongoClient = require('mongodb').MongoClient;
const url = 'mongodb://localhost:27017';
const mydb = 'testdb';
const client = new MongoClient(url, { useUnifiedTopology: true });

let records = [
    {"name": "Episode IV-A New Hope", "release": "May 25, 1977", "director": "George Lucas"},
    {"name": "Episode V-The Empire Strikes Back", "release": "May 21, 1980", "director": "Irvin Kershner"},
    {"name": "Episode VI-A New Hope", "release": "May 25, 1983", "director": "Richard Marquand"}
];

const insertRecords = function(db, callback) { // 2
    const movieColl = db.collection('movies');
    movieColl.insertMany(records, function(err, result) {
        console.log("Inserted many records into movieColl");
        callback(result);
    });
};

client.connect(function(err) {
    if (err) throw err;
    const db = client.db(mydb);
    insertRecords(db, function() { // 1
        client.close();
        console.log("Closed connection to MongoDB");
    })
});
```

Run it as follows (the results are below):

```bash
$ node app.js
Inserted many records into movieColl
Closed connection to MongoDB
```

> ###### Notes
>
> 1. insertRecords() is defined as a anonymous function what inserts records and takes as input a callback function
> 2. Callback function passed to insertRecords()



