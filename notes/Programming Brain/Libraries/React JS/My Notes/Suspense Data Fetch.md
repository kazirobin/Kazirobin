# Suspense Data Fetch

Managing data loading in a frontend application can become complex over time, so much so that there is a whole ecosystem of libraries dedicated to state management. The React core team have responded by releasing a set of concurrent features to make data fetching in React easier. [Suspense](https://react.dev/reference/react/Suspense) is among these features, and it aims to simplify managing loading states in React components.

## What is React Suspense?

Suspense is a feature for managing asynchronous operations in a React app. It lets your components communicate to React that they are waiting for some data. It is important to note that Suspense is not a data fetching library like react-async, nor is it a way to manage state like Redux. It simply lets you render a fallback declaratively while a component is waiting for some asynchronous operation (i.e., a network request) to be completed.

As we’ll see further down, this allows us to synchronize loading states across different components to allow for a better user experience. Suspense does this in a non-intrusive way that doesn’t require a complete rewrite of existing applications.

## How to use Suspense

Let’s look at the simplest use case of Suspense, which is handling a pending network request in a component:

```jsx
const [todos, isLoading] = fetchData('/todos')

if (isLoading) {
  return <Spinner />
}

return <Todos data={todos} />
```

This should look familiar, as it is how most people (me included) handle waiting for network calls. The implementation of the `fetchData` function, and the `Spinner` and `Todos` components is not relevant here.

The `isLoading` variable is used to track the status of the request. If `true`, we render a spinner to communicate this state to the user. There’s nothing wrong with doing it this way, but let’s see how we would handle this using Suspense:

```jsx
const todos = fetchData('/todos')

return (
  <Suspense fallback={<Spinner />}>
    <Todos data={todos} />
  </Suspense>
)
```

There’s a subtle but important change to the code. Instead of having the loading state as a state variable with logic to render a spinner based on the value, it’s instead being managed by React using Suspense. We’re now rendering a fallback declaratively.

In the previous example, React had no knowledge of the network call, so we had to manage the loading state using the `isLoading` variable. With this example, React knows that a network call is happening, and by wrapping the `Todos` component in Suspense, it delays rendering it until the network call is done.

Another important thing to note is the `fallback` property passed to Suspense. This is whatever we want to render while waiting for the network call to finish. It could be a spinner, skeleton loader, or nothing. React will render whatever the value of `fallback` is while waiting for the network request to finish.

But how exactly does React know that a network call is pending? As far as we’ve reviewed, Suspense only renders a fallback component while waiting. Where in the code do we communicate to React that we’re making a network call?

**This is where the data fetching libraries come in. Currently, Relay and SWR have integrations with Suspense to communicate loading states to React. I imagine more library authors will add integrations in the future.**

Now, let’s explore some common data fetching approaches, their limitations, and how Suspense improves the developer and user experience.

## React data fetching patterns

Using the fetch-on-render approach, the network request is triggered in the component itself after mounting. The reason it’s called fetch-on-render is because the request isn’t triggered until the component renders:

```jsx
const App = () => {
  const [userDetails, setUserDetails] = useState({})

  useEffect(() => {
    fetchUserDetails().then(setUserDetails)
  }, [])

  if (!userDetails.id) return <p>Fetching user details...</p>

  return (
    <div className="app">
      <h2>Simple Todo</h2>

      <UserWelcome user={userDetails} />
      <Todos />
    </div>
  )
}
```

A major drawback to this is that it can lead to a network waterfall problem. This is because every component has an async fetch request. If this component renders another component with similar fetch requests, it will result in multiple, nested waterfall-like requests that cause performance issues.

## Fetch-then-render

The fetch-then-render approach allows us to make an async request before the component is rendered. Let’s go back to the previous example and see how we would fix it:

```jsx
const fetchDataPromise = fetchUserDetailsAndTodos() // We start fetching here
const App = () => {
  const [userDetails, setUserDetails] = useState({})
  const [todos, setTodos] = useState([])

  useEffect(() => {
    fetchDataPromise.then((data) => {
      setUserDetails(data.userDetails)
      setTodos(data.todos)
    })
  }, [])

  return (
    <div className="app">
      <h2>Simple Todo</h2>

      <UserWelcome user={userDetails} />
      <Todos todos={todos} />
    </div>
  )
}
```

In this case, we’ve moved the fetching logic outside of the `App` component so that the network request begins before the component is even mounted.

Inspecting the networks tab clearly shows that both requests are started at the same time. While both `fetchUserDetails` and `fetchTodos()` are started in parallel, we would still need to wait for the slower request between the two to complete before we render any useful data. This is because `Promise.all` waits until all the promises are resolved before resolving.

## Data fetching using Suspense

We have seen how trivial data fetching patterns aren’t always very performant, and have issues when dealing with async calls. This is where we can tap into Suspense, which allows us to begin rendering our component immediately after triggering the network request. This particular data fetching pattern is called render-as-you-fetch.

As the name suggests, we are rendering UI consecutively as we fetch data from an API. This means that, just like fetch-then-render, we kick off fetching before rendering, but we don’t have to wait for a response before we start rendering. Let’s look at some code:

```jsx
const data = fetchData() // this is not a promise (we'll implement something similar)

const App = () => (
  <>
    <Suspense fallback={<p>Fetching user details...</p>}>
      <UserWelcome />
    </Suspense>

    <Suspense fallback={<p>Loading todos...</p>}>
      <Todos />
    </Suspense>
  </>
)

const UserWelcome = () => {
  const userDetails = data.userDetails.read()
  // code to render welcome message
}

const Todos = () => {
  const todos = data.todos.read()
  // code to map and render todos
}
```

When `App` mounts for the first time, it tries to render `UserWelcome` first, and this triggers the `data.userDetails.read()` line. If the data isn’t ready yet (i.e., the request hasn’t resolved), it is communicated back to Suspense, which then renders `<p>Fetching user details…</p>`. The same thing happens for `Todos`.

The best thing about this pattern is that no component has to wait for others to finish, which improves response time.

## Structuring the API folder

Now, we can create our `API` folder where we will be writing most of our logic. In this folder, there will be two files. The first is `wrapPromise.js`, which is simply a wrapper for handling various Promise states. The second file is `fetchData.js` where we will fetch from an actual `URL` endpoint.

### **`wrapPromise.js`**

This is probably the most important part of this whole tutorial because `wrapPromise.js` is what communicates with Suspense, and what any library author writing abstractions for the Suspense API would spend most of their time on.

`wrapPromise.js` is a wrapper that wraps over a Promise and provides a method that allows you to determine whether the data being returned from the Promise is ready to be read. If the Promise resolves, it returns the resolved data. If it rejects, it throws the error. And if it is still pending, it throws back the Promise.

This Promise argument is usually going to be a network request to retrieve some data from an API, but it could technically be any Promise object. The actual implementation is left for whoever is implementing it to figure out, so you could probably find other ways to do it.

The `wrapPromise.js` function has the following requirements:

1. It takes in a Promise as an argument
2. When the Promise is resolved, it returns the resolved value
3. When the Promise is rejected, it throws the rejected value
4. When the Promise is still pending, it throws back the Promise
5. It exposes a method to read the status of the Promise

With the requirements defined, it’s time to write some code. Open the `api/wrapPromise.js` file and we can get started:

```jsx
function wrapPromise(promise) {
  let status = 'pending'
  let response

  const suspender = promise.then(
    (res) => {
      status = 'success'
      response = res
    },
    (err) => {
      status = 'error'
      response = err
    },
  )

...to be continued...
```

What’s happening here? Inside the `wrapPromise.js` function, we’re defining two variables:

1. `status`: Tracks the status of the promise argument
2. `response`: Holds the result of the Promise (whether resolved or rejected)

`status` is initialized to `pending` by default, because that’s the default state of any new Promise. We then initialize a new variable, `suspender`, set its value to the Promise, and attach a `then` method to it.

Inside this `then` method, we have two callback functions: the first to handle the resolved value, and the second to handle the rejected value. If the Promise resolves successfully, we update the `status` variable to be `success` and set the `response` variable to the resolved value. If the Promise rejects, we update the `status` variable to be `error` and set the `response` variable to the rejected value:

```jsx
...continued from above...
  const read = () => {
    switch (status) {
      case 'pending':
        throw suspender
      case 'error':
        throw response
      default:
        return response
    }
  }

  return { read }
}

export default wrapPromise
```

Next, we create a new function called `read`, and inside this function, we have a `switch` statement that checks the value of the `status` variable. If the `status` of the promise is `pending`, we throw the `suspender` variable we just defined. If it is `error`, we throw the `response` variable. And, finally, if it is anything other than the two (i.e., `success`), we return the `response` variable.

The reason we throw either the `suspender` variable or the error `response` variable is because we want to communicate back to Suspense that the Promise is not yet resolved. We’re doing that by simulating an error in the component (using [`throw`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw)), which will be intercepted by the Suspense component. The Suspense component then looks at the thrown value to determine if it’s an actual error or a Promise.

If it is a Promise, the Suspense component will recognize that the component is still waiting for some data, and it will render the fallback. If it’s an error, it bubbles the error back up to the nearest [error boundary](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary) until it is either caught or it crashes the application.

At the end of the `wrapPromise.js` function, we return an object containing the `read` function as a method, and this is what our React components will interact with to retrieve the value of the Promise.

Lastly, we have a default export so that we can use the `wrapPromise.js` function in other files. Now let’s move on to the `fetchData.js` file.

### **`fetchData.js`**

Inside this file, we’ll create a function to fetch the data that our components require. It will return a Promise wrapped with the `wrapPromise.js` function we just reviewed:

```jsx
import wrapPromise from './wrapPromise'

function fetchData(url) {
  const promise = fetch(url)
    .then((res) => res.json())
    .then((res) => res.data)

  return wrapPromise(promise)
}

export default fetchData
```

The first thing we do here is import the `wrapPromise` function we created, and then define the `fetchData` function.

Inside this function, we initialize a new variable, `promise`, and set its value to a fetch request Promise. When this request is completed, we get the data from the `Response` object using `res.json()` and then return `res.data`, which contains the data that we need.

Finally, we pass this `promise` to the `wrapPromise` function and return it. At the end of this file, we export the `fetchData` function. Now on to the components!

## Building our app components

We now have the “backend” for our app ready, so it’s time to build out the components.

### `index.jsx`

`index.jsx` is the entry point of our application, and we’ll be creating it first. This is where we’ll mount our React app to the DOM:

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './components/App'

const mountNode = document.querySelector('#root')
ReactDOM.createRoot(mountNode).render(<App />)
```

Notice, we are using React 18, which means that the new `createRoot` API is being used.

### **`App.jsx`**

This is where we will import and use the majority of our components, wrapped in `Suspense` API. Here, we have used Suspense’s `fallback` for nearly every component that is supposed to fetch or deal with an asynchronous operation:

```jsx
import React, { Suspense } from 'react'

import UserWelcome from './UserWelcome'
import Todos from './Todos'

const App = () => {
  return (
    <div className="app">
      <h2>Simple Todo</h2>
      <Suspense fallback={<p>Loading user details...</p>}>
        <UserWelcome />
      </Suspense>
      <Suspense fallback={<p>Loading Todos...</p>}>
        <Todos />
      </Suspense>
    </div>
  )
}

export default App
```

### **`UserWelcome.jsx`**

`UserWelcome.jsx` is a component that renders username. Alternatively, you could have included this in `App.jsx` itself but for the sake of clean code, you can also modularize it:

```jsx
import React from 'react'
import fetchData from '../api/fetchData'

const resource = fetchData(
  'https://run.mocky.io/v3/d6ac91ac-6dab-4ff0-a08e-9348d7deed51'
)

const UserWelcome = () => {
  const userDetails = resource.read()

  return (
    <div>
      <p>
        Welcome <span className="user-name">{userDetails.name}</span>, here are
        your Todos for today
      </p>
      <small>Completed todos have a line through them</small>
    </div>
  )
}

export default UserWelcome
```

### **`Todos.jsx`**

This component reads `todos` and renders them on the UI:

```jsx
import React from 'react'
import fetchData from '../api/fetchData'

const resource = fetchData(
  'https://run.mocky.io/v3/8a33e687-bc2f-41ea-b23d-3bc2fb452ead'
)

const Todos = () => {
  const todos = resource.read()

  const renderTodos = todos.map((todo) => {
    const className = todo.status === 'Completed' ? 'todo-completed' : 'todo'
    return (
      <li className={`todo ${className}`} key={todo.id}>
        {todo.title}
      </li>
    )
  })

  return (
    <div>
      <h3>Todos</h3>
      <ol className="todos">{renderTodos}</ol>
    </div>
  )
}

export default Todos
```

Now that all our React components are in place, let’s look at how to manage rendering order with Suspense.

## Managing rendering order with Suspense

Imagine if the `Todos` component gets its data first, and you begin to go through the list only for `UserWelcome` to resolve a little while later. The new contents being rendered will push the existing todo contents down in an awkward way, and this could disorient your users:

![janky-loading-demo-app.gif](Suspense%20Data%20Fetch%201b2aeacbb299811da3d9c498c91c9050/janky-loading-demo-app.gif)

If you want the `Todos` component to render only when the `UserWelcome` component has finished rendering, then you could nest the `Suspense` component wrapping `Todos` like so:

```jsx
<Suspense fallback={<p>Loading user details...</p>}>
  <UserWelcome />
  <Suspense fallback={<p>Loading Todos...</p>}>
    <Todos />
  </Suspense>
</Suspense>
```

Another approach is to wrap both `Suspense` components in `SuspenseList` and specify a “reveal order,” like so:

```jsx
<SuspenseList revealOrder="forwards">
  <Suspense fallback={<p>Loading user details...</p>}>
    <UserWelcome />
  </Suspense>
  <Suspense fallback={<p>Loading Todos...</p>}>
    <Todos />
  </Suspense>
</SuspenseList>
```

This will cause React to render the components in the order they appear in your code, regardless of which one gets its data first:

![demo-app-top-down-loading.gif](Suspense%20Data%20Fetch%201b2aeacbb299811da3d9c498c91c9050/demo-app-top-down-loading.gif)

You can see how easy it becomes to organize your application’s loading states as opposed to having to manage `isLoading` variables yourself. A top-down loading style is much better.

## Handling errors in Suspense

We can even go a step further and add error handling capabilities to our application. Suspense provides an intuitive API to handle errors: Error Boundary. This API helps catch errors within the Suspense tree without affecting the rest of the React DOM nodes.

In a typical Suspense pattern, we are likely running an async operation using Promises. This Promise might not be resolved, and the Suspense boundary needs to take care of this scenario as well. This is where Error Boundary comes in to take care of a failed Promise state

To use Suspense effectively, we need to use Error Boundary. The official React docs provide an Error Boundary component that you can simply import in your component:

```jsx
import ErrorBoundary from "./errorboundary";

<ErrorBoundary fallback={<div>Failed to fetch data!</div>}>
  <Suspense fallback={<h3>Loading...</h3>}>
      // root component of our application
      <App />
  </Suspense>
</ErrorBoundary>
```

Notice how the entire app is wrapped in an `ErrorBoundary` component. This ensures a root-level error that will stop your entire app from rendering if the Promise fails.

There may be certain use cases where you want a global error boundary like we see above, such as when there is an internet connection interruption and you want to stop the entire to-do app.

However, in most cases, you want to delegate the error boundary close to each component only. This allows you to have component-wise error handling that doesn’t stop the entire app altogether or affect other DOM nodes from their usual operations:

[delegating-error-boundaries-graphic.avif](Suspense%20Data%20Fetch%201b2aeacbb299811da3d9c498c91c9050/delegating-error-boundaries-graphic.avif)