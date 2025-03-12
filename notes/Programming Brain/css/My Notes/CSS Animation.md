# CSS Animation

As the name implies, CSS animation allows users to animate some CSS properties by following a declarative pattern where users can specify what changes in the CSS property over a period of time. CSS animations make it possible to animate transitions from one CSS style configuration to another.

## Styles describing CSS animations

For every animation you create, you must describe the characteristics of the animation. This gives you total control over deciding exactly what the animation can or cannot do. Some examples of properties you can configure include the duration, direction, and number of times the animation repeats.

To describe the animation, you can use either the `animation` shorthand property or the `animation` sub-properties.

### `Animation` shorthand property

The `animation` shorthand property is a shorthand for the eight `animation` sub-properties. It prevents you from wasting time typing the sub-property names and animates elements that require all eight sub-properties:

```css
/* Here’s the syntax of the animation shorthand property */
.element {
  animation: name duration timing-function delay iteration-count direction fill-mode play-state;
}
```

```css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.square {
  background-color: blue;
  height: 200px;
  width: 200px;
  animation: move 3s ease 1s infinite normal none running;
}

@keyframes move {
  0% {
    transform: translate(0, 0);
  }

  50% {
    transform: translate(150px, 0);
  }
}
```

### `Animation` sub-properties

The eight sub-properties make up the actual `animation` shorthand property and configure the element’s animation in CSS. It becomes useful when you don’t want to use all the sub-properties simultaneously or when you forget the order of arrangement in the animation property:

```css
/* Here’s the syntax of the animation sub-properties. */
.element {
  animation-name: name;
  animation-duration: duration;
  animation-timing-function: timing-function;
  animation-delay: delay;
  animation-iteration-count: count;
  animation-direction: direction;
  animation-fill-mode: fill-mode;
  animation-play-state: play-state;
}
```

```css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.square {
  background-color: yellow;
  height: 200px;
  width: 200px;
  animation-name: move;
  animation-duration: 1.5s;
  animation-timing-function: ease;
  animation-delay: 0s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  animation-fill-mode: none;
  animation-play-state: running;
}

@keyframes move {
  0% {
    transform: rotate(20deg);
  }

  50% {
    transform: rotate(40deg);
  }
}
```

**Note:** that you can’t use the `animation` shorthand property and the `animation` sub-properties together because they produce the same thing. They should be used individually based on what you are trying to achieve.

## Using `@keyframe` to indicate an animation sequence

Keyframes describe how an animated element renders at a given time during the animation sequence. Since the animation’s timing is defined in the CSS style using the `animation` shorthand property or its sub-properties, keyframes use a percentage to indicate the animation sequence.

```css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.heart {
  background-color: red;
  height: 100px;
  width: 100px;
  transform: rotate(-45deg);
  animation-name: heartbeat;
  animation-duration: 2s;
  animation-iteration-count: infinite;
}

.heart::before,
.heart::after {
  content: "";
  background-color: red;
  height: 100px;
  width: 100px;
  position: absolute;
  border-radius: 50%;
}

.heart::before {
  top: -50px;
  left: 0;
}

.heart::after {
  left: 50px;
  top: 0;
}
```

To use keyframes, create a `@keyframes` at-rule with the same name passed to the `animation-name` property. In the heartbeat demo, the `animation-name` is `heartbeat`, so you must name the `@keyframes` at-rule `heartbeat` as well.

Each `@keyframes` at-rule contains a style list of keyframe selectors, specifying percentages for the animation when the keyframe occurs, and a block containing the styles for that keyframe:

```css
@keyframes heartbeat {
  0% {
    transform: scale(1) rotate(-45deg);
  }
  20% {
    transform: scale(1.25) rotate(-45deg);
  }
  40% {
    transform: scale(1.5) rotate(-45deg);
  }
}
```

`0%` indicates the first moment of the animation sequence while `100%` indicates the final state of the animation.

Now that you understand `@keyframes`. As you can see, the heart is now beating!

When you added a CSS `@keyframes` at-rule to make the size of the heart scale from `0%` to `40%`, you set:

- 0% of the time to no transformation
- 20% of the time to scale the heart to 125% of its initial size through `scale(1.25)`
- 40% of the time to scale the heart 150% of its initial size through `scale(1.5)`

`rotate(-45deg)` was added to maintain the original direction of the heart you created with CSS.