# Render and Commit

Before your components are displayed on screen, they must be rendered by React. Understanding the steps in this process will help you think about how your code executes and explain its behavior.

Imagine that your components are cooks in the kitchen, assembling tasty dishes from ingredients. In this scenario, React is the waiter who puts in requests from customers and brings them their orders. This process of requesting and serving UI has three steps:

1. **Triggering** a render (delivering the guest’s order to the kitchen)
2. **Rendering** the component (preparing the order in the kitchen)
3. **Committing** to the DOM (placing the order on the table)

![Screenshot_1.jpg](Render%20and%20Commit%201b2aeacbb29981de84b6cad6ca85213f/Screenshot_1.jpg)

## Step 1: Trigger A Render

---

There are two reasons for a component to render:

1. It’s the component’s initial render.
2. The component’s (or one of its ancestors’) state or props has been updated.

### Initial Render

When your app starts, you need to trigger the initial render. Frameworks and sandboxes sometimes hide this code, but it’s done by calling createRoot with the target DOM node, and then calling its render method with your component:

Create a filed named **“./src/main.jsx”**

```jsx
import Image from './Image.jsx';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'))
root.render(<Image />);
```

Create a filed named **“./src/Image.jsx”**

```jsx
export default function Image() {
  return (
    <img
      src="https://i.imgur.com/ZF6s192.jpg"
      alt="'Floralis Genérica' by Eduardo Catalano: a gigantic metallic flower sculpture with reflective petals"
    />
  );
}
```

Try commenting out the root.render() call and see the component disappear!

### Re-renders When State Updates

Once the component has been initially rendered, you can trigger further renders by updating its state with the `set function`. Updating your component’s state automatically queues a render. (You can imagine these as a restaurant guest ordering tea, dessert, and all sorts of things after putting in their first order, depending on the state of their thirst or hunger.)

![Screenshot_2.jpg](Render%20and%20Commit%201b2aeacbb29981de84b6cad6ca85213f/Screenshot_2.jpg)

## Step 2: React Renders Your Components

---

After you trigger a render, React calls your components to figure out what to display on screen. “Rendering” is React calling your components.

- On initial render, React will call the root component.
- For subsequent renders, React will call the function component whose state update triggered the render.

This process is recursive: if the updated component returns some other component, React will render that component next, and if that component also returns something, it will render that component next, and so on. The process will continue until there are no more nested components and React knows exactly what should be displayed on screen.

In the following example, React will call `Gallery()` and `Image()` several times:

Create a file named **“./src/main.jsx”**

```jsx
import Gallery from './Gallery.jsx';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'))
root.render(<Gallery />);
```

Create a file named **“./src/Gallery.jsx”**

```jsx
export default function Gallery() {
  return (
    <section>
      <h1>Inspiring Sculptures</h1>
      <Image />
      <Image />
      <Image />
    </section>
  );
}

function Image() {
  return (
    <img
      src="https://i.imgur.com/ZF6s192.jpg"
      alt="'Floralis Genérica' by Eduardo Catalano: a gigantic metallic flower sculpture with reflective petals"
    />
  );
}
```

- During the initial render, React will create the DOM nodes for `<section>`, `<h1>`, and three `<img>` tags.
- During a re-render, React will calculate which of their properties, if any, have changed since the previous render. It won’t do anything with that information until the next step, the commit phase.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> NOTE

Rendering must always be a pure calculation:

- Same inputs, same output. Given the same inputs, a component should always return the same JSX. (When someone orders a salad with tomatoes, they should not receive a salad with onions!)
- It minds its own business. It should not change any objects or variables that existed before rendering. (One order should not change anyone else’s order.)

Otherwise, you can encounter confusing bugs and unpredictable behavior as your codebase grows in complexity. When developing in “Strict Mode”, React calls each component’s function twice, which can help surface mistakes caused by impure functions.

</aside>

## Step 3: React Commits Changes To The DOM

---

After rendering (calling) your components, React will modify the DOM.

- **For the initial render**, React will use the `appendChild()` DOM API to put all the DOM nodes it has created on screen.
- **For re-renders**, React will apply the minimal necessary operations (calculated while rendering!) to make the DOM match the latest rendering output.

```jsx
export default function Clock({ time }) {
  return (
    <>
      <h1>{time}</h1>
      <input />
    </>
  );
}
```

This works because during this last step, React only updates the content of `<h1>` with the new time. It sees that the `<input>` appears in the JSX in the same place as last time, so React doesn’t touch the `<input>`—or its value!

After rendering is done and React updates the DOM, the browser will repaint the screen. Although this process is known as “browser rendering”, we’ll refer to it as “painting” to avoid confusion throughout the docs.