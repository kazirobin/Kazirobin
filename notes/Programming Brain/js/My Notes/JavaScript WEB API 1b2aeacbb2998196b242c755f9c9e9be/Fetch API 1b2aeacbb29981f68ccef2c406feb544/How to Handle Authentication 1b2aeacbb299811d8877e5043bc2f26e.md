# How to Handle Authentication

Many APIs require authentication to access protected resources. The Fetch API provides a way to include authentication information in your requests using headers. Let's explore how to handle authentication when making a request.

Suppose we have an API that requires an API key for authentication. Here's how you can include the API key in the request headers:

```jsx
// API endpoint requiring authentication
const apiUrl = 'https://api.example.com/protected/resource';

// API key for authentication
const apiKey = 'your-api-key';

// Make a GET request with authentication using the Fetch API
fetch(apiUrl, {
  headers: {
    Authorization: `Bearer ${apiKey}`,
  },
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(protectedData => {
    // Process the protected data
    console.log('Protected Data:', protectedData);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

In this example, we include the API key in the request headers using the `Authorization` header. The `Bearer` keyword is commonly used for API key authentication, followed by the actual API key.