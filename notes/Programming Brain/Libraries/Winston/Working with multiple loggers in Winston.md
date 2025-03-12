# Working with multiple loggers in Winston

A large application will often have multiple loggers with different settings for logging in different areas of the application. This is exposed in Winston through `winston.loggers`:

Create a filed named `./src/utils/loggers.js`

```jsx
import winston, { format, transports } from "winston";

winston.loggers.add('serviceALogger', {
  level: process.env.LOG_LEVEL || 'info',
  defaultMeta: {
    service: 'service-a',
  },
  format: format.logstash(),
  transports: [
    new transports.File({
      filename: 'service-a.log',
    }),
  ],
});

winston.loggers.add('serviceBLogger', {
  level: process.env.LOG_LEVEL || 'info',
  defaultMeta: {
    service: 'service-b',
  },
  format: format.json(),
  transports: [new transports.Console()],
});
```

The `serviceALogger` shown above logs to a `service-a.log` file using the built-in Logstash format, while `serviceBLogger` logs to the console using the JSON format. Once you've configured the loggers for each service, you can access them in any file using the `winston.loggers.get()` provided that you import the configuration preferably in the entry file of the application:

```jsx
import winston from "winston";
import "./utils/logger";

const serviceALogger = winston.loggers.get('serviceALogger');
const serviceBLogger = winston.loggers.get('serviceBLogger');

serviceALogger.error('logging to a file');
serviceBLogger.warn('logging to the console');
```

**Output:**

```jsx
{"level":"warn","message":"logging to the console","service":"service-b"}
```

```jsx
cat service-a.log
```

**Output:**

```jsx
{"@fields":{"level":"error","service":"service-a"},"@message":"logging to a file"}
```