# Route Protect Middleware

Next. js middleware **provides a powerful tool to implement server-side protection for your routes**. Middleware functions generally run before the request from the user completes, allowing you to execute custom logic to determine whether they should be granted access to a particular route.

## All Route Protected

Create a file named **./src/middleware.ts**

```jsx
import { NextRequest, NextResponse } from "next/server";

export default function middleware(request: NextRequest) {
	const { nextUrl } = request;
  const isAuthenticated = false; // Replace with your own authentication logic

  // Prevent redirect loop by allowing access to the login page
  if (request.nextUrl.pathname === "/login") {
    return NextResponse.next();
  }

  if (!isAuthenticated) {
    // If no authentication is found, redirect to the login page
    return NextResponse.redirect(new URL("/login", nextUrl));
  }

  // If authentication is found, allow the request to proceed
  return NextResponse.next();
}

// Specify the paths where the middleware should be applied
export const config = {
  matcher: ["/((?!api|_next/static|_next/image|favicon.ico|public).*)"],
};
```

## Specific Route Protected

Create a file named **./src/lib/routes.ts**

```jsx
export const LOGIN = "/login";
export const ROOT = "/";

export const PRIVATE_ROUTES = ["/dashboard"];

export const AUTH_ROUTES = [
  "/login",
  "/register",
  "/forgot-password",
  "/reset-password",
  "/two-factor",
];
```

Create a file named **./src/middleware.ts**

```jsx
import { NextRequest, NextResponse } from "next/server";
import { AUTH_ROUTES, LOGIN, PRIVATE_ROUTES, ROOT } from "./lib/routes";

export default function middleware(request: NextRequest) {
  const { nextUrl } = request;
  const isAuthenticated = false; // Replace with your own authentication logic

  // Check if the route is private
  const isPrivateRoute = PRIVATE_ROUTES.find((route) =>
    nextUrl.pathname.startsWith(route),
  );

  // Check if the route is auth
  const isAuthRoute = AUTH_ROUTES.find((route) =>
    nextUrl.pathname.startsWith(route),
  );

  // Redirect to login if the route is private and the user is not authenticated
  if (!isAuthenticated && isPrivateRoute) {
    return NextResponse.redirect(new URL(LOGIN, nextUrl));
  }

  // Redirect to root if the user is authenticated and the route is auth
  if (isAuthenticated && isAuthRoute) {
    return NextResponse.redirect(new URL(ROOT, nextUrl));
  }

  return NextResponse.next();
}

export const config = {
  matcher: ["/((?!.+\\.[\\w]+$|_next).*)", "/", "/(api|trpc)(.*)"],
};
```