# Introducing Framer Motion

Animations, when done right, are powerful. However, creating eye-catching animations with CSS can be tricky. In comes Framer Motion. With Framer Motion, you don’t need to be a CSS expert to make beautiful animations. Framer Motion provides us with production-ready animations and a low-level API we can interact with to integrate these animations into our applications.

## What Is Framer Motion?

Framer Motion is an animation library that makes creating animations easy. Its simplified API helps us abstract the complexities behind animations and allows us to create animations with ease.

## Motion Components

These are the building blocks of Framer motion. Motion components are created by prefixing `motion` to your regular HTML and SVG element (e.g, `motion.h1`). Motion components can accept several props, with the basic one being the `animate` prop. This prop takes in an object where we define the properties of that component we want to animate. The properties we define will be animated when the component mounts in the DOM.

Let’s animate an h1 text using Framer Motion. First, we install the framer-motion library and import `motion`.

```jsx
npm i framer-motion
import { motion } from 'framer-motion';
```

Then we convert the h1 into a motion component.

```jsx
<motion.h1 
  animate={{x: 20, y: -20}}>
  This is a motion component
</motion.h1>
```

This will cause the `h1` to slide 20px to the right and move 20px up when it loads. When units aren’t added, calculations are done using pixels. However, you can explicitly set the units you want the calculations to be based on, `animate={{x: "20rem", y: "-20rem"}}>`.

By default, a motion component will be animated from the state defined from its styles to those in the `animate` prop. However, if we wanted to, we could hijack and define the initial animation state of the component using the `initial` prop. While the `animate` prop is used to define the behavior of components when they mount, the `initial` prop defines their behavior before they mount.

If we want our h1 to come in from the left, we control that using the initial prop.

```jsx
<motion.h1
    initial={{x: -1000}}
    animate={{x: 20}}>
   This is a motion component
</motion.h1>
```

Now, when the `h1` mounts, it slides in from the left.
We are not limited to a single animation. We can define a series of animations called `keyframes` in an array of values. Each value will get animated in sequence.

```jsx
<motion.h1
    initial={{x: -1000}}
    animate={{x: [20, 50, 0, -70, 40] }}>
   This is a motion component
</motion.h1>
```

The `transition` prop allows us to define how the animations occur. With it, we define how values animate from one state to another. Among other things, we can define the `duration`, `delay`, and `type` of animation using this prop.

```jsx
<motion.h1
    initial={{ x: -1000 }}
    animate={{ x: 0 }}
    transition={{
        type: "tween",
        duration: "2",
        delay: "1"
    }}>
    This is a motion component
</motion.h1>
```

Say we were to animate several motion components simultaneously, like in the code snippet below.

While this works, the `variants` prop in Framer Motion enables us to extract our animation definitions into a variants object. Not only do `variants` make our code cleaner, but they allow us to create even more powerful and complex animations.

Extracting our animation definitions into variants objects, we have this:

```jsx
const H1Variants = {
  initial: { x: -1000 },
  animate: { x: 0 },
  transition: {
    type: "tween",
    duration: 2,
    delay: 1
  }
} 
const H2Variants = {
  initial: { y: -1000 },
  animate: { y: 0 },
  transition: {
    type: "tween",
    duration: 1,
    delay: .4
  }
}
const H3Variants = {
  initial:{ x: 100, opacity: 0 },
  animate:{ x: 0, opacity: 1 }
}
const H4Variants = {
  initial:{ scale: 0.7 },
  animate:{ scale: 1.7 },
  transition:{
    type: "tween",
    duration: "2",
    delay: "1"
  }
}
```

Instead of passing the animation definitions into a component’s `initial` and `animate` props directly, we extract these definitions into standalone variant objects. In the variant objects, we define variant names that describe each animation’s name as variants.

```jsx
<div className="App">
      <motion.h1
      variants={H1Variants}
      initial='initial'
      animate='animate'
      >
        This is a motion h1
      </motion.h1>
      <motion.h2  
        variants={H2Variants}
        initial='initial'
        animate='animate'
       >
        This is a motion h2
      </motion.h2>
      <motion.h3
        variants={H3Variants}
        initial='initial'
        animate='animate'
       >
         This is a motion h3
      </motion.h3>
      <motion.h4
        variants={H4Variants}
        initial='initial'
        animate='animate'
       >
         This is a motion h4
      </motion.h4>
</div>
```

In the `variants` prop, we pass in the name of the variant objects for each motion component and then pass in the animations to the `initial` and `animate` props.

We can take our current setup with variants further to reduce repetition. Using variants, we can propagate animation attributes down through the DOM from a parent motion component. For this to work, we create variants for the parent `motion.div` with similar animation names in its variant object as its children. By doing this, we won’t have to pass the animation names’ to each child component. Behind the scenes, the parent element handles that for us.

```jsx
const ContainerVariants = {
  initial: {},
  animate: {}
};
const H1Variants = {
  initial: { x: -1000 },
  animate: { x: 0 },
  transition: {
    type: "tween",
    duration: 2,
    delay: 1
  }
};
//more variants below

<motion.div
      className="App"
      variants={ContainerVariants}
      initial="initial"
      animate="animate"
    >
      <motion.h1 variants={H1Variants}>This is a motion h1</motion.h1>
      <motion.h2 variants={H2Variants}>This is a motion h2</motion.h2>
      <motion.h3 variants={H3Variants}>This is a motion h3</motion.h3>
      <motion.h4 variants={H4Variants}>This is a motion h4</motion.h4>
</motion.div>
```

Now we have a cleaner code with no repetitions. We turned the container div to a motion component so we could pass in the `ContainerVariants` object we defined. Since we don’t define any animations on the container, we pass in empty objects to `initial` and `animate`. Your animation names must be the same in every variant object for the propagation to work.