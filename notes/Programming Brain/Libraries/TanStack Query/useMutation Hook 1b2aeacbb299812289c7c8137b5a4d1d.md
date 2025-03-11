# useMutation Hook

React Query is a popular library in the React community. It’s known for its efficient and intuitive approach to server state management.

While many are familiar with its querying capabilities, React Query also offers tools for handling mutations - changes to your server data. One such tool is the useMutation hook. In this post, we'll delve into the workings of useMutation and talk about why it’s important.

## What is React Query useMutation?

useMutation is a hook provided by React Query that helps you handle server-side mutations like `POST`, `PUT`, `DELETE` requests, etc. Beyond just making the request, it provides out-of-the-box functionalities for managing local UI state, handling optimistic updates, and even retrying failed mutations.

## How useMutation differs from traditional approaches

While React’s built-in hooks like useState and useEffect can be used to handle server state, useMutation abstracts away a lot of the complexities. Unlike traditional methods which require manual management of loading states, error states, and cache updates, useMutation provides these features out-of-the-box, which leads to cleaner code that’s easier to maintain.

## How to implement React Query useMutation

Setting up a mutation in React Query is quite simple. Here's a basic example:

```jsx
import { useMutation} from "@tanstack/react-query";
import axios from "axios";

export default function MyComponent() {
  const mutation = useMutation({
    mutationFn: (newProduct) =>
      axios.post("http://localhost:3000/products", newProduct),
  });

  return (
    <button onClick={() => mutation.mutate({ id: 1, title: "New Product" })}>
      Add New Data
    </button>
  );
}
```

In the above example, when the button is clicked, a POST request is made to `http://localhost:3000/products`

## Feedback and UI states

One significant advantage of React Query `useMutation` is the immediate feedback on the mutation's status. It provides status flags like `isLoading`, `isError`, and `data` that can be used to update the UI accordingly.

```jsx
if (mutation.isLoading) return 'Submitting...';
if (mutation.isError) return 'An error occurred';
if (mutation.isSuccess) return `Data added: ${mutation.data.name}`;
```

## Optimistic updates

To make apps feel faster, it's a common practice to update the UI optimistically before a server response is received. `useMutation` makes this straightforward with the `onMutate` and `onError` callbacks.

```jsx
const mutation = useMutation({
    mutationFn: (newProduct) =>
      axios.post("http://localhost:3000/products", newProduct),
    onMutate: (newData) => {
      // Optimistically update the UI here
    },
    onError: (error, variables, context) => {
      // Rollback the optimistic update in case of an error
    },
  });
```

## Invalidating and refetching after mutation

React Query allows seamless integration between queries and mutations. After a successful mutation, you often want to refetch some queries to keep the data in sync. Using the previously discussed `invalidateQueries`, this is pretty easy to do:

```jsx
import { useMutation, useQueryClient } from "@tanstack/react-query";

const queryClient = useQueryClient();

  const mutation = useMutation({
    mutationFn: (newProduct) =>
      axios.post("http://localhost:3000/products", newProduct),
    onSuccess: () => {
      queryClient.invalidateQueries(["products"]);
    },
  });
```

## Mutation side effects

**If we want to directly update the data at any point in the mutation lifecycle, `useMutation` provides us with `callback` functions for side effects:**

1. **`onMutate`: Fires before the mutation function fires**
2. **`onError`: Will fire if the mutation fails**
3. **`onSuccess`: Fires when the mutation is successful**
4. **`onSettled`: Will fire when the mutation succeeds or fails**

As an example, let’s say we have a return greeting message before mutation.

```jsx
const queryClient = useQueryClient();

  const mutation = useMutation({
    mutationFn: (newProduct) =>
      axios.post("http://localhost:3000/products", newProduct),
    onSuccess: (data, variables, context) => {
      console.log(context);
      queryClient.invalidateQueries(["products"]);
    },
    onMutate: () => {
      return { greeting: "Say hello" };
    },
  });
```