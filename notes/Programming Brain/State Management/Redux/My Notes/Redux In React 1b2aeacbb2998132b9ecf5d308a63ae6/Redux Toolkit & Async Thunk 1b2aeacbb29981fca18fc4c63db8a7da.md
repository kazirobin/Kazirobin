# Redux Toolkit & Async Thunk

`CreatedAt- 29 Feb 2024 / RevisedAt-`

Redux Toolkit is a library designed to simplify common Redux use cases. One of the standout features of Redux Toolkit is its handling of asynchronous logic with `createAsyncThunk`. An async thunk represents a function that can be dispatched to Redux and perform asynchronous operations.

## What is a thunk?

Before we delve into async thunks, let’s understand what a thunk is. A thunk is a function that wraps an expression to delay its evaluation. In Redux, thunks are used to handle side effects, like API calls.

## Setting up Redux Toolkit

Firstly, ensure you have set up Redux Toolkit in your project:

```bash
npm install @reduxjs/toolkit react-redux
```

## Async Thunk Basics

With Redux Toolkit’s `createSlice` and `createAsyncThunk`, we can easily manage actions, reducers, and asynchronous operations.

Here’s the basic structure of an async thunk:

Create a file name `src/features/posts/postsSlice.js`

```jsx
import { createAsyncThunk } from "@reduxjs/toolkit";
import { getPosts } from "./api";

export const fetchPosts = createAsyncThunk("posts/fetchPosts", async () => {
  const posts = await getPosts();
  return posts;
});
```

Create a file name `src/features/posts/api.js`

```jsx
export async function getPosts() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  return response.json();
}
```

This function fetches user data based on a given ID. When dispatched, it automatically manages three action types:

1. posts/fetchPosts/pending
2. posts/fetchPosts/fulfilled
3. posts/fetchPosts/rejected

## Handling Actions in a Slice

The associated slice might look like this: `src/features/posts/postsSlice.js`

```jsx
import { createAsyncThunk, createSlice } from "@reduxjs/toolkit";
import { getPosts } from "./api";

const initialState = {
  posts: [],
  isLoading: false,
  isError: false,
  error: null,
};

export const fetchPosts = createAsyncThunk("posts/fetchPosts", async () => {
  const posts = await getPosts();
  return posts;
});

const postsSlice = createSlice({
  name: "posts",
  initialState,
  extraReducers: (builder) => {
    builder.addCase(fetchPosts.pending, (state) => {
      state.isError = false;
      state.isLoading = true;
    });
    builder.addCase(fetchPosts.fulfilled, (state, action) => {
      state.isLoading = false;
      state.posts = action.payload;
    });
    builder.addCase(fetchPosts.rejected, (state, action) => {
      state.isLoading = false;
      state.isError = true;
      state.error = action.error?.message;
    });
  },
});

export default postsSlice.reducer;
```

Notice how `extraReducers` handle each of the three action types the async thunk can dispatch.

## Using Async Thunks in Components

Dispatching and selecting data is straightforward:

```jsx
import { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import { fetchPosts } from "../features/posts/postsSlice";

export default function Posts() {
  const { posts, error, isLoading, isError } = useSelector(
    (state) => state.posts
  );

  const dispatch = useDispatch();

  useEffect(() => {
    dispatch(fetchPosts());
  }, [dispatch]);

  if (isLoading) return <h1>Loading...</h1>;
  if (!isLoading && isError) return <h1>{error}</h1>;
  if (!isLoading && !isError && posts.length === 0) {
    return <h1>No posts found</h1>;
  }

  if (!isLoading && !isError && posts.length > 0) {
    return (
      <ul>
        {posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    );
  }
}
```