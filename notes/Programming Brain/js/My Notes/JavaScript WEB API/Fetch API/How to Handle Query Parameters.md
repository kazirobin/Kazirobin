# How to Handle Query Parameters

Often, when working with APIs, you need to include query parameters in your requests to filter or modify the data you receive. Let's explore how to handle query parameters when making a GET request.

Suppose we want to retrieve a list of users based on a specific criteria, such as users who have registered in the last 30 days. We can achieve this by including query parameters in the URL:

```jsx
// API endpoint for fetching recent users
const apiUrl = 'https://api.example.com/users/recent';

// Set up query parameters
const queryParams = {
  timeframe: '30days',
};

// Convert query parameters to a string
const queryString = new URLSearchParams(queryParams).toString();

// Combine API endpoint with query parameters
const fullUrl = `${apiUrl}?${queryString}`;

// Make a GET request using the Fetch API
fetch(fullUrl)
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(recentUsers => {
    // Process the list of recent users
    console.log('Recent Users:', recentUsers);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

In this example, we define the API endpoint for fetching recent users (`https://api.example.com/users/recent`). We set up query parameters using an object (`queryParams`) and convert them to a string using `URLSearchParams`. The resulting string is then appended to the API endpoint to form the full URL.