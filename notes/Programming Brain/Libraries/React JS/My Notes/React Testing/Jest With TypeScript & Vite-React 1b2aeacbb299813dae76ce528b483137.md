# Jest With TypeScript & Vite-React

`CreatedAt- 08 Nov 2024 / RevisedAt-` 

Let's get started by creating a simple Vite project. Run the following command to create a React application using Vite: `npm create vite@latest` . Follow the instructions and select the necessary dependencies.

Now, cd into your project directory and `run npm install` to install all dependencies.

## Installing Jest and React testing library

Now let's install `Jest` and `RTL` and other related dependencies:

```bash
npm install -D jest @testing-library/react @testing-library/user-event ts-jest @types/jest ts-node @testing-library/jest-dom jest-environment-jsdom
```

And wait for the packages to finish installing.

Great, now if you open your `package.json` file, you should see all of these packages as dev dependencies.

Now create a `jest.setup.ts` file in root directory with the following code :

```jsx
import "@testing-library/jest-dom";
```

Also, create a `jest.config.ts` file in root directory with the following configuration code:

```jsx
export default {
  testEnvironment: "jsdom",
  setupFilesAfterEnv: ["<rootDir>/jest.setup.ts"]
};
```

## Handling Styles and SVG's

Now we need 2 more packages for our test to run correctly, the first package is `identity-obj-proxy` which will help jest transform files with the extension `.css, .less, .sass, or .scss` When a file with any of these extensions is imported into your code during testing, Jest will substitute the import with the identity-obj-proxy module. This is a common technique for mocking stylesheets in Jest tests.

The second package we need is `jest-transformer-svg` When an SVG file is imported into your code during testing, Jest will substitute the import with the jest-transformer-svg module. This suggests that there might be a custom transformer (jest-transformer-svg) configured for transforming SVG files during the testing process.

To install this package, run:

```bash
npm install -D identity-obj-proxy jest-transformer-svg
```

After successfully installing, modify your `jest.config.ts` file to look like so:

```jsx
export default {
  testEnvironment: "jsdom",

  moduleNameMapper: {
    "\\.(css|less|sass|scss)$": "identity-obj-proxy",
    "^.+\\.svg$": "jest-transformer-svg",
  },

  setupFilesAfterEnv: ["<rootDir>/jest.setup.ts"],
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

Let's create a simple component that renders a list of users, with some tests for that component. Create a `components` folder in the `src` directory and create `*users.tsx*` file and a `user.test.tsx` file

The `users.tsx` component looks like this:

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

Our test for this component in the `users.test.tsx` file looks like this:

```jsx
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

![https___dev-to-uploads.s3.amazonaws.com_uploads_articles_6tis7rxfd41hjd766igk.png](Jest%20With%20TypeScript%20&%20Vite-React%201b2aeacbb299813dae76ce528b483137/https___dev-to-uploads.s3.amazonaws.com_uploads_articles_6tis7rxfd41hjd766igk.png)

Our test passes..in some cases, this will fail because of the following Typescript error:

![https___dev-to-uploads.s3.amazonaws.com_uploads_articles_39ervmfpxp8dazjfejgq.png](Jest%20With%20TypeScript%20&%20Vite-React%201b2aeacbb299813dae76ce528b483137/https___dev-to-uploads.s3.amazonaws.com_uploads_articles_39ervmfpxp8dazjfejgq.png)

We fix this by including our `jest.setup.ts` file in our `tsconfig.json` file like so:

```json
{
  "include": ["src", "./jest.setup.ts"]
}
```

Specifically, we add `./jest.setup.ts` as an array value of the include property. Our Typescript error now disappears and our test runs smoothly.

## Handling absolute imports

When setting up our applications, some of our applications might be making use of absolutes imports for clean and readable import statements. However, using absolute imports with Jest will need tiny adjustments, Firstly let's set up absolute import or path aliases in our Vite app and then make it work with Jest. To do that, we need to install the following package

```bash
npm install -D vite-tsconfig-paths
```

After successful installation, we need to modify the `vite.config.ts` file and the `tsconfig.json` file. add the following code as part of the `compilerOptions` property.

```json
"baseUrl": "./src",
    "paths": {
      "@/*": ["./*"]
    }
```

Our `tsconfig.json` file looks like this

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,

    //absolute import
    "baseUrl": "./src",
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["src", "./jest.setup.ts"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

We also modify our `vite.config.ts` file

```jsx
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tsconfigPaths from "vite-tsconfig-paths";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react(), tsconfigPaths()],
});
```

In your `jest.config.ts` file, add `"^@/(.*)$": "/src/$1"` to the `moduleNameMapper` property.

```jsx

export default {
  testEnvironment: "jsdom",
  transform: {
    "^.+\\.tsx?$": "ts-jest",
  },

  moduleNameMapper: {
    "\\.(css|less|sass|scss)$": "identity-obj-proxy",
    "^.+\\.svg$": "jest-transformer-svg",
    "^@/(.*)$": "<rootDir>/src/$1",
  },

  setupFilesAfterEnv: ["<rootDir>/jest.setup.ts"],
};
```

Amazing!! now you can import components like so:

```jsx
import Counter from "@/components/counter-two/Counter-two";
```

using the `@` path alias and use them in your test.

## Getting test coverage report

Most often when writing tests, we need to know the test coverage. Code coverage reports provide insights into how much of your code is covered by tests. We need a command to Instruct Jest to generate code coverage reports after running the tests. Add the following command to your script in the `package.json` file

```json
"coverage": "npm test --coverage --watchAll --collectCoverageFrom='src/components/**/*.{ts,tsx}'",
```

We then run `npm run coverage` . This runs Jest in watch mode and provides the coverage report after every test run.

![https___dev-to-uploads.s3.amazonaws.com_uploads_articles_4gmgejd5tydyjv4lrqni.png](Jest%20With%20TypeScript%20&%20Vite-React%201b2aeacbb299813dae76ce528b483137/https___dev-to-uploads.s3.amazonaws.com_uploads_articles_4gmgejd5tydyjv4lrqni.png)