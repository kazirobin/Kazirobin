# Redux In JavaScript

`CreatedAt- 29 Feb 2024 / RevisedAt-`

Using Redux in vanilla JavaScript involves setting up the Redux store, defining actions, reducers, and dispatching actions to update the state. Here's a basic example to illustrate how to use Redux in vanilla JavaScript

First, install Redux using npm or include it via a CDN.

```bash
npm install redux
```

or use a CDN

```html
<script src="https://unpkg.com/redux/dist/redux.min.js"></script>
```

**Setting up Redux Store:** First, you need to create the Redux store using the **`createStore()`** function from Redux.

```jsx
import { createStore } from 'redux';

// Define initial state
const initialState = {
  count: 0
};

// Define reducer function
function reducer(state = initialState, action) {
  switch(action.type) {
    case 'INCREMENT':
      return { ...state, count: state.count + 1 };
    case 'DECREMENT':
      return { ...state, count: state.count - 1 };
    default:
      return state;
  }
}

// Create Redux store
const store = createStore(reducer);
```

**Defining Actions:** Define action creators, which are functions that return action objects.

```jsx
function increment() {
  return { type: 'INCREMENT' };
}

function decrement() {
  return { type: 'DECREMENT' };
}
```

**Dispatching Actions:** Dispatch actions to the Redux store to update the state.

```jsx
// Dispatch actions
store.dispatch(increment());
store.dispatch(decrement());
```

**Subscribing to Store Changes:** Subscribe to the Redux store to be notified of state changes.

```jsx
// Subscribe to store changes
store.subscribe(() => {
  console.log('Current state:', store.getState());
});
```

When you run this code, you should see the current state logged to the console after each dispatch. This demonstrates the basic usage of Redux in vanilla JavaScript.