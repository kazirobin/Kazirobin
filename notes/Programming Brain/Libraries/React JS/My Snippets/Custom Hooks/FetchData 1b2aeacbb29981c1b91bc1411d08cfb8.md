# FetchData

Fetching data from the backend is one of the crucial parts of the web application. For every application to work dynamically, it fetches the data from the server and then displays it in the user interface.

### Create custom data fetching hook use with fetch API

```jsx
import { useEffect, useState } from "react";

export default function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        const response = await fetch(url);
        const data = await response.json();

        if (!response.ok) {
          const errorMessage = `There was an error, Status code: ${response.status}`;
          throw new Error(errorMessage);
        }

        setData(data);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return [data, loading, error];
}
```

### Create custom data fetching hook use with Axios

```jsx
import { useEffect, useState } from "react";
import axios from "axios";

export default function useAxios(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        const response = await axios.get(url);
        setData(response.data);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return [data, loading, error];
}
```