# How to Make a POST Request

While GET requests are used for retrieving data, POST requests are used to send data to a server. This is commonly used when submitting forms or sending data to create a new resource. Let's explore how to make a POST request using the Fetch API.

Suppose we have a simple form with user details, and we want to send this data to a server to create a new user. Here's how you can make a POST request:

```jsx
// API endpoint for creating a new user
const apiUrl = 'https://api.example.com/users';

// Form data to be sent in the request body
const formData = {
  username: 'john_doe',
  email: 'john@example.com',
  password: 'securepassword123',
};

// Make a POST request using the Fetch API
fetch(apiUrl, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(formData),
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(newUserData => {
    // Process the newly created user data
    console.log('New User Data:', newUserData);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

In this example, we specify the API endpoint for creating a new user (`https://api.example.com/users`). We use the `method` property in the fetch options to set it as a POST request. Additionally, we include the `headers` property to indicate that we are sending JSON data in the request body.