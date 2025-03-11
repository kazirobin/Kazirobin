# TanStack Query

TanStack Query (FKA React Query) is often described as **the missing data-fetching library for web applications**, but in more technical terms, it makes fetching, caching, synchronizing and updating server state in your web applications a breeze.

---

[My Notes](TanStack%20Query%201b2aeacbb29981768b66e84956c7d9ca/My%20Notes%201b2aeacbb29981b99b67ddd71e26c941.md)

[My Snippets](TanStack%20Query%201b2aeacbb29981768b66e84956c7d9ca/My%20Snippets%201b2aeacbb299810f846af7397c68d294.md)

React Query is a powerful library developed by TanStack that simplifies data fetching and state management in React applications. It provides a straightforward way to manage remote data and keep it in sync with the UI.

---

## Key Features

1. **Declarative Data Fetching:** React Query promotes a declarative approach to data fetching. You define queries and mutations using hooks like `useQuery` and `useMutation`. This leads to cleaner and more organized code.
2. **Automatic Caching:** React Query includes a built-in cache that stores query results. It automatically updates data when mutations occur, ensuring your UI remains consistent.
3. **Background Data Sync:** It can automatically refetch data in the background, keeping your data fresh without manual intervention.
4. **Pagination and Infinite Scrolling:** React Query provides utilities for handling pagination and infinite scrolling effortlessly.
5. **Optimistic Updates:** You can implement optimistic updates with ease, making your app feel more responsive.

## Getting Started with React Query

Let’s dive into a basic example to see how simple it is to get started with React Query. The first thing you need to do is install the `@tanstack/react-query`library. I will use npm for the execution.

```bash
npm install @tanstack/react-query
```

After the library is installed in our application, create a provider and client to use React Query. You can create it in the `index.jsx`file in the `src`folder.

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient();

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
    </QueryClientProvider>
  </React.StrictMode>
);
```

After that, you can immediately use React Query Hooks. Let’s apply it to the `App.jsx` or something else as needed.

[**Devtools**](TanStack%20Query%201b2aeacbb29981768b66e84956c7d9ca/Devtools%201b2aeacbb299813ebad1f63480baa703.md)

[useQuery Hook](TanStack%20Query%201b2aeacbb29981768b66e84956c7d9ca/useQuery%20Hook%201b2aeacbb2998148b54ed70046aa1fd5.md)

[**useMutation Hook**](TanStack%20Query%201b2aeacbb29981768b66e84956c7d9ca/useMutation%20Hook%201b2aeacbb299812289c7c8137b5a4d1d.md)