# Count Animation

This effect is commonly used for displaying numbers and statistics and is often used in countdown timers.

To implement this effect, we'll utilize `MotionValues` to monitor the state and velocity of the values, and we'll employ the `animate` function to specify the animation duration.

```css
import { motion, useMotionValue, animate } from "framer-motion";
```

We will pass it an initial state or value which will be 0. Then we will count up to 50. Keep in mind that you need to round the count to make sure no decimal points are shown. For this, `useTransform` will be used.

```jsx
import "./styles.css";
import { motion, useMotionValue, useTransform, animate } from "framer-motion";
import { useEffect } from "react";

export default function App() {
  const count = useMotionValue(0);
  const rounded = useTransform(count, Math.round);

  useEffect(() => {
    const animation = animate(count, 50, { duration: 2 });

    return animation.stop;
  }, []);

  return <motion.h1>{rounded}</motion.h1>;
}

```

In the code above, `animation.stop` is being used to stop the animation when the component is unmounted. This ensures that the animation is terminated, and any resources associated with the animation are released.

Style.css

```css
.App {
  font-family: sans-serif;
  text-align: center;
}

body {
  background-color: #b53bff;
  color: #fff;
  font-family: sofia-pro, sans-serif;
  font-weight: 400;
  font-style: normal;
  font-size: 40px;
}
```