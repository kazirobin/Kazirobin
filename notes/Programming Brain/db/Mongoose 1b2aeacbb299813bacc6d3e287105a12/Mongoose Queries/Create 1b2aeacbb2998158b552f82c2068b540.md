# Create

The `create` method in Mongoose is used to **create and save a new document** to the database. It can be used to create one or multiple documents at once, and it will automatically validate the data before saving it to the database.

## **Syntax**

```jsx
Model.create(docs, options)
```

- **`docs`**: A single document object or an array of documents to be created.
- **`options`** (optional): Additional settings like `timestamps` and `validateBeforeSave`.
- Returns a promise that resolves to the created document(s).

Suppose you have a `User` model and you want to create a new user.

```jsx
const mongoose = require('mongoose');

// Define a schema
const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
  status: String,
});

// Create a model
const User = mongoose.model('User', userSchema);

// Create a single document
User.create({
  name: 'John Doe',
  age: 30,
  status: 'active',
})
  .then((newUser) => {
    console.log('Created User:', newUser);
  })
  .catch((error) => {
    console.error('Error creating user:', error);
  });
```

**Output**

```jsx
Created User: {
  "_id": "64d3f8e6c4e1a2b3c4d5e6f9",
  "name": "John Doe",
  "age": 30,
  "status": "active",
  "__v": 0
}
```

This will create a new document with the specified `name`, `age`, and `status`.

You can also create multiple documents at once by passing an array of objects.

```jsx
User.create([
  { name: 'Alice', age: 28, status: 'inactive' },
  { name: 'Bob', age: 25, status: 'active' },
  { name: 'Charlie', age: 35, status: 'inactive' }
])
  .then((newUsers) => {
    console.log('Created Users:', newUsers);
  })
  .catch((error) => {
    console.error('Error creating users:', error);
  });
```

**Output**

```jsx
Created Users: [
  { "_id": "64d3f8e6c4e1a2b3c4d5e6f9", "name": "Alice", "age": 28, "status": "inactive", "__v": 0 },
  { "_id": "64d3f8e6c4e1a2b3c4d5e6fa", "name": "Bob", "age": 25, "status": "active", "__v": 0 },
  { "_id": "64d3f8e6c4e1a2b3c4d5e6fb", "name": "Charlie", "age": 35, "status": "inactive", "__v": 0 }
]
```

This will create three new documents in the collection, each with its own `name`, `age`, and `status`.

Mongoose automatically validates the data before saving it to the database based on the schema. If the data doesn't match the validation rules, it will throw an error.

For instance, if the `status` field is required in the schema, the following code will fail.

```jsx
const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
  status: { type: String, required: true },
});

// Create a model
const User = mongoose.model('User', userSchema);

// Create a document without the required `status` field
User.create({
  name: 'John Doe',
  age: 30,
})
  .then((newUser) => {
    console.log('Created User:', newUser);
  })
  .catch((error) => {
    console.error('Error creating user:', error);
  });
```

**Output**

```jsx
Error creating user: ValidationError: User validation failed: status: Path `status` is required.
```

This will result in a validation error because the `status` field is required but was missing.

You can pass additional options, such as `timestamps`, which will automatically set the `createdAt` and `updatedAt` fields in the document.

```jsx
const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
  status: String,
}, { timestamps: true });

// Create a model
const User = mongoose.model('User', userSchema);

// Create a user with timestamps
User.create({
  name: 'John Doe',
  age: 30,
  status: 'active',
})
  .then((newUser) => {
    console.log('Created User with Timestamps:', newUser);
  })
  .catch((error) => {
    console.error('Error creating user:', error);
  });
```

Output

```jsx
Created User with Timestamps: {
  "_id": "64d3f8e6c4e1a2b3c4d5e6f9",
  "name": "John Doe",
  "age": 30,
  "status": "active",
  "createdAt": "2025-03-09T10:12:12.000Z",
  "updatedAt": "2025-03-09T10:12:12.000Z",
  "__v": 0
}
```