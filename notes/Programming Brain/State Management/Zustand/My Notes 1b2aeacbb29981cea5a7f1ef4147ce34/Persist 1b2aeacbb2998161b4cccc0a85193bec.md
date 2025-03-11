# Persist

Zustand’s `persist` middleware allows you to persist the state of your store across page reloads by saving it to local storage or session storage. This is particularly useful for keeping user settings, preferences, or any other state that you want to retain even after a browser refresh.

### Create a Store with Persist Middleware

Here’s a basic example of how to set up a Zustand store with the `persist` middleware:

```jsx
import create from 'zustand';
import { persist } from 'zustand/middleware';

// Define a Zustand store with persist middleware
const useStore = create(persist(
  (set) => ({
    count: 0,
    increment: () => set((state) => ({ count: state.count + 1 })),
    reset: () => set({ count: 0 }),
  }),
  {
    name: 'my-store', // Unique name for the storage key
    getStorage: () => localStorage, // Use localStorage to persist data
  }
));

export default useStore;
```

In this example:

- `persist` is imported from `zustand/middleware`.
- The `create` function from Zustand is used to create a store.
- The store state is defined with methods to increment and reset the `count`.
- The `persist` middleware configuration includes:
    - `name`: A unique key for local storage to identify the persisted data.
    - `getStorage`: Function to specify which storage to use (`localStorage` or `sessionStorage`).

You might want to customize the behavior of the `persist` middleware further, for instance, by handling migrations or versioning.

You can add migration logic to handle changes in your store schema over time:

```jsx
import create from 'zustand';
import { persist } from 'zustand/middleware';

// Define a Zustand store with persist middleware and migration
const useStore = create(persist(
  (set) => ({
    count: 0,
    increment: () => set((state) => ({ count: state.count + 1 })),
    reset: () => set({ count: 0 }),
  }),
  {
    name: 'my-store',
    getStorage: () => localStorage,
    version: 1, // Version of your persisted data schema
    migrate: (persistedState, version) => {
      if (version === 1) {
        // Handle migration for version 1
        return persistedState;
      }
      // Handle migration for other versions or return default state
      return { count: 0 };
    },
  }
));

export default useStore;
```

If you prefer to use session storage instead of local storage:

```jsx
import create from 'zustand';
import { persist } from 'zustand/middleware';

// Define a Zustand store with persist middleware using session storage
const useStore = create(persist(
  (set) => ({
    count: 0,
    increment: () => set((state) => ({ count: state.count + 1 })),
    reset: () => set({ count: 0 }),
  }),
  {
    name: 'my-session-store', // Unique name for session storage key
    getStorage: () => sessionStorage, // Use sessionStorage to persist data
  }
));

export default useStore;
```