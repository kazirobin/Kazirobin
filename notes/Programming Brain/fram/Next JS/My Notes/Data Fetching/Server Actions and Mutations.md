# Server Actions and Mutations

Server Actions are **asynchronous functions** that are executed on the server. They can be used in Server and Client Components to handle form submissions and data mutations in Next.js applications.

## Convention

A Server Action can be defined with the React `"use server"` directive. You can place the directive at the top of an `async` function to mark the function as a Server Action, or at the top of a separate file to mark all exports of that file as Server Actions.

## Server Components

Server Components can use the inline function level or module level `"use server"` directive. To inline a Server Action, add `"use server"` to the top of the function body:

```jsx
// Server Component
export default function Page() {
  // Server Action
  async function create() {
    'use server'
 
    // ...
  }
 
  return (
    // ...
  )
}
```

## Client Components

Client Components can only import actions that use the module-level `"use server"` directive.

To call a Server Action in a Client Component, create a new file and add the `"use server"` directive at the top of it. All functions within the file will be marked as Server Actions that can be reused in both Client and Server Components:

```jsx
'use server'
 
export async function create() {
  // ...
}
```

```jsx
import { create } from '@/app/actions'
 
export function Button() {
  return (
    // ...
  )
}
```

You can also pass a Server Action to a Client Component as a prop:

```jsx
<ClientComponent updateItem={updateItem} />
```

```jsx
'use client'
 
export default function ClientComponent({ updateItem }) {
  return <form action={updateItem}>{/* ... */}</form>
}
```

## Behavior

- Server actions can be invoked using the `action` attribute in a `<form>` element:
    - Server Components support progressive enhancement by default, meaning the form will be submitted even if JavaScript hasn't loaded yet or is disabled.
    - In Client Components, forms invoking Server Actions will queue submissions if JavaScript isn't loaded yet, prioritizing client hydration.
    - After hydration, the browser does not refresh on form submission.
- Server Actions are not limited to `<form>` and can be invoked from event handlers, `useEffect`, third-party libraries, and other form elements like `<button>`.
- Server Actions integrate with the Next.js caching and revalidation architecture. When an action is invoked, Next.js can return both the updated UI and new data in a single server roundtrip.
- Behind the scenes, actions use the `POST` method, and only this HTTP method can invoke them.
- The arguments and return value of Server Actions must be serializable by React. See the React docs for a list of serializable arguments and values.
- Server Actions are functions. This means they can be reused anywhere in your application.
- Server Actions inherit the runtime from the page or layout they are used on.
- Server Actions inherit the Route Segment Config from the page or layout they are used on, including fields like `maxDuration`.

## Examples

---

[**Forms**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Forms%201b2aeacbb29981e4944ff863681bb626.md)

[Non-form Elements](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Non-form%20Elements%201b2aeacbb29981f2ab4fd32cc46cbb10.md)

[**Error Handling**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Error%20Handling%201b2aeacbb29981f5903ee49d9e43b968.md)

[**Revalidating data**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Revalidating%20data%201b2aeacbb29981f1b233cccc1c051e0e.md)

[Redirecting](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Redirecting%201b2aeacbb29981da936fde210f1cb81f.md)

[**Cookies**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Cookies%201b2aeacbb2998109b912fd3d71526187.md)

## Security

---

[**Authentication and authorization**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Authentication%20and%20authorization%201b2aeacbb299818c9ea2c630438cc82e.md)

[**Closures and encryption**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Closures%20and%20encryption%201b2aeacbb29981a18e9dc5d88ef91eef.md)

[**Overwriting encryption keys (advanced)**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Overwriting%20encryption%20keys%20(advanced)%201b2aeacbb29981169763e5e3483bee9b.md)

[**Allowed origins (advanced)**](Server%20Actions%20and%20Mutations%201b2aeacbb2998126a622edc1b7bb0059/Allowed%20origins%20(advanced)%201b2aeacbb299815e8d27d02acfd8a8a8.md)