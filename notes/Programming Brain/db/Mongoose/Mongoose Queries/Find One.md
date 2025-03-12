# Find One

The `findOne` method in Mongoose is used to **find a single document** in a collection that matches a given condition. If multiple documents match, it returns the **first** one it finds based on the default sorting order.

## Syntax

```jsx
Model.findOne(conditions, projection, options)
```

- **`conditions`**: An object specifying the fields to match (like a filter).
- **`projection`** (optional): An object specifying which fields to include or exclude.
- **`options`** (optional): Additional settings like sorting or limiting results.
- Returns a promise that resolves to the **found document** or **`null`** if not found.

Suppose you have a `User` model and want to find a user by their name.

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

// Find a user by name
User.findOne({ name: 'John Doe' })
  .then((user) => {
    if (user) {
      console.log('User Found:', user);
    } else {
      console.log('User not found');
    }
  })
  .catch((error) => {
    console.error('Error finding user:', error);
  });
```

**Output**

```jsx
User Found: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30, "status": "active" }
```

You can search using multiple conditions like name and status.

```jsx
User.findOne({ name: 'John Doe', status: 'active' })
  .then((user) => console.log('User Found:', user))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
User Found: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30, "status": "active" }
```

To return only the name and age fields

```jsx
User.findOne({ name: 'John Doe' }, 'name age')
  .then((user) => console.log('User Found:', user))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
User Found: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30 }
```

To exclude the `status` field

```jsx
User.findOne({ name: 'John Doe' }, '-status')
  .then((user) => console.log('User Found:', user))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
User Found: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30 }
```

Find the oldest active user

```jsx
User.findOne({ status: 'active' }, null, { sort: { age: -1 } })
  .then((user) => console.log('Oldest Active User:', user))
  .catch((error) => console.error('Error:', error));
```

**Output**

```jsx
Oldest Active User: { "_id": "64d2f8e2c4e1a2b3c4d5e6f8", "name": "Alice", "age": 45, "status": "active" }
```