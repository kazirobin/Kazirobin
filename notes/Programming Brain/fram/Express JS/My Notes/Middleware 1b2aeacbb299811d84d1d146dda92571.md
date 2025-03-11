# Middleware

Express.js Middleware are different types of functions that are invoked by the Express.js routing layer before the final request handler. As the name specified, Middleware appears in the middle between an initial request and final intended route. In stack, middleware functions are always invoked in the order in which they are added.

Middleware is commonly used to perform tasks like body parsing for URL-encoded or JSON requests, cookie parsing for basic cookie handling, or even building JavaScript modules on the fly.

## What Is Middleware?

- A request handler with access to the application's request-response cycle is known as middleware.
- It's a function that holds the request object, the response object, and the middleware function.
- Middleware can also send the response to the server before the request.
- The next middleware function is commonly represented as a variable named next.
- Simply middleware is a function that can only be applied using routes.
- We can access and modify request and response data using middleware.

[ExpressJS_Middleware_1.avif](Middleware%201b2aeacbb299811d84d1d146dda92571/ExpressJS_Middleware_1.avif)

## Functions of Middleware

- Executes any code
- We can make changes to the request-response objects
- Middleware can call the next middleware function in a stack

We use these functions to modify our middleware to perform many tasks. If we want to block our site for some country or if we're going to check the authentication of a user etc., we use middleware for that.

## Creating Middleware

Now we will create an Express middleware for that we will create a simple Express API. We can create middleware in a router file, but the easiest method is to create a separate middleware file and then execute it; creating and using middleware is very simple.

So to create middleware, we need to install all the packages to run express middleware.

- Now open your terminal and run this file we will see our server is running.
- After this, go to the local server and type localhost:4000
- Now we will call our next parameter,
- In express framework, next is a function

```jsx
const express = require("express");
const app = express();
const port = 3000;

const middleware = (req, res, next) => {
  console.log("Middleware executed");
  next();
};

app.use(middleware);

app.get("/", (req, res) => {
  res.send("Hello World!");
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```