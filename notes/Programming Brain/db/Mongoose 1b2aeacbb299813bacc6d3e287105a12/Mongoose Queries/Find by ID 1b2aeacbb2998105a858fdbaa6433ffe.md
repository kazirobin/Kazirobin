# Find by ID

The `findById` method in Mongoose is used to **retrieve a single document** by its **`_id`** field. It’s a convenient shortcut for using `findOne` with an ID condition.

## Syntax

```jsx
Model.findById(id, projection, options)
```

- **`id`**: The ID of the document to find (as a string or `ObjectId`).
- **`projection`**: Specifies which fields to include or exclude (optional).
- **`options`**: Additional query options (optional).
- Returns a promise that resolves to a **single document** or **`null`** if not found.

Suppose you have a `User` model, and you want to find a user by their ID.

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

// Find a user by ID
User.findById('64d2f8e2c4e1a2b3c4d5e6f7')
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

Retrieve only **name** and **age** for a user by ID.

```jsx
User.findById('64d2f8e2c4e1a2b3c4d5e6f7', 'name age')
  .then((user) => {
    console.log('User with Selected Fields:', user);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

**Output**

```jsx
User with Selected Fields: { "_id": "64d2f8e2c4e1a2b3c4d5e6f7", "name": "John Doe", "age": 30 }
```