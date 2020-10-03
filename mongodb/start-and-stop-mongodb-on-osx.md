### Problem
* You want to start MongoDB on OSX
* You want to stop MongoDB on OSX

### Assumptions
* You are using the community version of MongoDB

### References
* Visit the [guide](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/) by MongoDB.


***

### Recipes

#### Option 1 (Use `brew`)

Start MongoDB:
```
$ brew services start mongodb-community@4.4
```

Stop MongoDB:
```
$ brew services stop mongodb-community@4.4
```

#### Option 2 (run MongoDB manually as a background process)

Start MongoDB:
```
$ mongod --config /usr/local/etc/mongod.conf --fork
```

Stop MongoDB:
* To stop a mongod running as a background process, connect to the mongod from the mongo shell, and issue the shutdown command.


