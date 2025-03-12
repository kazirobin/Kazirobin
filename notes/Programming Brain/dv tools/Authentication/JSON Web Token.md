# JSON Web Token

[JSON Web Tokens](https://jwt.io/) (JWTs) supports authorization and information exchange.  One common use case is for allowing clients to preserve their session information after logging in. By storing the session information locally and passing it to the server for authentication when making requests, the server can trust that the client is a registered user.

In this article, you will learn about the applications of JWTs in a server-client relationship using Node.js and vanilla JavaScript.

## Step 1 — Generating a Token

`jsonwebtoken` is an implementation of JSON Web Tokens. You can add it to your JavaScript project by running the following command in your terminal:

```bash
npm install jsonwebtoken
```

And import it into your files like so:

```jsx
const jwt = require('jsonwebtoken');
```

To sign a token, you will need to have 3 pieces of information:

1. The token secret
2. The piece of data to hash in the token
3. The token expires time

The *token secret* is a long random string used to encrypt and decrypt the data.
To generate this secret, one option is to use Node.js’s built-in `crypto` library, like so:

```jsx
> require('crypto').randomBytes(64).toString('hex')
// '09f26e402586e2faa8da4c98a35f1b20d6b033c6097befa8be3486a829587fe2f90a832bd3ff9d42710a4da095a2ce285b009f0c3730cd9b8e1af3eb84df6611'
```

Now, store this secret in your project’s `.env` file:

```jsx
JWT_SECRET=09f26e402586e2faa8da4c98a35f1b20d6b033c60...
```

To bring this token into a Node.js file and to use it, you have to use `dotenv`:

```bash
npm install dotenv
```

And import it into your files like so:

```jsx
require('dotenv').config();

// Other imports...

```

The *piece of data* that you hash in your token can be something either a user ID or username or a much more complex object. In either case, it should be an *identifier* for a *specific* user.

The *token expire time* is a string, such as 1800 seconds (30 minutes), that details how long until the token will be invalid.

## Step 2 — Authenticating a Token

There are many ways to go about implementing a JWT authentication system in an Express.js application.

One approach is to utilize the middleware functionality in Express.js.

How it works is when a request is made to a specific route, you can have the `(req, res)` variables sent to an intermediary function before the one specified in the `app.get((req, res) => {})`.

The middleware is a function that takes parameters of `(req, res, next)`.

- The `req` is the sent request (GET, POST, DELETE, PUT, etc.).
- The `res` is the response that can be sent back to the user in a multitude of ways (`res.sendStatus(200)`, `res.json()`, etc.).
- The `next` is a function that can be called to move the execution past the piece of middleware and into the actual `app.get` server response.

Here is an example middleware function for authentication:

```jsx
const jwt = require("jsonwebtoken");

const checkLogin = (req, res, next) => {
  const { authorization } = req.headers;

  try {
    const token = authorization.split(" ")[1];
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    next(new Error("Authentication failed!"));
  }
};

module.exports = checkLogin;

```

An example request using this middleware function would resemble something like this:

```
GET https://example.com:4000/api/userOrders
Authorization: Bearer JWT_ACCESS_TOKEN
```

## Step 3 — Generate Access Token

```jsx
// User login route
app.post("/login", async (req, res, next) => {
  const { email, password } = req.body;

  try {
    const isUserExisting = await UserModel.findOne({ email });

    if (!isUserExisting) {
      return res.json({
        success: false,
        message: "User not found!",
      });
    }

    if (isUserExisting.password !== password) {
      return res.json({
        success: false,
        message: "Invalid credentials!",
      });
    }

    // Generate a token
    const token = jwt.sign(
      {
        email: isUserExisting.email,
        userId: isUserExisting._id,
      },
      process.env.JWT_SECRET,
      { expiresIn: "1h" }
    );

    res.json({
      success: true,
      access_token: token,
      message: "User logged in successfully!",
    });
  } catch (error) {
    next(new Error(error));
  }
});
```