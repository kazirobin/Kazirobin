# Protected Route

React Router is a powerful library that allows you to easily create complex routing systems in your React applications. With React Router v6, you can create protected routes using a `PrivateRoute` component. Private routes are routes that require authentication, meaning the user needs to be logged in to access them.

---

## What is a PrivateRoute?

A `PrivateRoute` is a custom route component that you can create to restrict access to certain routes in your application. It requires authentication before allowing the user to access the route. If the user is not authenticated, they will be redirected to the login page or another page that you specify.

## Creating a `PrivateRoute` Component

To create a `PrivateRoute` component, you need to define a new component that takes a `component` prop as well as any additional props you want to pass to the component. Here's an example of what the `PrivateRoute` component could look like:

Create a file named **src/routes/PrivateRoute.jsx**

```jsx
import { Outlet, Navigate } from "react-router-dom";
import useAuth from '../hooks/useAuth';

export default function PrivateRoute() {
  const { auth } = useAuth();

  return (
    <>
      {auth ? <Outlet /> : <Navigate to="/login" replace />}
    </>
  );
}
```

## What is a PublicRoute?

In a React application, we can use Private and `Public Routes` to handle Authentication. Public routes are accessible to everyone, whether they are authenticated or not. On the other hand, Private routes are only accessible to authenticated users.

## Creating a `PublicRoute` Component

To create a `PublicRoute` component, you need to define a new component that takes a `component` prop as well as any additional props you want to pass to the component. Here's an example of what the `PublicRoute` component could look like:

Create a file named **src/routes/PublicRoute.jsx**

```jsx
import { Outlet, Navigate } from "react-router-dom";
import useAuth from '../hooks/useAuth';

export default function PublicRoute() {
  const { auth } = useAuth();

  return (
    <>
      {!auth ? <Outlet /> : <Navigate to="/" replace />}
    </>
  );
}
```

In this example, we’re using the `<Route>` component from React Router v6 to render the component if the user is authenticated. If the user is not authenticated, we're using the `<Navigate>` component to redirect them to the login page.

## Using the `PrivateRoute` & `PublicRoute` Components

Now that we’ve created our `PrivateRoute` and `PublicRoute` components, we can use them to protect routes in our application. Here's an example of how you could use it to protect our all routes:

```jsx
import { Routes, Route } from "react-router-dom";
import PrivateRoute from "./routes/PrivateRoute";
import PublicRoute from "./routes/PublicRoute";

// All others import...

export default function App() {
  return (
    <Routes>
    
      <Route element={<PrivateRoute />}>
        <Route path="/profile" element={<Profile />} />
        <Route path="/blogs/:id" element={<SingleBlog />} />
        <Route path="/create-blog" element={<CreateBlog />} />
      </Route>
      
      <Route element={<PublicRoute />}>
         <Route path="/login" element={<Login />} />
         <Route path="/register" element={<Register />} />
       </Route>
       
      <Route path="/" element={<Home />} />
      <Route path="*" element={<NotFound />} />
    </Routes>
  );
}
```

In this example, we’re using the `<PrivateRoute>` component to protect the `/` route. If the user is not authenticated, they will be redirected to the `/login` route. If the user is authenticated, they will be able to access the protected component.