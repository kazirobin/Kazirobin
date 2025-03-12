# useNavigate

The `useNavigate` hook is a new addition to React Router 6. It's a replacement for the `useHistory` and `useLocation` hooks in previous versions of React Router. The `useNavigate` hook provides a simple and intuitive API for navigating between pages in your React application. It's designed to be used with functional components and hooks, and it simplifies the process of handling URL changes in your application.

## **How to use `useNavigate` in React application**

To use `useNavigate`, you first need to install React Router 6 and add it to your project:

```bash
npm install react-router-dom
```

Once you have React Router 6 installed, you can import the `useNavigate` hook from the `react-router-dom` package:

```bash
import { useNavigate } from 'react-router-dom';
```

You can then use the `useNavigate` hook in your functional components to navigate between pages:

```jsx
import { useNavigate } from 'react-router-dom';

export default function MyComponent() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate('/other-page');
  };

  return (
    <button onClick={handleClick}>Go to other page</button>
  );
}
```

In this example, we’re using the `useNavigate` hook to create a `navigate` function that we can use to navigate to a different page. We then use this function in the `handleClick` function to navigate to the `/other-page` URL when the button is clicked.

The `navigate` function can also accept an options object as a second parameter, which can be used to control the navigation behavior. For example, you can use the `replace` option to replace the current URL in the history stack instead of adding a new entry:

```jsx
import { useNavigate } from 'react-router-dom';

export default function MyComponent() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate('/other-page', { replace: true });
  };

  return (
    <button onClick={handleClick}>Go to other page</button>
  );
}
```

In this example, we’re using the `replace` option to replace the current URL in the history stack instead of adding a new entry. This can be useful if you want to navigate to a new page without creating a new entry in the history stack.

## Pass Data Between Pages

Now in order to pass our full blog post into the page to which were navigating, we will define state as the second argument in the navigate hook as seen here in CardPost..

```jsx
const handleClick = (data) => {
    navigate("/post", {state: data});
  };
```

So now whenever you navigate to the page you’ll have the data available inside the state. The next step is how to receive this data in the post page? A very important question. This is where the hook called useLocation comes in.

And to make it easier we’ll go ahead and destructure the body and title variables held in state..

```jsx
export default function Post(props) {
    const postData = useLocation();
    console.log(postData.state);
  return <div>this is my post page</div>;
}
```