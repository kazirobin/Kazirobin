# Yarn Cheat Sheet

Okay, so you’ve heard about this new JavaScript package manager called `yarn`, installed it with `npm i -g yarn`, and now you want to know how to use it? For the most part if you know NPM, you’re already set! Here are the key notes for switching.

---

➤ Initialize a new `package.json` file interactively.

```bash
yarn init
```

➤ Initializes a new `package.json` file with default values.

```bash
yarn init -y
```

➤ Installs all dependencies listed in the `package.json` file and generates a `yarn.lock` file.

```bash
yarn install
```

➤ Installs a package and adds it to `dependencies`.

```bash
yarn add <package-name>
```

➤ Installs a specific version of a package.

```bash
yarn add <package-name>@<version>
```

➤ Installs a package and adds it to `devDependencies`.

```bash
yarn add <package-name> --dev
```

➤ Upgrades a package to the latest version.

```bash
yarn upgrade <package-name>
```

➤ Upgrades a package to a specific version.

```bash
yarn upgrade <package-name>@<version>
```

➤ Upgrades all package to the latest version.

```bash
yarn upgrade --latest
```

➤ Removes a package from `dependencies`.

```bash
yarn remove <package-name>
```

➤ Lists outdated dependencies in the project.

```bash
yarn outdated
```

➤ Deduplicates dependencies in the `yarn.lock` file.

```bash
yarn dedupe
```

➤ Clears the global Yarn cache.

```bash
**yarn cache clean**
```

➤ Runs a script defined in the `package.json` file.

```bash
yarn run <script-name>
```

➤ Lists all available scripts and allows you to select one interactively.

```bash
yarn run
```

➤ Runs a script in all workspaces.

```bash
yarn workspaces foreach run <script>
```

➤ Adds a package to a specific workspace.

```bash
yarn workspace <workspace-name> add <package-name>
```

➤ Displays all workspaces in the project.

```bash
yarn workspaces list
```

➤ Installs a package globally.

```bash
yarn global add <package-name>
```

➤ Removes a globally installed package.

```bash
yarn global remove <package-name>
```

➤ Displays globally installed packages.

```bash
yarn global list
```

➤ Verifies that all dependencies match their expected versions.

```bash
yarn check
```

➤ Scans dependencies for known vulnerabilities.

```bash
yarn audit
```

➤ Creates a tarball from the project, which is useful for publishing.

```bash
yarn pack
```

➤ Publishes a package to the npm registry.

```bash
yarn publish
```

➤ Sets a global Yarn configuration.

```bash
yarn config set <key> <value>
```

➤ Lists all Yarn configurations.

```bash
yarn config list
```

➤ Deletes a configuration.

```bash
yarn config delete <key>
```