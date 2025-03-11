# Formatting your log messages

Winston outputs its logs in JSON format by default, but it also supports other formats which are accessible on the `winston.format` object. For example, if you're creating a CLI application, you may want to switch this to the `cli` format which will print a color coded output:

```jsx
export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  format: format.json(),
  transports: [new transports.Console()],
});
```

The formats available in `winston.format` are defined in the logform module . This module provides the ability to customize the format used by Winston to your heart's content. You can create a completely custom format or modify an existing one to add new properties.

Here's an example that adds a `timestamp` field to the each log entry:

```jsx
import { createLogger, format, transports } from "winston";
const { combine, timestamp, json } = format;

export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  format: combine(timestamp(), json()),
  transports: [new transports.Console()],
});
```

When you use a level method on the `logger`, you'll see a datetime value formatted as `new Date().toISOString()`.

```jsx
logger.info('Info message')
```

**Output:**

```jsx
{"level":"info","message":"Info message","timestamp":"2022-01-25T15:50:09.641Z"}
```

You can change the format of this datetime value by passing an object to `timestamp()` as shown below. The string value of the `format` property below must be one acceptable by the [fecha module](https://github.com/taylorhakes/fecha) .

```jsx
timestamp({
  format: 'YYYY-MM-DD hh:mm:ss.SSS A', // 2022-01-25 03:23:10.350 PM
})
```

You can also create a entirely different format as shown below:

```jsx
import { createLogger, format, transports } from "winston";
const { combine, timestamp, colorize, printf, align } = format;

export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  format: combine(
    colorize({ all: true }),
    timestamp({ format: "YYYY-MM-DD hh:mm:ss.SSS A" }),
    align(),
    printf((info) => `[${info.timestamp}] ${info.level}: ${info.message}`)
  ),
  transports: [new transports.Console()],
});
```

The `combine()` method merges multiple formats into one, while `colorize()` assigns colors to the different log levels so that each level is easily identifiable. The `timestamp()` method outputs a datatime value that corresponds to the time that the message was emitted. The `align()` method aligns the log messages, while `printf()` defines a custom structure for the message. In this case, it outputs the timestamp and log level followed by the message.

**Output:**

```jsx
[2022-01-27 06:37:27.653 AM] info:      Info message
[2022-01-27 06:37:27.656 AM] error:     Error message
[2022-01-27 06:37:27.656 AM] warn:      Warning message
```

While you can format your log entries in any way you wish, the recommended practice for server applications is to stick with a structured logging format (like JSON) so that your logs can be easily machine readable for filtering and gathering insights.