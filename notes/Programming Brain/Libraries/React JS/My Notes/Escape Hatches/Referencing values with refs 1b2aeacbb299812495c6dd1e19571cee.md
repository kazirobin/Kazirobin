# Referencing values with refs

When you want a component to “remember” some information, but you don’t want that information to trigger new renders, you can use a *ref*:

```jsx
const ref = useRef(0);
```

Like state, refs are retained by React between re-renders. However, setting state re-renders a component. Changing a ref does not! You can access the current value of that ref through the `ref.current` property.

```jsx
import { useRef } from 'react';

export default function Counter() {
  let ref = useRef(0);

  function handleClick() {
    ref.current = ref.current + 1;
    alert('You clicked ' + ref.current + ' times!');
  }

  return (
    <button onClick={handleClick}>
      Click me!
    </button>
  );
}
```

A ref is like a secret pocket of your component that React doesn’t track. For example, you can use refs to store timeout IDs, DOM elements, and other objects that don’t impact the component’s rendering output.

[**Adding a ref to your component**](Referencing%20values%20with%20refs%201b2aeacbb299812495c6dd1e19571cee/Adding%20a%20ref%20to%20your%20component%201b2aeacbb2998140b03bd36c99d9e6f4.md)

[**Example: building a stopwatch**](Referencing%20values%20with%20refs%201b2aeacbb299812495c6dd1e19571cee/Example%20building%20a%20stopwatch%201b2aeacbb299813e8de4eff5c4ed70dc.md)

[**Differences between refs and state**](Referencing%20values%20with%20refs%201b2aeacbb299812495c6dd1e19571cee/Differences%20between%20refs%20and%20state%201b2aeacbb29981bd862ff7b1df6917a0.md)

[**When to use refs**](Referencing%20values%20with%20refs%201b2aeacbb299812495c6dd1e19571cee/When%20to%20use%20refs%201b2aeacbb299814aa1fbd578952b0286.md)

[**Best practices for refs**](Referencing%20values%20with%20refs%201b2aeacbb299812495c6dd1e19571cee/Best%20practices%20for%20refs%201b2aeacbb29981e3b363d9f9ae3a11ae.md)

[**Refs and the DOM**](Referencing%20values%20with%20refs%201b2aeacbb299812495c6dd1e19571cee/Refs%20and%20the%20DOM%201b2aeacbb299814391e1d489c42e4a90.md)