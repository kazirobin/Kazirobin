# Router Cache

Next.js has an in-memory client-side cache that stores the React Server Component Payload, split by individual route segments, for the duration of a user session. This is called the Router Cache.

**How the Router Cache Works**

[router-cache.avif](Router%20Cache%201b2aeacbb299814cb23adf3a16dc9dc9/router-cache.avif)

As a user navigates between routes, Next.js caches visited route segments and prefetches the routes the user is likely to navigate to (based on `<Link>` components in their viewport).

This results in an improved navigation experience for the user:

- Instant backward/forward navigation because visited routes are cached and fast navigation to new routes because of prefetching and partial rendering.
- No full-page reload between navigations, and React state and browser state are preserved.

### Difference between the Router Cache and Full Route Cache:

The Router Cache temporarily stores the React Server Component Payload in the browser for the duration of a user session, whereas the Full Route Cache persistently stores the React Server Component Payload and HTML on the server across multiple user requests.

While the Full Route Cache only caches statically rendered routes, the Router Cache applies to both statically and dynamically rendered routes.

### Duration

The cache is stored in the browser's temporary memory. Two factors determine how long the router cache lasts:

- **Session**: The cache persists across navigation. However, it's cleared on page refresh.
- **Automatic Invalidation Period**: The cache of an individual segment is automatically invalidated after a specific time. The duration depends on how the resource was prefetched:
    - **Default Prefetching** (`prefetch={null}` or unspecified): 30 seconds
    - **Full Prefetching**: (`prefetch={true}` or `router.prefetch`): 5 minutes
    

While a page refresh will clear **all** cached segments, the automatic invalidation period only affects the individual segment from the time it was prefetched.

### Invalidation

There are two ways you can invalidate the Router Cache:

- In a **Server Action**:
    - Revalidating data on-demand by path with (`revalidatePath`) or by cache tag with (`revalidateTag`)
    - Using `cookies.set` or `cookies.delete` invalidates the Router Cache to prevent routes that use cookies from becoming stale (e.g. authentication).
- Calling `router.refresh` will invalidate the Router Cache and make a new request to the server for the current route.

### Opting out

It's not possible to opt out of the Router Cache. However, you can invalidate it by calling `router.refresh`, `revalidatePath`, or `revalidateTag` (see above). This will clear the cache and make a new request to the server, ensuring the latest data is shown.

You can also opt out of **prefetching** by setting the `prefetch` prop of the `<Link>` component to `false`. However, this will still temporarily store the route segments for 30s to allow instant navigation between nested segments, such as tab bars, or back and forward navigation. Visited routes will still be cached.