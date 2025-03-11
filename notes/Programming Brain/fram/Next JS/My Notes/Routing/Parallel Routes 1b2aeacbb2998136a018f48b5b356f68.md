# Parallel Routes

Parallel Routes allows you to simultaneously or conditionally render one or more pages within the same layout. They are useful for highly dynamic sections of an app, such as dashboards and feeds on social sites.

For example, considering a dashboard, you can use parallel routes to simultaneously render the `team` and `analytics` pages:

[parallel-routes.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/parallel-routes.avif)

## Slots

Parallel routes are created using named **slots**. Slots are defined with the `@folder` convention. For example, the following file structure defines two slots: `@analytics` and `@team`:

[parallel-routes-file-system.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/parallel-routes-file-system.avif)

Slots are passed as props to the shared parent layout. For the example above, the component in `app/layout.js` now accepts the `@analytics` and `@team` slots props, and can render them in parallel alongside the `children` prop:

Create a file named **layout.jsx**

```jsx
export default function Layout({ children, team, analytics }) {
  return (
    <>
      {children}
      {team}
      {analytics}
    </>
  )
}
```

However, slots are **not** route segments and do not affect the URL structure. For example, for `/@analytics/views`, the URL will be `/views` since `@analytics` is a slot.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know**:

- The `children` prop is an implicit slot that does not need to be mapped to a folder. This means `app/page.js` is equivalent to `app/@children/page.js`.
</aside>

## Active state and navigation

By default, Next.js keeps track of the active *state* (or subpage) for each slot. However, the content rendered within a slot will depend on the type of navigation:

- **Soft Navigation**: During client-side navigation, Next.js will perform a partial render, changing the subpage within the slot, while maintaining the other slot's active subpages, even if they don't match the current URL.
- **Hard Navigation**: After a full-page load (browser refresh), Next.js cannot determine the active state for the slots that don't match the current URL. Instead, it will render a `default.js` file for the unmatched slots, or `404` if `default.js` doesn't exist.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know**:

- The `404` for unmatched routes helps ensure that you don't accidentally render a parallel route on a page that it was not intended for.
</aside>

## `default.js`

You can define a `default.js` file to render as a fallback for unmatched slots during the initial load or full-page reload.

Consider the following folder structure. The `@team` slot has a `/settings` page, but `@analytics` does not.

[parallel-routes-unmatched-routes.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/parallel-routes-unmatched-routes.avif)

When navigating to `/settings`, the `@team` slot will render the `/settings` page while maintaining the currently active page for the `@analytics` slot.

On refresh, Next.js will render a `default.js` for `@analytics`. If `default.js` doesn't exist, a `404` is rendered instead.

Additionally, since `children` is an implicit slot, you also need to create a `default.js` file to render a fallback for `children` when Next.js cannot recover the active state of the parent page.

## `useSelectedLayoutSegment(s)`

Both `useSelectedLayoutSegment` and `useSelectedLayoutSegments` accept a `parallelRoutesKey` parameter, which allows you to read the active route segment within a slot.

Create a file named **layout.jsx**

```jsx
'use client'
 
import { useSelectedLayoutSegment } from 'next/navigation'
 
export default function Layout({ auth }) {
  const loginSegments = useSelectedLayoutSegment('auth')
  // ...
}
```

When a user navigates to `app/@auth/login` (or `/login` in the URL bar), `loginSegments` will be equal to the string `"login"`.

## Examples

### Conditional Routes

You can use Parallel Routes to conditionally render routes based on certain conditions, such as user role. For example, to render a different dashboard page for the `/admin` or `/user` roles:

[conditional-routes-ui.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/conditional-routes-ui.avif)

Create a file named **app/dashboard/layout.js**

```jsx
import { checkUserRole } from '@/lib/auth'
 
export default function Layout({ user, admin }) {
  const role = checkUserRole()
  return <>{role === 'admin' ? admin : user}</>
}
```

### Tab Groups

You can add a `layout` inside a slot to allow users to navigate the slot independently. This is useful for creating tabs.

For example, the `@analytics` slot has two subpages: `/page-views` and `/visitors`.

[parallel-routes-tab-groups.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/parallel-routes-tab-groups.avif)

Within `@analytics`, create a `layout` file to share the tabs between the two pages:

Create a file named **app/@analytics/layout.js**

```jsx
import Link from 'next/link'
 
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <nav>
        <Link href="/page-views">Page Views</Link>
        <Link href="/visitors">Visitors</Link>
      </nav>
      <div>{children}</div>
    </>
  )
}
```

### Modals

Parallel Routes can be used together with Intercepting Routes to create modals. This allows you to solve common challenges when building modals, such as:

- Making the modal content **shareable through a URL**.
- **Preserving context** when the page is refreshed, instead of closing the modal.
- **Closing the modal on backwards navigation** rather than going to the previous route.
- **Reopening the modal on forwards navigation**.

Consider the following UI pattern, where a user can open a login modal from a layout using client-side navigation, or access a separate `/login` page:

[parallel-routes-auth-modal.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/parallel-routes-auth-modal.avif)

To implement this pattern, start by creating a `/login` route that renders your **main** login page.

[parallel-routes-modal-login-page.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/parallel-routes-modal-login-page.avif)

Create a file named **app/login/page.js**

```jsx
import { Login } from '@/app/ui/login'
 
export default function Page() {
  return <Login />
}
```

Then, inside the `@auth` slot, add `default.js` file that returns `null`. This ensures that the modal is not rendered when it's not active.

Create a file named **app/@auth/default.js**

```jsx
export default function Default() {
  return null
}
```

Inside your `@auth` slot, intercept the `/login` route by updating the `/(.)login` folder. Import the `<Modal>` component and its children into the `/(.)login/page.tsx` file:

Create a file named **app/@auth/(.)login/page.js**

```jsx
import { Modal } from '@/app/ui/modal'
import { Login } from '@/app/ui/login'
 
export default function Page() {
  return (
    <Modal>
      <Login />
    </Modal>
  )
}
```

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know:**

- The convention used to intercept the route, e.g. `(.)`, depends on your file-system structure. See Intercepting Routes convention.
- By separating the `<Modal>` functionality from the modal content (`<Login>`), you can ensure any content inside the modal, e.g. forms, are Server Components. See Interleaving Client and Server Components for more information.
</aside>

### Opening the modal

Now, you can leverage the Next.js router to open and close the modal. This ensures the URL is correctly updated when the modal is open, and when navigating backwards and forwards.

To open the modal, pass the `@auth` slot as a prop to the parent layout and render it alongside the `children` prop.

Create a file named **app/layout.js**

```jsx
import Link from 'next/link'
 
export default function Layout({ auth, children }) {
  return (
    <>
      <nav>
        <Link href="/login">Open modal</Link>
      </nav>
      <div>{auth}</div>
      <div>{children}</div>
    </>
  )
}
```

When the user clicks the `<Link>`, the modal will open instead of navigating to the `/login` page. However, on refresh or initial load, navigating to `/login` will take the user to the main login page.

### Closing the modal

You can close the modal by calling `router.back()` or by using the `Link` component.

Create a file named **app/ui/modal.js**

```jsx
'use client'
 
import { useRouter } from 'next/navigation'
 
export function Modal({ children }) {
  const router = useRouter()
 
  return (
    <>
      <button
        onClick={() => {
          router.back()
        }}
      >
        Close modal
      </button>
      <div>{children}</div>
    </>
  )
}
```

**app/@auth/[...catchAll]/page.js**

```jsx
export default function CatchAll() {
  return null
}
```

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know:**

- We use a catch-all route in our `@auth` slot to close the modal because of the behavior described in Active state and navigation. Since client-side navigations to a route that no longer match the slot will remain visible, we need to match the slot to a route that returns `null` to close the modal.
- Other examples could include opening a photo modal in a gallery while also having a dedicated `/photo/[id]` page, or opening a shopping cart in a side modal.
- View an example of modals with Intercepted and Parallel Routes.
</aside>

### Loading and Error UI

Parallel Routes can be streamed independently, allowing you to define independent error and loading states for each route:

[parallel-routes-cinematic-universe.avif](Parallel%20Routes%201b2aeacbb2998136a018f48b5b356f68/parallel-routes-cinematic-universe.avif)