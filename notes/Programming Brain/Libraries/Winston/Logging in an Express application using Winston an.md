# Logging in an Express application using Winston and Morgan

Morgan  is an HTTP request logger middleware for Express  that automatically logs the details of incoming requests to the server (such as the remote IP Address, request method, HTTP version, response status, user agent, etc.), and generate the logs in the specified format. The main advantage of using Morgan is that it saves you the trouble of writing a custom middleware for this purpose.

Here's a simple program demonstrating Winston and Morgan being used together in an Express application. When you connect Morgan with a Winston logger, all your logging is formatted the same way and goes to the same place.

```jsx
const winston = require('winston');
const express = require('express');
const morgan = require('morgan');
const axios = require('axios');

const app = express();

const { combine, timestamp, json } = winston.format;

const logger = winston.createLogger({
  level: 'http',
  format: combine(
    timestamp({
      format: 'YYYY-MM-DD hh:mm:ss.SSS A',
    }),
    json()
  ),
  transports: [new winston.transports.Console()],
});

const morganFormat =
  ":method :url :status :res[content-length] - :response-time ms";

const morganMiddleware = morgan(morganFormat, {
  stream: {
    write: (message) => {
      const logObject = {
        method: message.split(" ")[0],
        url: message.split(" ")[1],
        status: message.split(" ")[2],
        contentLength: message.split(" ")[3],
        responseTime: message.split(" ")[5],
      };

      logger.http(logObject);
    },
  },
});

app.use(morganMiddleware);

app.get('/crypto', async (req, res) => {
  try {
    const response = await axios.get(
      'https://api2.binance.com/api/v3/ticker/24hr'
    );

    const tickerPrice = response.data;

    res.json(tickerPrice);
  } catch (err) {
    logger.error(err);
    res.status(500).send('Internal server error');
  }
});

app.listen('5000', () => {
  console.log('Server is running on port 5000');
});
```

The `morgan()` middleware function takes two arguments: a string describing the format of the log message and the configuration options for the logger. The format is composed up of [individual tokens](https://github.com/expressjs/morgan#tokens) , which can be combined in any order. You can also use a [predefined format](https://github.com/expressjs/morgan#predefined-formats)  instead. In the second argument, the `stream` property is set to log the provided message using our custom logger at the `http` severity level. This reflects the severity that all Morgan events will be logged at.

Before you execute this code, install all the required dependencies first:

```jsx
npm install winston express morgan axios
```

Afterward, start the server and send requests to the `/crypto` route through the commands below:

You should observe the following output:

```jsx
{"level":"http","message":{"contentLength":"12","method":"GET","responseTime":"2.272","status":"200","url":"/crypto"},"timestamp":"2024-10-06 03:08:43.344 PM"}
```

Notice that the all the request metadata outputted by Morgan is placed as a string in the `message` property which makes it harder to search and filter. Let's configure Morgan such that the message string will be a stringified JSON object.

```jsx
. . .
const morganMiddleware = morgan(
  function (tokens, req, res) {
    return JSON.stringify({
      method: tokens.method(req, res),
      url: tokens.url(req, res),
      status: Number.parseFloat(tokens.status(req, res)),
      content_length: tokens.res(req, res, 'content-length'),
      response_time: Number.parseFloat(tokens['response-time'](req, res)),
    });
  },
  {
    stream: {
      // Configure Morgan to use our custom logger with the http severity
      write: (message) => {
        const data = JSON.parse(message);
        logger.http(`incoming-request`, data);
      },
    },
  }
);
. . .

```

The string argument to the `morgan()` function has been changed to a function that returns a stringified JSON object. In the `write()` function, the JSON string is parsed and the resulting object is passed as metadata to the `logger.http()` method. This ensures that each metric is produced as a separate property in the log entry.

Restart the server and send requests to the `/crypto` route once again. You'll observe the following output:

```jsx
{"content_length":"12","level":"http","message":"incoming-request","method":"GET","response_time":1.993,"status":200,"timestamp":"2024-10-06 03:11:04.672 PM","url":"/crypto"}
```