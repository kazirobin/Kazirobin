# Redux In React

`CreatedAt- 29 Feb 2024 / RevisedAt-`

Create a new React project by running the following command in your terminal. Replace *"your-project-name"* with the name of your project.

```bash
npm create vite@latest
```

The above command sequence will create a new React project using the Vite build tool and install all necessary dependencies.

## How to install Redux

Redux requires a few dependencies for its operations, namely:

- **Redux:** The core library enables the redux architecture.
- **React Redux:** Simplifies connecting your React components to the Redux store.
- **Redux Thunk:** Allows you to write asynchronous logic in your Redux actions.
- **Redux DevTools Extension:** Connects your Redux application to Redux DevTools

You can install them using npm, as shown below:

```bash
npm install redux react-redux
```

## How to set up reducers

Now let's create the reducer for our application.

In the `src/services` directory, create a new folder called `reducers`, and inside that folder, create two new files: `index.js` and `taskReducer.js`.

The `index.js` file represents the root reducer, which combines all the individual reducers in the application. In contrast, the `taskReducer.js` file is one of the individual reducers that will be combined in the root reducer.

```jsx
import taskReducer from "./taskReducer";
import { combineReducers } from "redux";

const rootReducer = combineReducers({
  tasks: taskReducer,
});

export default rootReducer;
```

In the above `index.js` file, we use the `combineReducers` function to combine all the individual reducers into a single root reducer. In this case, we only have one reducer (`taskReducer`), so we pass it in as an argument to `combineReducers`.

The resulting combined reducer is then exported so that other files in the application can import and use it to create the store.

Here's the code for `taskReducer`:

```jsx
const initialState = {
  tasks: []
};

const taskReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'ADD_TASK':
      return {
        ...state,
        tasks: [...state.tasks, action.payload]
      };
    case 'DELETE_TASK':
      return {
        ...state,
        tasks: state.tasks.filter(task => task.id !== action.payload)
      };
    default:
      return state;
  }
};

export default rootReducer;
```

Inside the above `taskReducer.js` file, we define a reducer function that takes two arguments: `state` and `action`. The `state` argument represents the current state of the application, while the `action` argument represents the action being dispatched to update the state.

The `switch` statement inside the reducer handles different cases based on the "type" of the action. For example, if the action type is `ADD_TASK`, the reducer returns a new state object with a new task added to the `tasks` array. And if the action type is `DELETE_TASK`, the reducer returns a new state object with the current tasks filtered to remove the task with the specified `id`.

## How to create the Redux store

Now that we have our basic setup ready, let's create a new file called `store.js` in the `src/app` directory. This is where you'll define your Redux store:

```jsx
import { createStore} from "redux";
import taskReducer from "./reducers/taskReducer";

const store = createStore(taskReducer);

export default store;
```

The code above sets up a Redux store by creating a new instance of the store using the `createStore` function. Then, the rootReducer – which combines all the application's reducers into a single reducer – is passed as an argument to `createStore`.

## How to connect the Redux Store to the application

To connect the Redux store to the ToDo application, we need to use the `Provider` component from the `react-redux` library.

First, we import the `Provider` function and the Redux store we created into our `main.jsx`. Then, we wrap our `App` component with the `Provider` function and pass the `store` as a prop. This makes the Redux store available to all the components inside the `App`.

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./index.css";

import { Provider } from "react-redux";
import store from "./store";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

## How to set up Redux Actions

Now that we have everything set up, let's create our actions. As I mentioned before, actions represent something that happened in the application. For example, when a user adds a new task, it triggers an "add task" action. Similarly, when a user deletes a task, it triggers a "delete task" action

To create the actions, create a new folder called `actions` in the `src/services` directory and then create a new file called `index.js`. This file will contain all of the action creators for our application.

```jsx
export const addTodo = (text) => {
  return {
    type: "ADD_TASK",
    payload: {
      id: new Date().getTime(),
      text: text,
    },
  };
};

export const deleteTodo = (id) => {
  return {
    type: "DELETE_TASK",
    payload: id,
  };
};
```

The above code exports two action creators: `addTodo` and `deleteTodo`. These functions return an object with a `type` property that describes the action that has occurred.

In the case of `addTodo`, the `type` property is set to `"ADD_TASK"`, indicating that a new task has been added. The `payload` property contains an object with the new task's `id` and `text` values. The `id` is generated using the `new Date().getTime()` method creates a unique identifier based on the current timestamp.

In the case of `deleteTodo`, the `type` property is set to `"DELETE_TASK"`, indicating that a task has been deleted. The `payload` property contains the `id` of the task to be deleted.

These action creators can be dispatched to the Redux store using the `dispatch()` method, which will trigger the corresponding reducer function to update the application state accordingly.

## How to dispatch actions

Now that we have created the necessary actions, we can move on to creating the components that will dispatch these actions.

Let's create a new folder named "components" inside the *src* directory. Inside this folder, we will create two new files: `Task.jsx` and `TaskList.jsx`.

The `Task.jsx` component will be responsible for adding tasks. But before we proceed, we need to import the following into the file:

- *addTodo action*: To add new tasks to the state.
- *useDispatch hook*: To dispatch the `addTodo` action.
- *useRef*: ****Allows us to obtain a reference to HTML elements.

```jsx
import { useRef } from "react";
import { useDispatch } from "react-redux";
import { addTodo } from "../actions";
```

Once we have imported these necessary components, we can proceed to write code for `Task.jsx`.

```jsx
const Task = () => {
  const dispatch = useDispatch();
  const inputRef = useRef(null);

  function addNewTask() {
    const task = inputRef.current.value.trim();
    if (task !== "") {
      dispatch(addTodo(task));
      inputRef.current.value = "";
    }
  }

  return (
    <div className="task-component">
      <div className="add-task">
        <input
          type="text"
          placeholder="Add task here..."
          ref={inputRef}
          className="taskInput"
        />
        <button onClick={addNewTask}>Add task</button>
      </div>
    </div>
  );
};

export default Task;
```

In the code above, we created a component consisting of an input field and a button. When a user clicks on the "Add task" button, the `addNewTask` function is executed. This function uses the `useRef` hook to obtain the input field's value, removes any leading or trailing whitespaces, and then dispatches the `addTodo` action with the new task as the payload.

Now, let's move on to the `TaskList.jsx` component, responsible for rendering the list of tasks and handling task deletions. To achieve this, we need to import the following:

- The **useSelector hook** provides access to the state from the Redux store.
- The **deleteTodo action**, is responsible for removing a task from the list of tasks in the Redux store

```jsx
import { useSelector, useDispatch } from "react-redux";
import { deleteTodo } from "../actions";
```

We will now write code for `TaskList.jsx` that maps over the tasks array and renders each task:

```jsx
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { deleteTodo } from '../actions';

const TaskList = () => {
  const tasks = useSelector((state) => state.tasks);
  const dispatch = useDispatch();

  const handleDelete = (id) => {
    dispatch(deleteTodo(id));
  };

  return (
    <div className="tasklist">
      <div className="display-tasks">
        <h3>Your tasks:</h3>
        <ul className="tasks">
          {tasks.map((task) => (
            <li className="task" key={task.id}>
              {task.text}
              <button
                className="delete-btn"
                onClick={() => handleDelete(task.id)}
              >
                delete
              </button>
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
};

export default TaskList;
```

Here, the component loops over each task in the tasks array and displays text and a delete button. When the user clicks the delete button, the `handleDelete` function is called, dispatching the `deleteTodo` action with the task's `id` as the payload.

Finally, import the components into your `App.jsx` file and render them.

```jsx
import Task from "./components/Task";
import TaskList from "./components/TaskList";

function App() {
  return (
    <div className="App">
      <Task />
      <TaskList />
    </div>
  );
}

export default App;
```

[Redux Toolkit](Redux%20In%20React%201b2aeacbb2998132b9ecf5d308a63ae6/Redux%20Toolkit%201b2aeacbb29981a0a1a3c793d9370624.md)

[Redux Toolkit & **`Async Thunk`**](Redux%20In%20React%201b2aeacbb2998132b9ecf5d308a63ae6/Redux%20Toolkit%20&%20Async%20Thunk%201b2aeacbb29981fca18fc4c63db8a7da.md)