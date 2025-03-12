# Create Firebase Project

So, head over to [https://firebase.google.com/](https://firebase.google.com/) and create a project.

Click "Add Project" in the Firebase console.

![Screenshot-2021-11-06-184523.png](Create%20Firebase%20Project%201b2aeacbb29981a3b40fe35e5269d543/Screenshot-2021-11-06-184523.png)

After you have created a new project in Firebase, you need to create an application.

![Screenshot-2021-11-06-184708.png](Create%20Firebase%20Project%201b2aeacbb29981a3b40fe35e5269d543/Screenshot-2021-11-06-184708.png)

Click Add app, and choose Web.

![Screenshot-2021-11-06-184807.png](Create%20Firebase%20Project%201b2aeacbb29981a3b40fe35e5269d543/Screenshot-2021-11-06-184807.png)

Give the application a name of your choice, and Register the App.

![Screenshot-2021-11-06-184906.png](Create%20Firebase%20Project%201b2aeacbb29981a3b40fe35e5269d543/Screenshot-2021-11-06-184906.png)

You'll see the above screen. And we need a file where we can store all this config data, so we'll go ahead and create it.

Create a file called `src/config/firebase.js` and store all these config data in that file.

```jsx
import { initializeApp } from "firebase/app";

const firebaseConfig = {
    apiKey: "AIzaSyBtRIMLkSVfptH4ASinlEfnKhP-mBwUV24",
    authDomain: "react-register-12564.firebaseapp.com",
    projectId: "react-register-12564",
    storageBucket: "react-register-12564.appspot.com",
    messagingSenderId: "1074586181097",
    appId: "1:1074586181097:web:47236fd450006cd1fabf78",
    measurementId: "G-JSN76LC2EC"
};

export const app = initializeApp(firebaseConfig);
```

Now, let's install React Router and Firebase using the command below.

```bash
npm install firebase react-router-dom
```