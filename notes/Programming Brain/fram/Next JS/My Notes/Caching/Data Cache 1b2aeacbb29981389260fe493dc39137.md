# Data Cache

Next.js has a built-in Data Cache that **persists** the result of data fetches across incoming **server requests** and **deployments**. This is possible because Next.js extends the native `fetch` API to allow each request on the server to set its own persistent caching semantics.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" />

**Good to know**: In the browser, the `cache` option of `fetch` indicates how a request will interact with the browser's HTTP cache, in Next.js, the `cache` option indicates how a server-side request will interact with the server's Data Cache.

</aside>

By default, data requests that use `fetch` are **cached**. You can use the `cache` and `next.revalidate` options of `fetch` to configure the caching behavior.

**How the Data Cache Works**

[data-cache.avif](Data%20Cache%201b2aeacbb29981389260fe493dc39137/data-cache.avif)

- The first time a `fetch` request is called during rendering, Next.js checks the Data Cache for a cached response.
- If a cached response is found, it's returned immediately and memoized.
- If a cached response is not found, the request is made to the data source, the result is stored in the Data Cache, and memoized.
- For uncached data (e.g. `{ cache: 'no-store' }`), the result is always fetched from the data source, and memoized.
- Whether the data is cached or uncached, the requests are always memoized to avoid making duplicate requests for the same data during a React render pass.

### Differences between the Data Cache and Request Memoization

While both caching mechanisms help improve performance by re-using cached data, the Data Cache is persistent across incoming requests and deployments, whereas memoization only lasts the lifetime of a request.

With memoization, we reduce the number of **duplicate** requests in the same render pass that have to cross the network boundary from the rendering server to the Data Cache server (e.g. a CDN or Edge Network) or data source (e.g. a database or CMS). With the Data Cache, we reduce the number of requests made to our origin data source.

### Duration

The Data Cache is persistent across incoming requests and deployments unless you revalidate or opt-out.

### Revalidating

Cached data can be revalidated in two ways, with:

- **Time-based Revalidation**: Revalidate data after a certain amount of time has passed and a new request is made. This is useful for data that changes infrequently and freshness is not as critical.
- **On-demand Revalidation:** Revalidate data based on an event (e.g. form submission). On-demand revalidation can use a tag-based or path-based approach to revalidate groups of data at once. This is useful when you want to ensure the latest data is shown as soon as possible (e.g. when content from your headless CMS is updated).

**Time-based Revalidation**

To revalidate data at a timed interval, you can use the `next.revalidate` option of `fetch` to set the cache lifetime of a resource (in seconds).

```jsx
// Revalidate at most every hour
fetch('https://...', { next: { revalidate: 3600 } })
```

**How Time-based Revalidation Works**

[time-based-revalidation.avif](Data%20Cache%201b2aeacbb29981389260fe493dc39137/time-based-revalidation.avif)

- The first time a fetch request with `revalidate` is called, the data will be fetched from the external data source and stored in the Data Cache.
- Any requests that are called within the specified timeframe (e.g. 60-seconds) will return the cached data.
- After the timeframe, the next request will still return the cached (now stale) data.
    - Next.js will trigger a revalidation of the data in the background.
    - Once the data is fetched successfully, Next.js will update the Data Cache with the fresh data.
    - If the background revalidation fails, the previous data will be kept unaltered.
    

**On-demand Revalidation**

Data can be revalidated on-demand by path (`revalidatePath`) or by cache tag (`revalidateTag`).

**How On-Demand Revalidation Works**

[on-demand-revalidation.avif](Data%20Cache%201b2aeacbb29981389260fe493dc39137/on-demand-revalidation.avif)

- The first time a `fetch` request is called, the data will be fetched from the external data source and stored in the Data Cache.
- When an on-demand revalidation is triggered, the appropriate cache entries will be purged from the cache.
    - This is different from time-based revalidation, which keeps the stale data in the cache until the fresh data is fetched.
- The next time a request is made, it will be a cache `MISS` again, and the data will be fetched from the external data source and stored in the Data Cache.

### Opting out

For individual data fetches, you can opt out of caching by setting the `cache` option to `no-store`. This means data will be fetched whenever `fetch` is called.

```jsx
// Opt out of caching for an individual `fetch` request
fetch(`https://...`, { cache: 'no-store' })
```

```jsx
// Opt out of caching for all data requests in the route segment
export const dynamic = 'force-dynamic'
```