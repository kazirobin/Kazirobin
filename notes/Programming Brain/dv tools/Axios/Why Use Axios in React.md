# Why Use Axios in React

---

There are a number of different libraries you can use to make these requests, so why choose Axios?

Here are **five reasons** why you should use Axios as your client to make HTTP requests:

1. It has good defaults to work with JSON data. Unlike alternatives such as the Fetch API, you often don't need to set your headers. Or perform tedious tasks like converting your request body to a JSON string.
2. Axios has function names that match any HTTP methods. To perform a GET request, you use the `.get()` method.
3. Axios does more with less code. Unlike the Fetch API, you only need one `.then()` callback to access your requested JSON data.
4. Axios has better error handling. Axios throws 400 and 500 range errors for you. Unlike the Fetch API, where you have to check the status code and throw the error yourself.
5. Axios can be used on the server as well as the client. If you are writing a Node.js application, be aware that Axios can also be used in an environment separate from the browser.

## How to Set Up Axios with React

---

Using Axios with React is a very simple process. You need three things:

1. An existing React project
2. To install Axios with npm/yarn
3. An API endpoint for making requests

If you have an existing React project, you just need to install Axios with npm

```bash
npm install axios
```

In this guide, you'll use the JSON Placeholder API to get and change post data.

Here is a list of all the different routes you can make requests to, along with the appropriate HTTP method for each:

Here is a quick example of all of the operations you'll be performing with Axios and your API endpoint — retrieving, creating, updating, and deleting posts:

[**How to Make a GET Request**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20Make%20a%20GET%20Request%201b2aeacbb29981848a7fca1b2c5872e6.md)

[**How to Make a POST Request**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20Make%20a%20POST%20Request%201b2aeacbb29981b288ece2169be7c9c0.md)

[**How to Make a PUT Request**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20Make%20a%20PUT%20Request%201b2aeacbb29981ef8990dcf8830026fa.md)

[**How to Make a DELETE Request**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20Make%20a%20DELETE%20Request%201b2aeacbb299816ca445ddf984211028.md)

[**How to Handle Errors with Axios**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20Handle%20Errors%20with%20Axios%201b2aeacbb29981888a46e768c1d3b7ac.md)

[**How to Create an Axios Instance**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20Create%20an%20Axios%20Instance%201b2aeacbb299813883d3d60fb3b04192.md)

[**How to Use the Async-Await Syntax with Axios**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20Use%20the%20Async-Await%20Syntax%20with%20Axios%201b2aeacbb29981e29177f4db9318ae75.md)

[**How to use interceptor in Axios**](Why%20Use%20Axios%20in%20React%201b2aeacbb29981cb8d18ed115d77ed05/How%20to%20use%20interceptor%20in%20Axios%201b2aeacbb299810b8138c419213817c1.md)