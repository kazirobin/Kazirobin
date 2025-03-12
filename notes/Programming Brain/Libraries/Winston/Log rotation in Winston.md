# Log rotation in Winston

Logging into files can quickly get out of hand if you keep logging to the same file as it can get extremely large and become cumbersome to manage. This is where the concept of log rotation  can come in handy. The main purpose of log rotation is to restrict the size of your log files and create new ones based on some predefined criteria. For example, you can create a new log file every day and automatically delete those older than a time period (say 30 days).

Winston provides the [winston-daily-rotate-file module](https://github.com/winstonjs/winston-daily-rotate-file)  for this purpose. It is a transport that logs to a rotating file that is configurable based on date or file size, while older logs can be auto deleted based on count or elapsed days. Go ahead and install it through `npm` as shown below:

```bash
npm install winston-daily-rotate-file
```

Once installed, it may be used to replace the default `File` transport as shown below:

```jsx
import "winston-daily-rotate-file"

const fileRotateTransport = new transports.DailyRotateFile({
  filename: 'combined-%DATE%.log',
  datePattern: 'YYYY-MM-DD',
  maxFiles: '14d',
});

export default createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: combine(timestamp(), json()),
  transports: [fileRotateTransport],
});
```

The `datePattern` property controls how often the file should be rotated (every day), and the `maxFiles` property ensures that log files that are older than 14 days are automatically deleted. You can also listen for the following events on a rotating file transport if you want to perform some action on cue:

```jsx
// fired when a log file is created
fileRotateTransport.on('new', (filename) => {});
// fired when a log file is rotated
fileRotateTransport.on('rotate', (oldFilename, newFilename) => {});
// fired when a log file is archived
fileRotateTransport.on('archive', (zipFilename) => {});
// fired when a log file is deleted
fileRotateTransport.on('logRemoved', (removedFilename) => {});
```