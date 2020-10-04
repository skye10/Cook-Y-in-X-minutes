### Start and stop mongodb on OSX

#### Problem

* You want to start MongoDB on OSX
* You want to stop MongoDB on OSX

#### Assumptions
* You are using the community version of MongoDB

#### References
* Visit the [guide](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/) by MongoDB.


***

#### Recipes

##### Option 1 (Using `brew` is easiest)

Start MongoDB:
```bash
$ brew services start mongodb-community@4.4
```

Stop MongoDB:
```bash
$ brew services stop mongodb-community@4.4
```



##### Verify if mongo service is still running

Search for "mongod" in your running processes:

```bash
$ ps aux | grep -v grep | grep mongod
```



##### Option 2 (Manually)

Start MongoDB:

```bash
$ mongod --config /usr/local/etc/mongod.conf --fork
```

Stop MongoDB:

* To stop a mongod running as a background process, connect to the mongod from the mongo shell, and issue the shutdown command.

