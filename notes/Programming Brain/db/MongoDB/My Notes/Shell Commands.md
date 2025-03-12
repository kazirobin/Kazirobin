# Shell Commands

The mongo shell is an interactive JavaScript interface to MongoDB. You can use the mongo shell to query and update data as well as perform administrative operations.

---

Run the MongoDB Shell.

```bash
mongosh
```

Shows help-related information on the MongoDB shell.

```bash
help
```

Lists all the databases available for use on the connected MongoDB instance.

```bash
show dbs
#or
show databases
```

Lists all the collections available for use on the current database.

```bash
show collections
```

Lists all the users available on the current database.

```bash
show users
```

Lists all the roles (both built-in roles and user-defined roles) on the current database.

```bash
show roles
```

Lists the last 5 recent operations that took 1 millisecond or more.

```bash
show profile
```

Executes a specified JavaScript file.

```bash
load()
```

Create a new database or switch to an existing one on MongoDB Shell.

```bash
use <name of database>
```

Create a collection on the MongoDB Shell.

```bash
db.createCollection("user")
```

Show all of the collections on MongoDB Shell.

```bash
show collections
```

Check active collection or database on the MongoDB Shell.

```bash
db
```

Insert a document into a collection on MongoDB Shell.

```bash
db.<name of collection>.insert({}) #For single document
#or
db.<name of collection>.insertMany([{}]) #For multiple documents
#or
db.<name of collection>.insertOne({}) #For single document

```

Updates one single document in the collection on MongoDB Shell.

```bash
db.<name of collection>.updateOne({},{$set: {}})
#or
db.<name of collection>.update({},{$set: {}})
```

Updates multiple documents in the collection on MongoDB Shell.

```bash
db.<name of collection>.updateMany()
```

Delete one single document in the collection on MongoDB Shell.

```bash
db.<name of collection>.deleteOne({})
```

Show all documents in a collection from the database.

```bash
db.<collection Name>.find().pretty()
```

Drops the current database on MongoDB Shell.

```bash
db.dropDatabase("database name")
```

To authenticate in MongoDB using the terminal follow these steps, switch to the `admin` database

```bash
use admin
```

Now, authenticate using your credentials, If authentication is successful, it will return `1`.

```bash
db.auth("myUser", "myPassword")
```

If you don't have an admin user yet, create one with full access:

```bash
use admin

db.createUser({
  user: "adminUser",
  pwd: "securePassword",
  roles: [{ role: "root", db: "admin" }]
});
```