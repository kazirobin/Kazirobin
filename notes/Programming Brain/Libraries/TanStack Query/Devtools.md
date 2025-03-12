# Devtools

When you begin your React Query journey, you'll want these devtools by your side. They help visualize all of the inner workings of React Query and will likely save you hours of debugging if you find yourself in a pinch!

## Install and Import the Devtools

Install the react-query-devtools package from NPM by running the following command in your terminal:

```bash
npm i @tanstack/react-query-devtools
```

Import ReactQueryDevtools from the react-query-devtools package in your React application and add the ReactQueryDevtools component to your application’s render method, usually in your `App.jsx` or `main.jsx`file.

```jsx
import { ReactQueryDevtools } from '@tanstack/react-query-devtools'
```

By default, React Query Devtools are only included in bundles when **`process.env.NODE_ENV === 'development'`**, so you don't need to worry about excluding them during a production build.

## Floating Mode

Floating Mode will mount the devtools as a fixed, floating element in your app and provide a toggle in the corner of the screen to show and hide the devtools. This toggle state will be stored and remembered in localStorage across reloads.

Place the following code as high in your React app as you can. The closer it is to the root of the page, the better it will work!

```jsx
import { ReactQueryDevtools } from '@tanstack/react-query-devtools'

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/* The rest of your application */}
      <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  )
}
```