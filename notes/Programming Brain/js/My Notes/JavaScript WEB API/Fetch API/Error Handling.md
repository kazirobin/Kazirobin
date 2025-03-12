# Error Handling

Handling errors is a crucial part of making robust applications. The Fetch API provides a convenient way to catch and handle errors that may occur during a network request.

Let's modify our earlier examples to include more comprehensive error handling:

```jsx
// API endpoint for user data
const apiUrl = 'https://api.example.com/users/123';

// Make a GET request using the Fetch API
fetch(apiUrl)
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.json();
  })
  .then(userData => {
    // Process the retrieved user data
    console.log('User Data:', userData);
  })
  .catch(error => {
    console.error('Error:', error.message);
  });
```

In this modified example, we include additional information about the HTTP status in the error message when the response is not okay. This can be helpful for debugging and providing more context about the nature of the error.