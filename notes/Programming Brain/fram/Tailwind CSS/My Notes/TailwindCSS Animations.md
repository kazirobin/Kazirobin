# TailwindCSS Animations

Tailwind CSS is a utility-first CSS framework that has shown tremendous growth in its adoption, making it a popular choice for all your styling needs. While it allows you to build modern websites without writing a single line of CSS, styling a website is only part of providing a positive user experience.

Crafting meaningful interactions via animations plays an important role in capturing the visitor’s attention, too, and they can take your website to the next level. In this post, you’ll learn how to use CSS animations with Tailwind CSS, explore the built-in animations it comes with, and create custom animations for that extra flair.

## Using built-in CSS animations with Tailwind CSS

CSS animations is a CSS module that lets you animate the values of CSS properties through keyframes. The nature of these keyframe animations can be altered by tweaking its properties such as duration, easing function, direction, delay, and more.

Just like other CSS properties and modules, Tailwind CSS also ships with some utility classes for CSS animations. By default, it comes with four basic animations: spin, pulse, ping, and bounce.
These utility classes are prefixed by the animate keyword, such as animate-spin or animate-pulse. Let’s take the animate-spin utility as an example.

This utility class is used to add a linear and infinite spin animation to your HTML elements. This is especially useful for loading indicators, such as the ones that you might find on a button in forms.

Here’s a code snippet that shows you how to add an infinite spinning animation to an SVG. You can toggle this utility class depending upon the state of your app:

```html
<button type="button" class="bg-indigo-500 ..." disabled>
  <svg class="animate-spin h-5 w-5 mr-3 ..." viewBox="0 0 24 24">
    <!-- ... -->
  </svg>
  Loading...
</button>
```

Using animation in such cases helps the user understand that their action has been acknowledged and the appropriate response is being triggered. Besides functionality, animations can also be used just for aesthetics.

To check out the other built-in animations in action, I recommend you to check out the official Tailwind CSS documentation. Using built-in CSS for animations is ideal for projects that already have a dedicated stylesheet linked to the markup and do not require Tailwind CSS as a dependency.

## Creating custom animations in Tailwind CSS

While the four built-in CSS animations might be sufficient for some general use cases, you might not want to be restricted to only these. Animations are highly project-specific, and perhaps you want to use custom animations instead.

Thankfully, there’s no need to create a new stylesheet and link it to your markup just to add a new animation to your app. Instead, define the keyframes of your animation and extend the theme configuration to create a new animation:

![Custom-waving-hand-animation-Tailwind-CSS.gif](TailwindCSS%20Animations%201b2aeacbb2998166947ce684fb66bc6d/Custom-waving-hand-animation-Tailwind-CSS.gif)

Let’s assume we want to create a custom waving hand animation like the one above and use it with Tailwind CSS. Here’s how.

## Adding `@keyframes` to a Tailwind CSS config file

First, we must define a keyframes rule for the animation. The `@keyframes` CSS at-rule is used to define the value of CSS properties of an element during the initial, intermediate and final waypoints of the animation. Through this, you can have multiple different styles at different stages of the animation.

Open up the `tailwind.config.js` file inside the root of your project directory and create an empty `keyframes` object inside `theme.extend`. Now, inside this `keyframes` object, let’s add our new wave animation and define its behavior.

```jsx
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      keyframes: {
        wave: {
          '0%': { transform: 'rotate(0.0deg)' },
          '10%': { transform: 'rotate(14deg)' },
          '20%': { transform: 'rotate(-8deg)' },
          '30%': { transform: 'rotate(14deg)' },
          '40%': { transform: 'rotate(-4deg)' },
          '50%': { transform: 'rotate(10.0deg)' },
          '60%': { transform: 'rotate(0.0deg)' },
          '100%': { transform: 'rotate(0.0deg)' },
        },
      },
    },
  },
  plugins: [],
}
```

The `content` array in your Tailwind CSS config file might look different for you depending on the frontend framework or library you’re using, if any. But the main thing to focus on in the above snippet is the `keyframes` object.

## Extending the theme in Tailwind CSS

Now that we’ve added the keyframes rule to our theme object inside `tailwind.config.js`, let’s add our custom animation that uses this rule. We can customize the animation duration, delay, iterations, timing function, and more.

Let’s assume that we want the animation to transition for two seconds linearly in each cycle and keep animating infinitely. Here’s how the CSS animation shorthand property should look:

```jsx
animation: wave 2s linear infinite;
```

`Wave` is the name of the keyframes rule we defined earlier. `2s` is used to denote that this animation should transition for two seconds in one cycle, and `linear` is used to denote that we want the easing function to be linear, and `infinite` will keep it animating perpetually.

Let’s add this animation inside `tailwind.config.js` in the `theme.extend.animation` object:

```jsx
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      keyframes: {
        wave: {
          '0%': { transform: 'rotate(0.0deg)' },
          '10%': { transform: 'rotate(14deg)' },
          '20%': { transform: 'rotate(-8deg)' },
          '30%': { transform: 'rotate(14deg)' },
          '40%': { transform: 'rotate(-4deg)' },
          '50%': { transform: 'rotate(10.0deg)' },
          '60%': { transform: 'rotate(0.0deg)' },
          '100%': { transform: 'rotate(0.0deg)' },
        },
      },
      animation: {
        'waving-hand': 'wave 2s linear infinite',
      },
    },
  },
  plugins: [],
}
```

Utility classes are generated based on the keys of the `animation` object. Because we’ve used `waving-hand` as the key for this animation, we need to add `animate-waving-hand` to the element we want to animate in our markup, like this:

```jsx
<h1 class="flex font-semibold text-purple-600">
  Hello <span class="animate-waving-hand">👋🏻</span>, Hossain
</h1>
```

You’ve successfully created your custom animation for your Tailwind CSS app. To add more animations, you can follow the same steps: add the keyframes to `theme.extend.keyframes` object, then add the animation to `theme.extend.animation`.

## Smoother Tailwind animations with transition utilities

Tailwind CSS provides a set of utility classes to handle transitions in your UI elements. These utilities let you control the transition properties such as duration, timing function, delay, and the properties being animated giving a smooth transition from different states.

Here’s an overview and examples of how to use Tailwind’s transition utilities.

## Basic `transition` class

The `transition` class is used to enable transitions on an element. By default, it applies a transition to all properties:

```html
<div class="transition bg-blue-500 hover:bg-blue-700 p-4">
  Hover me
</div>
```

Tailwind provides utility classes to specify which properties should transition. For example:

- `transition-colors` – Transitions color-related properties
- `transition-opacity` – Transitions opacity
- `transition-transform` – Transitions transform properties

You can use these utility classes like so:

```html
<div class="transition-transform transform scale-100 hover:scale-110 bg-green-500 p-4">
  Hover me to scale
</div>
```

## Transition `duration` class

You can control the duration of transitions in Tailwind with the `duration-{time}` class, where `{time}` is a value in milliseconds:

- `duration-75` – 75ms
- `duration-100` – 100ms
- `duration-150` – 150ms

For example:

```html
<div class="transition-transform duration-300 transform scale-100 hover:scale-110 bg-blue-500 p-4">
  Hover me for a 300ms scale transition
</div>
```

## Transition timing function with `ease`

Specify the timing function of the transition with the `ease-{type}` class, where `{type}` can be:

- `ease-linear`
- `ease-in`
- `ease-out`
- `ease-in-out`

For example, with this `ease-in-out` timing function that combines the `ease-in` and `ease-out` functions, our transition animation starts slowly, speeds up in the middle, and slows down again at the end for a fluid visual effect:

```html
<div class="transition-transform duration-500 ease-in-out transform scale-100 hover:scale-110 bg-yellow-500 p-4">
  Smooth transition with ease-in-out
</div>
```

## Transition `delay` class

Control when the transition starts with the `delay-{time}` class, where `{time}` is in milliseconds:

- `delay-75` – 75ms
- `delay-100` – 100ms

Here, we add a delay of 150 milliseconds to our animation:

```html
<div class="transition-opacity duration-300 delay-150 opacity-100 hover:opacity-50 bg-red-500 p-4">
  Transition opacity with delay
</div>
```

## Combining Tailwind transition utilities

You can combine various transition utilities to create more complex effects. For instance, you might want to apply a transition to multiple properties with a specific duration, easing function, and delay:

```html
<div class="transition-transform transition-opacity duration-500 ease-in-out delay-200 transform scale-100 opacity-100 hover:scale-110 hover:opacity-50 bg-purple-500 p-4">
  Hover to scale and fade
</div>
```

## Responsive and state variants

You can also apply transition utilities responsively or based on different states like `hover`, `focus`, or `active`:

```html
<div class="transition-all duration-300 ease-in-out hover:bg-pink-500 hover:text-white p-4">
  Hover me to change background and text color
</div>
```

## Understanding Tailwind’s JIT (Just-in-Time) engine

Browsers start to behave funny when your website’s CSS becomes too large, somewhere around 10 MB in size. You may start to notice some performance drawbacks, especially when using devtools in development.

With Tailwind CSS, the file size after installation can reach up to 3 MB. But as you configure and customize Tailwind further, the file can balloon to 15 MB or more.

Tailwind purges all unused styles in production, so the stylesheet is smaller. However, in development scenarios when your stylesheet is as big as 10 to 20 MB, you’re bound to run into problems.

As we incorporate a significant number of custom CSS animations into Tailwind, the stylesheet size will inevitably increase, which may lead to slower development and testing experiences. To address this, we can use Tailwind’s JIT engine to load only the CSS that we need in our app.

## Enabling JIT mode

To enable just-in-time mode, set the `mode` option to `'jit'` in your `tailwind.config.js` file:

```jsx
  // tailwind.config.js
  module.exports = {
+   mode: 'jit',
    purge: [
      // ...
    ],
    theme: {
      // ...
    }
    // ...
  }
```

Make sure to configure the purge option in your `tailwind.config.js` file with all relevant template paths. Since JIT mode generates CSS on demand by scanning your template files, this config is crucial; otherwise, you may end up with an empty CSS output:

```jsx
  // tailwind.config.js
  module.exports = {
    mode: 'jit',
+   //Customize these paths to match your project structure
+   purge: [
+     './public/**/*.html',
+     './src/**/*.{js,jsx,ts,tsx,vue}',
+   ],
    theme: {
      // ...
    }
    // ...
  }
```

Now Tailwind will generate styles on demand rather than pre-generating them all at once.