# Logging errors in Winston

One of the most surprising behaviors of Winston for newcomers to the library is in its way of handling errors. Logging an instance of the `Error` object results in an empty message:

```jsx
import { createLogger, format, transports } from "winston";
const { combine, timestamp, colorize, printf, align, json } = format;

export default createLogger({
  level: "info",
  format: combine(timestamp(), json()),
  transports: [new transports.Console()],
});
```

```jsx
logger.error(new Error("an error"));
```

**Output:**

```jsx
{"level":"error","timestamp":"2022-07-03T19:58:26.516Z"}
```

Notice how the `message` property is omitted, and other properties of the `Error` (like its `name` and `stack`) are also not included in the output. This can result in a nightmare situation where errors in production are not recorded leading to lost time when troubleshooting.

Fortunately, you can fix this issue by importing and specifying the `errors` format as shown below:

```jsx
import { createLogger, format, transports } from "winston";
const { combine, timestamp, colorize, printf, align, json, errors } = format;

export default createLogger({
  level: "info",
  format: combine(errors({ stack: true }), timestamp(), json()),
  transports: [new transports.Console()],
});
```

You will now get the proper output:

```jsx
{"level":"error","message":"an error","stack":"Error: an error\n    at Object.<anonymous> (/home/ayo/dev/betterstack/betterstack-community/demo/snippets/main.js:9:14)\n    at Module._compile (node:internal/modules/cjs/loader:1105:14)\n    at Module._extensions..js (node:internal/modules/cjs/loader:1159:10)\n    at Module.load (node:internal/modules/cjs/loader:981:32)\n    at Module._load (node:internal/modules/cjs/loader:827:12)\n    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:77:12)\n    at node:internal/main/run_main_module:17:47","timestamp":"2022-07-03T20:11:23.303Z"}
```