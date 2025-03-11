# TypeScript Type Check

Log real-time type error on the terminal that comes from the code editor.

- Create a `tsconfig.watch.json` with the following content

```json
{
 "extends": "./tsconfig.json",
 "exclude": ["node_modules", ".next/types/**/*.ts"]
}
```

- Use the following content to `package.json`

```json
"scripts": {
    "ts:watch": "npm run ts -- --watch --project tsconfig.watch.json",
    "ts": "tsc --noEmit --incremental --preserveWatchOutput --pretty",
  },
```

This way I don't see any errors from files within `.next/types` in my TSC watch but would still see them in the IDE or on `build`, which both still use the original `tsconfig.json` which includes that folder.