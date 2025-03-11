# NPM Workspace

`CreatedAt- 19 Jan 2025 / RevisedAt-` 

A strong toolkit for managing multiple package repositories inside of a single repository is offered by npm workspaces. With the help of this functionality, developers may manage dependencies, version many related packages, and develop more quickly. We'll go over the foundations of npm workspaces and how to use them successfully.

NPM Workspaces are a game-changer when it comes to organizing and managing multi-package projects. They allow you to handle dependencies and scripts across multiple packages in a streamlined way, making your development process smoother and more efficient.

## What Are NPM Workspaces?

Before we get our hands dirty, let’s clarify what NPM Workspaces are. In simple terms, NPM Workspaces allow you to manage multiple packages within a single repository (often called a monorepo). Think of them as a way to organize and streamline your projects by grouping related packages together under one umbrella.

For example, let’s say you’re working on a project that includes a core library, a CLI tool, and a set of plugins. Instead of managing each of these packages separately, you can bring them together using NPM Workspaces, making it easier to share dependencies and scripts between them.

## **How Do They Work?**

NPM Workspaces are configured through your main `package.json` file. By adding a `workspaces` field, you can specify which directories (or patterns) contain your packages. NPM then knows to treat these as part of a unified project.

Here’s what a basic setup might look like:

```json
{
  "name": "my-monorepo",
  "version": "1.0.0",
  "private": true,
  "workspaces": [
    "packages/*"
  ]
}
```

In this example, any package located under the `packages/` directory is included in the workspace. NPM will automatically link these packages together, allowing you to share dependencies and run scripts across them.

## Setting Up Your First Workspace

Let’s walk through setting up NPM Workspaces from scratch. Don’t worry, it’s easier than you might think!

### Step 1: Create Your Project Structure

Start by creating a new directory for your project:

```bash
mkdir my-monorepo
cd my-monorepo
```

Inside this directory, create a `package.json` file. This file will act as the root configuration for your workspace:

```bash
npm init -y
```

Next, create a `packages/` directory to hold your individual packages:

```bash
mkdir packages
```

### Step 2: Configure Your Workspaces

Open your `package.json` file and add the `workspaces` field:

```json
{
  "name": "my-monorepo",
  "version": "1.0.0",
  "private": true,
  "workspaces": [
    "packages/*"
  ]
}
```

The `"private": true` flag is important because it prevents you from accidentally publishing your workspace root as a package. The `workspaces` field tells NPM to treat everything under `packages/` as part of the same project.

### Step 3: Add Packages to Your Workspace

Now, let’s add some packages to your workspace. Inside the `packages/` directory, create two new directories for your packages:

```bash
mkdir packages/core
mkdir packages/cli
```

Navigate into each package directory and create a `package.json` for each:

```bash
cd packages/core
npm init -y

cd packages/cli
npm init -y
```

You now have a basic workspace setup with two packages: `core` and `cli`.

## Managing Dependencies Across Workspaces

One of the biggest advantages of using NPM Workspaces is how it simplifies dependency management. Dependencies declared in any workspace package are automatically installed and shared across the entire workspace, avoiding duplication and version conflicts.

## Installing Dependencies

Let’s say the `core` package needs `lodash` as a dependency. You can install it from the root of your workspace:

```bash
npm install lodash --workspace=packages/core
```

NPM will install `lodash` and make it available to the `core` package, while also linking it to the workspace. This means you won’t have multiple versions of `lodash` floating around in different parts of your project.

## Linking Internal Packages

If your `cli` package depends on `core`, you can link these packages together without publishing `core` to a registry. Just declare `core` as a dependency in the `cli` package’s `package.json`:

```json
{
  "name": "cli",
  "version": "1.0.0",
  "dependencies": {
    "core": "1.0.0"
  }
}
```

When you run `npm install`, NPM will automatically link the `core` package to `cli`, allowing `cli` to use it as if it were an external dependency.

## Running Scripts Across Workspaces

NPM Workspaces make it easy to run scripts across multiple packages simultaneously. This can be a huge time-saver for tasks like testing, building, or linting all your packages at once.

## Running a Script in a Specific Package

To run a script in a specific package, use the `--workspace` flag:

```bash
npm run build --workspace=packages/core
```

## Running Scripts Across All Packages

If you want to run a script across all packages in your workspace, you can use the `npm run` command at the root level:

```bash
npm run test --workspaces
```

This will execute the `test` script in each package that has it defined in its `package.json`.

## Best Practices for NPM Workspaces

To ensure your NPM Workspaces setup runs smoothly, here are a few best practices to keep in mind:

1. **Keep Your Workspace Organized**: Use a consistent directory structure for your packages, and clearly name your directories and packages. This will help keep everything easy to manage and navigate.
2. **Use a Single Version Policy**: Whenever possible, try to keep all your packages on compatible versions of their dependencies. This avoids version conflicts and makes it easier to upgrade dependencies across your workspace.
3. **Leverage the Power of `.npmrc`**: Customize your workspace environment by creating an `.npmrc` file at the root of your workspace. This file can be used to set global NPM configurations, such as registry URLs or custom scripts.
4. **Automate Common Tasks**: Use the `workspaces` feature to automate common tasks across your packages, like testing or building. This can save you a lot of time and ensure consistency across your project.
5. **Document Your Workspace Setup**: Make sure to document your workspace structure, dependency management strategy, and any special configurations. This will help new contributors (and your future self) understand how everything is set up.