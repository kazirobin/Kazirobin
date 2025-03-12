# Update Many

The `updateMany` method in Mongoose is used to **update multiple documents** that match a given condition. It allows you to apply the same update to all documents that meet the criteria. Unlike `updateOne`, which only updates the first document that matches, `updateMany` will update **all matching documents**.

## Syntax

```jsx
Model.updateMany(conditions, update, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`update`**: An object specifying the fields to update, which can include MongoDB update operators such as `$set`, `$inc`, `$push`, etc.
- **`options`** (optional): Additional settings such as `upsert` (create if not found), `multi` (deprecated), etc.
- Returns a promise that resolves to an object with details about the operation.

Suppose you have a `User` model and you want to **update the `status` field** for **all users** who are **inactive**

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

// Update the status to "active" for all users who are inactive
User.updateMany(
  { status: 'inactive' },  // Condition
  { $set: { status: 'active' } }  // Update operation
)
  .then((result) => {
    console.log('Update Result:', result);
  })
  .catch((error) => {
    console.error('Error updating users:', error);
  });
```

**Output**

```jsx
Update Result: { acknowledged: true, matchedCount: 5, modifiedCount: 5 }
```

This will update all documents where `status` is `'inactive'` and set their `status` to `'active'`.

You can use the `$inc` operator to **increment** a field for all matching documents. For example, incrementing the `age` by 1 for all users who are `18` years old:

```jsx
User.updateMany(
  { age: 18 },            // Condition
  { $inc: { age: 1 } }    // Increment the age by 1
)
  .then((result) => console.log('Update Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Update Result: { acknowledged: true, matchedCount: 3, modifiedCount: 3 }
```

This will increment the `age` by `1` for all users who are `18` years old.

The `upsert` option allows you to **create new documents** if no documents match the condition.

```jsx
User.updateMany(
  { status: 'inactive' },              // Condition
  { $set: { status: 'active' } },       // Update operation
  { upsert: true }                      // Create if no match
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
  "upsertedCount": 0
}
```

In this case, no document matched, so nothing was updated, but an upsert could have occurred if `upsert` was set to `true` and the condition didn't match any existing documents.

You can use the `$push` operator to **add elements to an array** in multiple documents.

```jsx
User.updateMany(
  { status: 'active' },                 // Condition
  { $push: { hobbies: 'painting' } }    // Add "painting" to the hobbies array
)
  .then((result) => console.log('Update Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Update Result: { acknowledged: true, matchedCount: 10, modifiedCount: 10 }
```

This will add `"painting"` to the `hobbies` array for all users with `status` set to `'active'`.

You can update multiple fields for multiple documents at once using the `$set` operator.

```jsx
User.updateMany(
  { status: 'inactive' },
  { $set: { status: 'active', age: 30 } }  // Update multiple fields
)
  .then((result) => console.log('Update Result:', result))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Update Result: { acknowledged: true, matchedCount: 5, modifiedCount: 5 }
```

This will set the `status` to `'active'` and `age` to `30` for all users with `status` set to `'inactive'`.