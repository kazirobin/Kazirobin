# APIs

The following table provides an overview of how different Next.js APIs affect caching:

| API | **Router Cache** | **Full Route Cache** | **Data Cache** | **React Cache** |
| --- | --- | --- | --- | --- |
| `<Link prefetch>` | Cache |  |  |  |
| `router.prefetch` | Cache |  |  |  |
| `router.refresh` | Revalidate |  |  |  |
| `fetch` |  |  | Cache | Cache |
| `fetch` `options.cache` |  |  | Cache or Opt out |  |
| `fetch` `options.next.revalidate` |  | Revalidate | Revalidate |  |
| `fetch` `options.next.tags` |  | Cache | Cache |  |
| `revalidateTag` | Revalidate (Server Action) | Revalidate | Revalidate |  |
| `revalidatePath` | Revalidate (Server Action) | Revalidate | Revalidate |  |
| `const revalidate` |  | Revalidate or Opt out | Revalidate or Opt out |  |
| `const dynamic` |  | Cache or Opt out | Cache or Opt out |  |
| `cookies` | Revalidate (Server Action) | Opt out |  |  |
| `headers`, `searchParams` |  | Opt out |  |  |
| `generateStaticParams` |  | Cache |  |  |
| `React.cache` |  |  |  | Cache |
| `unstable_cache` |  |  |  |  |

### `<Link>`

By default, the `<Link>` component automatically prefetches routes from the Full Route Cache and adds the React Server Component Payload to the Router Cache.

To disable prefetching, you can set the `prefetch` prop to `false`. But this will not skip the cache permanently, the route segment will still be cached client-side when the user visits the route.

Learn more about the [`<Link>`](https://nextjs.org/docs/app/api-reference/components/link) component.

### `router.prefetch`

The `prefetch` option of the `useRouter` hook can be used to manually prefetch a route. This adds the React Server Component Payload to the Router Cache.

See the [`useRouter`](https://nextjs.org/docs/app/api-reference/functions/use-router) hook API reference.

### `router.refresh`

The `refresh` option of the `useRouter` hook can be used to manually refresh a route. This completely clears the Router Cache, and makes a new request to the server for the current route. `refresh` does not affect the Data or Full Route Cache.

The rendered result will be reconciled on the client while preserving React state and browser state.

See the [`useRouter`](https://nextjs.org/docs/app/api-reference/functions/use-router) hook API reference.

### **`fetch`**

Data returned from `fetch` is automatically cached in the Data Cache.

```jsx
// Cached by default. `force-cache` is the default option and can be omitted.
fetch(`https://...`, { cache: 'force-cache' })
```

See the [`fetch`](https://nextjs.org/docs/app/api-reference/functions/fetch) API Reference for more options.

### `fetch options.cache`

You can opt out individual `fetch` requests of data caching by setting the `cache` option to `no-store`:

```jsx
// Opt out of caching
fetch(`https://...`, { cache: 'no-store' })
```

Since the render output depends on data, using `cache: 'no-store'` will also skip the Full Route Cache for the route where the `fetch` request is used. That is, the route will be dynamically rendered every request, but you can still have other cached data requests in the same route.

See the [`fetch`](https://nextjs.org/docs/app/api-reference/functions/fetch) API Reference for more options.

### `fetch options.next.revalidate`

You can use the `next.revalidate` option of `fetch` to set the revalidation period (in seconds) of an individual `fetch` request. This will revalidate the Data Cache, which in turn will revalidate the Full Route Cache. Fresh data will be fetched, and components will be re-rendered on the server.

```jsx
// Revalidate at most after 1 hour
fetch(`https://...`, { next: { revalidate: 3600 } })
```

See the [`fetch`](https://nextjs.org/docs/app/api-reference/functions/fetch) API Reference for more options.

### `fetch options.next.tags` and `revalidateTag`

Next.js has a cache tagging system for fine-grained data caching and revalidation.

1. When using `fetch` or `unstable_cache`, you have the option to tag cache entries with one or more tags.
2. Then, you can call `revalidateTag` to purge the cache entries associated with that tag.

For example, you can set a tag when fetching data:

```jsx
// Cache data with a tag
fetch(`https://...`, { next: { tags: ['a', 'b', 'c'] } })
```

Then, call `revalidateTag` with a tag to purge the cache entry:

```jsx
// Revalidate entries with a specific tag
revalidateTag('a')
```

There are two places you can use `revalidateTag`, depending on what you're trying to achieve:

1. Route Handlers - to revalidate data in response of a third party event (e.g. webhook). This will not invalidate the Router Cache immediately as the Router Handler isn't tied to a specific route.
2. Server Actions - to revalidate data after a user action (e.g. form submission). This will invalidate the Router Cache for the associated route.

See the [`revalidateTag`](https://nextjs.org/docs/app/api-reference/functions/revalidateTag) API reference for more information.

## `revalidatePath`

`revalidatePath` allows you manually revalidate data **and** re-render the route segments below a specific path in a single operation. Calling the `revalidatePath` method revalidates the Data Cache, which in turn invalidates the Full Route Cache.

```jsx
revalidatePath('/')
```

There are two places you can use `revalidatePath`, depending on what you're trying to achieve:

1. Route Handlers - to revalidate data in response to a third party event (e.g. webhook).
2. Server Actions - to revalidate data after a user interaction (e.g. form submission, clicking a button).

See the [`revalidatePath`](https://nextjs.org/docs/app/api-reference/functions/revalidatePath) API reference for more information.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **`revalidatePath`** vs. **`router.refresh`**:

Calling `router.refresh` will clear the Router cache, and re-render route segments on the server without invalidating the Data Cache or the Full Route Cache.

The difference is that `revalidatePath` purges the Data Cache and Full Route Cache, whereas `router.refresh()` does not change the Data Cache and Full Route Cache, as it is a client-side API.

</aside>

### Dynamic Functions

Dynamic functions like `cookies` and `headers`, and the `searchParams` prop in Pages depend on runtime incoming request information. Using them will opt a route out of the Full Route Cache, in other words, the route will be dynamically rendered.

### `cookies`

Using `cookies.set` or `cookies.delete` in a Server Action invalidates the Router Cache to prevent routes that use cookies from becoming stale (e.g. to reflect authentication changes).

See the [`cookies`](https://nextjs.org/docs/app/api-reference/functions/cookies) API reference.

### Segment Config Options

The Route Segment Config options can be used to override the route segment defaults or when you're not able to use the `fetch` API (e.g. database client or 3rd party libraries).

The following Route Segment Config options will opt out of the Data Cache and Full Route Cache:

- `const dynamic = 'force-dynamic'`
- `const revalidate = 0`

See the [Route Segment Config](https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config) documentation for more options.

### `generateStaticParams`

For dynamic segments (e.g. `app/blog/[slug]/page.js`), paths provided by `generateStaticParams` are cached in the Full Route Cache at build time. At request time, Next.js will also cache paths that weren't known at build time the first time they're visited.

You can disable caching at request time by using

`export const dynamicParams = false` option in a route segment. When this config option is used, only paths provided by `generateStaticParams` will be served, and other routes will 404 or match (in the case of catch-all routes).

See the [`generateStaticParams`](https://nextjs.org/docs/app/api-reference/functions/generate-static-params) API reference.

### React `cache` function

The React `cache` function allows you to memoize the return value of a function, allowing you to call the same function multiple times while only executing it once.

Since `fetch` requests are automatically memoized, you do not need to wrap it in React `cache`. However, you can use `cache` to manually memoize data requests for use cases when the `fetch` API is not suitable. For example, some database clients, CMS clients, or GraphQL clients.

Create a file named **src/utils/getItem.js**

```jsx
import { cache } from 'react'
import db from '@/lib/db'
 
export const getItem = cache(async (id) => {
  const item = await db.item.findUnique({ id })
  return item
})
```