# Pages and Layouts

The special files layout.js, page.js, and template.js allow you to create UI for a route. This page will guide you through how and when to use these special files.

## Pages

A page is UI that is **unique** to a route. You can define a page by default exporting a component from a `page.js` file.

For example, to create your `index` page, add the `page.js` file inside the `app` directory:

[page-special-file.avif](Pages%20and%20Layouts%201b2aeacbb2998123b103f218ab8b1fa6/page-special-file.avif)

```jsx
// `app/page.js` is the UI for the `/` URL
export default function Page() {
  return <h1>Hello, Home page!</h1>
}
```

Then, to create further pages, create a new folder and add the `page.js` file inside it. For example, to create a page for the `/dashboard` route, create a new folder called `dashboard`, and add the `page.js` file inside it:

```jsx
// `app/dashboard/page.js` is the UI for the `/dashboard` URL
export default function Page() {
  return <h1>Hello, Dashboard Page!</h1>
}
```

### **Good to know**:

- The `.js`, `.jsx`, or `.tsx` file extensions can be used for Pages.
- A page is always the leaf of the route subtree.
- A `page.js` file is required to make a route segment publicly accessible.
- Pages are Server Components by default, but can be set to a Client Component.
- Pages can fetch data. View the Data Fetching section for more information.

## Layouts

A layout is UI that is **shared** between multiple routes. On navigation, layouts preserve state, remain interactive, and do not re-render. Layouts can also be nested.

You can define a layout by default exporting a React component from a `layout.js` file. The component should accept a `children` prop that will be populated with a child layout (if it exists) or a page during rendering.

For example, the layout will be shared with the `/dashboard` and `/dashboard/settings` pages:

[layout-special-file.avif](Pages%20and%20Layouts%201b2aeacbb2998123b103f218ab8b1fa6/layout-special-file.avif)

Create a file named **app/dashboard/layout.js**

```jsx
export default function DashboardLayout({
  children, // will be a page or nested layout
}) {
  return (
    <section>
      {/* Include shared UI here e.g. a header or sidebar */}
      <nav></nav>
 
      {children}
    </section>
  )
}
```

## Root Layout (Required)

The root layout is defined at the top level of the `app` directory and applies to all routes. This layout is **required** and must contain `html` and `body` tags, allowing you to modify the initial HTML returned from the server.

Create a file named **app/layout.js**

```jsx
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        {/* Layout UI */}
        <main>{children}</main>
      </body>
    </html>
  )
}
```

## Nesting Layouts

By default, layouts in the folder hierarchy are **nested**, which means they wrap child layouts via their `children` prop. You can nest layouts by adding `layout.js` inside specific route segments (folders).

For example, to create a layout for the `/dashboard` route, add a new `layout.js` file inside the `dashboard` folder:

[nested-layout.avif](Pages%20and%20Layouts%201b2aeacbb2998123b103f218ab8b1fa6/nested-layout.avif)

Create a file named **app/dashboard/layout.js**

```jsx
export default function DashboardLayout({ children }) {
  return <section>{children}</section>
}
```

If you were to combine the two layouts above, the root layout (`app/layout.js`) would wrap the dashboard layout (`app/dashboard/layout.js`), which would wrap route segments inside `app/dashboard/*`.

The two layouts would be nested as such:

[nested-layouts-ui.avif](Pages%20and%20Layouts%201b2aeacbb2998123b103f218ab8b1fa6/nested-layouts-ui.avif)

### **Good to know**:

- `.js`, `.jsx`, or `.tsx` file extensions can be used for Layouts.
- Only the root layout can contain `<html>` and `<body>` tags.
- When a `layout.js` and `page.js` file are defined in the same folder, the layout will wrap the page.
- Layouts are Server Components by default but can be set to a Client Component.
- Layouts can fetch data. View the Data Fetching section for more information.
- Passing data between a parent layout and its children is not possible. However, you can fetch the same data in a route more than once, and React will automatically dedupe the requests without affecting performance.
- Layouts do not have access to the route segments below itself. To access all route segments, you can use `useSelectedLayoutSegment` or `useSelectedLayoutSegments` in a Client Component.
- You can use Route Groups to opt specific route segments in and out of shared layouts.
- You can use Route Groups to create multiple root layouts.
- **Migrating from the `pages` directory:** The root layout replaces the `_app.js` and `_document.js` files.

## Templates

Templates are similar to layouts in that they wrap each child layout or page. Unlike layouts that persist across routes and maintain state, templates create a new instance for each of their children on navigation. This means that when a user navigates between routes that share a template, a new instance of the component is mounted, DOM elements are recreated, state is **not** preserved, and effects are re-synchronized.

There may be cases where you need those specific behaviors, and templates would be a more suitable option than layouts. For example:

- Features that rely on `useEffect` (e.g logging page views) and `useState` (e.g a per-page feedback form).
- To change the default framework behavior. For example, Suspense Boundaries inside layouts only show the fallback the first time the Layout is loaded and not when switching pages. For templates, the fallback is shown on each navigation.

A template can be defined by exporting a default React component from a `template.js` file. The component should accept a `children` prop.

[template-special-file.avif](Pages%20and%20Layouts%201b2aeacbb2998123b103f218ab8b1fa6/template-special-file.avif)

Create a file named **app/template.js**

```jsx
export default function Template({ children }) {
  return <div>{children}</div>
}
```

In terms of nesting, `template.js` is rendered between a layout and its children. Here's a simplified output:

```jsx
<Layout>
  {/* Note that the template is given a unique key. */}
  <Template key={routeParam}>{children}</Template>
</Layout>
```

## Metadata

In the `app` directory, you can modify the `<head>` HTML elements such as `title` and `meta` using the Metadata APIs.

Metadata can be defined by exporting a `metadata` object or `generateMetadata` function in a `layout.js` or `page.js` file.

Create a file named **app/page.js**

```jsx
export const metadata = {
  title: 'Next.js',
}
 
export default function Page() {
  return '...'
}
```

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Good to know**: You should **not** manually add `<head>` tags such as `<title>` and `<meta>` to root layouts. Instead, you should use the Metadata API which automatically handles advanced requirements such as streaming and de-duplicating `<head>` elements.

</aside>