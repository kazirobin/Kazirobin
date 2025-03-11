# Getting started with Winston

Winston is available as an [npm package](https://www.npmjs.com/package/winston) , so you can install it through the command below.

```bash
npm install winston
```

Next, import it into your Node.js application:

```jsx
import { createLogger, format, transports } from "winston";
```

Although Winston provides a default logger that you can use by calling a level method on the `winston` module, it the recommended way to use it is to create a custom logger through the `createLogger()` method:

Create a file named `./src/utils/logger.js`

```jsx
import { createLogger, format, transports } from "winston";

export default createLogger({
  level: 'info',
  format: format.json(),
  transports: [new transports.Console()],
});
```

Afterwards, you can start logging through methods on the `logger` object:

```jsx
logger.info('Info message');
logger.error('Error message');
logger.warn('Warning message');
```

This yields the following output:

```jsx
{"level":"info","message":"Info message"}
{"level":"error","message":"Error message"}
{"level":"warn","message":"Warning message"}
```

In subsequent sections, we'll examine all the properties that you can use to customize your `logger` so that you will end up with an optimal configuration for your Node.js application.