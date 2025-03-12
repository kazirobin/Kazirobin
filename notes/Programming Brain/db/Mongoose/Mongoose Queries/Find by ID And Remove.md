# Find by ID And Remove

The `findByIdAndRemove` method in Mongoose is similar to `findByIdAndDelete` and is used to **find a document by its `_id`** and **remove** it from the collection. The difference is mainly historical, as `findByIdAndDelete` was introduced later for clarity, but they both function the same way.

## Syntax

```jsx
Model.findByIdAndRemove(id, options)
```

- **`id`**: The ID of the document to remove (as a string or `ObjectId`).
- **`options`**: Additional settings like `{ projection: { ... } }` to control returned fields (optional).
- Returns a promise that resolves to the **removed document** or **`null`** if not found.

Suppose you have a `User` model and want to remove a user by their ID.

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

// Remove a user by ID
User.findByIdAndRemove('64d2f8e2c4e1a2b3c4d5e6f7')
  .then((removedUser) => {
    if (removedUser) {
      console.log('Removed User:', removedUser);
    } else {
      console.log('User not found');
    }
  })
  .catch((error) => {
    console.error('Error removing user:', error);
  });
```

**Output**

```jsx
Removed User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30, "status": "active" }
```

You can specify which fields to return from the removed document.

```jsx
User.findByIdAndRemove('64d2f8e2c4e1a2b3c4d5e6f7', { projection: 'name age' })
  .then((removedUser) => {
    console.log('Removed User with Selected Fields:', removedUser);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

**Output**

```jsx
Removed User with Selected Fields: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30 }
```

- **`findByIdAndRemove`** uses the legacy `remove()` internally.
- **`findByIdAndDelete`** uses the newer `deleteOne()` internally.

Both behave the same way in practice. Using `findByIdAndDelete` is recommended for clarity and modern code.