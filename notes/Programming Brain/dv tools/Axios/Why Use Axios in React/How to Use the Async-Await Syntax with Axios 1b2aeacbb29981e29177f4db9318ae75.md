# How to Use the Async-Await Syntax with Axios

A big benefit to using promises in JavaScript (including React applications) is the async-await syntax.

Async-await allows you to write much cleaner code without `then` and `catch` callback functions. Plus, code with async-await looks a lot like synchronous code, and is easier to understand.

But how do you use the async-await syntax with Axios?

In the example below, posts are fetched and there's still a button to delete that post:

```jsx
import axios from "axios";
import React from "react";

const client = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com/posts" 
});

export default function App() {
  const [post, setPost] = React.useState(null);

  React.useEffect(() => {
    async function getPost() {
      const response = await client.get("/1");
      setPost(response.data);
    }
    getPost();
  }, []);

  async function deletePost() {
    await client.delete("/1");
    alert("Post deleted!");
    setPost(null);
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

However in `useEffect`, there's an `async` function called `getPost`.

Making it `async` allows you to use the `await` keword to resolve the GET request and set that data in state on the next line without the `.then()` callback.

Note that the `getPost` function is called immediately after being created.

Additionally, the `deletePost` function is now `async`, which is a requirement to use the `await` keyword which resolves the promise it returns (every Axios method returns a promise to resolve).

After using the `await` keyword with the DELETE request, the user is alerted that the post was deleted, and the post is set to `null`.

As you can see, async-await cleans up the code a great deal, and you can use it with Axios very easily.