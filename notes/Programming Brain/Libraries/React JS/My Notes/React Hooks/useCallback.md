# useCallback

`CreatedAt- 15 Nov 2024 / RevisedAt-` 

The `useCallback` hook is a built-in hook in React that lets you memoize a callback function by preventing it from being recreated on every render. In simple terms, it means that the callback function is cached and does not get redefined on every render. This will optimize and improve the overall performance of your application.

When you define a function inside a component, it is recreated on every render, even if the component’s state or props have not changed. This can lead to unnecessary re-renders, which can slow down your application’s performance. The useCallback hook helps you avoid this problem by memoizing the function and only recreating it when necessary.

Memoization can be compared to a real-world scenario where you ask someone to calculate the result of 2 multiplied by 200. After a while, you randomly ask the same question again. You naturally expect that person to give you the answer immediately because they have already done the calculation before. This time-saving concept is similar to memoization, where previously computed results are stored and reused when needed.

## The useCallback syntax

This hook follows a very simple pattern for utilization. It takes two arguments: the function you want to memoize, and the dependencies array.

```jsx
useCallback(function, dependencies)
```

```jsx
const updatedFunction = useCallback(
  (args) => {
    //action goes in here	
  },
  [dependencies] 
);
```

- The first argument is the function you want to memoize.
- The second argument is an array of dependencies. The elements in this array are the values on which the function to be memoized depends. If any of these values change, the function will be recreated.

**Note:** if you omit the dependencies array, the function will be re-defined on every render.

## How to Memoize a React Component

In React, we implement memoization via `React.memo()`, which is a higher-order component. The `React.memo` serves as a wrapper for a component and returns a memoized output of that component, which prevents the component or sub-components from unnecessary re-rendering.

There are two ways by which we can use `React.memo` in our component. We can either use it to wrap the entire component or add it to the part where we export the component.

In the example below you will find the first way of using it:

```jsx
const newComponent = React.memo((props) => {
    return (
      //render with props
    );
});

export default newComponent;
```

In the syntax above, the `newComponent` component is wrapped with `React.memo()`, which creates a memoized version of the component. This memoized version of the component will only re-render if the props passed to it have changed.

And here is the second way you can use `React.memo`:

```jsx
const newComponent = (props) => {
  //render with props
}

export default React.memo(newComponent);
```

The syntax above denotes that we can memoize a component by simply passing it as an argument to `React.memo` and exporting the result.

**Note:** `React.memo` has nothing to do with React hooks. It is an in-built method in React used to aid the optimization of our React applications. If you prefer using a hook to memoize your component, you can use `memo` in place of `React.memo`.

## When to use the useCallback hook

Now you understand how the `useCallback` hook can optimize your app, let’s see some use cases:

- When you need to pass a function as props to a child component.
- If you have a function that is expensive to compute and you need to call it in multiple places.
- When dealing with functional components.
- When you are working with a function that relies on external data or state.

**Note:** Given the scenarios highlighted above, it’s still important to weigh the benefits and drawbacks of the hook and use it judiciously only where needed.

## The difference between useCallback and useMemo

According to the [React documentation](https://react.dev/), there is a hook called `useMemo` which also falls under the performance hooks category. Despite being under the same category of hooks division, these hooks differ in purpose and usage.

Let’s look at the `useMemo` syntax before discussing how it differs from `useCallback`.

Just like `useCallback`, this hook also takes two arguments – a function and the dependencies array.

```jsx
const updatedValue = useMemo((args) => {
  //function body that returns the value to memoize	
  },
  [dependencies] 
);
```

The major difference between the hooks is that the `useCallback` returns a memoized function while the `useMemo` returns a memoized value. It means that `useMemo` can help prevent unnecessary computations as it caches the computed value of the function and `useCallback` can help prevent unnecessary re-renders as it returns the memoized function that can be passed as props to the children’s components.

The `useCallback` hook is ideal for functions that take a long time to compute or depend on external resources. In contrast, `useMemo` is ideal for values that take a long time to compute or depend on external resources.

```jsx
import React, {useMemo, useState} from 'react';

const addition = (counter) => {
  let newValue = counter;
  for (let n = 0; n <= 10; n++) {
    newValue += 1;
  }
  return newValue;
}

export function App(props) {
  const [initial, setInitial] = useState(0);

  const result = useMemo(()=> {
    return addition(initial);
  }, [initial])
  console.log("useMemo:", result )
  return (
    <div className='App'>
      <h1>Hello this is the {result}</h1>
    </div>
  );
}
```

When using `useMemo` the console prints: `“useMemo: 11”`

Let’s now test what `useCallback` results to in the same scenario:

```jsx
import React, {useCallback, useState} from 'react';

export function App(props) {
  const [count, setCount] = useState(0);

  // Define a callback function using useCallback
  const handleClick = useCallback(() => {
    return count;
  }, [count]);

  console.log("useCallback:", handleClick )

  return (
    <div className='App'>
       <p>Count: {count}</p>
    </div>
  );
}
```

In this example, the console prints a function `“useCallback: f()”`. When using this function in a properly-bootstrapped React project, the returned function is `( ) => { return count }`.

## Benefits of using the useCallback hook

There are several advantages attached to using the `useCallback` hook. Here are a few:

- Performance optimization: This hook optimizes the performance of your application by preventing a series of unnecessary re-rendering in your components.
- Restricting rendering of child components: The useCallback hook in React allows us to selectively render important child components in a parent component. By using the `useCallback` hook, we can create memoized functions and pass them as props to child components. This ensures that only the necessary child components are rendered and updated when specific actions occur, resulting in improved performance.
- Preventing memory leaks: Since the hook returns the memoized function, it prevents recreating functions, which can lead to memory leaks.

## Drawbacks of the useCallback hook

Before making use of this hook, take into consideration its challenges, then weigh if it is still important to apply it in a particular case. The drawbacks:

- **Complex code**: While this hook can help you create memoized functions, it can as well make your code complex. You must strike a balance between the usage of the hook and the complexity it adds to your code. Hence, only use the hook only when you need to memoize an expensive function which needs to be passed down to children components as a prop.
- **Excessive memory usage**: If you do not use the `useCallbck` hook properly, it can lead to excessive memory usage. For instance, if a memoized function holds onto references to objects or variables that are no longer needed, those resources may not be freed up by garbage collection and could use more memory than needed.