# Form Validations With Yup

Validating user input on forms prior to submission, in my opinion, is one of the most important and fundamental things about a website these days.

Thank god we have several options to validate them, in the React ecosystem there are lots of libraries. However many of these libraries either end up having a huge boilerplate, which is sometimes scary, even when implementing in a form with few fields. Or they decrease application performance.

Keeping these points in mind, I always end up looking for a solution that is simple, with little boilerplate and that has a great performance.

Apart from that, another thing I'm looking for is a form validation library that lets you use a library to validate schemas, such as Joi, Yup, etc. This way I can reuse the schema code in the frontend and backend.

It's exactly for all these reasons that I love working with React Hook Form.

First we will add the following dependencies to our React application:

```jsx
npm install react-hook-form @hookform/resolvers yup
```

Now let's pretend this is your form:

```jsx
import React from "react";

const App = () => {
  return (
    <form>
      <h2>Lets sign you in.</h2>
      <br />

      <input placeholder="email" type="email" required />
      <br />

      <input
        placeholder="password"
        type="password"
        required
      />
      <br />

      <button type="submit">Sign in</button>
    </form>
  );
};

export default App;
```

Now let's import `React Hook Form` into our project:

```jsx
import { useForm } from "react-hook-form";
```

Then let's get the following things from the `useForm()` hook:

```jsx
const App = () => {
  const { register, handleSubmit, formState: { errors }, reset } = useForm();
  return (
    // other code
};
```

## Quick overview

- The `register()` method allows registering an element and applying the appropriate validation rules.
- The `handleSubmit()` function will receive the form data if validation is successful.
- The `reset()` function will clear all form fields or reset to initial values.
- In this case, we are using `formState` to return form errors in an easier way.

Now we have to import Yup into our project and then let's create our schema.

```jsx
import * as yup from "yup";

const schema = yup.object({
  email: yup.string().email().required(),
  password: yup.string().min(8).max(32).required(),
});
```

Now we have to import `@hookform/resolvers` so we can use our Yup schema to validate input values. Like this:

```jsx
import { yupResolver } from "@hookform/resolvers/yup";

const App = () => {
  const { register, handleSubmit, formState: { errors }, reset } = useForm({
    resolver: yupResolver(schema),
  });
  return (
    // other code
};
```

Now we have to create our function to submit the data (which in this example will be a simple log). Just like we're going to add the `reset()` method inside our function so that form inputs are cleared as soon as they're submitted.

Lastly let's add the `handleSubmit()` method to our form. Similar to this:

```jsx
const App = () => {
  const { register, handleSubmit, formState: { errors, isSubmitSuccessful }, reset } = useForm({
    resolver: yupResolver(schema),
  });
  const onSubmitHandler = (data) => {
    console.log({ data });
  };
  
    useEffect(() => {
    if (isSubmitSuccessful) {
      reset();
    }
  }, [isSubmitSuccessful, reset]);
  
  return (
    <form onSubmit={handleSubmit(onSubmitHandler)}>
      // other code
    </form>
};
```

The next step is to register our inputs, assigning their names according to the properties of our schema:

```jsx
const App = () => {
  return (
    <form onSubmit={handleSubmit(onSubmitHandler)}>
      <h2>Lets sign you in.</h2>
      <br />

      <input {...register("email")} placeholder="email" type="email" required />
      <br />

      <input
        {...register("password")}
        placeholder="password"
        type="password"
        required
      />
      <br />

      <button type="submit">Sign in</button>
    </form>
  );
};
```