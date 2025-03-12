# Redux Middleware

`CreatedAt- 13 Jan 2025 / RevisedAt-` 

Redux Middleware allows you to intercept every action sent to the reducer so you can make changes to the action or cancel the action. Middleware helps you with logging, error reporting, making asynchronous requests, and a whole lot more.

```jsx
const { createStore } = require("redux");

const reducer = (state = 0, action) => {
  switch (action.type) {
    case "INCREMENT":
      return state + action.payload;
    case "DECREMENT":
      return state - action.payload;
    default:
      return state;
  }
};

const store = createStore(reducer);

store.subscribe(() => {
  console.log("current state", store.getState());
});

store.dispatch({
  type: "INCREMENT",
  payload: 1,
});

store.dispatch({
  type: "INCREMENT",
  payload: 5,
});

store.dispatch({
  type: "DECREMENT",
  payload: 2,
});
```

## How to Create Middleware

To create a middleware, we first need to import the `applyMiddleware` function from Redux like this:

```jsx
import { applyMiddleware } from "redux";
```

Let's say we're creating a `loggerMiddleware`. Then to define the middleware we need to use the following syntax:

```jsx
const loggerMiddleware = (store) => (next) => (action) => {
  // your code
};
```

The above code is equivalent to the below code:

```jsx
const loggerMiddleware = function (store) {
  return function (next) {
    return function (action) {
      // your code
    };
  };
};
```

Once the middleware function is created, we pass it to the `applyMiddleware` function like this:

```jsx
const middleware = applyMiddleware(loggerMiddleware);
```

And finally, we pass the middleware to the `createStore` function like this:

```jsx
const store = createStore(reducer, middleware);
```

Even though we mentioned above that middleware is the third argument to the `createStore` function, the second argument (initial state) is optional. So based on the type of arguments, the `createStore` function automatically identifies that the passed argument is a middleware because it has the specific syntax of nested functions.

```jsx
const loggerMiddleware = (store) => (next) => (action) => {
  console.log("action", action);
  return next(action);
};
```

If you check the console, you will see the following output:

![middleware_output.png](Redux%20Middleware%201b2aeacbb29981fc9c0ed1de00784d01/middleware_output.png)

Before the action is dispatched to the store, the middleware gets executed as we can see the action logged to the console. Because we're calling the `next` function inside the `loggerMiddleware` by passing the action, the reducer will also be executed which results in the change in the store.

Now, what will happen If we don't call the `next` function inside the `loggerMiddleware`?

Then the action will not be sent to the reducer so the store will not be updated.

If you check the console, you will see the following output:

![middleware_removed_next.png](Redux%20Middleware%201b2aeacbb29981fc9c0ed1de00784d01/middleware_removed_next.png)

As you can see, we only get the actions logged to the console. And as the action is not forwarded to the reducer, it will not be executed – so we don't see the `console.log` from the `store.subscribe` function.

As described earlier, we can modify the action from the middleware before it's sent to the reducer.

The code for the middleware looks like this:

```jsx
const loggerMiddleware = (store) => (next) => (action) => {
  console.log("action", action);
  action.payload = 3;
  return next(action);
};
```

![changed_payload.png](Redux%20Middleware%201b2aeacbb29981fc9c0ed1de00784d01/changed_payload.png)

As per the code, once the action is logged to the console, we're setting the action payload to a value of `3`. So the action `type` remains the same but the `payload` is changed.

So we see the state changed to `3` initially. Then again it's incremented by `3` which makes it `6`. Finally it's decremented by `3` making the final state value `3`.

Before the action is sent to the reducer, our `loggerMiddleware` gets called where we're changing the payload value and we're always setting it to 3 before it's sent to the reducer. So based on the action type `INCREMENT` or `DECREMENT`, the reducer will always be changed by a value of `3`.

Even though we're changing the action in the above code, there is no issue in this case because it's a middleware and not a reducer.

**Note:** Reducers should be a pure function and we shouldn't make any changes to state and action inside the reducer.

In the above code examples, we've created a single middleware. But you can create multiple middlewares and pass them to the `applyMiddleware` function like this:

```jsx
const middleware = applyMiddleware(loggerMiddleware, secondMiddleware, thirdMiddleware);
```

All the middlewares mentioned in the `applyMiddleware` function will be executed one after the another.