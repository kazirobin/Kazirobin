# Sharing State Between Components

`CreatedAt- 24 Jan 2024 / RevisedAt-`

Sometimes, you want the state of two components to always change together. To do it, remove state from both of them, move it to their closest common parent, and then pass it down to them via props. This is known as lifting state up, and it’s one of the most common things you will do writing React code.

---

## **Lifting state up by example**

In this example, a parent `Accordion` component renders two separate `Panel`s:

- `Accordion`
    - `Panel`
    - `Panel`

Each `Panel` component has a boolean `isActive` state that determines whether its content is visible.

Press the Show button for both panels:

```jsx
import { useState } from 'react';

function Panel({ title, children }) {
  const [isActive, setIsActive] = useState(false);
  return (
    <section className="panel">
      <h3>{title}</h3>
      {isActive ? (
        <p>{children}</p>
      ) : (
        <button onClick={() => setIsActive(true)}>
          Show
        </button>
      )}
    </section>
  );
}

export default function Accordion() {
  return (
    <>
      <h2>Almaty, Kazakhstan</h2>
      <Panel title="About">
        With a population of about 2 million, Almaty is Kazakhstan's largest city. From 1929 to 1997, it was its capital city.
      </Panel>
      <Panel title="Etymology">
        The name comes from <span lang="kk-KZ">алма</span>, the Kazakh word for "apple" and is often translated as "full of apples". In fact, the region surrounding Almaty is thought to be the ancestral home of the apple, and the wild <i lang="la">Malus sieversii</i> is considered a likely candidate for the ancestor of the modern domestic apple.
      </Panel>
    </>
  );
}
```

Notice how pressing one panel’s button does not affect the other panel—they are independent.

![Untitled](Sharing%20State%20Between%20Components%201b2aeacbb299819b9c55c1bf184dc99e/Untitled.png)

**But now let’s say you want to change it so that only one panel is expanded at any given time.** With that design, expanding the second panel should collapse the first one. How would you do that?

To coordinate these two panels, you need to “lift their state up” to a parent component in three steps:

1. **Remove** state from the child components.
2. **Pass** hardcoded data from the common parent.
3. **Add** state to the common parent and pass it down together with the event handlers.

This will allow the `Accordion` component to coordinate both `Panel`s and only expand one at a time.

[**Step 1: Remove state from the child components**](Sharing%20State%20Between%20Components%201b2aeacbb299819b9c55c1bf184dc99e/Step%201%20Remove%20state%20from%20the%20child%20components%201b2aeacbb29981b08412fb9f7d348ca8.md)

[**Step 2: Pass hardcoded data from the common parent**](Sharing%20State%20Between%20Components%201b2aeacbb299819b9c55c1bf184dc99e/Step%202%20Pass%20hardcoded%20data%20from%20the%20common%20parent%201b2aeacbb29981598289fdc3b1186cce.md)

[**Step 3: Add state to the common parent**](Sharing%20State%20Between%20Components%201b2aeacbb299819b9c55c1bf184dc99e/Step%203%20Add%20state%20to%20the%20common%20parent%201b2aeacbb2998194a275cf8e43b59bc1.md)

## **A single source of truth for each state**

In a React application, many components will have their own state. Some state may “live” close to the leaf components (components at the bottom of the tree) like inputs. Other state may “live” closer to the top of the app. For example, even client-side routing libraries are usually implemented by storing the current route in the React state, and passing it down by props!

**For each unique piece of state, you will choose the component that “owns” it.** This principle is also known as having a [“single source of truth”.](https://en.wikipedia.org/wiki/Single_source_of_truth) It doesn’t mean that all state lives in one place—but that for *each* piece of state, there is a *specific* component that holds that piece of information. Instead of duplicating shared state between components, *lift it up* to their common shared parent, and *pass it down* to the children that need it.

our app will change as you work on it. It is common that you will move state down or back up while you’re still figuring out where each piece of the state “lives”. This is all part of the process!

To see what this feels like in practice with a few more components, read [Thinking in React.](https://react.dev/learn/thinking-in-react)