# RTK Query Overview

`CreatedAt- 24 Jan 2025 / RevisedAt-`

Web applications normally need to fetch data from a server in order to display it. They also usually need to make updates to that data, send those updates to the server, and keep the cached data on the client in sync with the data on the server. This is made more complicated by the need to implement other behaviors used in today's applications:

- Tracking loading state in order to show UI spinners
- Avoiding duplicate requests for the same data
- Optimistic updates to make the UI feel faster
- Managing cache lifetimes as the user interacts with the UI

RTK Query takes inspiration from other tools that have pioneered solutions for data fetching, like Apollo Client, React Query, Urql, and SWR, but adds a unique approach to its API design:

- The data fetching and caching logic is built on top of Redux Toolkit's `createSlice` and `createAsyncThunk` APIs
- Because Redux Toolkit is UI-agnostic, RTK Query's functionality can be used with any UI layer
- API endpoints are defined ahead of time, including how to generate query parameters from arguments and transform responses for caching
- RTK Query can also generate React hooks that encapsulate the entire data fetching process, provide `data` and `isLoading` fields to components, and manage the lifetime of cached data as components mount and unmount
- RTK Query provides "cache entry lifecycle" options that enable use cases like streaming cache updates via websocket messages after fetching the initial data
- We have early working examples of code generation of API slices from OpenAPI and GraphQL schemas
- Finally, RTK Query is completely written in TypeScript, and is designed to provide an excellent TS usage experience

## What's included

RTK Query is included within the installation of the core Redux Toolkit package. It is available via either of the two entry points below:

```jsx
import { createApi } from '@reduxjs/toolkit/query'

/* React-specific entry point that automatically generates
   hooks corresponding to the defined endpoints */
import { createApi } from '@reduxjs/toolkit/query/react'
```

RTK Query includes these APIs:

- `createApi()`: The core of RTK Query's functionality. It allows you to define a set of "endpoints" that describe how to retrieve data from backend APIs and other async sources, including the configuration of how to fetch and transform that data. In most cases, you should use this once per app, with "one API slice per base URL" as a rule of thumb.
- `fetchBaseQuery()`: A small wrapper around `fetch` that aims to simplify requests. Intended as the recommended `baseQuery` to be used in `createApi` for the majority of users.
- `<ApiProvider />`: Can be used as a `Provider` if you **do not already have a Redux store**.
- `setupListeners()`: A utility used to enable `refetchOnMount` and `refetchOnReconnect` behaviors.

## Create an API Slice

For typical usage with React, start by importing `createApi` and defining an "API slice" that lists the server's base URL and which endpoints we want to interact with:

```jsx
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

export const apiSlice = createApi({
  reducerPath: "api",
  baseQuery: fetchBaseQuery({
    baseUrl: "https://jsonplaceholder.typicode.com/",
  }),
  endpoints: (builder) => ({
    fetchTodos: builder.query({
      query: () => "todos",
    }),
  }),
});

export const { useFetchTodosQuery } = apiSlice;
```

## Configure the Store

The "API slice" also contains an auto-generated Redux slice reducer and a custom middleware that manages subscription lifetimes. Both of those need to be added to the Redux store:

```jsx
import { configureStore } from "@reduxjs/toolkit";
import { apiSlice } from "../features/api/api-slice";

const store = configureStore({
  reducer: {
    [apiSlice.reducerPath]: apiSlice.reducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(apiSlice.middleware),
});

export default store;
```

## Use Hooks in Components

Finally, import the auto-generated React hooks from the API slice into your component file, and call the hooks in your component with any needed parameters. RTK Query will automatically fetch data on mount, re-fetch when parameters change, provide `{data, isFetching}` values in the result, and re-render the component as those values change:

```jsx
import { useFetchTodosQuery } from "./features/api/api-slice";

export default function App() {
  const { data, error, isLoading } = useFetchTodosQuery();

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (!isLoading && error) {
    return <div>Error: {error}</div>;
  }

  if (!isLoading && data) {
    return (
      <div>
        <h1>Todo List</h1>
        <ul>
          {data.map((todo) => (
            <li key={todo.id}>{todo.title}</li>
          ))}
        </ul>
      </div>
    );
  }
}
```