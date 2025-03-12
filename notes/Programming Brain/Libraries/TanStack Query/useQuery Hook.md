# useQuery Hook

---

useQuery is a custom hook within React Query used to fetch data in a React application. Under the hood, these hooks manage lots of things such as caching data after the initial fetch, re-fetching data in the background, etc.

Well clean the App.js and write the `fetchUsers` function to fetch data from the API. I’m using `fetch()`, but we can use Axios or other methods, as well.

```jsx
const fetchUsers = async () => {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  return res.json();
};
```

Now, import the `useQuery` from `react-query`.

```jsx
import { useQuery } from "@tanstack/react-query";
```

## How to Fetch Data With useQuery

And now we can use `useQuery` hook to manage the data fetching, as below:

```jsx
const response = useQuery({queryKey: ["users"], queryFn: fetchUsers});
```

A `useQuery` hook requires at least two arguments. The first one is a key for the query. I’m using the string `“users”` for that. We can also put an array as the first argument. If an array is passed, each item will be serialized into a stable query key. The second one is a function to fetch the data. I put the `fetchUsers` asynchronous function I created earlier.

The response useQuery returns is really important. It contains the following properties.

```jsx
{
	data,
  dataUpdatedAt,
  error,
  errorUpdatedAt,
  failureCount,
  isError,
  isFetched,
  isFetchedAfterMount,
  isFetching,
  isIdle,
  isLoading,
  isLoadingError,
  isPlaceholderData,
  isPreviousData,
  isRefetchError,
  isRefetching,
  isStale,
  isSuccess,
  refetch,
  remove,
  status,
}
```

useQuery also accepts aothers arguments

```jsx
{
  cacheTime,
  enabled,
  initialData,
  initialDataUpdatedAt
  isDataEqual,
  keepPreviousData,
  meta,
  notifyOnChangeProps,
  notifyOnChangePropsExclusions,
  onError,
  onSettled,
  onSuccess,
  placeholderData,
  queryKeyHashFn,
  refetchInterval,
  refetchIntervalInBackground,
  refetchOnMount,
  refetchOnReconnect,
  refetchOnWindowFocus,
  retry,
  retryOnMount,
  retryDelay,
  select,
  staleTime,
  structuralSharing,
  suspense,
  useErrorBoundary,
}
```

`Data` is the actual data we fetched, and status will either be `loading`, `error`, `success` or `idle`, according to the response. And all these properties have different uses.

For example, let’s use only the `data` and `status` properties. So we’ll deconstruct the useQuery response:

```jsx
const { data: users, error, isLoading } = useQuery({queryKey: ["users"], queryFn: fetchUsers});
```

Now, we can use `data` to display them in the browser. Here is the complete code:

```jsx
import { useQuery } from "react-query";

const fetchUsers = async () => {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  return response.json();
};

export default function Users() {
  const { data: users, error, isLoading } = useQuery({queryKey: ["users"], queryFn: fetchUsers});

  if (isLoading) return <div>Fetching users...</div>;
  if (error) return <div>An error Occurred: {error.message}</div>;

  return (
    <div>{users && users.map((user) => <p key={user.id}>{user.name}</p>)}</div>
  );
}
```

## Configuring Stale Time & Cache Time For a Particular API Request

```jsx
const { data: users, error, isLoading } = useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
  staleTime: 10 * (60 * 1000),  // 10 mins
  cacheTime: 15 * (60 * 1000),  // 15 mins
});
```

## Configuring StaleTime & CacheTime Globally

So if you want all of your data to be considered fresh for longer - you can! Instead of changing cacheTime and staleTime on useQuery, you'll set it on the QueryClient.

```jsx
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 10*(60*1000), // 10 mins
      cacheTime: 15*(60*1000), // 15 mins
    },
  },
});
```

## The main key difference between staleTime & cacheTime

1. staleTime determines how long React Query considers data fresh and usable without triggering a new fetch.
2. cacheTime determines how long the data remains in the cache before it's removed.

## Automatically refetching with React Query

A super cool feature of React Query is that we can auto refetch on a specified interval.

This could be useful if you have quickly changing data that needs to be rechecked every minute.

To use the auto refetch mode, you can pass an optional parameter to the React Query hook called `refetchInterval`. The value is in milliseconds.

```jsx
const { data: users, error, isLoading } = useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
  refetchInterval: 6000,  // 6 seconds
});
```

This call will refetch the data every 6000 milliseconds.

When implementing code like this, be aware that this can be heavy on your API's and one should be very wise about when to use this approach.

## Other refetching options

React Query comes with more of these refetch functions that we can leverage.

By default, it will auto refetch every time the window focusses, for instance, let's take a look at what other options there are:

- `refetchInterval`: See above example
- `refetchIntervalInBackground`: When set to true, the above function will even call when the tab is in the background
- `refetchOnMount`: You can set this to false to don't do the initial mount loading
- `refetchOnWindowFocus`: Will refetch every time the window focus is set. You can set this to false
- `refetchOnReconnect`: Will refetch once a connection has been remade

Between all of these, you can mix when data should be loaded.