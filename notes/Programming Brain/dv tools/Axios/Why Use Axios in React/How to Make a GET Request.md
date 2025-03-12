# How to Make a GET Request

To fetch data or retrieve it, make a GET request.

First, you're going to make a request for individual posts. If you look at the endpoint, you are getting the first post from the `/posts` endpoint:

```jsx
import axios from "axios";
import React from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts/1";

export default function App() {
  const [post, setPost] = React.useState(null);

  React.useEffect(() => {
    axios.get(baseURL).then((response) => {
      setPost(response.data);
    });
  }, []);

  if (!post) return null;

  return (
    <div>
      <h1>{post.title}</h1>
      <p>{post.body}</p>
    </div>
  );
}
```

To perform this request when the component mounts, you use the `useEffect` hook. This involves importing Axios, using the `.get()` method to make a GET request to your endpoint, and using a `.then()` callback to get back all of the response data.

The response is returned as an object. The data (which is in this case a post with `id`, `title`, and `body` properties) is put in a piece of state called `post` which is displayed in the component.

Note that you can always find the requested data from the `.data` property in the response.