# Routing

Routing is made from the word route. It is used to determine the specific behavior of an application. It specifies how an application responds to a client request to a particular route, URI or path and a specific HTTP request method (GET, POST, etc.). It can handle different types of HTTP requests.

Let's take an example to see basic routing.

### GET Request Routes

Create a new file, let's say `app.js`, and set up a basic Express application:

```jsx
const express = require('express');
const app = express();
const port = 3000; // Choose any port you like

// Example route - GET request
app.get('/', (req, res) => {
  res.send('Hello World!');
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

You can add more routes to handle different GET requests. Here's an example with multiple routes:

```jsx
// GET request for the homepage
app.get('/', (req, res) => {
  res.send('Welcome to the homepage!');
});

// GET request for about page
app.get('/about', (req, res) => {
  res.send('This is the about page.');
});

// GET request with route parameters
app.get('/users/:userId', (req, res) => {
  const userId = req.params.userId;
  res.send(`User ID: ${userId}`);
});
```

### POST Request Routes

Create a new file, let's say `app.js`, and set up a basic Express application:

```jsx
const express = require('express');
const app = express();
const port = 3000; // Choose any port you like

// Middleware to parse JSON bodies
app.use(express.json());

// Example route - POST request
app.post('/login', (req, res) => {
  const { username, password } = req.body;

  // Check if username and password are correct (example logic)
  if (username === 'admin' && password === 'password') {
    res.send('Login successful!');
  } else {
    res.status(401).send('Invalid credentials');
  }
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

In the above code, `express.json()` middleware is used to parse JSON bodies of incoming requests. This middleware is necessary to handle POST requests where data is sent in JSON format.

The `/login` route handles POST requests for user login. It checks if the `username` and `password` sent in the request body match the expected values (`admin` and `password` in this example). Adjust the logic to fit your application's needs.

You can test this route using tools like Postman or by sending POST requests from your frontend or using curl commands in your terminal.

Example curl command to test the `/login` route:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"username":"admin","password":"password"}' http://localhost:3000/login
```

### DELETE Request Routes

Create a new file, let's say `app.js`, and set up a basic Express application:

```jsx
const express = require("express");
const app = express();
const port = 3000; // Choose any port you like

// Middleware to parse JSON bodies
app.use(express.json());

// Example data (simulate a database)
let users = [
  { id: 1, name: "John Doe" },
  { id: 2, name: "Jane Doe" },
];

// GET request to retrieve all users
app.get("/users", (req, res) => {
  res.json(users);
});

// DELETE request to delete a user by ID
app.delete("/users/:id", (req, res) => {
  const id = parseInt(req.params.id);

  // Find the index of the user with the given id
  const index = users.findIndex((user) => user.id === id);

  if (index !== -1) {
    // Remove the user from the array
    users.splice(index, 1);
    res.send(`User with ID ${id} has been deleted.`);
  } else {
    res.status(404).send("User not found.");
  }
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

Just like in the previous tutorial for POST requests, `express.json()` middleware is used here to parse JSON bodies of incoming requests.

The `/users/:id` route handles DELETE requests to delete a user from the `users` array based on their `id`. Adjust the logic to fit your application's data structure and requirements.

You can test this route using tools like Postman or by sending DELETE requests from your frontend or using curl commands in your terminal.

Example curl command to delete a user with ID 1:

```bash
curl -X DELETE http://localhost:3000/users/1
```

### PUT Request Routes

Create a new file, let's say `app.js`, and set up a basic Express application:

```jsx
const express = require("express");
const app = express();
const port = 3000; // Choose any port you like

// Middleware to parse JSON bodies
app.use(express.json());

// Example data (simulate a database)
let users = [
  { id: 1, name: "John Doe" },
  { id: 2, name: "Jane Doe" },
];

// GET request to retrieve all users
app.get("/users", (req, res) => {
  res.json(users);
});

// PUT request to update a user by ID
app.put("/users/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const updatedUser = req.body; // Assuming the request body contains updated user data

  // Find the index of the user with the given id
  const index = users.findIndex((user) => user.id === id);

  if (index !== -1) {
    // Update the user in the array
    users[index] = { ...users[index], ...updatedUser };
    res.send(`User with ID ${id} has been updated.`);
  } else {
    res.status(404).send("User not found.");
  }
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});

```

Just like in the previous tutorials for POST and DELETE requests, `express.json()` middleware is used here to parse JSON bodies of incoming requests.

The `/users/:id` route handles PUT requests to update a user in the `users` array based on their `id`. Adjust the logic to fit your application's data structure and requirements.

You can test this route using tools like Postman or by sending PUT requests from your frontend or using curl commands in your terminal.

Example curl command to update a user with ID 1:

```bash
curl -X PUT -H "Content-Type: application/json" -d '{"name":"Updated Name"}' http://localhost:3000/users/1
```

### PATCH Request Routes

Create a new file, let's say `app.js`, and set up a basic Express application:

```jsx
const express = require("express");
const app = express();
const port = 3000; // Choose any port you like

// Middleware to parse JSON bodies
app.use(express.json());

// Example data (simulate a database)
let users = [
  { id: 1, name: "John Doe", age: 30 },
  { id: 2, name: "Jane Doe", age: 25 },
];

// GET request to retrieve all users
app.get("/users", (req, res) => {
  res.json(users);
});

// PATCH request to partially update a user by ID
app.patch("/users/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const updatedFields = req.body; // Assuming the request body contains updated fields

  // Find the index of the user with the given id
  const index = users.findIndex((user) => user.id === id);

  if (index !== -1) {
    // Update the user's fields in the array
    users[index] = { ...users[index], ...updatedFields };
    res.send(`User with ID ${id} has been partially updated.`);
  } else {
    res.status(404).send("User not found.");
  }
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});

```

As in previous tutorials, `express.json()` middleware is used here to parse JSON bodies of incoming requests.

The `/users/:id` route handles PATCH requests to partially update a user in the `users` array based on their `id`. Adjust the logic to fit your application's data structure and requirements.

You can test this route using tools like Postman or by sending PATCH requests from your frontend or using curl commands in your terminal.

Example curl command to partially update a user with ID 1 (updating the age):

```bash
curl -X PATCH -H "Content-Type: application/json" -d '{"age": 32}' http://localhost:3000/users/1
```