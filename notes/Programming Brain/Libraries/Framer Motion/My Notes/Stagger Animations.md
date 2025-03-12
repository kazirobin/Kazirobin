# Stagger Animations

Stagger animations, as demonstrated in dropdowns and navigation menus, involve animating elements in a sequential manner, each appearing one after the other, with a subtle delay distinguishing their appearances. You can create much more complex effects using this method as opposed to the ones mentioned above.

In this example, we will animate in some menu items when a menu button is clicked. We will use the `stagger` function alongside `motion` and `useAnimate`. 

```jsx
import { useAnimate, stagger, motion } from "framer-motion";
```

Start by creating an array that holds the list of items to be displayed in the menu. To achieve this effect, the list items are initially mapped within a `<ul>` element. When the button is clicked, the `<ul>` is first made visible. Then, the list items will animate in a staggered fashion one by one.

We will utilize the `useAnimate` hook to generate the animations for both the `<ul>` and `<li>` elements. These animations will be triggered by a change in state, which can be toggled using the button.

```jsx
import "./styles.css";
import { useState, useEffect } from "react";
import { useAnimate, stagger, motion } from "framer-motion";

export default function App() {
  const [open, setOpen] = useState(false);
  const [scope, animate] = useAnimate();
  const items = ["Item 1", "Item 2", "Item 3", "Item 4"];

  // the stagger effect
  const staggerList = stagger(0.1, { startDelay: 0.25 });

  // create the animations that will be applied
  // whenever the open state is toggled

  useEffect(() => {
    animate(
      "ul",
      {
        width: open ? 150 : 0,
        height: open ? 200 : 0,
        opacity: open ? 1 : 0
      },
      {
        type: "spring",
        bounce: 0,
        duration: 0.4
      }
    );
    animate(
      "li",
      open
        ? { opacity: 1, scale: 1, x: 0 }
        : { opacity: 0, scale: 0.3, x: -50 },
      {
        duration: 0.2,
        delay: open ? staggerList : 0
      }
    );
  }, [open]);

  return (
    <div className="App" ref={scope}>
      <motion.button onClick={() => setOpen(!open)} whileTap={{ scale: 0.95 }}>
        Menu
      </motion.button>
      <ul>
        {items.map((item, index) => (
          <motion.li key={index}>{item}</motion.li>
        ))}
      </ul>
    </div>
  );
}

```

Style.css

```css
.App {
  font-family: sans-serif;
}

button {
  padding: 12px 20px;
  font-family: sofia-pro, sans-serif;
  font-weight: 400;
  font-style: normal;
  font-size: 16px;
  color: #fff;
  border: none;
  background-color: #752596;
  cursor: pointer;
  border-radius: 8px;
  width: 160px;
}

ul {
  padding: 10px 10px 10px 0px;
  background-color: #752596;
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 0px;
  height: 0px;
  border-radius: 8px;
  align-items: center;
  opacity: 0;
}

li {
  list-style: none;
  margin: 0;
  padding: 10px 0;
  font-family: sofia-pro, sans-serif;
  font-weight: 400;
  font-style: normal;
  font-size: 17px;
  color: #fff;
}
```