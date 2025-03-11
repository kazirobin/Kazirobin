# Quick Start

React Hook Form is a library that helps you validate forms in React. It is a minimal library without any other dependencies, while being performant and straightforward to use, requiring developers to write fewer lines of code than other form libraries.

## What is React Hook Form?

React Hook Form takes a slightly different approach than other form libraries in the React ecosystem by adopting the use of uncontrolled inputs using `ref` instead of depending on the state to control the inputs. This approach makes the forms more performant and reduces the number of re-renders.

The API is very intuitive, which provides a seamless experience to developers. React Hook Form follows HTML standards for validating the forms using a constraint-based validation API.

To install React Hook Form, run the following command:

```bash
npm install react-hook-form
```

## How to use React Hooks in a form

In this section, you will learn about the fundamentals of the `useForm` Hook by creating a very basic registration form. 

First, import the `useForm` Hook from the `react-hook-form` package:

```jsx
import { useForm } from "react-hook-form";
```

Then, inside your component, use the Hook as follows:

```jsx
const { register, handleSubmit } = useForm();
```

The `useForm` Hook returns an object containing a few properties. For now, you only require `register` and `handleSubmit`.

The `register` method helps you register an input field into React Hook Form so that it is available for the validation, and its value can be tracked for changes.

To register the input, we’ll pass the `register` method into the input field as such:

```jsx
<input type="text" name="firstName" {...register('firstName')} />
```

This spread operator syntax is a new implementation to the library that enables strict type checking in forms with TypeScript. You can learn more about strict type checking in React Hook Form here.

Versions older than v7 had the register method attached to the `ref` attribute as such:

```jsx
<input type="text" name="firstName" ref={register} />
```

Note that the input component must have a `name` prop, and its value should be unique.

The `handleSubmit` method, as the name suggests, manages form submission. It needs to be passed as the value to the `onSubmit` prop of the `form` component.

The `handleSubmit` method can handle two functions as arguments. The first function passed as an argument will be invoked along with the registered field values when the form validation is successful. The second function is called with errors when the validation fails.

```jsx
const onFormSubmit  = data => console.log(data);

const onErrors = errors => console.error(errors);

<form onSubmit={handleSubmit(onFormSubmit, onErrors)}>
 {/* ... */}
</form>
```

Now that you have a fair idea about the basic usage of the `useForm` Hook, let’s take a look at a more realistic example:

```jsx
import React from "react";
import { useForm } from "react-hook-form";

const RegisterForm = () => {
  const { register, handleSubmit } = useForm();
  const handleRegistration = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(handleRegistration)}>
      <div>
        <label>Name</label>
        <input name="name" {...register('name')} />
      </div>
      <div>
        <label>Email</label>
        <input type="email" name="email" {...register('email')} />
      </div>
      <div>
        <label>Password</label>
        <input type="password" name="password" {...register('password')} />
      </div>
      <button>Submit</button>
    </form>
  );
};
export default RegisterForm;
```

As you can see, no other components were imported to track the input values. The `useForm` Hook makes the component code cleaner and easier to maintain, and because the form is uncontrolled, you do not have to pass props like `onChange` and `value` to each input.