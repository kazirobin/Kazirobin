# Defining Routes

This page will guide you through how to define and organize routes in your Next.js application.

## Creating Routes

Next.js uses a file-system based router where **folders** are used to define routes.
Each folder represents a **route** segment that maps to a **URL** segment. To create a nested route, you can nest folders inside each other.

[route-segments-to-path-segments.avif](Defining%20Routes%201b2aeacbb29981cf9184f691379cd1ab/route-segments-to-path-segments.avif)

A special `page.js` file is used to make route segments publicly accessible.

[defining-routes.avif](Defining%20Routes%201b2aeacbb29981cf9184f691379cd1ab/defining-routes.avif)

In this example, the `/dashboard/analytics` URL path is *not* publicly accessible because it does not have a corresponding `page.js` file. This folder could be used to store components, stylesheets, images, or other colocated files.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know**: `.js`, `.jsx`, or `.tsx` file extensions can be used for special files.

</aside>

## Creating UI

Special file conventions are used to create UI for each route segment. The most common are pages to show UI unique to a route, and layouts to show UI that is shared across multiple routes.

For example, to create your first page, add a `page.js` file inside the `app` directory and export a React component:

Create a file named **app/page.js**

```jsx
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```