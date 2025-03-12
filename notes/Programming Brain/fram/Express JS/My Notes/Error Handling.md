# Error Handling

Error handling often doesn’t get the attention and prioritization it deserves. Especially for newbie developers, there is more focus on setting up routing, route handlers, business logic, optimizing performance, etc. As a result, the equally (if not more) crucial error-handling part will likely be overlooked. Striving for the most optimized code and squeezing out every last ounce of performance is all well and good; yet, it’s important to remember all it takes is one unhandled error leak into your user interface to override all the seconds you helped your users save.

Because there are so many components involved in a successful, functioning web application, it is vital to foolproof your application by preparing for all possible errors and exceptions. If left mishandled, these errors can lead to a bad user experience and end up affecting your business. At the same time, errors provide critical information about potential errors in your application that could bring the whole thing down. Therefore, you must be thoughtful and intelligent about error handling in your application. 

## How Does Error Handling Work in Express.js?

[Express.js](https://expressjs.com/) is the most popular Javascript server-side framework, perhaps, primarily because of its ease of usage and getting started. One of the many ways it makes things easier is by automatically catching all errors in route handlers, and allowing developers to extend route handling functionalities by leveraging useful middleware functions. 

## Express Middleware Functions

Middleware functions in Express are essentially functions that come into play after the server receives the request and before the response fires to the client. They have access to the request and the response objects. They can be used for any data processing, database querying, making API calls, sending the response, or calling the next middleware function (using the *next()* function). 

Two aspects of middleware functions to keep in mind are:

- They are triggered sequentially (top to bottom) based on their sequence in code.
- They operate until the process exits, or the response has been sent back to the client.

Let’s understand this through a small example. Below we define two middleware functions using the *.use()* function and one route handler:

```jsx
app.use((req, res, next) => {
  console.log("Middleware 1 called.")
  console.log(req.path)
  next() // calling next middleware function or handler
})

app.get('/', (req, res) => {
  console.log("Route handler called.")
  res.send("Hello world!") // response sent back – no more middleware called
})

app.use((req, res, next) => {
  console.log("Last middleware called❓") // not called
})
```

Here, each time the server receives a request, the first middleware is fired, followed by the corresponding route handler (using the *next()* function). However, because the response returns in this handler, the last middleware function is not called. Here’s the output:

Several native as well as third-party middleware functions have been made available by the Express community and are widely for adding functionalities like session management, authentication, logging, redirecting, and so much more. This was a basic example of how middleware functions work. We will come back to them when discussing how to utilize them for error handling in our applications.

## Default Error Handling in Express.js

Express implicitly takes care of catching your errors to prevent your application from crashing when it comes to error handling. This is especially true for synchronous route handler code. Let’s see how:

### Synchronous Code

Synchronous code refers to statements of code that execute sequentially and one at a time. When an error encounters synchronous code, Express catches it automatically. Here’s an example of a route handler function where we simulate an error condition by throwing an error:

```jsx
app.get("/", (req, res) => {
  throw new Error("Hello error!");
});
```

Express catches this error for us and responds to the client with the error’s status code, message, and even the stack trace (for non-production environments).

![unnamed (24).png](Error%20Handling%201b2aeacbb29981b68a47fc2043bc69c3/unnamed_(24).png)

All of this is taken care of thanks to Express’s **default built-in error handler middleware** function inserted at the end of your code’s middleware stack. This automatic handling saves you from bulky try/catch blocks and explicit calls to the in-built middleware (shown below) while also providing some fundamental default error handling functionality. 

```jsx
app.get("/", (req, res, next) => {
  try {
    throw new Error("Hello error!");
  } catch (error) {
    next(error);
  }
});
```

You can also choose to create your own middleware function to specify your error handling logic. 

### Asynchronous Code

When writing server-side code, most of your route handlers are likely using asynchronous Javascript logic to read and write files on the server, query databases, and make external API requests. Let’s see whether Express can catch errors raised from asynchronous code as well. We’ll throw an error from inside the asynchronous *setTimeout()* function and see what happens:

```jsx
app.get("/", (req, res) => {
  setTimeout(() => {
    console.log("Async code example.");
    throw new Error("Hello Error!");
  }, 1000);
});
```

As you can see, our server crashed because Express didn’t handle the error for us. 

![pasted image 0 (28).png](Error%20Handling%201b2aeacbb29981b68a47fc2043bc69c3/pasted_image_0_(28).png)

For handling errors raised during asynchronous code execution in Express (versions < 5.x), developers need to themselves catch their errors and invoke the in-built error handler middleware using the *next()* function. Here’s how:

```jsx
app.get("/", (req, res, next) => {
  setTimeout(() => {
    try {
      console.log("Async code example.");
      throw new Error("Hello Error!");
    } catch (error) {
      // manually catching
      next(error); // passing to default middleware error handler
    }
  }, 1000);
});
```

![pasted image 0 (29).png](Error%20Handling%201b2aeacbb29981b68a47fc2043bc69c3/pasted_image_0_(29).png)

This is much better – we caught the error, and our server didn’t crash. This does look a little bulky because we used the setTimeout() function to demonstrate async behavior. This function does not return a promise and, therefore, can’t be chained with a quick *.catch()* function. However, most libraries that help with async operations return promises these days (e.g., the file system API). Below is an example of a more convenient and common way of catching errors from promises:

```jsx
app.get("/", (req, res, next) => {
  fs.readFile("file-does-not-exist", (err, data) => {
    if (err) {
      next(err);
    } else {
      res.send(data);
    }
  });
});
```

## Handling Custom Errors

Express’s default error-handling middleware is super helpful for beginners to take care of unexpected, unhandled errors. However, different developers and organizations would want their errors handled in their own way – some might want to write these to log files, others might want to alert the user or redirect them to another page, or all of the above.

A much better option would be to leverage Express’s middleware functions here. You could write one or more middleware functions for handling errors in your application that all of your routes could utilize by making simple *next()* calls. 

Middleware functions are much more convenient to work with than conventional ones because they automatically access the error, request, and response objects and can be invoked (or invoked by others) based on their ordering using the *next()* function.

You can create your own error-handling middleware functions by adding the `err` **argument, apart from *request*, *response*, and *next*. Here is an example:

```jsx
// Custom error handler
app.use((err, req, res, next) => {
  if (err.message) {
    console.error(err.stack);
    res.status(500).send(err.message);
  } else {
    res.status(500).send("Something went wrong");
  }
});
```