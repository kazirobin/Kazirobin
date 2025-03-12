# Find One And Delete

The `findOneAndDelete` method in Mongoose is used to **find a single document** that matches a given condition and **delete** it from the collection. It returns the **deleted document** if found, or **`null`** if no document matches the condition.

## Syntax

```jsx
Model.findOneAndDelete(conditions, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`options`** (optional): Additional settings like sorting or projection.
- Returns a promise that resolves to the **deleted document** or **`null`** if not found.

Suppose you have a `User` model and want to delete a user by their name.

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

// Delete a user by name
User.findOneAndDelete({ name: 'John Doe' })
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

You can delete a document that matches multiple conditions.

```jsx
User.findOneAndDelete({ name: 'John Doe', status: 'inactive' })
  .then((deletedUser) => console.log('Deleted User:', deletedUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Deleted User: null  // If no inactive user named John Doe is found
```

To return only the name and age fields of the deleted document

```jsx
User.findOneAndDelete({ name: 'John Doe' }, { projection: 'name age' })
  .then((deletedUser) => console.log('Deleted User:', deletedUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Deleted User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30 }
```

Delete with Sorting Option

```jsx
User.findOneAndDelete({ status: 'active' }, { sort: { age: -1 } })
  .then((deletedUser) => console.log('Deleted Oldest Active User:', deletedUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Deleted Oldest Active User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f8", "name": "Alice", "age": 45, "status": "active" }
```