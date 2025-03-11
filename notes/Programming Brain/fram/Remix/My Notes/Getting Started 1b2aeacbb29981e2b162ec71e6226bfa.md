# Getting Started

`CreatedAt- 09 Dec 2024 / RevisedAt-` 

**This guide will get you familiar with the basic plumbing required to run a Remix app as quickly as possible. While there are many starter templates with different runtimes, deploy targets, and databases, we're going to create a bare-bones project from scratch.**

When you're ready to get serious about your Remix project, you might consider starting with a community template. They include TypeScript setups, databases, testing harnesses, authentication, and more. 

## Installation

The `create-remix` CLI will create a new Remix project. Without passing arguments, this command will launch an interactive CLI to configure the new project and set it up in a given directory.

```bash
npx create-remix@latest
```

Optionally you can pass the desired directory path as an argument:

```bash
npx create-remix@latest <projectDir>
```

The default application is a TypeScript app using the built in Remix App Server. If you wish to create your application based on a different setup, you can use the `--template` flag:

```bash
npx create-remix@latest --template <templateUrl>
```

To get a full list of available commands and flags, run:

```bash
npx create-remix@latest --help
```

However, this guide will explain everything the CLI does to set up your project, and instead of using the CLI you can follow these steps. If you're just getting started with Remix, we recommend following this guide to understand all of the different pieces that make up a Remix app.

```bash
mkdir my-remix-app
cd my-remix-app
npm init -y

# install runtime dependencies
npm i @remix-run/node @remix-run/react @remix-run/serve isbot@4 react react-dom

# install dev dependencies
npm i -D @remix-run/dev vite
```

## Vite Config

```bash
touch vite.config.js
```

Since Remix uses Vite, you'll need to provide a Vite config with the Remix Vite plugin. Here's the basic configuration you'll need:

```jsx
import { vitePlugin as remix } from "@remix-run/dev";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [remix()],
});
```

## The Root Route

```bash
mkdir app
touch app/root.jsx
```

`app/root.jsx` is what we call the "Root Route". It's the root layout of your entire app. Here's the basic set of elements you'll need for any project:

```jsx
import {
  Links,
  Meta,
  Outlet,
  Scripts,
} from "@remix-run/react";

export default function App() {
  return (
    <html>
      <head>
        <link
          rel="icon"
          href="data:image/x-icon;base64,AA"
        />
        <Meta />
        <Links />
      </head>
      <body>
        <h1>Hello world!</h1>
        <Outlet />

        <Scripts />
      </body>
    </html>
  );
}
```

## Build and Run

First build the app for production:

```bash
npx remix vite:build
```

You should now see a `build` folder containing a `server` folder (the server version of your app) and a `client` folder (the browser version) with some build artifacts in them.

**Run the app with `remix-serve`**

First you will need to specify the type in `package.json` as module so that `remix-serve` can run your app.

```json
{
  "type": "module"
  // ...
}
```

Now you can run your app with `remix-serve`:

```bash
# note the dash!
npx remix-serve build/server/index.js
```

You should be able to open up `http://localhost:3000` and see the "hello world" page.

Aside from the unholy amount of code in `node_modules`, our Remix app is just one file:

```bash
├── app/
│   └── root.jsx
└── package.json
└── vite.config.js
```

## Bring Your Own Server

The `build/server` directory created by `remix vite:build` is just a module that you run inside a server like Express, Cloudflare Workers, Netlify, Vercel, Fastly, AWS, Deno, Azure, Fastify, Firebase, ... anywhere.

If you don't care to set up your own server, you can use `remix-serve`. It's a simple express-based server maintained by the Remix team. However, Remix is specifically designed to run in *any* JavaScript environment so that you own your stack. It is expected many —if not most— production apps will have their own server. You can read more about this in Runtimes, Adapters, and Stacks.

Just for kicks, let's stop using `remix-serve` and use express instead.

Install Express, the Remix Express adapter, and [cross-env](https://www.npmjs.com/package/cross-env) for running in production mode

```bash
npm i express @remix-run/express cross-env

# not going to use this anymore
npm uninstall @remix-run/serve
```

Create an Express server

```bash
touch server.js
```

```jsx
import { createRequestHandler } from "@remix-run/express";
import express from "express";

// notice that the result of `remix vite:build` is "just a module"
import * as build from "./build/server/index.js";

const app = express();
app.use(express.static("build/client"));

// and your app is "just a request handler"
app.all("*", createRequestHandler({ build }));

app.listen(3000, () => {
  console.log("App listening on http://localhost:3000");
});
```

Run your app with express

```bash
node server.js
```

Now that you own your server, you can debug your app with whatever tooling your server has. For example, you can inspect your app with chrome devtools with the Node.js inspect flag:

```bash
node --inspect server.js
```