# Update One

The `updateOne` method in Mongoose is used to **update a single document** that matches a given condition. It applies the specified update to the document, but it does not replace the entire document. Instead, it **modifies** the matched document, allowing you to update specific fields. If no document matches the condition, the document is not updated unless you use the `upsert` option.

## Syntax

```jsx
Model.updateOne(conditions, update, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`update`**: An object specifying the fields to update. It can use MongoDB update operators such as `$set`, `$inc`, `$push`, etc.
- **`options`** (optional): Additional settings such as `upsert` (create if not found), `multi` (update multiple documents), etc.
- Returns a promise that resolves to an object with details about the operation.

Suppose you have a `User` model and you want to **update** a user's **age** by their **name**.

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
User.updateOne(
  { name: 'John Doe' },             // Condition
  { $set: { age: 35 } }             // Update operation
)
  .then((result) => {
    console.log('Update Result:', result);
  })
  .catch((error) => {
    console.error('Error updating user:', error);
  });
```

**Output**

```jsx
Update Result: { acknowledged: true, modifiedCount: 1 }
```

In this example, the `age` of the user with the name "John Doe" is updated to `35`.

You can use MongoDB's `$inc` operator to **increment** a field. For example, incrementing the **age** by 1:

```jsx
User.updateOne(
  { name: 'John Doe' },
  { $inc: { age: 1 } }  // Increment the age by 1
)
  .then((result) => console.log('Update Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Update Result: { acknowledged: true, modifiedCount: 1 }
```

The `age` of "John Doe" would increase by 1

The `upsert` option allows you to **create a new document** if no matching document is found.

```jsx
User.updateOne(
  { name: 'Alice' },                       // Condition
  { $set: { name: 'Alice', age: 28, status: 'active' } }, // Update or create
  { upsert: true }                          // Create if no match
)
  .then((result) => console.log('Upsert Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Upsert Result: {
  "acknowledged": true,
  "matchedCount": 0,
  "modifiedCount": 0,
  "upsertedCount": 1,
  "upsertedId": "64d2f8e2c4e1a2b3c4d5e6f9"
}
```

This means no document matched the condition, and a new document was created with the `upsertedId`.

You can update multiple fields at once using the `$set` operator.

```jsx
User.updateOne(
  { name: 'John Doe' },
  { $set: { age: 30, status: 'active' } }
)
  .then((result) => console.log('Update Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Update Result: { acknowledged: true, modifiedCount: 1 }
```

This will set the `age` to `30` and the `status` to `'active'`

If you have an array in the document, you can use the `$push` operator to add an item to that array.

```jsx
const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
  hobbies: [String],
});

const User = mongoose.model('User', userSchema);

// Add a hobby to the hobbies array
User.updateOne(
  { name: 'John Doe' },
  { $push: { hobbies: 'reading' } }  // Add "reading" to the hobbies array
)
  .then((result) => console.log('Update Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Update Result: { acknowledged: true, modifiedCount: 1 }
```

The `hobbies` array will now include `"reading"`.

- **Does not replace** the entire document like `replaceOne`, but only **modifies specific fields**.
- **Can use multiple update operators** like `$set`, `$inc`, `$push`, etc.
- **`upsert`** creates a new document if no match is found.
- **Returns an object** with details about the operation, including `matchedCount`, `modifiedCount`, and `upsertedCount`.