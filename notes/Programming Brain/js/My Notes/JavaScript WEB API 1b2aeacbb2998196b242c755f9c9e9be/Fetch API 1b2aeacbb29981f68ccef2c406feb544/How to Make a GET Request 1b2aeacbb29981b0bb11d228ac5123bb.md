# How to Make a GET Request

The most common type of request when working with APIs is the GET request. It's used to retrieve data from a server. Let's walk through an example of making a simple GET request using the Fetch API.

Suppose we want to retrieve information about a user from a hypothetical API. Here's how you can do it:

```jsx
// Specify the API endpoint for user data
const apiUrl = 'https://api.example.com/users/123';

// Make a GET request using the Fetch API
fetch(apiUrl)
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(userData => {
    // Process the retrieved user data
    console.log('User Data:', userData);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

In this example, we define the API endpoint for user data (`https://api.example.com/users/123`). The fetch function is used to make the GET request, and we handle the response by checking if it's okay using the `response.ok` property. If the response is okay, we convert it to JSON and process the user data.