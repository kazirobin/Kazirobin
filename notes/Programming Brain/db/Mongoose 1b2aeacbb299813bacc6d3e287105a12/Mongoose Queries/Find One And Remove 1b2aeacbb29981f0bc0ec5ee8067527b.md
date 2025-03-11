# Find One And Remove

In Mongoose, the `findOneAndRemove` method is used to **find a single document** that matches a given condition and **remove** it from the collection. It returns the **removed document** if found, or **`null`** if no document matches the condition.

**Note:** `findOneAndRemove` is similar to `findOneAndDelete` but is considered more aligned with Mongoose's internal mechanics. However, both work almost the same.

## Syntax

```jsx
Model.findOneAndRemove(conditions, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`options`** (optional): Additional settings like sorting or projection.
- Returns a promise that resolves to the **removed document** or **`null`** if not found.

Suppose you have a `User` model and want to remove a user by their name.

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

// Remove a user by name
User.findOneAndRemove({ name: 'John Doe' })
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

You can remove a document that matches multiple conditions.

```jsx
User.findOneAndRemove({ name: 'John Doe', status: 'inactive' })
  .then((removedUser) => console.log('Removed User:', removedUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Removed User: null  // If no inactive user named John Doe is found
```

To return only the name and age fields of the removed document

```jsx
User.findOneAndRemove({ name: 'John Doe' }, { projection: 'name age' })
  .then((removedUser) => console.log('Removed User:', removedUser))
  .catch((error) => console.error('Error:', error));
```

Output

```jsx
Removed User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30 }
```

Remove with Sorting Option

```jsx
User.findOneAndRemove({ status: 'active' }, { sort: { age: -1 } })
  .then((removedUser) => console.log('Removed Oldest Active User:', removedUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Removed Oldest Active User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f8", "name": "Alice", "age": 45, "status": "active" }
```