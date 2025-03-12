# Scroll Animation

We’ll use a combination of the `useAnimation` hook and `react-intersection-observer` to create scroll-triggered animations.

## All Components

- `App.js`: we set up the animations for the `Box` component and render it in `App`
- `Styles.js`: create, style, and export the motion components. The components are styled using styled-components.

```jsx
import React, { useEffect } from "react";
import { useAnimation } from "framer-motion";
import { useInView } from "react-intersection-observer";
import { Container, H1,StyledBox } from "./Styles";

const BoxVariants = {
  visible: { opacity: 1, x: 0, transition: { duration: 1 } },
  hidden: { opacity: 0, x: 300 },
};

const Box = () => {
  const controls = useAnimation();
  const [ref, inView] = useInView();
  useEffect(() => {
    if (inView) {
      controls.start("visible");
    }
  }, [controls, inView]);
  return (
    <StyledBox
      ref={ref}
      animate={controls}
      initial="hidden"
      variants={BoxVariants}
    />
  );
};
```

The `useAnimation` hook allows us to control the sequences in which our animations occur. We have access to `controls.start` and `controls.stop` methods that we can use to manually start and stop our animations. We pass in the initial `hidden` animaton to `StyledBox`. We pass in the controls we defined with the `start` method to `StyledBox` animate prop.

`react-intersection-observer`’s `useInView` hook allows us to track when a component is visible in the viewport. The `useInView` hook gives us access to `ref`, which we pass to the component we want to watch, and the `inView` boolean, that tells us if that element is `inView` or not. We use the `useEffect` to call `controls.start` whenever the element we’re watching, `StyledBox` is in view. We pass in `controls` and `inView` as `useEffect`’s dependencies. Also, we pass in the variants we defined, `BoxVariants` to `StyledBox`.