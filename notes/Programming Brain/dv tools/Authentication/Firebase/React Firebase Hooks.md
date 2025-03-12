# React Firebase Hooks

React Firebase Hooks provides a convenience listener for Firebase Auth's auth state. The hook wraps around the `auth.onAuthStateChange(...)` method to ensure that it is always up to date.

All hooks can be imported from `react-firebase-hooks/auth`, e.g.

```jsx
import { useAuthState } from 'react-firebase-hooks/auth';
```

Now, let's install useAuthState using the command below.

```bash
npm install --save react-firebase-hooks
```

### The `useAuthState` hook takes the following parameters:

- `auth`: `auth.Auth` instance for the app you would like to monitor
- `options`: (optional) `Object with the following parameters:
- `onUserChanged`: (optional) function to be called with `auth.User` each time the user changes. This allows you to do things like load custom claims.

### The `useAuthState` hook return the following values:

- `user`: The `auth.UserCredential` if logged in, or `null` if not
- `loading`: A `boolean` to indicate whether the authentication state is still being loaded
- `error`: Any `AuthError` returned by Firebase when trying to load the user, or `undefined` if there is no error

```jsx
const [user, loading, error] = useAuthState(auth, options);
```

If you are registering or signing in the user for the first time consider using useCreateUserWithEmailAndPassword, useSignInWithEmailAndPassword. See this example

```jsx
import { auth } from "../firebase";
import { useAuthState } from "react-firebase-hooks/auth";

export default function Home() {
  const [user, loading, error] = useAuthState(auth);

  if (loading && !user && !error) return <p>User Loading...</p>;
  if (!loading && !user && error) return <p>User Not Found</p>;

  return (
    <h1 >
        Welcome, {user?.email ?? "User not login"}
    </h1>
  );
}
```