# Set Up Firebase Authentication

Before you set up and initialize the Firebase SDK for your React app, you'll need to sign up for Firebase using your Google account.

If you have a Firebase account already, sign in and follow the prompts to create a new project. Pick a suitable name for your project and click **Continue.**

For this tutorial, we will name our project **Focus-app.** Your next screen will be a prompt to enable Google Analytics. We won’t be needing it. You can choose to turn it off.

Congratulations, you have successfully set up your Firebase Console. Your next screen will be the Firebase console dashboard which will look like this:

![Screenshot--197-.png](Set%20Up%20Firebase%20Authentication%201b2aeacbb2998126b30fd8e56dedb164/Screenshot--197-.png)

There are a lot of ways to authenticate users using Firebase. For this tutorial, we will authenticate our users with their email addresses and passwords.

To start using the Firebase SDK Authentication, select the Authentication SDK among the **Build** categories.

Next, we will set up our sign-in method. Click on **Set up sign-in method** and select **Email/Password** from the list of sign-in providers.

![Screenshot--209--3.png](Set%20Up%20Firebase%20Authentication%201b2aeacbb2998126b30fd8e56dedb164/Screenshot--209--3.png)

Enable the **Email/Password** option to let users sign up using their email address and password and click on **Save**.

## Firebase Functions To Login

We use `getAuth` for authentication. And we use `signInWithEmailAndPassword` for Signing in the email and password.

```jsx
import { initializeApp } from "firebase/app";
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyCAqz7QW404kJ3LDfFHy1vVsRQBTkHvA3I",
  authDomain: "guest-book-67cdb.firebaseapp.com",
  projectId: "guest-book-67cdb",
  storageBucket: "guest-book-67cdb.appspot.com",
  messagingSenderId: "164353810421",
  appId: "1:164353810421:web:20fab12b4cfdc95b4b8abc",
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);

// Login in user with email and password
export async function loginWithEmailAndPassword(email, password) {
  try {
    await signInWithEmailAndPassword(auth, email, password);
  } catch (error) {
    console.error(error);
  }
}
```

## Firebase Functions To Register

We use `getAuth` for authentication. And we use `createUserWithEmailAndPassword` to Register a new user with the new email and password.

```jsx
import { initializeApp } from "firebase/app";
import { createUserWithEmailAndPassword, getAuth } from "firebase/auth";

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyCAqz7QW404kJ3LDfFHy1vVsRQBTkHvA3I",
  authDomain: "guest-book-67cdb.firebaseapp.com",
  projectId: "guest-book-67cdb",
  storageBucket: "guest-book-67cdb.appspot.com",
  messagingSenderId: "164353810421",
  appId: "1:164353810421:web:20fab12b4cfdc95b4b8abc",
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);

// Register user with email and password
export async function registerWithEmailAndPassword(email, password) {
  try {
    await createUserWithEmailAndPassword(auth, email, password);
  } catch (error) {
    console.error(error);
  }
}
```

## Firebase Functions To Reset Password

We use `getAuth` for authentication. And we use `sendPasswordResetEmail` to reset the user password via email address.

```jsx
import { initializeApp } from "firebase/app";
import { getAuth, sendPasswordResetEmail } from "firebase/auth";

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyCAqz7QW404kJ3LDfFHy1vVsRQBTkHvA3I",
  authDomain: "guest-book-67cdb.firebaseapp.com",
  projectId: "guest-book-67cdb",
  storageBucket: "guest-book-67cdb.appspot.com",
  messagingSenderId: "164353810421",
  appId: "1:164353810421:web:20fab12b4cfdc95b4b8abc",
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);

// User password reset with email
export async function sendPasswordReset(email) {
  try {
    await sendPasswordResetEmail(auth, email);
  } catch (error) {
    console.error(error);
  }
}
```

## Firebase Functions To Signout

We use `signOut` function to sign out current users who have already logged in to our application. This handler function triggers when the user presses sign out button.

```jsx
import { useNavigate } from "react-router-dom";
import { auth } from "../firebase";
import { signOut } from "firebase/auth";

export default function Home() {
  const navigate = useNavigate();

  const handleSignOut = () => {
    signOut(auth)
      .then(() => {
        navigate("/login");
        console.log("Signed out");
      })
      .catch((error) => {
        console.error(error);
      });
  };

  return (
    <button onClick={handleSignOut} type="button">
      SING OUT
    </button>
  );
}

```

## Firebase Functions To Social Login With Google And Facebook

In today’s world, social login options such as Google and Facebook Login have become increasingly popular. They provide an easy and convenient way for users to sign up and log in to websites without the need to create and remember new usernames and passwords.

```jsx
import { initializeApp } from "firebase/app";
import {
  getAuth,
  GoogleAuthProvider,
  FacebookAuthProvider,
  signInWithPopup,
} from "firebase/auth";

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyCAqz7QW404kJ3LDfFHy1vVsRQBTkHvA3I",
  authDomain: "guest-book-67cdb.firebaseapp.com",
  projectId: "guest-book-67cdb",
  storageBucket: "guest-book-67cdb.appspot.com",
  messagingSenderId: "164353810421",
  appId: "1:164353810421:web:20fab12b4cfdc95b4b8abc",
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
const googleAuthProvider = new GoogleAuthProvider();
const facebookAuthProvider = new FacebookAuthProvider();

// User sign in with google
export async function signInWithGoogle() {
  try {
    await signInWithPopup(auth, googleAuthProvider);
  } catch (error) {
    console.error(error);
  }
}

// User sign in with facebook
export async function signInWithFacebook() {
  try {
    await signInWithPopup(auth, facebookAuthProvider);
  } catch (error) {
    console.error(error);
  }
}
```

React Component Structure

```jsx
import { useNavigate } from "react-router-dom";
import { signInWithFacebook, signInWithGoogle } from "../firebase";

export default function Login() {
  const navigate = useNavigate();

  const handleSocialLogin = async (loginType) => {
    try {
      if (loginType === "google") {
        await signInWithGoogle();
        navigate("/home");
      } else {
        await signInWithFacebook();
        navigate("/home");
      }
    } catch (error) {
      console.error(error);
    }
  };

  return (
    <div className="flex justify-between w-full gap-5 mt-3">
      <button
        onClick={() => handleSocialLogin("google")}
        type="button"
        className="w-full p-1 text-xl text-white bg-blue-500 border rounded-md hover:bg-blue-600"
      >
        Google
      </button>

      <button
        onClick={() => handleSocialLogin("facebook")}
        type="button"
        className="w-full p-2 text-xl text-white bg-blue-500 border rounded-md tex hover:bg-blue-600"
      >
        Facebook
      </button>
    </div>
  );
}

```