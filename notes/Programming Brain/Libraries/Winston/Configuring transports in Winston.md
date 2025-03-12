# Configuring transports in Winston

Transports in Winston refer to the storage location for your log entries. Winston provides great flexibility in choosing where you want your log entries to be outputted to. The following transport options are available in Winston by default:

- [Console](https://github.com/winstonjs/winston/blob/master/docs/transports.md#console-transport) : output logs to the Node.js console.
- [File](https://github.com/winstonjs/winston/blob/master/docs/transports.md#file-transport) : store log messages to one or more files.
- [HTTP](https://github.com/winstonjs/winston/blob/master/docs/transports.md#http-transport) : stream logs to an HTTP endpoint.
- [Stream](https://github.com/winstonjs/winston/blob/master/docs/transports.md#stream-transport) : output logs to any Node.js stream.

Thus far, we've demonstrated the default Console transport  to output log messages to the Node.js console. Let's look at how we can store logs in a file next.

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
  transports: [
    new transports.Console(),
    new transports.File({
      filename: "logs/combined.log",
    }),
  ],
});
```

The snippet above configures the `logger` to output all emitted log messages to a file named `combined.log`. When you run the snippet above, this file will be created with the following contents:

```jsx
{"level":"info","message":"Info message","timestamp":"2022-01-26T09:38:17.747Z"}
{"level":"error","message":"Error message","timestamp":"2022-01-26T09:38:17.748Z"}
{"level":"warn","message":"Warning message","timestamp":"2022-01-26T09:38:17.749Z"}
```

In a production application, it may not be ideal to log every single message into a single file as that will make filtering critical issues harder since it will be mixed together with inconsequential messages. A potential solution would be to use two `File` transports, one that logs all messages to a `combined.log` file, and another that logs messages with a minimum severity of `error` to a separate file.

```jsx
export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  format: combine(timestamp(), json()),
  transports: [
    new transports.Console(),
    new transports.File({
      filename: "combined.log",
    }),
    new transports.File({
      filename: 'app-error.log',
      level: 'error',
    })
  ],
});
```

With this change in place, all your log entries will still be outputted to the `combined.log` file, but a separate `app-error.log` will also be created and it will contain only `error` messages. Note that the `level` property on the `File()` transport signifies the minimum severity that should be logged to the file. If you change it from `error` to `warn`, it means that any message with a minimum severity of `warn` will be logged to the `app-error.log` file (`warn` and `error` levels in this case).

A common need that Winston does not enable by default is the ability to log each level into different files so that only `info` messages go to an `app-info.log` file, `debug` messages into an `app-debug.log` file, and so on (see [this GitHub issue](https://github.com/winstonjs/winston/issues/614) ). To get around this, use a custom format on the transport to filter the messages by level. This is possible on any transport (not just `File`), since they all inherit from [winston-transport](https://github.com/winstonjs/winston-transport) .

```jsx
const errorFilter = format((info, opts) => {
  return info.level === "error" ? info : false;
});

const infoFilter = format((info, opts) => {
  return info.level === "info" ? info : false;
});

export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  format: combine(timestamp(), json()),
  transports: [
    new transports.File({
      filename: "combined.log",
    }),
    new transports.File({
      filename: "app-error.log",
      level: "error",
      format: combine(errorFilter(), timestamp(), json()),
    }),
    new transports.File({
      filename: "app-info.log",
      level: "info",
      format: combine(infoFilter(), timestamp(), json()),
    }),
  ],
});
```

The above code logs only `error` messages in the `app-error.log` file and `info` messages to the `app-info.log` file. What happens is that the custom functions (`infoFilter()` and `errorFilter()`) checks the level of a log entry and returns `false` if it doesn't match the specified level which causes the entry to be omitted from the transport. You can customize this further or create other filters as you see fit.