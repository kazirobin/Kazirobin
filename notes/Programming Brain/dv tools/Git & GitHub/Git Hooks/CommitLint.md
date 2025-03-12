# CommitLint

Commitlint is triggered by Husky, a tool that manages Git hooks and runs the validation script automatically before committing.

First, we install the Commitlint CLI and the Conventional Commits configuration as development dependencies:

```bash
npm install @commitlint/cli @commitlint/config-conventional --save-dev
```

Then, we need to extend the Commitlint conventional  and cli configuration:

Create a file in the root directory name `commitlint.config.js`

```jsx
module.exports = {
  extends: ["@commitlint/cli", "@commitlint/config-conventional"],
  rules: {
    "type-enum": [
      2,
      "always",
      [
        "feat",
        "fix",
        "ui",
        "docs",
        "style",
        "refactor",
        "pref",
        "test",
        "build",
        "ci",
        "chore",
        "revert"
      ]
    ],
    "subject-case": [0, "never"]
  }
};
```

Now you need to install `husky`, already do that following this:

After installing the dependency, you will have to create a `commit-msg` file in the `.husky` folder to add commit message linting to commit-msg hook.

It can be done in a single line of code:

```jsx
npx --no-install commitlint --edit
```