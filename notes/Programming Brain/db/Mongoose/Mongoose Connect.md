# Mongoose Connect

---

MongoDB is one of the most popular NoSQL database and it’s a open-source document-oriented database and database server. The data stored in the collections and documents. It provides cloud-hosted services.

- The collections is like a database table
- The documents is key and value pairs instead of rows and columns .
- It can store large structured and unstructured data

## Connect Mongoose to MongoDB Atlas

Create a file named **src/utils/db.config.js**

```jsx
import mongoose from "mongoose";

// MongoDB connection string
const conncetionString = process.env.MONGODB_CONNECTION_STRING;

// Track the database is connected
let isConnected = false;

export default async function connectMongoDB() {
  if (isConnected) {
    console.log("Database is already connected");
    return;
  }

  try {
    await mongoose.connect(conncetionString, {
      dbName: "<db-name>",
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    isConnected = true;
    console.log("Database is connected");
  } catch (error) {
    console.log(error.message);
  }
}
```

```jsx
import mongoose from "mongoose";

// MongoDB connection string
let conncetionString = process.env.MONGODB_CONNECTION_STRING;

// Cached connection promise
const cached = {};

export default async function connectMongoDB() {
  // If the connection string is not defined, throw an error
  if (!conncetionString) {
    throw new Error("Please define the environment variable file");
  }

  // If the connection is already cached, return it
  if (cached.connection) {
    console.log("Database is already connected");
    return cached.connection;
  }

  // If the connection is not already cached, create a new connection
  if (!cached.promise) {
    const options = {
      bufferCommands: false,
      dbName: "<db-name>",
    };

    cached.promise = mongoose.connect(conncetionString, options);
  }

  // Wait for the connection to be ready and return it
  try {
    cached.connection = await cached.promise;
    console.log("Database is connected");
  } catch (error) {
    cached.promise = undefined;
    throw error;
  }
  return cached.connection;
}
```

## Connect Mongoose to MongoDB Localhost

Create a file named **src/utils/db.config.js**

```jsx
import mongoose from 'mongoose';

export default async function connectMongoDB() {
  try {
    await mongoose.connect("mongodb://127.0.0.1/productsDB");
    console.log("Database is connected");
  } catch (error) {
    console.log("Database is not connected");
    console.log(error.message);
    process.exit(1);
  }
};
```

## .env File Example

```
# MongoDB connection string
MONGODB_CONNECTION_STRING=mongodb+srv://<username>:<password>@cluster0.kf4wlap.mongodb.net/
DATABASE_USERNAME=hossainpalin
DATABASE_PASSWORD=8GeNRxQpuTOiWVN4
```