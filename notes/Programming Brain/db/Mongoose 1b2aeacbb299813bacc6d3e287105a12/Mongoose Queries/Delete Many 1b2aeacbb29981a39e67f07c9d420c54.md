# Delete Many

The `deleteMany` method in Mongoose is used to delete multiple documents from a collection that match a specified condition. If no condition is provided, it deletes all documents in the collection.

## Syntax

```jsx
Model.deleteMany(filter, options)
```

- **`filter`**: Specifies the condition to match documents that should be deleted.
- **`options`**: Optional settings (like `{ limit: n }` to limit the number of deletions).
- Returns a promise that resolves with an object containing information about the deletion.

Suppose you have a `User` model and you want to delete all users who are inactive.

```jsx
const mongoose = require('mongoose');

// Define a schema
const userSchema = new mongoose.Schema({
  name: String,
  status: String,
});

// Create a model
const User = mongoose.model('User', userSchema);

// Delete all users with status 'inactive'
User.deleteMany({ status: 'inactive' })
  .then((result) => {
    console.log('Deleted documents:', result.deletedCount);
  })
  .catch((error) => {
    console.error('Error deleting documents:', error);
  });
```

**Output**

```jsx
Deleted documents: 5
```