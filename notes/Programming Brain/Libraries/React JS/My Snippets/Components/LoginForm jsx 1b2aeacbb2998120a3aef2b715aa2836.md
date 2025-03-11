# LoginForm.jsx

Make a reusable form component using this snippet of code.

Crate a file named **LoginForm.jsx**

```jsx
import Field from "../Field";
import Fieldset from "../Fieldset";

export default function LoginForm() {
  return (
    <div>
      <form>
        <Fieldset label="Enter login details">
          <Field label="Email">
            <input
              className="p-2 border border-gray-500 rounded-md"
              type="text"
              name="email"
              id="email"
              placeholder="Enter email"
            />
          </Field>

          <Field label="Password">
            <input
              className="p-2 border border-gray-500 rounded-md"
              type="password"
              name="password"
              id="password"
              placeholder="Enter password"
            />
          </Field>
        </Fieldset>
        <button className="p-1 text-white bg-blue-500 border rounded-md cursor-pointer w-[100px]" type="submit">Login</button>
      </form>
    </div>
  );
}
```

Crate a file named **Field.jsx**

```jsx
import React from "react";

export default function Field({ label, children, htmlFor, error }) {
  const id = htmlFor || getChildId(children);

  return (
    <div className="flex flex-col items-start justify-start w-full p-0 mt-2 mr-2">
      {label && <label htmlFor={id} className="mb-1">{label}</label>}
      {children}
      {error && <div className="text-red-500">{error.message}</div>}
    </div>
  );
}

const getChildId = (children) => {
  const child = React.Children.only(children);

  if ("id" in child?.props) {
    return child.props.id;
  }
};
```

Crate a file named **FieldSet.jsx**

```jsx
export default function Fieldset({ label, children }) {
  return (
    <fieldset className="p-0 m-2 border-none">
      {label && <legend className="mb-2 font-bold text-md">{label}</legend>}
      <div className="flex flex-col self-start justify-between">{children}</div>
    </fieldset>
  );
}
```