# NPM Cheat Sheet

This handy cheat sheet gives you all the essentials you need to know about npm. Including how to install, how it works, npm commands, commonly used npm packages, working with JFrog CLI and more.

---

➤ Initialize a new `package.json` file interactively.

```bash
npm init
```

➤ Initializes a new `package.json` file with default values.

```bash
npm init -y
```

➤ NPM list packages installed globally.

```bash
npm list -g
```

➤ NPM install a package and add it to package.json.

```bash
npm install <package-name>
npm i <package-name>
```

➤ NPM install a package and add it to package.json as a development dependency.

```bash
npm install <package-name> --save-dev
npm install -D <package-name>
```

➤ NPM install a package globally without adding it to package.json

```bash
npm install <package-name> -g
npm install -g <package-name>
```

➤ NPM install a package globally and add it to package.json.

```bash
npm install <package-name> -g --save
```

➤ NPM uninstall a package and remove it from package.json.

```bash
npm uninstall <package-name>
npm un <package-name>
```

➤ NPM uninstall a package and remove it from package.json as a development dependency.

```bash
npm uninstall <package-name> --save-dev
npm uninstall -D <package-name>
```

➤ NPM update a package and update it in package.json.

```bash
npm update <package-name>
npm up <package-name>
```

➤ NPM update a package and update it in package.json as a development dependency.

```bash
npm update <package-name> --save-dev
npm update -D <package-name>
```

➤ NPM update all packages and update them in package.json.

```bash
npm update
```

➤ NPM update all packages and update them in package.json as a development dependency.

```markdown
npm update --save-dev
npm update -D
```

➤ NPM global update all packages.

```bash
npm update -g
```

➤ NPM installs a specific version of a package.

```bash
npm install <package-name>@<version>
```

➤ NPM updates a package and checks if it is up to date.

```bash
npm outdated
```

➤ NPM outdates a package and checks if it is up to date globally.

```bash
npm outdated -g
```

➤ NPM doctor checks for known issues.

```bash
npm doctor
```

➤ NPM installs touch CLI globally.

```bash
npm install touch-cli -g
```

➤ NPM install globally to check for updates of all packages.

```bash
npm install npm-check-updates -g
```

After installing `npm-check-updates` globally to check for updates of all packages and update `package.json`

```bash
npx npm-check-updates -u #First command
npm install #Second command
```