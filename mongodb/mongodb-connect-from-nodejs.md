### Connect Node.js to MongoDB using the native driver

#### Problem

You want to connect Node.js to MongoDB using the official driver.

#### Assumptions
* You have [Node.js](https://nodejs.org/en/) and [MongoDB](https://www.mongodb.com/try/download/community) installed on your system
* Assumes version 3.6 of the MongoDB Node.js driver

#### References
* Visit the excellent [guide](https://mongodb.github.io/node-mongodb-native/) by MongoDB itself


***


#### Recipes

[Start MongoDB](https://github.com/skye10/Cook-Y-in-X-minutes/wiki/Start-and-stop-MongoDB-on-OSX) on your machine. We will assume it is serving on `localhost:27017`, the default port. Create a file called `app.js` with the following code:

```javascript
// File app.js

const MongoClient = require('mongodb').MongoClient; // 1
const url = 'mongodb://localhost:27017'; // 2
const mydb = 'testdb'; // 3
const client = new MongoClient(url, { useUnifiedTopology: true }); // 4

client.connect(function(err) {  // 5 
		if (err) throw err;
    console.log("Connected successfully to MongoDB server");
    client.close();
    console.log("Closed connection to MongoDB");
});
```


##### Notes
1. The MongoDB client
2. The default port on which MongoDB is running
3. Your test database (actually created only after you add some data to it)
4. The client constructor itself, which will be used to connect to MongoDB. If you don't pass the option `{ useUnifiedTopology: true }`, you will get a deprecation warning.
5. The connect object `client.connect(function(err) { … })` makes the connection; if it errors out 
