# Async Actions

Just call `set` when you're ready, zustand doesn't care if your actions are async or not.

```jsx
const useFishStore = create((set) => ({
  fishies: {},
  fetch: async (pond) => {
    const response = await fetch(pond)
    set({ fishies: await response.json() })
  },
}))
```

For example:

```jsx
import { create } from "zustand";

interface PostStoreState {
  posts: {
    userId: number;
    id: number;
    title: string;
    body: string;
  }[];
  loading: boolean;
  getPosts: (posts: string) => Promise<void>;
}

export const usePostStore = create<PostStoreState>((set) => ({
  posts: [],
  loading: false,
  getPosts: async (url) => {
    set({ loading: true });
    const response = await fetch(url);
    set({ posts: await response.json(), loading: false });
  },
}));
```

```jsx
import { usePostStore } from "./store/post-store";

export default function App() {
  const { posts, getPosts, loading } = usePostStore((state) => state);

  return (
    <div>
      <button
        onClick={() => getPosts("https://jsonplaceholder.typicode.com/posts")}
      >
        Add Data
      </button>
      {loading && <p>Loading...</p>}
      <ul>
        {posts?.map((item) => (
          <li key={item.id}>{item.title}</li>
        ))}
      </ul>
    </div>
  );
}
```