# Jest With JavaScript & Vite-React

Let's get started by creating a simple Vite project. Run the following command to create a React application using Vite: `npm create vite@latest` . Follow the instructions and select the necessary dependencies.

Now, cd into your project directory and `run npm install` to install all dependencies.

## Installing Jest and React testing library

Now let's install `Jest` and `RTL` and other related dependencies:

```bash
npm install -D jest @testing-library/react @testing-library/user-event @testing-library/jest-dom jest-environment-jsdom
```

And wait for the packages to finish installing.

Great, now if you open your `package.json` file, you should see all of these packages as dev dependencies.

Now create a `jest.setup.js` file in root directory with the following code :

```jsx
import "@testing-library/jest-dom";
```

Also, create a `jest.config.js` file in root directory with the following configuration code:

```jsx
export default {
  testEnvironment: "jsdom",
  setupFilesAfterEnv: ["./jest.setup.js"]
};
```

## Handling Styles and SVG's

Now we need 2 more packages for our test to run correctly, the first package is `identity-obj-proxy` which will help jest transform files with the extension `.css, .less, .sass, or .scss` When a file with any of these extensions is imported into your code during testing, Jest will substitute the import with the identity-obj-proxy module. This is a common technique for mocking stylesheets in Jest tests.

The second package we need is `jest-transformer-svg` When an SVG file is imported into your code during testing, Jest will substitute the import with the jest-transformer-svg module. This suggests that there might be a custom transformer (jest-transformer-svg) configured for transforming SVG files during the testing process.

To install this package, run:

```bash
npm install -D identity-obj-proxy jest-transformer-svg
```

After successfully installing, modify your `jest.config.js` file to look like so:

```jsx
export default {
  testEnvironment: "jsdom",

  moduleNameMapper: {
    "\\.(css|less|sass|scss)$": "identity-obj-proxy",
    "^.+\\.svg$": "jest-transformer-svg",
  },

  setupFilesAfterEnv: ["./jest.setup.ts"],
};
```

Great!!, we have done a lot of configuration, let's write a test and see if things work correctly. Firstly, head over to your package.json and add the following script : `"test": "jest"`

```json
 "scripts": {
    "test": "jest"
  }
```

For JSX support, add babel presets and add  `babel.config.json` to your project

```jsx
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

And install all dependencies from babel

```bash
npm install -D @babel/preset-env @babel/preset-react
```

Extends `eslint.config.js` with following code for avoiding `eslint` error

```jsx
extends: ["react-app", "react-app/jest"]
```

Let's create a simple component that renders a list of users, with some tests for that component. Create a `components` folder in the `src` directory and create `*users.jsx*` file and a `user.test.jsx` file.

The `users.jsx` component looks like this:

```jsx
import React from "react";

export default function Users() {
  return (
    <div>
      <h1>Users</h1>
      <ul>
        <li>name 1</li>
        <li>name 2</li>
      </ul>
    </div>
  );
}
```

Our test for this component in the `users.test.jsx` file looks like this:

```jsx
import React from "react";
import { render, screen } from "@testing-library/react";
import Users from "./User";

describe("User", () => {
  test("renders heading", async () => {
    render(<Users />);
    expect(screen.getByRole("heading", { name: "Users" })).toBeInTheDocument();
  });

  test("renders a list of users", async () => {
    render(<Users />);
    const users = await screen.findAllByRole("listitem");
    expect(users).toHaveLength(2);
  });
});
```

We have a simple component with some test setup. let's try to run our test using the `npm run test` command.

![https___dev-to-uploads.s3.amazonaws.com_uploads_articles_6tis7rxfd41hjd766igk.png](Jest%20With%20JavaScript%20&%20Vite-React%201b2aeacbb299810485cac780ea8ee09a/https___dev-to-uploads.s3.amazonaws.com_uploads_articles_6tis7rxfd41hjd766igk.png)