# Dynamic Routes

When you don't know the exact segment names ahead of time and want to create routes from dynamic data, you can use Dynamic Segments that are filled in at request time or prerendered at build time.

### Convention

A Dynamic Segment can be created by wrapping a folder's name in square brackets: `[folderName]`. For example, `[id]` or `[slug]`.

### Example

For example, a blog could include the following route `app/blog/[slug]/page.js` where `[slug]` is the Dynamic Segment for blog posts.

Create a file named **app/blog/[slug]/page.js**

```jsx
export default function Page({ params }) {
  return <div>My Post: {params.slug}</div>
}
```

| **Route** | **Example URL** | Params |
| --- | --- | --- |
| app/blog/[slug]/page.js | /blog/a | { slug: 'a' } |
| app/blog/[slug]/page.js | /blog/b | { slug: 'b' } |
| app/blog/[slug]/page.js | /blog/c | { slug: 'c' } |

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know**: Dynamic Segments are equivalent to Dynamic Routes in the `pages` directory.

</aside>

## Generating Static Params

The `generateStaticParams` function can be used in combination with dynamic route segments to **statically generate** routes at build time instead of on-demand at request time.

Create a file named **app/blog/[slug]/page.js**

```jsx
export async function generateStaticParams() {
  const posts = await fetch('https://.../posts').then((res) => res.json())
 
  return posts.map((post) => ({
    slug: post.slug,
  }))
}
```

The primary benefit of the `generateStaticParams` function is its smart retrieval of data. If content is fetched within the `generateStaticParams` function using a `fetch` request, the requests are automatically memoized. This means a `fetch` request with the same arguments across multiple `generateStaticParams`, Layouts, and Pages will only be made once, which decreases build times.

## Catch-all Segments

Dynamic Segments can be extended to **catch-all** subsequent segments by adding an ellipsis inside the brackets `[...folderName]`.

For example, `app/shop/[...slug]/page.js` will match `/shop/clothes`, but also `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`, and so on.

| **Route** | **Example URL** | Params |
| --- | --- | --- |
| app/shop/[...slug]/page.js | /shop/a | { slug: ['a'] } |
| app/shop/[...slug]/page.js | /shop/a/b | { slug: ['a', 'b'] } |
| /shop/a/b/c | /shop/a/b/c | { slug: ['a', 'b', 'c'] } |

## Optional Catch-all Segments

Catch-all Segments can be made **optional** by including the parameter in double square brackets: `[[...folderName]]`.

For example, `app/shop/[[...slug]]/page.js` will **also** match `/shop`, in addition to `/shop/clothes`, `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`.

The difference between **catch-all** and **optional catch-all** segments is that with optional, the route without the parameter is also matched (`/shop` in the example above).

| **Route** | **Example URL** | Params |
| --- | --- | --- |
| app/shop/[[...slug]]/page.js | /shop | {} |
| app/shop/[...slug]/page.jsapp/shop/[[...slug]]/page.js | /shop/a | { slug: ['a'] } |
| app/shop/[[...slug]]/page.js | /shop/a/b | { slug: ['a', 'b'] } |
| app/shop/[[...slug]]/page.js | /shop/a/b/c | { slug: ['a', 'b', 'c'] } |