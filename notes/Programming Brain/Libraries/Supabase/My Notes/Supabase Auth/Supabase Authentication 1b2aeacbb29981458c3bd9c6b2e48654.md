# Supabase Authentication

Supabase Auth **makes it easy to implement authentication and authorization in your app**. We provide client SDKs and API endpoints to help you create and manage users. Your users can use many popular Auth methods, including password, magic link, one-time password (OTP), social login, and single sign-on (SSO).

## Supabase User Signup

```jsx
"use client";

import { useRouter } from "next/navigation";
import { singupAction } from "~/src/actions/auth-action";

export default function SignupPage() {
  const router = useRouter();
  
  const handleSubmit = async (e) => {
    e.preventDefault();

    try {
      const formData = new FormData(e.currentTarget);
      const response = await singupAction(formData);
      
      if (response) {
        router.push("/login");
      }

    } catch (error) {
      console.error(error);
    }
  };

  return (
    <form
      onSubmit={handleSubmit}
      className="flex max-w-[400px] flex-col bg-gray-400 p-5">
      <label htmlFor="email">Email</label>
      <input type="email" name="email" id="email" />

      <label htmlFor="password">Password</label>
      <input type="password" name="password" id="password" />

      <button className="mt-5 w-full bg-blue-600 p-2" type="submit">
        Sign UP
      </button>
    </form>
  );
}
```

And server action look like this

```jsx
"use server";

import { createClient } from "../lib/supabase/server";

export const registerAction = async (formData) => {
  const supabase = createClient();

  try {
    let { data, error } = await supabase.auth.signUp({
      email: formData.get("email"),
      password: formData.get("password"),
    });

    if (error) {
      throw error;
    }

    return data;
  } catch (error) {
    console.error(error);
  }
};
```

## Supabase User Login

```jsx
"use client";

import { useRouter } from "next/navigation";
import { loginAction } from "~/src/actions/register-action";

export default function LoginPage() {
  const router = useRouter();
  
  const handleSubmit = async (e) => {
    e.preventDefault();

    try {
      const formData = new FormData(e.currentTarget);
      const response = await loginAction(formData);
      if (response) router.push("/");
    } catch (error) {
      console.error(error);
    }
  };

  return (
    <form
      onSubmit={handleSubmit}
      className="flex max-w-[400px] flex-col bg-gray-400 p-5">
      <label htmlFor="email">Email</label>
      <input type="email" name="email" id="email" />

      <label htmlFor="password">Password</label>
      <input type="password" name="password" id="password" />

      <button className="mt-5 w-full bg-blue-600 p-2" type="submit">
        Login
      </button>
    </form>
  );
}
```

And server action look like this

```jsx
"use server";

import { createClient } from "../lib/supabase/server";

export const loginAction = async (formData) => {
  const supabase = createClient();

  try {
    let { data, error } = await supabase.auth.signInWithPassword({
      email: formData.get("email"),
      password: formData.get("password"),
    });

    if (error) {
      throw error;
    }

    return data;
  } catch (error) {
    console.error(error);
  }
};
```

## Supabase User Singout

```jsx
"use client";

import { useRouter } from "next/navigation";
import { createClient } from "../lib/supabase/client";

export default function HomePage() {
  const router = useRouter();
  const supabase = createClient();
  
  const handleLogout = async () => {
    const { error } = await supabase.auth.signOut();

    if (error) {
      console.error("Sign out error", error);
      return;
    }

    router.push("/login");
  };

  return (
    <div>
      <button onClick={handleLogout}>Sing Out</button>
    </div>
  );
}

```