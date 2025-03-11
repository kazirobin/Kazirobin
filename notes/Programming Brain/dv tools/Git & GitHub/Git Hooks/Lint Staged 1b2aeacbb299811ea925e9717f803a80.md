# Lint Staged

Lint-staged has been created with the purpose of linting only staged files. Lint-staged has very well-defined defaults that give us a headstart.

One of the benefits is that Lint-staged will run the commands that you define for the chosen staged files and also immediately add the changes to the staged section if possible.

Think of Prettier converting double quotes to single quotes for example. Lint-staged is also pre-configured to run the linting scripts on the staged files in parallel. This can be a huge time saver when there are many staged files.

Run the following command to install lint-staged:

```bash
npm install --save-dev lint-staged
```

Now you need to install `husky`, already do that following this:

Inside `.husky/pre-commit` replace `npm test` with `npx lint-staged`. Your file should look as follows:

```bash
npx lint-staged
```

Add a new `"lint-staged"` to your “package.json” file

```json
"lint-staged": {
    "*.ts": [
      "npm run lint:fix", // Already define in the script
      "npm run format:fix" // Already define in the script
    ]
  }
```