# HTTP Module

Node.js HTTP module is a built-in library that allows developers to create web servers, as well as communicate with other APIs using HTTP 1.1, HTTP 2, and HTTPS**.**

## Architecture

The HTTP module extends two built-in classes:

- **Net module**
    
    Provides network API for creating stream-based TCP servers or clients.
    
- **Events module**
    
    Provides an event-driven architecture using `EventEmitter` class.
    

This means that when working with an HTTP module, you can listen and act upon the events, while the data is processed using streams.

## Simple Server

To get started, create a JavaScript file on your machine (e.g. app.js) and import the HTTP module.

```jsx
const http = require('http');
```

Then create a server instance using `http.createServer()` function.

```jsx
const server = http.createServer((req, res) => { ... });
```

The function takes two arguments:

- request object (req)
- response object (res)

Both arguments are stream objects.

After creating a server, set a response in the handler (callback function).

```jsx
const server = http.createServer((req, res) => {
  res.end('Hello!');
});
```

The last thing to do is to set up a port on which this server will run. You can do that by calling `server.listen()` and passing any valid port number:

```jsx
const server = http.createServer((req, res) => {
  res.end('Hello!');
});

server.listen(3000, () => {
  console.log('Server started on localhost:3000!');
})
```

If you run this file (using `node app.js`), you should see a message
The server started on `localhost:3000`! printed in the console. Open a web browser, head over to `localhost:3000` and you should see the response from the server displayed in the browser:

## Request

The Request object is an instance of `http.IncomingMessage` that extends **readable stream** and contains information on the incoming client data, such as:

- request URL
- request method (GET/POST/PUT/DELETE)
- request body
- request headers, etc.

### Extract data from the URL

To pick up other information like the request path, or query you’ll have to do some extra work.

You can see request URL information doing the following:

```jsx
const server = http.createServer((req, res) => {
  console.log('Request Headers :>> ', req.headers);
  console.log('Request Method :>> ', req.method);
  console.log('Request URL :>> ', req.url);
  res.end('Thank you Mario, but our princess is in another castle...');
});
```

Now if you go to the route using **curl** or in a browser [`http://localhost:3000/api/users?userid=100`](http://localhost:3000/api/users?userid=100), it should print this response in the console:

```jsx
Request Headers :>>  {
  host: 'localhost:3000',
  connection: 'keep-alive',
  'cache-control': 'max-age=0',
  ...
}
Request Method :>>  GET
Request URL :>>  /api/users?userid=100
```

To extract the query you’ll have to make use of the URL module. The URL module will parse the request URL to a JavaScript object.

```jsx
const http = require('http');
const url = require('url');

const server = http.createServer((req, res) => {
  const urlData = url.parse(req.url, true);
  console.log('urlData :>> ', urlData);

  res.end('Thank you Mario, but our princess is in another castle...');
});
```

Now you can see more information on the request:

```jsx
urlData :>>  Url {
  protocol: null,
  slashes: null,
  auth: null,
  host: null,
  port: null,
  hostname: null,
  hash: null,
  search: '?userid=100',
  query: [Object: null prototype] { userid: '100' },
  pathname: '/api/users',
  path: '/api/users?userid=100',
  href: '/api/users?userid=100'
}
```

From here it’s very easy to extract the query, body, search, pathname, and other parameters.

### Extract Request Body

The incoming request body arrives through a stream. You can intercept it by subscribing to the `data` stream on the request object.

```jsx
const server = http.createServer((req, res) => {

  req
    .on('data', (chunk) => {
      // data arrives in chunks
    })
    
   }); 
```

Every time new a chunk arrives store it in a collection.

```jsx
const server = http.createServer((req, res) => {

const bodyStream = [];

  req
    .on('data', (chunk) => {
      bodyStream.push(chunk);
    })
    
   }); 
```

Then listen to the `end` event that will fire when the whole data is finished processing.

```jsx
const server = http.createServer((req, res) => {

const bodyStream = [];

   req
    .on('data', (chunk) => {
      bodyStream.push(chunk);
    })
    .on('end', () => {
      console.log('Request body collected!');
    });
    
   }); 
```

Inside the `end` callback you concat all chunks as Buffer object and then parse the Buffer to the JavaScript object.

```jsx
const server = http.createServer((req, res) => {

  const bodyStream = [];

  req
    .on('data', (chunk) => {
      bodyStream.push(chunk);
    })
    .on('end', () => {
      const bufferData = Buffer.concat(bodyStream);
      const requestBody =  JSON.parse(bufferData);

      console.log('Request Body :>> ',requestBody);
      res.end('All good!');
    });

    console.log('Hello World!');
});
```

If you make a POST request for `localhost:3000` with Request Body:

```jsx
{
    "name": "Super Mario",
    "level": 94,
    "job": "Plumber"
}
```

It should print the same object in the console:

```jsx
Hello World!
Request Body :>>  { name: 'Super Mario', level: 94, job: 'Plumber' }
```

Notice how the ‘Hello World!’ was printed before the Request Body, even though I put `console.log` after subscribing to the events. That’s the proof that streams, even though they process data in chunks, do not block the program execution.

This is particularly useful when dealing with large files or when you want to process data in chunks rather than loading the entire payload into memory.

## Response

The Response object is an instance of `http.ServerResponse` that extends a **writable stream** and is used to send the response to the client. Since it is a stream, you can send data in chunks (using `res.write();`):

```jsx
const server = http.createServer((req, res) => {
  res.write('Hello');
  res.write('World');
  res.write('!');
  res.end();
});
```

Or all at once (using `res.end()`).

```jsx
const server = http.createServer((req, res) => {
  res.end('Hello World!');
});
```

Keep in mind that you can call `res.end()` only once per request.

### Status Code

The response object can also be used to set the HTTP response code (The default status code is 200):

```jsx
const server = http.createServer((req, res) => {
  res.statusCode = 400;
  res.end('Something went wrong!');
});
```

### Response Headers

The Response object can also contain headers that will be useful to the client, such as:

- Authorization token
- Content-Type
- Content-Length (Total-Count),
- Various security headers, etc.

The Response object sends Content-Type text by default. If you want to send other types, like JSON, you need to specify it using headers:

```jsx
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'application/json');
  // Very important: you must stringify the data before sending
  res.end(JSON.stringify({ greetings: 'Hello World' }));
});

server.listen(3000, () => {
  console.log('Server started on localhost:3000!');
})
```

You can set any other response header you desire:

```jsx
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'application/json');
  res.setHeader('X-Auth', 'TOKEN');
  res.end(JSON.stringify({ greetings: 'Hello World' }));
});
```

![1_chIT3YTSgJdD_7-6YfFOXQ.webp](HTTP%20Module%201b2aeacbb299812e94dbc5b7c46366e2/1_chIT3YTSgJdD_7-6YfFOXQ.webp)

You can also set headers like this:

```jsx
const server = http.createServer((req, res) => {
  res.setHeader('X-Auth', 'TOKEN');
  // this header is tied to the status code
  res.writeHead(201, { 'Content-Type': 'text/plain' });
  res.end('Created!');
}); 
```

## Error Handling

To handle errors in the HTTP module you can listen to the error event on the request and response objects:

```jsx
const http = require('http');

const server = http.createServer((req, res) => {

  req.on('error', (err) => {
    console.log('Request error occurred :>> ', err);
    res.statusCode = 400;
    return res.end('Bad Request!');
  })

  res.on('error', (err) => {
    console.log('Response error occurred :>> ', err);
    res.statusCode = 500;
    return res.end('Internal Server Error!');
  })

  res.end('All good!');
});

server.listen(3000, () => {
  console.log('Server started on localhost:3000!');
})
```

You can handle errors using the Try-Catch block:

```jsx
const server = http.createServer((req, res) => {
  try {
    // ...

    res.end('All good!');
  } catch (err) {
    console.error('Request processing error:', err);
    res.statusCode = 500;
    res.end('Internal Server Error!');
  }
});
```

## Router

The HTTP module does not have a built-in router. If you need to display different content per route you can make use of the Request object:

- Request Method
- Request URL (and URL module)

```jsx
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'application/json');

  // GET default page
  if (req.url === '/') {
    const responseData = JSON.stringify({ greeting: 'Hello World' });
    res.write(responseData);
    res.end();
  }

  // GET profile page
  else if (req.url === '/profile') {
    const responseData = JSON.stringify({ data: 'Profile page!' });
    res.write(responseData);
    res.end();
  }

  // POST Create item
  else if (
    req.url === '/create' && 
    req.method === 'POST' &&
    req.headers['content-type'] === 'application/json'
  ) {
    // handle POST request like in Extract Request Body section
  }

  // if route is not set
  else {
    res.statusCode = 404;
    res.write('Page not found!');
    res.end();
  }

})
```

## HTTPS

HTTPS protocol is used to encrypt communication between a client and a server (using TLS/SSL).

### Prerequisites

To get started, you need to obtain an SSL certificate, either:

- self-signed or
- trusted certificate

To generate a self-signed certificate do the following:

### Windows

- First of all, download and install OpenSSL on your machine.
- Go to the directory where you installed it and open CMD there.
- Run the following commands:

```jsx
openssl genpkey -algorithm RSA -out private-key.pem
openssl req -new -key private-key.pem -out csr.pem
openssl x509 -req -days 365 -in csr.pem -signkey private-key.pem -out certificate.pem
```

### Unix

You can generate a certificate on UNIX using the `openssl` command:

```jsx
openssl genpkey -algorithm RSA -out private-key.pem
openssl req -new -key private-key.pem -out csr.pem
openssl x509 -req -days 365 -in csr.pem -signkey private-key.pem -out certificate.pem
```

These commands generate a private key (`private-key.pem`), a certificate signing request (`csr.pem`), and a self-signed certificate (`certificate.pem`).

### Creating HTTPS Server

This time around you’ll make use of the HTTPS module. Start by loading the certificates:

```jsx
const https = require('https');
const fs = require('fs');

// Load SSL/TLS key and certificate files
const privateKey = fs.readFileSync('path/to/private-key.pem', 'utf8');
const certificate = fs.readFileSync('path/to/certificate.pem', 'utf8');

const credentials = {
  key: privateKey,
  cert: certificate,
};
```

Then create a server instance:

```jsx
// HTTPS server
const httpsServer = https.createServer(credentials, (req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Secure Hello World!');
});
```

And then listen to a port. The default port for the HTTPS server is 443:

```jsx
// Start the HTTPS server on port 443
httpsServer.listen(443, () => {
  console.log('HTTPS server listening on port 443');
});
```

Referenc This Note - [Link](https://mirzaleka.medium.com/a-detailed-look-into-the-node-js-http-module-680eb5e4548a)