# Form Validations

To apply validations to a field, you can pass validation parameters to the register method. Validation parameters are similar to the existing HTML form validation standard.

These validation parameters include the following properties:

- `required` indicates if the field is required or not. If this property is set to `true`, then the field cannot be empty.
- `minlength` and `maxlength` set the minimum and maximum length for a string input value.
- `min` and `max` set the minimum and maximum values for a numerical value.
- `type` indicates the type of the input field; it can be email, number, text, or any other standard HTML input types.
- `pattern` defines a pattern for the input value using a regular expression.

If you want to mark a field as `required`, you code should turn out like this:

```jsx
<input name="name" type="text" {...register('name', { required: true } )} />
```

Now try submitting the form with this field empty. This will result in the following error object:

```jsx
{
name: {
  type: "required",
  message: "",
  ref: <input name="name" type="text" />
  }
}
```

Here, the `type` property refers to the type of validation that failed, and the `ref` property contains the native DOM input element.

You can also include a custom error message for the field by passing a string instead of a boolean to the validation property:

```jsx
// ...
<form onSubmit={handleSubmit(handleRegistration, handleError)}>
  <div>
      <label>Name</label>
      <input name="name" {...register('name', { required: "Name is required" } )} />
  </div>
</form>
```

Then, access the errors object by using the `useForm` Hook:

```jsx
const { register, handleSubmit, formState: { errors } } = useForm();
```

You can display errors to your users like so:

```jsx
const RegisterForm = () => {
  const { register, handleSubmit, formState: { errors } } = useForm();
  const handleRegistration = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(handleRegistration)}>
      <div>
        <label>Name</label>
        <input type="text" name="name" {...register('name', { required: "Name is required" })} />
        {errors?.name && errors.name.message}
      </div>
      {/* more input fields... */}
      <button>Submit</button>
    </form>
  );
};
```

```jsx
const RegisterForm = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();
  const handleRegistration = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(handleRegistration)}>
      <div>
        <label>Email</label>
        <input
          type="email"
          name="email"
          {...register("email", {
            required: "Email is required.",
            pattern: {
                value: /^[a-zA-Z0–9._-]+@[a-zA-Z0–9.-]+\.[a-zA-Z]{2,4}$/,
                message: "Invalid email address",
              },
          })}
        />
        {errors?.email && errors.email.message}
      </div>

      <div>
        <label>Email</label>
        <input
          type="password"
          name="password"
          {...register("password", {
            required: "Password is required.",
            minLength: {
              value: 6,
              message: "Password should be at-least 6 characters.",
            },
            
            pattern: {
                  value:
                    /^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#\$%\^&\?*])(?=.{8,})/,
                  message: "Enter strong password",
            }
          })}
        />
        {errors?.password && errors.password.message}
      </div>
      {/* more input fields... */}
      <button>Submit</button>
    </form>
  );
};
```

In the code above, we have changed the email and password validation code.

For the email input field, we changed this previous code:

```jsx
{...register("email", {
     required: true,
     pattern: /^[^@ ]+@[^@ ]+\.[^@ .]{2,}$/
 })}
```

to the below code:

```jsx
{...register("email", {
    required: "Email is required.",
    pattern: {
        value: /^[^@ ]+@[^@ ]+\.[^@ .]{2,}$/,
        message: "Email is not valid."
    }
})}
```

If you want to validate the field when there is an `onChange` or `onBlur` event, you can pass a `mode` property to the `useForm` Hook:

```jsx
const { register, handleSubmit, errors } = useForm({
  mode: "onBlur"
});
```

## How to Add a Multiple Validations

You can even provide multiple validations for the input field by adding a `validate` object. This is useful if you need to perform complex validations like this:

```jsx
 <input
    type="password"
    name="password"
    {...register("password", {
        required: true,
        validate: {
            checkLength: (value) => value.length >= 8,
            matchPattern: (value) =>
            /(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?!.*\s)(?=.*[!@#$*])/.test(
                value
            )
        }
    })}
/>
```

and to display the error messages, we use it like this:

```jsx
{errors.password?.type === "required" && (
    <p className="errorMsg">Password is required.</p>
)}
{errors.password?.type === "checkLength" && (
    <p className="errorMsg">
    	Password should be at-least 8 characters.
    </p>
)}
{errors.password?.type === "matchPattern" && (
    <p className="errorMsg">
    	Password should contain at least one uppercase letter, lowercase
letter, digit, and special symbol.
    </p>
)}
```