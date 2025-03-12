# Adding metadata to your logs

Winston supports the addition of metadata to log messages. You can add default metadata to all log entries, or specific metadata to individual logs. Let's start with the former which can be added to a `logger` instance through the `defaultMeta` property:

```jsx
export default createLogger({
  level: process.env.LOG_LEVEL || "info",
  defaultMeta: {
    service: "admin-service",
  },
  format: combine(timestamp(), json()),
  transports: [
    new transports.Console({
      format: combine(
        colorize(),
        align(),
        printf((info) => `${info.timestamp} ${info.level}: ${info.message}: ${info.service}`)
      ),
    }),
  ],
});
```

When you log any message using the `logger` above, the contents of the `defaultMeta` object will be injected into each entry:

**Output:**

```jsx
{"level":"info","message":"Info message","service":"admin-service"}
{"level":"error","message":"Error message","service":"admin-service"}
```

This default metadata can be used to differentiate log entries by service or other criteria when logging to the same location from different services.

Another way to add metadata to your logs is by creating a child logger through the `child` method. This is useful if you want to add certain metadata that should be added to all log entries in a certain scope. For example, if you add a `requestId` to your logs entries, you can search your logs and find the all the entries that pertain to a specific request.

```jsx
const childLogger = logger.child({ requestId: 'f9ed4675f1c53513c61a3b3b4e25b4c0' });

childLogger.info('Info message');
childLogger.info('Error message');
```

**Output:**

```jsx
{"level":"info","message":"Info message","requestId":"f9ed4675f1c53513c61a3b3b4e25b4c0","service":"admin-service"}
{"level":"error","message":"Error message","requestId":"f9ed4675f1c53513c61a3b3b4e25b4c0","service":"admin-service"}
```

A third way to add metadata to your logs is to pass an object to the level method at its call site:

```jsx
const childLogger = logger.child({ requestId: 'f9ed4675f1c53513c61a3b3b4e25b4c0' });

childLogger.info('File uploaded successfully', {
  file: 'something.png',
  type: 'image/png',
  userId: 'jdn33d8h2',
});
```

**Output:**

```jsx
{"file":"something.png","level":"info","message":"File uploaded successfully","requestId":"f9ed4675f1c53513c61a3b3b4e25b4c0","service":"admin-service","type":"image/png","userId":"jdn33d8h2"}
```