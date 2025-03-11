# Why Redux?

Essentially, Redux is a **JavaScript** library that helps manage the state of your application. “State” here means the data or variables that determine the current behavior and information shown to the user. For example, the contents of a shopping cart.

State is often managed directly in the components that display the data. For example, a component might store the current value of a form input in its own state, and update that state as the user types. As applications grow in size and complexity, managing this state can become difficult. This is where Redux comes in.

---

## What is Redux?

Redux is a popular Javascript library used to manage state in web applications. It was created by Dan Abramov around June 2015, inspired by Facebook’s Flux and **functional programming language Elm**. It’s particularly well-suited for applications with many different components that need to share data. 

## What is Redux used for?

What is Redux used for, you ask? Well, let’s say you have a lot of user data that controls how your web application behaves.

To go back to our eCommerce example, this could be the items in your shopping cart, suggested items, what page you’re on in a list of products, or the result of a search. Redux manages all this data by keeping it in one single place, called the “store”. 

## Advantages of using Redux

The main advantage of using Redux is that it provides a **predictable way to manage state** in your application. By making all state changes go through a central store, it’s easier to understand how the application’s state is modified. 

Having this single source of truth makes it much **easier to debug any issues** that come up. It’s also **easier to test**, and to reset the store to a known initial state.

When using Redux along with **JavaScript library React**, you can also manage state for React components. This makes it easier to build more complex, interactive applications with React. Using Redux also gives you a clear way to access and update the state of your individual components.

## Disadvantages of using Redux

One major downside of Redux is that it **adds a lot of extra boilerplate code**. You need to set up a store and manage reducers, in addition to your regular code. This adds complexity to your application, meaning more setup time and maintenance. 

Redux also introduces **less flexibility in handling data**. It’s more opinionated with its predictable way of managing state, both a plus and a minus depending on your needs. The lack of flexibility might help prevent bugs, but could also be a disadvantage in certain situations

## Redux FAQs

Now that you know what is Redux and its pros and cons, let’s go through some commonly-asked questions about the tool:

## Is Redux frontend or backend?

Redux is a framework used on the frontend of a web application. It’s a way to organize data in its store that controls the elements users see and interact with in the browser.

## What are the main concepts of Redux?

The three main concepts of Redux are **the store**, **actions** and **reducers**. Let’s take a brief look at each:

1. **Store**: The store holds the global state of the application. It's a JavaScript object that contains the entire state of the application. State modifications are performed through actions.
2. **Actions**: Actions are plain JavaScript objects that represent some intention to change the state. They must have a **`type`** property indicating the type of action being performed. Actions are dispatched to the store.
3. **Reducers**: Reducers are pure functions responsible for specifying how the application's state changes in response to actions. They take the previous state and an action, and return the new state.
4. **State**: The state represents the data of your application at a specific point in time. In Redux, the state is immutable, meaning it cannot be changed directly. Instead, when the state needs to be updated, a new state object is created based on the previous state and the action dispatched.
5. **Dispatch**: Dispatch is a function used to send actions to the Redux store. When an action is dispatched, the store invokes the corresponding reducer(s), which then updates the state accordingly.
6. **Middleware**: Middleware provides a third-party extension point between dispatching an action and the moment it reaches the reducer. It's useful for logging actions, performing asynchronous tasks, routing, and more.
7. **Selectors**: Selectors are functions used to extract specific pieces of data from the store's state. They help in keeping the component logic decoupled from the shape of the state.
8. **Subscription**: Redux provides a **`subscribe()`** method to add listeners to the store. These listeners are invoked whenever the state in the store changes, allowing components to react to those changes.

By following these concepts, Redux provides a predictable state management solution for JavaScript applications, making it easier to develop and maintain complex application states.

## Where is Redux stored?

Redux keeps the state of the entire application in a single object, called the store. This store is a JavaScript object that provides methods for updating that state. The Redux store is created using the createStore function from the Redux library.

## Why is Redux good with React?

Redux was originally designed to be used with React, so Redux is certainly good with React. The two libraries are often used together to build complex web applications.

For example, the Redux library includes a set of utility functions that make it easy to integrate Redux with React. The connect function is one example. Using connect, you can connect a React component to the Redux store. This allows the component to receive updates to the store’s state as props. This makes it easy to use Redux to manage state for React components.

Redux can also be used with other JavaScript frameworks though, **even with vanilla JavaScript**.

## What is Redux Thunk?

Redux Thunk is a solution for handling asynchronous code with Redux. Instead of returning an action, Redux Thunk allows you to write action creators that return a function. This means you can now perform an asynchronous action, like making an API call, before dispatching an action.

To use Redux Thunk, you need to install it as a dependency and apply it to your Redux store using the applyMiddleware function.

## Redux Inside My Head

I will not explain the concept of Redux itself, but I will mention the important points about Redux.

- Redux is a global state
- Redux is not necessary for every project.
- You may need Redux if you don't want to do props drilling (passing props too deep).
- If you are still confused about Redux, just think about the React state. The only difference is you can access the state from anywhere.