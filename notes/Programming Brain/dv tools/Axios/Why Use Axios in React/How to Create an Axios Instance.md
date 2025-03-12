# How to Create an Axios Instance

If you look at the previous examples, you'll see that there's a `baseURL` that you use as part of the endpoint for Axios to perform these requests.

However, it gets a bit tedious to keep writing that `baseURL` for every single request. Couldn't you just have Axios remember what `baseURL` you're using, since it always involves a similar endpoint?

In fact, you can. If you create an instance with the `.create()` method, Axios will remember that `baseURL`, plus other values you might want to specify for every request, including headers:

```jsx
import axios from "axios";
import React from "react";

const client = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com/posts" 
});

export default function App() {
  const [post, setPost] = React.useState(null);

  React.useEffect(() => {
    client.get("/1").then((response) => {
      setPost(response.data);
    });
  }, []);

  function deletePost() {
    client
      .delete("/1")
      .then(() => {
        alert("Post deleted!");
        setPost(null)
      });
  }

  if (!post) return "No post!"

  return (
    <div>
      <h1>{post.title}</h1>
      <p>{post.body}</p>
      <button onClick={deletePost}>Delete Post</button>
    </div>
  );
}
```

The one property in the config object above is `baseURL`, to which you pass the endpoint.

The `.create()` function returns a newly created instance, which in this case is called `client`.

Then in the future, you can use all the same methods as you did before, but you don't have to include the `baseURL` as the first argument anymore. You just have to reference the specific route you want, for example, `/`, `/1`, and so on.