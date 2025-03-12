# CURD Operations

MongoDB is a persistent document-oriented database used to store and process data in the form of documents. As with other database management systems, MongoDB allows you to manage and interact with data through four fundamental types of data operations:

- **`C`**reate operations, which involve writing data to the database
- **`R`**ead operations, which query a database to retrieve data from it
- **`U`**pdate operations, which change data that already exists in a database
- **`D`**elete operations, which permanently remove data from a database

These four operations are jointly referred to as *CRUD* operations.

## Connecting To The MongoDB Server

This guide involves using the MongoDB shell to interact with MongoDB. In order to follow along and practice CRUD operations in MongoDB, you must first connect to a MongoDB database by opening up the MongoDB shell.

If your machine already install the MongoDB shell, Just run this command:

```bash
mongosh
```

Now that you have connected to the MongoDB server using a MongoDB shell, you can move on to creating new documents.

## Creating Documents

In order to have data that you can practice reading, updating, and deleting in the later steps of this guide, this step focuses on how to create data documents in MongoDB.

```bash
use monuments
```

Imagine that you’re using MongoDB to build and manage a directory of famous historical monuments from around the world. This directory will store information like each monument’s name, country, city, and geographical location.

The documents in this directory will follow a format similar to this example, which represents **The Pyramids of Giza**:

```json
{
    "name": "The Pyramids of Giza",
    "city": "Giza",
    "country": "Egypt",
    "gps": {
        "lat": 29.976480,
        "lng": 31.131302
    }
}
```

This document, like all MongoDB documents, is written in BSON. BSON is a binary form of JSON, a human-readable data format. All data in BSON or JSON documents are represented as field-and-value pairs that take the form of `field: value`.

This document consists of four fields. First is the name of the monument, followed by the city and the country. All three of these fields contain strings. The last field, called `gps`, is a nested document which details the monument’s GPS location. This location is made up of a pair of latitude and longitude coordinates, represented by the `lat` and `lng` fields respectively, each of which hold floating point values.

Insert this document into a new collection called `monuments` using the `insertOne` method. As its name implies, `insertOne` is used to create individual documents, as opposed to creating multiple documents at once.

In the MongoDB shell, run the following operation:

```bash
db.monuments.insertOne(
  {
    "name": "The Pyramids of Giza",
    "city": "Giza",
    "country": "Egypt",
    "gps": {
      "lat": 29.976480,
      "lng": 31.131302
    }
  }
)
```

Notice that you haven’t explicitly created the `monuments` collection before executing this `insertOne` method. MongoDB allows you to run commands on non-existent collections freely, and the missing collections only get created when the first object is inserted. By executing this example `insertOne()` method, not only will it insert the document into the collection but it will also create the collection automatically.

MongoDB will execute the `insertOne` method and insert the requested document representing the Pyramids of Giza. The operation’s output will inform you that it executed successfully, and also provides the `ObjectId` which it generated automatically for the new document:

**Output:**

```json
{
  "acknowledged" : true,
  "insertedId" : ObjectId("6105752352e6d1ebb7072647")
}
```

In MongoDB, each document within a collection must have a unique `_id` field which acts as a primary key. You can include the `_id` field and provide it with a value of your own choosing, as long as you ensure each document’s `_id` field will be unique. However, if a new document omits the `_id` field, MongoDB will automatically generate an object identifier (in the form of an `ObjectId` object) as the value for the `_id` field.

You can verify that the document was inserted by checking the object count in the `monuments` collection:

```bash
db.monuments.count()
```

**Output:**

```bash
1
```

Inserting documents one by one like this would quickly become tedious if you wanted to create multiple documents. MongoDB provides the `insertMany` method which you can use to insert multiple documents in a single operation.

Run the following example command, which uses the `insertMany` method to insert six additional famous monuments into the `monuments` collection:

```bash
db.monuments.insertMany([
  {"name": "The Valley of the Kings", "city": "Luxor", "country": "Egypt", "gps": { "lat": 25.746424, "lng": 32.605309 }},
  {"name": "Arc de Triomphe", "city": "Paris", "country": "France", "gps": { "lat": 48.873756, "lng": 2.294946 }},
  {"name": "The Eiffel Tower", "city": "Paris", "country": "France", "gps": { "lat": 48.858093, "lng": 2.294694 }},
  {"name": "Acropolis", "city": "Athens", "country": "Greece", "gps": { "lat": 37.970833, "lng": 23.726110 }},
  {"name": "The Great Wall of China", "city": "Huairou", "country": "China", "gps": { "lat": 40.431908, "lng": 116.570374 }},
  {"name": "The Statue of Liberty", "city": "New York", "country": "USA", "gps": { "lat": 40.689247, "lng": -74.044502 }}
])
```

Notice the square brackets (`[` and `]`) surrounding the six documents. These brackets signify an *array* of documents. Within square brackets, multiple objects can appear one after another, delimited by commas. In cases where the MongoDB method requires more than one object, you can provide a list of objects in the form of an array like this one.

MongoDB will respond with several object identifiers, one for each of the newly inserted objects:

```bash
{
  "acknowledged" : true,
  "insertedIds" : [
    ObjectId("6105770952e6d1ebb7072648"),
    ObjectId("6105770952e6d1ebb7072649"),
    ObjectId("6105770952e6d1ebb707264a"),
    ObjectId("6105770952e6d1ebb707264b"),
    ObjectId("6105770952e6d1ebb707264c"),
    ObjectId("6105770952e6d1ebb707264d")
  ]
}
```

You can verify that the documents were inserted by checking the object count in the `monuments` collection:

```bash
db.monuments.count()
```

After adding these six new documents, the expected output of this command is `7`:

**Output:**

```bash
7
```

## Reading Documents

Now that your collection has some documents stored within it, you can query your database to retrieve these documents and read their data. This step first outlines how to query all of the documents in a given collection, and then describes how to use filters to narrow down the list of retrieved documents.

After completing the previous step, you now have seven documents describing famous monuments inserted into the `monuments` collection. You can retrieve all seven documents with a single operation using the `find()` method:

```bash
db.monuments.find()
```

This method, when used without any arguments, doesn’t apply any filtering and asks MongoDB to return all objects available in the specified collection, `monuments`. MongoDB will return the following output:

```bash
{ "_id" : ObjectId("6105752352e6d1ebb7072647"), "name" : "The Pyramids of Giza", "city" : "Giza", "country" : "Egypt", "gps" : { "lat" : 29.97648, "lng" : 31.131302 } }
{ "_id" : ObjectId("6105770952e6d1ebb7072648"), "name" : "The Valley of the Kings", "city" : "Luxor", "country" : "Egypt", "gps" : { "lat" : 25.746424, "lng" : 32.605309 } }
{ "_id" : ObjectId("6105770952e6d1ebb7072649"), "name" : "Arc de Triomphe", "city" : "Paris", "country" : "France", "gps" : { "lat" : 48.873756, "lng" : 2.294946 } }
{ "_id" : ObjectId("6105770952e6d1ebb707264a"), "name" : "The Eiffel Tower", "city" : "Paris", "country" : "France", "gps" : { "lat" : 48.858093, "lng" : 2.294694 } }
{ "_id" : ObjectId("6105770952e6d1ebb707264b"), "name" : "Acropolis", "city" : "Athens", "country" : "Greece", "gps" : { "lat" : 37.970833, "lng" : 23.72611 } }
{ "_id" : ObjectId("6105770952e6d1ebb707264c"), "name" : "The Great Wall of China", "city" : "Huairou", "country" : "China", "gps" : { "lat" : 40.431908, "lng" : 116.570374 } }
{ "_id" : ObjectId("6105770952e6d1ebb707264d"), "name" : "The Statue of Liberty", "city" : "New York", "country" : "USA", "gps" : { "lat" : 40.689247, "lng" : -74.044502 } }
```

The MongoDB shell prints out all seven documents one by one and in full. Notice that each of these objects have an `_id` property which you didn’t define. As mentioned previously, the `_id` fields serve as their respective documents’ primary key, and were created automatically when you ran the `insertMany` method in the previous step.

The default output from the MongoDB shell is compact, with each document’s fields and values printed in a single line. This can become difficult to read with objects containing multiple fields or nested documents, in particular.

To make the `find()` method’s output more readable, you can use its `pretty` printing feature, like this:

```bash
db.monuments.find().pretty()
```

This time, the MongoDB shell will print the documents on multiple lines, each with indentation:

```bash
{
  "_id" : ObjectId("6105752352e6d1ebb7072647"),
  "name" : "The Pyramids of Giza",
  "city" : "Giza",
  "country" : "Egypt",
  "gps" : {
    "lat" : 29.97648,
    "lng" : 31.131302
  }
}
{
  "_id" : ObjectId("6105770952e6d1ebb7072648"),
  "name" : "The Valley of the Kings",
  "city" : "Luxor",
  "country" : "Egypt",
  "gps" : {
    "lat" : 25.746424,
    "lng" : 32.605309
  }
}
. . .
```

Notice that in the two previous examples, the `find()` method was executed without any arguments. In both cases, it returned every object from the collection. You can apply filters to a query to narrow down the results.

Recall from the previous examples that MongoDB automatically assigned **The Valley of the Kings** an object identifier with the value of `ObjectId("6105770952e6d1ebb7072648")`. The object identifier is not just the hexadecimal string inside the `ObjectId("")`, but the whole `ObjectId` object — a special datatype used in MongoDB to store object identifiers.

The following `find()` method returns a single object by accepting a *query filter document* as an argument. Query filter documents follow the same structure as the documents you insert into a collection, consisting of fields and values, but they’re instead used to filter query results.

The query filter document used in this example includes the `_id` field, with **The Valley of the Kings’** object identifier as the value. To run this query on your own database, be sure to replace the highlighted object identifier with that of one of the documents stored in your own `monuments` collection:

```bash
db.monuments.find({"_id": ObjectId("6105770952e6d1ebb7072648")}).pretty()
```

The query filter document in this example uses the equality condition, meaning the query will return any documents that have a field and value pair matching the one specified in the document. Essentially, this example tells the `find()` method to only return the documents whose `_id` value is equal to `ObjectId("6105770952e6d1ebb7072648")`.

After executing this method, MongoDB will return a single object matching the requested object identifier:

```bash
{
  "_id" : ObjectId("6105770952e6d1ebb7072648"),
  "name" : "The Valley of the Kings",
  "city" : "Luxor",
  "country" : "Egypt",
  "gps" : {
    "lat" : 25.746424,
    "lng" : 32.605309
  }
}
```

You can use quality condition on any other field from the document as well. To illustrate, try searching for monuments in France:

```bash
db.monuments.find({"country": "France"}).pretty()
```

This method will return two monuments:

```bash
{
  "_id" : ObjectId("6105770952e6d1ebb7072649"),
  "name" : "Arc de Triomphe",
  "city" : "Paris",
  "country" : "France",
  "gps" : {
    "lat" : 48.873756,
    "lng" : 2.294946
  }
}
{
  "_id" : ObjectId("6105770952e6d1ebb707264a"),
  "name" : "The Eiffel Tower",
  "city" : "Paris",
  "country" : "France",
  "gps" : {
    "lat" : 48.858093,
    "lng" : 2.294694
  }
}
```

Query filter documents are quite powerful and flexible, and they allow you to apply complex filters to collection documents.

To select only one document, we can use the `findOne()` method. This method accepts a query object. If left empty, it will return the first document it finds.

```bash
db.monuments.findOne({})
```

## Updating Documents

It’s common for documents within a document-oriented database like MongoDB to change over time. Sometimes, their structures must evolve along with the changing requirements of an application, or the data itself might change. This step focuses on how to update existing documents by changing field values in individual documents as well as and adding a new field to every document in a collection.

Similar to the `insertOne()` and `insertMany()` methods, MongoDB provides methods that allow you to update either a single document or multiple documents at once. An important difference with these update methods is that, when creating new documents, you only need to pass the document data as method arguments. To update an existing document in the collection, you must also pass an argument that specifies which document you want to update.

To allow users to do this, MongoDB uses the same query filter document mechanism in update methods as the one you used in the previous step to find and retrieve documents. Any query filter document that can be used to retrieve documents can also be used to specify documents to update.

Try changing the name of **Arc de Triomphe** to the full name of **Arc de Triomphe de l’Étoile**. To do so, use the `updateOne()` method which updates a single document:

```bash
db.monuments.updateOne(
  { "name": "Arc de Triomphe" },
  {
    $set: { "name": "Arc de Triomphe de l'Étoile" }
  }
)
```

The first argument of the `updateOne` method is the query filter document with a single equality condition, as covered in the previous step. In this example, `{ "name": "Arc de Triomphe" }` finds documents with `name` key holding the value of `Arc de Triomphe`. Any valid query filter document can be used here.

The second argument is the update document, specifying what changes should be applied during the update. The update document consists of update operators as keys, and parameters for each of the operator as values. In this example, the update operator used is `$set`. It is responsible for setting document fields to new values and requires a JSON object with new field values. Here, `set: { "name": "Arc de Triomphe de l'Étoile" }` tells MongoDB to set the value of field `name` to `Arc de Triomphe de l'Étoile`.

The method will return a result telling you that one object was found by the query filter document, and also one object was successfully updated.

```bash
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

To check whether the update worked, try retrieving all the monuments related to `France`:

```bash
db.monuments.find({"country": "France"}).pretty()
```

This time, the method returns **Arc de Triomphe** but with its full name, which was changed by the update operation:

```bash
{
  "_id" : ObjectId("6105770952e6d1ebb7072649"),
  "name" : "Arc de Triomphe de l'Étoile",
  "city" : "Paris",
  "country" : "France",
  "gps" : {
    "lat" : 48.873756,
    "lng" : 2.294946
  }
}
. . .
```

To modify more than one document, you can instead use the `updateMany()` method.

As an example, say you notice there is no information about who created the entry and you’d like to credit the author who added each monument to the database. To do this, you’ll add a new `editor` field to each document in the `monuments` collection.

The following example includes an empty query filter document. By including an empty query document, this operation will match every document in the collection and the `updateMany()` method will affect each of them . The update document adds a new `editor` field to each document, and assigns it a value of `Palin`:

```bash
db.monuments.updateMany(
  { },
  {
    $set: { "editor": "Palin" }
  }
)
```

This method will return the following output:

```bash
{ "acknowledged" : true, "matchedCount" : 7, "modifiedCount" : 7 }
```

This output informs you that seven documents were matched and seven were also modified.

Confirm that the changes were applied:

```bash
db.monuments.find().pretty()
```

```bash
{
  "_id" : ObjectId("6105752352e6d1ebb7072647"),
  "name" : "The Pyramids of Giza",
  "city" : "Giza",
  "country" : "Egypt",
  "gps" : {
    "lat" : 29.97648,
    "lng" : 31.131302
  },
  "editor" : "Palin"
}
{
  "_id" : ObjectId("6105770952e6d1ebb7072648"),
  "name" : "The Valley of the Kings",
  "city" : "Luxor",
  "country" : "Egypt",
  "gps" : {
    "lat" : 25.746424,
    "lng" : 32.605309
  },
  "editor" : "Palin"
}
. . .
```

All the returned documents now have a new field called `editor` set to `Palin`. By providing a non-existing field name to the `$set` update operator, the update operation will create missing fields in all matched documents and properly set the new value.

Although you’ll likely use `$set` most often, many other update operators are available in MongoDB, allowing you to make complex alterations to your documents’ data and structure.

## Deleting Documents

There are times when data in the database becomes obsolete and needs to be deleted. As with Mongo’s update and insertion operations, there is a `deleteOne()` method, which removes only the *first* document matched by the query filter document, and `deleteMany()`, which deletes multiple objects at once.

To practice using these methods, begin by trying to remove the **Arc de Triomphe de l’Étoile** monument you modified previously:

```bash
db.monuments.deleteOne(
    { "name": "Arc de Triomphe de l'Étoile" }
)
```

Notice that this method includes a query filter document like the previous update and retrieval examples. As before, you can use any valid query to specify what documents will be deleted.

MongoDB will return the following result:

```bash
{ "acknowledged" : true, "deletedCount" : 1 }
```

Here, the result tells you how many documents were deleted in the process.

Check whether the document has indeed been removed from the collection by querying for monuments in France:

```bash
db.monuments.find({"country": "France"}).pretty()
```

This time the method returns only single monument, **The Eiffel Tower**, since you removed the **Arc de Triomphe de l’Étoile**:

**Output:**

```bash
{
  "_id" : ObjectId("6105770952e6d1ebb707264a"),
  "name" : "The Eiffel Tower",
  "city" : "Paris",
  "country" : "France",
  "gps" : {
    "lat" : 48.858093,
    "lng" : 2.294694
  },
  "editor" : "Palin"
}
```

To illustrate removing multiple documents at once, remove all the monument documents for which `Palin` was the editor. This will empty the collection, as you’ve previously designated `Palin` as the editor for every monument:

```bash
db.monuments.deleteMany(
  { "editor": "Palin" }
)
```

This time, MongoDB lets you know that this method removed six documents:

```bash
{ "acknowledged" : true, "deletedCount" : 6 }
```

You can verify that the `monuments` collection is now empty by counting the number of documents within it:

```bash
db.monuments.count()
```

**Output:**

```bash
0
```