# How to Handle Errors with Axios

What about handling errors with Axios?

What if there's an error while making a request? For example, you might pass along the wrong data, make a request to the wrong endpoint, or have a network error.

To simulate an error, you'll send a request to an API endpoint that doesn't exist: `/posts/asdf`.

This request will return a `404` status code:

```jsx
import axios from "axios";
import React from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts";

export default function App() {
  const [post, setPost] = React.useState(null);
  const [error, setError] = React.useState(null);

  React.useEffect(() => {
    // invalid url will trigger an 404 error
    axios.get(`${baseURL}/asdf`).then((response) => {
      setPost(response.data);
    }).catch(error => {
      setError(error);
    });
  }, []);
  
  if (error) return `Error: ${error.message}`;
  if (!post) return "No post!"

  return (
    <div>
      <h1>{post.title}</h1>
      <p>{post.body}</p>
    </div>
  );
}
```

In this case, instead of executing the `.then()` callback, Axios will throw an error and run the `.catch()` callback function.

In this function, we are taking the error data and putting it in state to alert our user about the error. So if we have an error, we will display that error message.

In this function, the error data is put in state and used to alert users about the error. So if there's an error, an error message is displayed.

When you run this code code, you'll see the text, "Error: Request failed with status code 404".

## How to Handle Errors in Axios with the try…catch Block

For the async/await scenario, the `try...catch` block will look like this:

```jsx
useEffect(() => {
    const fetchPosts = async () => {
      try {
        const response = await client.get("1");

        if (response && response.data) {
          setPosts(response.data);
        }
      } catch (error) {
        if (error.response) {
          // Error came from server
          setError(`Error from server: status: ${error.response.status}`);
        } else {
          // Network error, did not reach to server
          setError(error.message);
        }
      }
    };

    fetchPosts();
  }, []);
```