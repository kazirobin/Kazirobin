# Find One And Replace

The `findOneAndReplace` method in Mongoose is used to **find a single document** that matches a given condition and **replace** it entirely with a new document. It returns the **replaced document** (by default, the original one unless configured otherwise) or **`null`** if no document matches the condition.

## Syntax

```jsx
Model.findOneAndReplace(conditions, replacement, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`replacement`**: The new document that will replace the matched one. It **must match the schema**.
- **`options`** (optional): Additional settings like returning the new document or upserting.
- Returns a promise that resolves to the **replaced document** or **`null`** if not found.

Suppose you have a `User` model and want to replace a user by their name.

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
User.findOneAndReplace(
  { name: 'John Doe' },  // Condition
  { name: 'John Smith', age: 35, status: 'active' },  // Replacement document
  { returnDocument: 'after' }  // Options to return the new document
)
  .then((replacedUser) => {
    if (replacedUser) {
      console.log('Replaced User:', replacedUser);
    } else {
      console.log('User not found');
    }
  })
  .catch((error) => {
    console.error('Error replacing user:', error);
  });
```

**Output**

```jsx
Replaced User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Smith", "age": 35, "status": "active" }
```

- **`returnDocument: 'before'`** (default) returns the original document.
- **`returnDocument: 'after'`** returns the new, replaced document.

If you want to get the original document before replacement

```jsx
User.findOneAndReplace(
  { name: 'John Doe' },
  { name: 'John Smith', age: 35, status: 'active' },
  { returnDocument: 'before' }
)
  .then((originalUser) => console.log('Original User:', originalUser))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Original User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30, "status": "inactive" }
```

Using the `upsert` option to create a new document if no match is found.

```jsx
User.findOneAndReplace(
  { name: 'Alice' },
  { name: 'Alice', age: 28, status: 'active' },
  { upsert: true, returnDocument: 'after' }
)
  .then((user) => console.log('User:', user))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f9", "name": "Alice", "age": 28, "status": "active" }
```

## Important Considerations

- The **replacement document** must include **all required fields** according to the schema.
- **Fields not specified** in the replacement document will be **deleted**.
- **Does not merge** fields like `findOneAndUpdate` — it **replaces entirely**.