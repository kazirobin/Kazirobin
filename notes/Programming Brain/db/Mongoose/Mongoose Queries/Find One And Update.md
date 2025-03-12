# Find One And Update

The `findOneAndUpdate` method in Mongoose is used to **find a single document** that matches a given condition and **update** it with new values. It returns the **updated document** (by default, the original one unless configured otherwise) or **`null`** if no document matches the condition.

## Syntax

```jsx
Model.findOneAndUpdate(conditions, update, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`update`**: An object specifying the fields to update. Supports MongoDB update operators like `$set`, `$inc`, etc.
- **`options`** (optional): Additional settings like returning the new document, upserting, etc.
- Returns a promise that resolves to the **updated document** or **`null`** if not found.

Suppose you have a `User` model and want to update a user's age by their name.

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

// Update a user's age by name
User.findOneAndUpdate(
  { name: 'John Doe' },               // Condition
  { $set: { age: 35 } },              // Update
  { returnDocument: 'after' }         // Option to return the updated document
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
Updated User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 35, "status": "active" }
```

- **`returnDocument: 'before'`** (default) returns the original document.
- **`returnDocument: 'after'`** returns the updated document.

If you want to get the original document before updating

```jsx
User.findOneAndUpdate(
  { name: 'John Doe' },
  { $set: { age: 35 } },
  { returnDocument: 'before' }
)
  .then((originalUser) => console.log('Original User:', originalUser))
  .catch((error) => console.error('Error:', error));
```

Output

```jsx
Original User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30, "status": "active" }
```

To increment the age by 1

```jsx
User.findOneAndUpdate(
  { name: 'John Doe' },
  { $inc: { age: 1 } },
  { returnDocument: 'after' }
)
  .then((updatedUser) => console.log('Updated User:', updatedUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Updated User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 31, "status": "active" }
```

Using the `upsert` option to create a new document if no match is found.

```jsx
User.findOneAndUpdate(
  { name: 'Alice' },
  { $set: { age: 28, status: 'active' } },
  { upsert: true, returnDocument: 'after' }
)
  .then((user) => console.log('User:', user))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f9", "name": "Alice", "age": 28, "status": "active" }
```

Combining `$set` and `$unset` operators

```jsx
User.findOneAndUpdate(
  { name: 'John Doe' },
  {
    $set: { status: 'inactive' },
    $unset: { age: '' }
  },
  { returnDocument: 'after' }
)
  .then((updatedUser) => console.log('Updated User:', updatedUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Updated User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "status": "inactive" }
```