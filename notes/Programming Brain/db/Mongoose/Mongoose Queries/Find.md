# Find

The `find` method in Mongoose is used to **retrieve multiple documents** from a collection that match a specified condition. If no condition is provided, it returns **all documents**.

## Syntax

```jsx
Model.find(filter, projection, options)
```

- **`filter`**: Specifies the condition to match documents (optional, default is `{}` to match all).
- **`projection`**: Specifies which fields to include or exclude (optional).
- **`options`**: Additional query options like sorting, limiting, etc. (optional).
- Returns a promise that resolves to an **array of documents**.

Retrieve all documents from the `User` collection.

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

// Find all users
User.find({})
  .then((users) => {
    console.log('All Users:', users);
  })
  .catch((error) => {
    console.error('Error finding users:', error);
  });
```

**Output**

```jsx
All Users: [
  { "_id": "1", "name": "John Doe", "age": 30, "status": "active" },
  { "_id": "2", "name": "Jane Smith", "age": 25, "status": "inactive" }
]
```

Retrieve users who are **active**.

```jsx
User.find({ status: 'active' })
  .then((activeUsers) => {
    console.log('Active Users:', activeUsers);
  })
  .catch((error) => {
    console.error('Error finding active users:', error);
  });
```

**Output**

```jsx
Active Users: [
  { "_id": "1", "name": "John Doe", "age": 30, "status": "active" }
]
```

Retrieve only **name** and **age** of active users.

```jsx
User.find({ status: 'active' }, 'name age')
  .then((activeUsers) => {
    console.log('Active Users with Selected Fields:', activeUsers);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

**Output**

```jsx
Active Users with Selected Fields: [
  { "_id": "1", "name": "John Doe", "age": 30 }
]
```

Retrieve the **first 2 youngest** users, sorted by age.

```jsx
User.find({}, null, { sort: { age: 1 }, limit: 2 })
  .then((youngUsers) => {
    console.log('Youngest Users:', youngUsers);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

**Output**

```jsx
Youngest Users: [
  { "_id": "2", "name": "Jane Smith", "age": 25 },
  { "_id": "1", "name": "John Doe", "age": 30 }
]
```

- **`sort`**: `{ age: 1 }` for ascending, `{ age: -1 }` for descending.
- **`limit`**: Limits the number of documents returned.
- **`skip`**: Skips a specified number of documents.