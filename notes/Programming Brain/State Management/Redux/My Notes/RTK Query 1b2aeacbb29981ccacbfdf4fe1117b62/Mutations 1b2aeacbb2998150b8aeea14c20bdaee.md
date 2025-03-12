# Mutations

Mutations are used to send data updates to the server and apply the changes to the local cache. Mutations can also invalidate cached data and force re-fetches.

## Defining Mutation Endpoints

Mutation endpoints are defined by returning an object inside the `endpoints` section of `createApi`, and defining the fields using the `build.mutation()` method.

Mutation endpoints should define either a `query` callback that constructs the URL (including any URL query params), or a `queryFn` callback that may do arbitrary async logic and return a result. The `query` callback may also return an object containing the URL, the HTTP method to use and a request body.

If the `query` callback needs additional data to generate the URL, it should be written to take a single argument. If you need to pass in multiple parameters, pass them formatted as a single "options object".

Mutation endpoints may also modify the response contents before the result is cached, define "tags" to identify cache invalidation, and provide cache entry lifecycle callbacks to run additional logic as cache entries are added and removed.

When used with TypeScript, you should supply generics for the return type and the expected query argument: `build.mutation<ReturnType, ArgType>`. If there is no argument, use `void` for the arg type instead.

```jsx
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query'

const api = createApi({
  baseQuery: fetchBaseQuery({
    baseUrl: '/',
  }),
  tagTypes: ['Post'],
  endpoints: (build) => ({
    // The mutation accepts a `Partial<Post>` arg, and returns a `Post`
    updatePost: build.mutation({
      // note: an optional `queryFn` may be used in place of `query`
      query: ({ id, ...patch }) => ({
        url: `post/${id}`,
        method: 'PATCH',
        body: patch,
      }),
      // Pick out data and prevent nested properties in a hook or selector
      transformResponse: (response, meta, arg) => response.data,
      // Pick out errors and prevent nested properties in a hook or selector
      transformErrorResponse: (response, meta, arg) => response.status,
      invalidatesTags: ['Post'],
      // onQueryStarted is useful for optimistic updates
      // The 2nd parameter is the destructured `MutationLifecycleApi`
      async onQueryStarted(
        arg,
        { dispatch, getState, queryFulfilled, requestId, extra, getCacheEntry },
      ) {},
      // The 2nd parameter is the destructured `MutationCacheLifecycleApi`
      async onCacheEntryAdded(
        arg,
        {
          dispatch,
          getState,
          extra,
          requestId,
          cacheEntryRemoved,
          cacheDataLoaded,
          getCacheEntry,
        },
      ) {},
    }),
  }),
})
```

## Performing Mutations with React Hooks

Unlike `useQuery`, `useMutation` returns a tuple. The first item in the tuple is the "trigger" function and the second element contains an object with `status`, `error`, and `data`.

Unlike the `useQuery` hook, the `useMutation` hook doesn't execute automatically. To run a mutation you have to call the trigger function returned as the first tuple value from the hook.

## Frequently Used Mutation Hook Return Values

The `useMutation` hook returns a tuple containing a "mutation trigger" function, as well as an object containing properties about the "mutation result".

The "mutation trigger" is a function that when called, will fire off the mutation request for that endpoint. Calling the "mutation trigger" returns a promise with an `unwrap` property, which can be called to unwrap the mutation call and provide the raw response/error. This can be useful if you wish to determine whether the mutation succeeds/fails inline at the call-site.

The "mutation result" is an object containing properties such as the latest `data` for the mutation request, as well as status booleans for the current request lifecycle state.

Below are some of the most frequently used properties on the "mutation result" object. Refer to `useMutation` for an extensive list of all returned properties.

- `data` - The data returned from the latest trigger response, if present. If subsequent triggers from the same hook instance are called, this will return undefined until the new data is received. Consider component level caching if the previous response data is required for a smooth transition to new data.
- `error` - The error result if present.
- `isUninitialized` - When true, indicates that the mutation has not been fired yet.
- `isLoading` - When true, indicates that the mutation has been fired and is awaiting a response.
- `isSuccess` - When true, indicates that the last mutation fired has data from a successful request.
- `isError` - When true, indicates that the last mutation fired resulted in an error state.
- `reset` - A method to reset the hook back to its original state and remove the current result from the cache

## Shared Mutation Results

By default, separate instances of a `useMutation` hook are not inherently related to each other. Triggering one instance will not affect the result for a separate instance. This applies regardless of whether the hooks are called within the same component, or different components.

```jsx
export const ComponentOne = () => {
  // Triggering `updatePostOne` will affect the result in this component,
  // but not the result in `ComponentTwo`, and vice-versa
  const [updatePost, result] = useUpdatePostMutation()

  return <div>...</div>
}

export const ComponentTwo = () => {
  const [updatePost, result] = useUpdatePostMutation()

  return <div>...</div>
}
```

RTK Query provides an option to share results across mutation hook instances using the `fixedCacheKey` option. Any `useMutation` hooks with the same `fixedCacheKey` string will share results between each other when any of the trigger functions are called. This should be a unique string shared between each mutation hook instance you wish to share results.

```jsx
export const ComponentOne = () => {
  // Triggering `updatePostOne` will affect the result in both this component,
  // but as well as the result in `ComponentTwo`, and vice-versa
  const [updatePost, result] = useUpdatePostMutation({
    fixedCacheKey: 'shared-update-post',
  })

  return <div>...</div>
}

export const ComponentTwo = () => {
  const [updatePost, result] = useUpdatePostMutation({
    fixedCacheKey: 'shared-update-post',
  })

  return <div>...</div>
}
```

## Standard Mutation Example

This is a modified version of the complete example you can see at the bottom of the page to highlight the `updatePost` mutation. In this scenario, a post is fetched with `useQuery`, and then an `EditablePostName` component is rendered that allows us to edit the name of the post.

```jsx
export const PostDetail = () => {
  const { id } = useParams<{ id: any }>()

  const { data: post } = useGetPostQuery(id)

  const [
    updatePost, // This is the mutation trigger
    { isLoading: isUpdating }, // This is the destructured mutation result
  ] = useUpdatePostMutation()

  return (
    <Box p={4}>
      <EditablePostName
        name={post.name}
        onUpdate={(name) => {
          // If you want to immediately access the result of a mutation, you need to chain `.unwrap()`
          // if you actually want the payload or to catch the error.
          // Example: `updatePost().unwrap().then(fulfilled => console.log(fulfilled)).catch(rejected => console.error(rejected))

          return (
            // Execute the trigger with the `id` and updated `name`
            updatePost({ id, name })
          )
        }}
        isLoading={isUpdating}
      />
    </Box>
  )
}
```

## Advanced Mutations with Revalidation

In the real world, it's very common that a developer would want to resync their local data cache with the server after performing a mutation (aka "revalidation"). RTK Query takes a more centralized approach to this and requires you to configure the invalidation behavior in your API service definition. See Advanced Invalidation with abstract tag IDs for details on advanced invalidation handling with RTK Query.

### Revalidation Example[​](https://redux-toolkit.js.org/rtk-query/usage/mutations#revalidation-example)

This is an example of a CRUD service for Posts. This implements the Selectively invalidating lists strategy and will most likely serve as a good foundation for real applications.

```jsx
// Or from '@reduxjs/toolkit/query' if not using the auto-generated hooks
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react'

export const postApi = createApi({
  reducerPath: 'postsApi',
  baseQuery: fetchBaseQuery({ baseUrl: '/' }),
  tagTypes: ['Posts'],
  endpoints: (build) => ({
    getPosts: build.query({
      query: () => 'posts',
      // Provides a list of `Posts` by `id`.
      // If any mutation is executed that `invalidate`s any of these tags, this query will re-run to be always up-to-date.
      // The `LIST` id is a "virtual id" we just made up to be able to invalidate this query specifically if a new `Posts` element was added.
      providesTags: (result) =>
        // is result available?
        result
          ? // successful query
            [
              ...result.map(({ id }) => ({ type: 'Posts', id })),
              { type: 'Posts', id: 'LIST' },
            ]
          : // an error occurred, but we still want to refetch this query when `{ type: 'Posts', id: 'LIST' }` is invalidated
            [{ type: 'Posts', id: 'LIST' }],
    }),
    addPost: build.mutation({
      query(body) {
        return {
          url: `post`,
          method: 'POST',
          body,
        }
      },
      // Invalidates all Post-type queries providing the `LIST` id - after all, depending of the sort order,
      // that newly created post could show up in any lists.
      invalidatesTags: [{ type: 'Posts', id: 'LIST' }],
    }),
    getPost: build.query({
      query: (id) => `post/${id}`,
      providesTags: (result, error, id) => [{ type: 'Posts', id }],
    }),
    updatePost: build.mutation({
      query(data) {
        const { id, ...body } = data
        return {
          url: `post/${id}`,
          method: 'PUT',
          body,
        }
      },
      // Invalidates all queries that subscribe to this Post `id` only.
      // In this case, `getPost` will be re-run. `getPosts` *might*  rerun, if this id was under its results.
      invalidatesTags: (result, error, { id }) => [{ type: 'Posts', id }],
    }),
    deletePost: build.mutation({
      query(id) {
        return {
          url: `post/${id}`,
          method: 'DELETE',
        }
      },
      // Invalidates all queries that subscribe to this Post `id` only.
      invalidatesTags: (result, error, id) => [{ type: 'Posts', id }],
    }),
  }),
})

export const {
  useGetPostsQuery,
  useAddPostMutation,
  useGetPostQuery,
  useUpdatePostMutation,
  useDeletePostMutation,
} = postApi
```