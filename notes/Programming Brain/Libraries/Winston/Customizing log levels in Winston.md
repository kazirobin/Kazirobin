# Customizing log levels in Winston

Winston allows you to readily customize the log levels to your liking. The default log levels are defined in `winston.config.npm.levels`, but you can also use the Syslog levels  through `winston.config.syslog.levels`:

```jsx
export default createLogger({
  levels: winston.config.syslog.levels,
  level: process.env.LOG_LEVEL || "info",
  format: format.json(),
  transports: [new transports.Console()],
});
```

The `syslog` levels are shown below:

```jsx
{
  emerg: 0,
  alert: 1,
  crit: 2,
  error: 3,
  warning: 4,
  notice: 5,
  info: 6,
  debug: 7
}
```

Afterwards, you can log using the methods that correspond to each defined level:

```jsx
winston.emerg("Emergency");
winston.crit("Critical");
winston.warning("Warning");
```

If you prefer to change the levels to a completely custom system, you'll need to create an object and assign a number priority to each one starting from the most severe to the least. Afterwards, assign that object to the `levels` property in the configuration object passed to the `createLogger()` method.

```jsx
const logLevels = {
  fatal: 0,
  error: 1,
  warn: 2,
  info: 3,
  debug: 4,
  trace: 5,
};

export default createLogger({
  levels: logLevels,
  level: process.env.LOG_LEVEL || 'info',
  format: format.cli(),
  transports: [new transports.Console()],
});
```

You can now use methods on the `logger` that correspond to your custom log levels as shown below:

```jsx
logger.fatal('fatal!');
logger.trace('trace!');
```