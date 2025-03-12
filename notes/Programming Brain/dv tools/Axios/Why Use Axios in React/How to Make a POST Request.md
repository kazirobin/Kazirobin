# How to Make a POST Request

To create new data, make a POST request.

According to the API, this needs to be performed on the `/posts` endpoint. If you look at the code below, you'll see that there's a button to create a post:

```jsx
import axios from "axios";
import React from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts";

export default function App() {
  const [post, setPost] = React.useState(null);

  React.useEffect(() => {
    axios.get(`${baseURL}/1`).then((response) => {
      setPost(response.data);
    });
  }, []);

  function createPost() {
    axios
      .post(baseURL, {
        title: "Hello World!",
        body: "This is a new post."
      })
      .then((response) => {
        setPost(response.data);
      });
  }

  if (!post) return "No post!"

  return (
    <div>
      <h1>{post.title}</h1>
      <p>{post.body}</p>
      <button onClick={createPost}>Create Post</button>
    </div>
  );
}
```

When you click on the button, it calls the `createPost` function.

To make that POST request with Axios, you use the `.post()` method. As the second argument, you include an object property that specifies what you want the new post to be.

Once again, use a `.then()` callback to get back the response data and replace the first post you got with the new post you requested.

This is very similar to the `.get()` method, but the new resource you want to create is provided as the second argument after the API endpoint.