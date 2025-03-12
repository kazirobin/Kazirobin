# Find by ID And Update

The `findByIdAndUpdate` method in Mongoose is used to **find a document by its `_id`** and **update** it with new data. It returns the **updated document** by default (or the original document if not configured otherwise).

## Syntax

```jsx
Model.findByIdAndUpdate(id, update, options)
```

- **`id`**: The ID of the document to update (as a string or `ObjectId`).
- **`update`**: An object with the fields to update.
- **`options`**: Optional settings like:
    - `{ new: true }`: Returns the **updated** document instead of the original.
    - `{ runValidators: true }`: Validates the update according to the schema.
    - `{ upsert: true }`: Creates a new document if none is found.

Returns a promise that resolves to the **updated document** or **`null`** if not found.

Suppose you have a `User` model and want to update a user's name and age by their ID.

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

// Update a user by ID
User.findByIdAndUpdate(
  '64d2f8e2c4e1a2b3c4d5e6f7',
  { name: 'Jane Doe', age: 28 },
  { new: true }  // Return the updated document
)
  .then((updatedUser) => {
    if (updatedUser) {
      console.log('Updated User:', updatedUser);
    } else {
      console.log('User not found');
    }
  })
  .catch((error) => {
    console.error('Error updating user:', error);
  });
```

**Output**

```jsx
Updated User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "Jane Doe", "age": 28, "status": "active" }
```

Using Validation options

```jsx
User.findByIdAndUpdate(
  '64d2f8e2c4e1a2b3c4d5e6f7',
  { age: 'twenty-eight' },  // Invalid age
  { new: true, runValidators: true }
)
  .then((updatedUser) => {
    console.log('Updated User:', updatedUser);
  })
  .catch((error) => {
    console.error('Validation Error:', error.message);
  });
```

**Output**

```jsx
Validation Error: Cast to Number failed for value "twenty-eight" at path "age"
```

Using Upsert Option (Update or Insert)

```jsx
User.findByIdAndUpdate(
  '64d2f8e2c4e1a2b3c4d5e6f0',  // Non-existent ID
  { name: 'New User', age: 25, status: 'active' },
  { new: true, upsert: true }
)
  .then((user) => {
    console.log('User Created or Updated:', user);
  })
  .catch((error) => {
    console.error('Error:', error);
  });

```

**Output**

```jsx
User Created or Updated: { "_id": "64d2f8e2c4e1a2b3c4d5e6f0", "name": "New User", "age": 25, "status": "active" }
```