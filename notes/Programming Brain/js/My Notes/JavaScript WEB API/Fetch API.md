# Fetch API

APIs allow different software applications to communicate with each other, enabling developers to access and retrieve data from various sources. One popular way to perform API requests in JavaScript is by using the Fetch API.

## How the Fetch API Works

---

The Fetch API is a modern JavaScript interface for making network requests, primarily designed to replace the older XMLHttpRequest. It provides a more straightforward and flexible way to handle HTTP requests, making it easier for developers to work with APIs and fetch data from servers.

In addition, the Fetch API is much simpler and cleaner. It uses the `Promise` to deliver more flexible features to make requests to servers from the web browsers. The `fetch()` method is available in the global scope that instructs the web browsers to send a request to a URL.

## Sending a Request

---

The `fetch()` requires only one parameter which is the URL of the resource that you want to fetch:

```jsx
let response = fetch(url);
```

The `fetch()` method returns a `Promise` so you can use the `then()` and `catch()` methods to handle it:

```jsx
fetch(url)
    .then(response => {
        // handle the response
    })
    .catch(error => {
        // handle the error
    });
```

When the request is completed, the resource is available. At this time, the promise will resolve into a `Response` object. The `Response` object is the API wrapper for the fetched resource. The `Response` object has a number of useful properties and methods to inspect the response.

## Reading the Response

If the contents of the response are in the raw text format, you can use the `text()` method. The `text()` method returns a `Promise` that resolves with the complete contents of the fetched resource:

```jsx
fetch('/readme.txt')
    .then(response => response.text())
    .then(data => console.log(data));
```

In practice, you often use the [`async`/`await`](https://www.javascripttutorial.net/es-next/javascript-async-await/) with the `fetch()` method like this:

```jsx
async function fetchText() {
    let response = await fetch('/readme.txt');
    let data = await response.text();
    console.log(data);
}
```

Besides the `text()` method, the `Response` object has other methods such as `json()`, `blob()`, `formData()` and `arrayBuffer()` to handle the respective type of data.

## Handling the status codes of the Response

The `Response` object provides the status code and status text via the `status` and `statusText` properties. When a request is successful, the status code is `200` and status text is `OK`:

```jsx
async function fetchText() {
    let response = await fetch('/readme.txt');

    console.log(response.status); // 200
    console.log(response.statusText); // OK

    if (response.status === 200) {
        let data = await response.text();
        // handle data
    }
}

fetchText();

// output is
// 200
// ok
```

If the requested resource doesn’t exist, the response code is `404`:

```jsx
let response = await fetch('/non-existence.txt');

console.log(response.status); // 400
console.log(response.statusText); // Not Found

// output is
// 400
// Not Found
```

[**How to Make a GET Request**](Fetch%20API%201b2aeacbb29981f68ccef2c406feb544/How%20to%20Make%20a%20GET%20Request%201b2aeacbb29981b0bb11d228ac5123bb.md)

[**How to Make a POST Request**](Fetch%20API%201b2aeacbb29981f68ccef2c406feb544/How%20to%20Make%20a%20POST%20Request%201b2aeacbb2998121a24ace803794ae48.md)

[**How to Handle Query Parameters**](Fetch%20API%201b2aeacbb29981f68ccef2c406feb544/How%20to%20Handle%20Query%20Parameters%201b2aeacbb2998167be4fd1927312867a.md)

[**How to Handle Authentication**](Fetch%20API%201b2aeacbb29981f68ccef2c406feb544/How%20to%20Handle%20Authentication%201b2aeacbb299811d8877e5043bc2f26e.md)

[**Error Handling**](Fetch%20API%201b2aeacbb29981f68ccef2c406feb544/Error%20Handling%201b2aeacbb299819fbbf4cfa17d4450a4.md)