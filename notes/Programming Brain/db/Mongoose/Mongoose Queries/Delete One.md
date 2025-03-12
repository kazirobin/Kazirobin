# Delete One

The `deleteOne` method in Mongoose is used to delete a **single document** from a collection that matches a specified condition. If multiple documents match the condition, only the **first one** found will be deleted.

## Syntax

```jsx
Model.deleteOne(filter, options)
```

- **`filter`**: Specifies the condition to match the document that should be deleted.
- **`options`**: Optional settings (rarely used with `deleteOne`).
- Returns a promise that resolves with an object containing information about the deletion.

Suppose you have a `User` model and you want to delete a user with the name **"John Doe"**.

```jsx
const mongoose = require('mongoose');

// Define a schema
const userSchema = new mongoose.Schema({
  name: String,
  status: String,
});

// Create a model
const User = mongoose.model('User', userSchema);

// Delete one user with the name 'John Doe'
User.deleteOne({ name: 'John Doe' })
  .then((result) => {
    console.log('Deleted document:', result.deletedCount);
  })
  .catch((error) => {
    console.error('Error deleting document:', error);
  });
```

**Output**

```jsx
Deleted document: 1
```

To delete a document by its **`_id`**, you can use

```jsx
User.deleteOne({ _id: '64d2f8e2c4e1a2b3c4d5e6f7' })
  .then((result) => {
    console.log('Deleted document by ID:', result.deletedCount);
  })
  .catch((error) => {
    console.error('Error deleting document by ID:', error);
  });
```

**Output**

```jsx
Deleted document by ID: 1
```