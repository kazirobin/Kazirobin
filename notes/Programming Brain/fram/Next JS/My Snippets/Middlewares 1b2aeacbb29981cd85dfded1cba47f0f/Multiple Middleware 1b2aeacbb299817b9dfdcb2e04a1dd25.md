# Multiple Middleware

We’ll show you how to combine multiple middleware functions using a chain utility. We’ll create middleware for two separate tasks, and then chain them together to create a single middleware function. This approach allows us to easily add more middleware functions in the future without cluttering our codebase. You can use this setup to add additional features like logging, caching, or error handling to your Next.js application.

### 1. Middleware With Two Separate Functions

Create a file named **src/middleware.ts**

```tsx
import type { NextRequest } from "next/server";
import { NextResponse } from "next/server";

// Middleware 1 that logs the request URL
async function middleware1(request: NextRequest) {
  const url = request.url;
  console.log(`Request to -> ${url}`);

  return NextResponse.next();
}

// Middleware 2 that logs the request pathname
async function middleware2(request: NextRequest) {
  const pathname = request.nextUrl.pathname;
  console.log(`Request to pathname -> ${pathname}`);

  return NextResponse.next();
}

export async function middleware(request: NextRequest) {
  await middleware1(request);
  await middleware2(request);
}

export const config = {
  matcher: ["/((?!api|_next/static|_next/image|favicon.ico).*)"],
};
```

### 2. Middleware With Higher Order Function

Create a file named **src/middleware.ts**

```tsx
import type { NextFetchEvent, NextMiddleware, NextRequest } from "next/server";
import { NextResponse } from "next/server";

// Higher order function that logs the request URL
function withMiddleware(middleware: NextMiddleware) {
  return async (request: NextRequest, event: NextFetchEvent) => {
    const url = request.url;
    console.log(`Request to -> ${url}`);

    return middleware(request, event);
  };
}

// Middleware 2 that logs the request pathname
function middleware2(request: NextRequest) {
  const pathname = request.nextUrl.pathname;
  console.log(`Request to pathname -> ${pathname}`);

  return NextResponse.next();
}

export default withMiddleware(middleware2);

export const config = {
  matcher: ["/((?!api|_next/static|_next/image|favicon.ico).*)"],
};

```

### 3. Middleware With Chaining

Create a `chain.ts` file in the `/src/middlewares` directory:

```tsx
import { NextMiddlewareResult } from "next/dist/server/web/types";
import type { NextFetchEvent, NextRequest } from "next/server";
import { NextResponse } from "next/server";

export type CustomMiddleware = (
  request: NextRequest,
  event: NextFetchEvent,
  response: NextResponse,
) => NextMiddlewareResult | Promise<NextMiddlewareResult>;

type MiddlewareFactory = (middleware: CustomMiddleware) => CustomMiddleware;

export function chain(
  functions: MiddlewareFactory[],
  index = 0,
): CustomMiddleware {
  const currentMiddleware = functions[index];

  if (currentMiddleware) {
    const next = chain(functions, index + 1);
    return currentMiddleware(next);
  }

  return (
    request: NextRequest,
    event: NextFetchEvent,
    response: NextResponse,
  ) => {
    return response;
  };
}
```

Create a `withMiddleware1.ts` file in the `/src/middlewares` directory:

```tsx
import { NextFetchEvent, NextRequest } from "next/server";
import { CustomMiddleware } from "./chain";

export function withMiddleware1(middleware: CustomMiddleware) {
  return async (request: NextRequest, event: NextFetchEvent) => {
    const url = request.url;
    console.log(`Request to -> ${url}`);

    return middleware(request, event);
  };
}
```

Create a `withMiddleware2.ts` file in the `/src/middlewares` directory:

```tsx
import { NextFetchEvent, NextMiddleware, NextRequest } from "next/server";

export function withMiddleware2(middleware: NextMiddleware) {
  return async (request: NextRequest, event: NextFetchEvent) => {
    const pathname = request.nextUrl.pathname;
    console.log(`Request to pathname -> ${pathname}`);

    return middleware(request, event);
  };
}
```

Create a `middleware.ts` file in the `/src` directory:

```tsx
import { chain } from '@/middlewares/chain'
import { withMiddleware1 } from '@/middlewares/middleware1'
import { withMiddleware2 } from '@/middlewares/middleware2'

const middlewares = [withMiddleware1, withMiddleware2];
export default chain(middlewares);

export const config = {
  matcher: ['/((?!api|_next/static|_next/image|favicon.ico).*)']
}
```