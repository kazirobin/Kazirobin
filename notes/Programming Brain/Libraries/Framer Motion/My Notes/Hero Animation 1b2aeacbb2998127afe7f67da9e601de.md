# Hero Animation

We’ll build a cool hero banner animation using the `useCycle` hook. We’ll understand how `useCycle` allows us to cycle through animations.

```jsx
import React, { useEffect } from "react";
import { useCycle } from "framer-motion";
import { Container, H1, HeroSection, Banner, TextBox } from "./Styles";
import { ReactComponent as BannerIllustration } from "./bighead.svg";

const H1Variants = {
  initial: { y: -200, opacity: 0 },
  animate: { y: 0, opacity: 1, transition: { delay: 1 } },
};
const TextVariants = {
  initial: { x: 400 },
  animate: { x: 0, transition: { duration: 0.5 } },
};
const BannerVariants = {
  animationOne: { x: -250, opacity: 1, transition: { duration: 0.5 } },
  animationTwo: {
    y: [0, -20],
    opacity: 1,
    transition: { yoyo: Infinity, ease: "easeIn" },
  },
};
```

We define 3 variants, `H1Variants`, `TextVariants`, and `BannerVariants`. However, our focus is `BannerVariants`. We define 2 animations, `animationOne` and `animationTwo` in `BannerVariants`. These are the animations we pass into the `useCycle` to cycle through.

```jsx
const [animation, cycleAnimation] = useCycle("animationOne", "animationTwo");
  useEffect(() => {
    setTimeout(() => {
      cycleAnimation();
    }, 2000);
  }, []);
```

`useCycle` works similar to the `useState` hook. In the destructured array, `animation` represents the animation that is active, whether `animationOne` or `animationTwo`. The `cylceAnimation` function that cycles between the animation we defined. We pass in the animations we want to cycle through into `useCycle` and call `cylceAnimation` after 2 seconds in `useEffect`.

```jsx
<div className="App">
      <Container>
        <H1 variants={H1Variants} initial="initial" animate="animate">
          Cool Hero Section Anmiation
        </H1>
        <HeroSection>
          <TextBox variants={TextVariants} initial="initial" animate="animate">
            Storage shed, troughs feed bale manure, is garden wheat oats at
            augers. Bulls at rose garden cucumbers mice sunflower wheat in pig.
            Chainsaw foal hay hook, herbs at combine harvester, children is
            mallet. Goat goose hen horse. Pick up truck livestock, pets and
            storage shed, troughs feed bale manure, is garden wheat oats at
            augers. Lamb.
          </TextBox>
          <Banner variants={BannerVariants} animate={animation}>
            <BannerIllustration />
          </Banner>
        </HeroSection>
      </Container>
    </div>
```

At the end of everything, we pass in the variants to their respective components and watch the magic happen. With this, the `Banner` will initially slide in from the right based on the animations we defined in `animationOne`, and after 2 seconds, `cycleAnimation` will be called which will trigger `animationTwo`.