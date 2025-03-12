# Data Fetching and Caching

This guide will walk you through the basics of data fetching and caching in Next.js, providing practical examples and best practices.

Here's a minimal example of data fetching in Next.js:

Create a file named app/page.js

```jsx
export default async function Page() {
  const data = await fetch('https://api.vercel.app/blog')
  const posts = await data.json()
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  )
}
```

This example demonstrates a basic server-side data fetch using the `fetch` API in an asynchronous React Server Component.

[**Fetching data on the server with the `fetch` API**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Fetching%20data%20on%20the%20server%20with%20the%20fetch%20API%201b2aeacbb29981709932e7d30f96351c.md)

[**Fetching data on the server with an ORM or database**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Fetching%20data%20on%20the%20server%20with%20an%20ORM%20or%20databas%201b2aeacbb299811b9594defd4cf68aec.md)

[**Fetching data on the client**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Fetching%20data%20on%20the%20client%201b2aeacbb299816682cee37764854f1a.md)

[**Caching data with an ORM or Database**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Caching%20data%20with%20an%20ORM%20or%20Database%201b2aeacbb299818aa96be464fc62479f.md)

[**Reusing data across multiple functions**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Reusing%20data%20across%20multiple%20functions%201b2aeacbb2998171835ed1d1945aeef8.md)

[**Parallel and sequential data fetching**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Parallel%20and%20sequential%20data%20fetching%201b2aeacbb299816da0bcc1b2326bea40.md)

[**Preloading Data**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Preloading%20Data%201b2aeacbb29981368ed5d4a001a83980.md)

[**Preventing sensitive data from being exposed to the client**](Data%20Fetching%20and%20Caching%201b2aeacbb29981a9bd14c54b32515dc0/Preventing%20sensitive%20data%20from%20being%20exposed%20to%20th%201b2aeacbb29981e3b865f81f8d26c66f.md)