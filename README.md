# Dev Helper DB

This is a mongodb store to work with the dev-helper application

## Setup
1.- Add the following environment variables to your machine.
```
# Initial setup and root credentials
MONGO_DEV_HELPER_DB=dev-helper-db # we'll be using this name
MONGO_DEV_HELPER_ROOT_USER
MONGO_DEV_HELPER_ROOT_PASSWORD

# Database user
MONGO_DEV_HELPER_USERNAME
MONGO_DEV_HELPER_PASSWORD
```

You can use the following syntax to set them:
```
# Linux or Mac OS
export MONGO_DEV_HELPER_USERNAME=some_username
```
For Windows, follow these [instructions](https://docs.oracle.com/en/database/oracle/machine-learning/oml4r/1.5.1/oread/creating-and-modifying-environment-variables-on-windows.html#GUID-DD6F9982-60D5-48F6-8270-A27EC53807D0)

Use this syntax to verify they have been set to the correct values.
```
# Linux or Mac OS
echo $MONGO_DEV_HELPER_USERNAME
```

1.- Pull an official mongo image from [Docker Hub](https://hub.docker.com/_/mongo?tab=tags) by running:
```
docker pull mongo:148e744ca319
```

## Running Mongo
Run the container with docker compose using the following command
```
docker-compose up

# Or with the -d flag to run in the background
docker-compose up -d
```

## Shell into mongodb, authenticate and access your database
Once your db instance is running, you can open another terminal and access it. To do this, run the following in another terminal.
```
# verify container is running and with the expected name
docker ps

# open shell
docker exec -it dev-helper-db bash

# authenticate with mongodb using the db root user, root pass and admin as the db
mongo -u my-secret-root-user -p my-secret-root-pass --authenticationDatabase admin

# switch to the dev-helper db
use dev-helper

# *you can use common operations below
```

## Connect with your API or DB Management Tool
Now you can use the following connection string to access your database with an API or with a tool like Compass.

```
mongodb://YourUsername:YourPasswordHere@127.0.0.1:27017/dev-helper
```
*Note, in an API, you would also pass the username and password as env variables.


## Perform common operations
[CREATE](https://docs.mongodb.com/manual/reference/method/db.createCollection/)
```
# create a collection (Collection: Analogous to a table in a RDBMS)
db.createCollection('notes')

# insert a document - CREATE
db.notes.insertOne({
 name: 'monday_note',
 content: '# This is some of the markdown we needed\n\n -Some list goes here'
})
```

[READ](https://docs.mongodb.com/manual/reference/method/db.collection.find/#mongodb-method-db.collection.find) /
[Queries](https://docs.mongodb.com/manual/tutorial/query-documents/)
```
# retrieve all documents in collection - READ
db.notes.find()

# retrieve a document by ID - READ
db.notes.find({"_id" : ObjectId("61acf5eb641c51a8cdb65d63")})

# simple query
db.notes.find({ name: "monday_note" })

# query to find either or in key
db.notes.find({ name: { $in: ["monday_note", "tuesday_note"] }})

# Further reading in Queries link above
```


[UPDATE](https://docs.mongodb.com/manual/tutorial/update-documents/)

[DELETE](https://docs.mongodb.com/manual/tutorial/remove-documents/)

# dev-helper-db
