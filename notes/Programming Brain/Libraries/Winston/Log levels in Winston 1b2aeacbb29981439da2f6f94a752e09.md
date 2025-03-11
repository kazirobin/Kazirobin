# Log levels in Winston

Winston supports six log levels by default. It follows the order specified by the RFC5424  document. Each level is given an integer priority with the most severe being the lowest number and the least one being the highest.

```jsx
{
  error: 0,
  warn: 1,
  info: 2,
  http: 3,
  verbose: 4,
  debug: 5,
  silly: 6
}
```

The six log levels above each correspond to a method on the logger:

```jsx
logger.error('error');
logger.warn('warn');
logger.info('info');
logger.verbose('verbose');
logger.debug('debug');
logger.silly('silly');
```

You can also pass a string representing the logging level to the `log()` method:

```jsx
logger.log('error', 'error message');
logger.log('info', 'info message');
```

The `level` property on the `logger` determines which log messages will be emitted to the configured transports. For example, since the `level` property was set to `info` in the previous section, only log entries with a minimum severity of `info` (or maximum integer priority of 2) will be written while all others are suppressed. This means that only the `info`, `warn`, and `error` messages will produce output with the current configuration.

To cause the other levels to produce output, you'll need to change the value of `level` property to the desired minimum. The reason for this configuration is so that you'll be able to run your application in production at one level (say `info`) and your development/testing/staging environments can be set to a less severe level like `debug` or `silly`, causing more information to be emitted.

The accepted best practice for setting a log level is to use an environmental variable. This is done to avoid modifying the application code when the log level needs to be changed.

```jsx
export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  format: format.json(),
  transports: [new transports.Console()],
});
```

With this change in place, the application will log at the `info` level if the `LOG_LEVEL` variable is not set in the environment.