# How to use interceptor in Axios

Axios interceptors are the default configurations that are added automatically to every request or response that a user receives. It is useful to check response status code for every response that is being received.

**Interceptors are methods which are triggered before or after the main method**. There are two types of interceptors:

1. **request interceptor**: - It allows you to write or execute a piece of your code before the request gets sent.
2. **response interceptor**: - It allows you to write or execute a piece of your code before response reaches the calling end.

![axios-interceptors.png](How%20to%20use%20interceptor%20in%20Axios%201b2aeacbb299810b8138c419213817c1/axios-interceptors.png)

### The steps to create Axios request & response interceptors are:

1. Create a new **Axios instance** with a custom config
2. Create request, response & error handlers
3. Configure/make use of **request & response interceptors** from Axios
4. Export the newly created **Axios instance** to be used in different locations

### Request interceptor

```jsx
client.interceptors.request.use(
  (config) => {
    const token = "1GH2DF345J6GH78G9";
    if (token) {
      config.headers["Authorization"] = `Bearer: ${token}`;
    }
    return config;
  },
  (error) => {
		// Do something with request error
    return Promise.reject(error);
  }
);
```

### Response interceptor

```jsx
client.interceptors.response.use(
  (response) => {
    // Do something with response data
    return response;
  },
  (error) => {
    if (error.response) {
      error.message = `Error from server: ${error.response.status}`;
    }
    return Promise.reject(error);
  }
);
```