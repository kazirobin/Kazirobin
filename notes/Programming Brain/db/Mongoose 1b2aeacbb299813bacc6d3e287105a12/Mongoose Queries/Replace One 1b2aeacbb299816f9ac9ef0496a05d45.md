# Replace One

The `replaceOne` method in Mongoose is used to **replace a single document** that matches a given condition with a completely new document. It replaces the entire document, meaning it will **remove** any fields that are not specified in the new document. If no document matches the condition, it will not update anything unless you use the `upsert` option.

## Syntax

```jsx
Model.replaceOne(conditions, replacement, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`replacement`**: The new document that will completely replace the matched document. The new document **must match the schema**.
- **`options`** (optional): Additional settings like `upsert` (create if not found) and others.
- Returns a promise that resolves to an object with information about the operation, not the replaced document.

Suppose you have a `User` model and want to replace a user's document by their name.

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

// Replace a user by name
User.replaceOne(
  { name: 'John Doe' },               // Condition
  { name: 'John Smith', age: 35, status: 'active' }  // Replacement document
)
  .then((result) => {
    if (result.nModified > 0) {
      console.log('User replaced successfully');
    } else {
      console.log('No user found to replace');
    }
  })
  .catch((error) => {
    console.error('Error replacing user:', error);
  });
```

**Output**

```jsx
User replaced successfully
```

You can use the `upsert` option to **create** a new document if no match is found.

```jsx
User.replaceOne(
  { name: 'Alice' },                          // Condition
  { name: 'Alice', age: 28, status: 'active' }, // Replacement document
  { upsert: true }                            // Create if not found
)
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

**Output**

```jsx
{
  "acknowledged": true,
  "matchedCount": 0,
  "modifiedCount": 0,
  "upsertedCount": 1,
  "upsertedId": "64d2f8e2c4e1a2b3c4d5e6f9"
}
```

This means no document matched the condition, so a new document was created with the `upsertedId`.

Since `replaceOne` replaces the entire document, make sure the new document includes **all required fields**. If you want to replace just some fields, use `updateOne` instead.

```jsx
User.replaceOne(
  { name: 'John Doe' },
  { name: 'John Smith', age: 40, status: 'inactive' }  // Full replacement
)
  .then((result) => console.log('Replacement Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Replacement Result: {
  "acknowledged": true,
  "matchedCount": 1,
  "modifiedCount": 1
}
```

- **Completely replaces** the document.
- **Does not merge fields**. Any missing fields in the replacement document will be deleted from the original document.
- **`upsert`** creates a new document if no match is found.
- **Returns an object**, not the replaced document, but you can check for the operation's result with `matchedCount` and `modifiedCount`.