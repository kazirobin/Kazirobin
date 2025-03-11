# Find by ID And Delete

The `findByIdAndDelete` method in Mongoose is used to **find a document by its `_id`** and **delete** it in a single operation. It returns the deleted document if found and deleted, or **`null`** if no document matches the ID.

## Syntax

```jsx
Model.findByIdAndDelete(id, options)
```

- **`id`**: The ID of the document to delete (as a string or `ObjectId`).
- **`options`**: Additional settings like `{ projection: { ... } }` to control returned fields (optional).
- Returns a promise that resolves to the **deleted document** or **`null`** if not found.

Suppose you have a `User` model and want to delete a user by their ID.

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

// Delete a user by ID
User.findByIdAndDelete('64d2f8e2c4e1a2b3c4d5e6f7')
  .then((deletedUser) => {
    if (deletedUser) {
      console.log('Deleted User:', deletedUser);
    } else {
      console.log('User not found');
    }
  })
  .catch((error) => {
    console.error('Error deleting user:', error);
  });
```

**Output**

```jsx
Deleted User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30, "status": "active" }
```

You can specify which fields to return from the deleted document.

```jsx
User.findByIdAndDelete('64d2f8e2c4e1a2b3c4d5e6f7', { projection: 'name age' })
  .then((deletedUser) => {
    console.log('Deleted User with Selected Fields:', deletedUser);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```