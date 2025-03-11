# Handling uncaught exceptions and uncaught promise rejections

Winston provides the ability to automatically catch and log uncaught exceptions and uncaught promise rejections on a logger. You'll need to specify the transport where these events should be emitted to through the `exceptionHandlers` and `rejectionHandlers` properties respectively:

```jsx
export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  format: format.json(),
  transports: [new transports.Console()],
  exceptionHandlers: [new transports.File({ filename: "exception.log" })],
  rejectionHandlers: [new transports.File({ filename: "rejections.log" })],
});
```

The `logger` above is configured to log uncaught exceptions to an `exception.log` file, while uncaught promise rejections are placed in a `rejections.log` file. You can try this out by throwing an error somewhere in your code without catching it.

```jsx
throw new Error('An uncaught error');
```

You'll notice that the entire stack trace is included in the log entry for the exception, along with the date and message.

**Output:**

```jsx
{"date":"Sun Oct 06 2024 13:44:57 GMT+0600 (Bangladesh Standard Time)","error":{},"exception":true,"level":"error","message":"uncaughtException: An uncaught error\nError: An uncaught error\n    at Object.<anonymous> (E:\\Coding Practice\\Learn Express\\index.ts:21:7)\n    at Module._compile (node:internal/modules/cjs/loader:1469:14)\n    at Module.m._compile (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\index.ts:1618:23)\n    at Module._extensions..js (node:internal/modules/cjs/loader:1548:10)\n    at Object.require.extensions.<computed> [as .ts] (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\index.ts:1621:12)\n    at Module.load (node:internal/modules/cjs/loader:1288:32)\n    at Function.Module._load (node:internal/modules/cjs/loader:1104:12)\n    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:174:12)\n    at phase4 (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\bin.ts:649:14)\n    at bootstrap (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\bin.ts:95:10)","os":{"loadavg":[0,0,0],"uptime":13814.984},"process":{"argv":["E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\dist\\bin.js","E:\\Coding Practice\\Learn Express\\index.ts"],"cwd":"E:\\Coding Practice\\Learn Express","execPath":"C:\\Program Files\\nodejs\\node.exe","gid":null,"memoryUsage":{"arrayBuffers":4645855,"external":7528969,"heapTotal":151392256,"heapUsed":122243240,"rss":188936192},"pid":25208,"uid":null,"version":"v20.17.0"},"stack":"Error: An uncaught error\n    at Object.<anonymous> (E:\\Coding Practice\\Learn Express\\index.ts:21:7)\n    at Module._compile (node:internal/modules/cjs/loader:1469:14)\n    at Module.m._compile (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\index.ts:1618:23)\n    at Module._extensions..js (node:internal/modules/cjs/loader:1548:10)\n    at Object.require.extensions.<computed> [as .ts] (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\index.ts:1621:12)\n    at Module.load (node:internal/modules/cjs/loader:1288:32)\n    at Function.Module._load (node:internal/modules/cjs/loader:1104:12)\n    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:174:12)\n    at phase4 (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\bin.ts:649:14)\n    at bootstrap (E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\bin.ts:95:10)","timestamp":"2024-10-06T07:44:57.207Z","trace":[{"column":7,"file":"E:\\Coding Practice\\Learn Express\\index.ts","function":null,"line":21,"method":null,"native":false},{"column":14,"file":"node:internal/modules/cjs/loader","function":"Module._compile","line":1469,"method":"_compile","native":false},{"column":23,"file":"E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\index.ts","function":"Module.m._compile","line":1618,"method":"_compile","native":false},{"column":10,"file":"node:internal/modules/cjs/loader","function":"Module._extensions..js","line":1548,"method":".js","native":false},{"column":12,"file":"E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\index.ts","function":"Object.require.extensions.<computed> [as .ts]","line":1621,"method":"ts]","native":false},{"column":32,"file":"node:internal/modules/cjs/loader","function":"Module.load","line":1288,"method":"load","native":false},{"column":12,"file":"node:internal/modules/cjs/loader","function":"Module._load","line":1104,"method":"_load","native":false},{"column":12,"file":"node:internal/modules/run_main","function":"Function.executeUserEntryPoint [as runMain]","line":174,"method":"executeUserEntryPoint [as runMain]","native":false},{"column":14,"file":"E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\bin.ts","function":"phase4","line":649,"method":null,"native":false},{"column":10,"file":"E:\\Coding Practice\\Learn Express\\node_modules\\ts-node\\src\\bin.ts","function":"bootstrap","line":95,"method":null,"native":false}]}

```