# How does Axios work?

Axios works by making HTTP requests with NodeJS and XMLHttpRequests on the browser. If the request was successful, you will receive a **`response`** with the data requested. If the **`request`** failed, you will get an error. You can also **`intercept`** the requests and responses and transform or modify them. I will go into more detail about that later in this tutorial.

This diagram shows a representation of how Axios interacts with an application.

[2023-07-01-axios-operation.avif](How%20does%20Axios%20work%201b2aeacbb2998107b75bcae8fa92a149/2023-07-01-axios-operation.avif)

Axios is able to determine whether the request is made to the browser or to NodeJS. Once this is established, it then identifies the proper way to make the API requests and returns a transformed response back to the client that made the server request.