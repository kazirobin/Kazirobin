# Response Object

The Response object (res) specifies the HTTP response which is sent by an Express app when it gets an HTTP request.

## What it does

- It sends response back to the client browser.
- It facilitates you to put new cookies value and that will write to the client browser (under cross domain rule).
- Once you res.send() or res.redirect() or res.render(), you cannot do it again, otherwise, there will be uncaught error.

## Response Object Properties

Let's see some properties of response object.

| **Properties** | **Description** |
| --- | --- |
| res.app | It holds a reference to the instance of the express application that is using the middleware. |
| res.headersSent | It is a Boolean property that indicates if the app sent HTTP headers for the response. |
| res.locals | It specifies an object that contains response local variables scoped to the request |

## Response Object Methods

Following are some methods:

### Response Cookie method

This method is used to set a cookie name to value. The value can be a string or object converted to JSON.

**Syntax:**

```jsx
res.cookie(name, value [, options])
```

**Examples:**

```jsx
res.cookie('name', 'Aryan', { domain: '.xyz.com', path: '/admin', secure: true });  
res.cookie('Section', { Names: [Aryan,Sushil,Priyanka] });  
res.cookie('Cart', { items: [1,2,3] }, { maxAge: 900000 });  
```

### Response End method

This method is used to end the response process.

**Syntax:**

```jsx
res.end([data] [, encoding])
```

**Examples:**

```jsx
res.end();
res.status(404).end();
```

### Response Format method

This method performs content negotiation on the Accept HTTP header on the request object, when present.

**Syntax:**

```jsx
res.format(object)
```

**Examples:**

```jsx
res.format({  
  'text/plain': function(){  
    res.send('hey');  
  },  
 'text/html': function(){  
    res.send('  
hey');  
  },  
  'application/json': function(){  
    res.send({ message: 'hey' });  
  },  
 'default': function() {  
    //Log the request and respond with 406  
    res.status(406).send('Not Acceptable');  
  }  
});
```

### Response JSON method

This method returns the response in JSON format.

**Syntax:**

```jsx
res.json([body])
```

**Examples:**

```jsx
res.json(null)  
res.json({ name: 'ajeet' })
```

### Response Location method

This method is used to set the response location HTTP header field based on the specified path parameter.

**Syntax:**

```jsx
res.location(path)
```

**Examples:**

```jsx
res.location('http://xyz.com');
```

### Response Redirect method

This method redirects to the URL derived from the specified path, with specified HTTP status

**Syntax:**

```jsx
res.redirect([status,] path)
```

**Examples:**

```jsx
res.redirect('http://example.com');
```

### Response Render method

This method renders a view and sends the rendered HTML string to the client.

**Syntax:**

```jsx
res.render(view [, locals] [, callback])
```

**Examples:**

```jsx
res.render("index", { title: "Home" });
```

### Response Send method

This method is used to send HTTP response.

**Syntax:**

```jsx
res.send([body])
```

**Examples:**

```jsx
res.send("Hello World!");
```

### Response sendFile method

This method is used to transfer the file at the given path. It sets the Content-Type response HTTP header field based on the filename's extension.

**Syntax:**

```jsx
res.sendFile(path [, options] [, fn])
```

**Examples:**

```jsx
res.sendFile("index", { root: dirname });
```

### Response Type method

This method sets the content-type HTTP header to the MIME type.

**Syntax:**

```jsx
res.type(type)
```

**Examples:**

```jsx
res.type('.html');              // => 'text/html'  
res.type('html');               // => 'text/html'  
res.type('json');               // => 'application/json'  
res.type('application/json');   // => 'application/json'  
res.type('png');                // => image/png:  
```