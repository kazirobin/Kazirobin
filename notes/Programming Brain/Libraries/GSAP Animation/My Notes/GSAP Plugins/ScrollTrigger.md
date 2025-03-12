# ScrollTrigger

`CreatedAt- 24 Nov 2024 / RevisedAt-` 

GSAP (GreenSock Animation Platform) is a powerful and flexible JavaScript library used for creating animations and interactive elements on web pages. One of its most popular plugins is **ScrollTrigger**, which allows you to create animations that are tied to the scroll position of a webpage. This makes it easy to animate elements as the user scrolls, creating engaging and dynamic experiences.

## GSAP ScrollTrigger Plugin Features

- **Scroll-based Animation**: Trigger animations based on scroll position, either by scrolling a specific distance or reaching certain elements.
- **Pinning**: Pin elements during scrolling, so they stay in place while the user scrolls past them.
- **Scrubbing**: Link animations to the scroll position, so they move in sync with the user's scrolling.
- **Triggers**: Start animations when an element comes into view or when a specific scroll position is reached.
- **Performance Optimized**: ScrollTrigger is highly optimized for performance, with minimal impact on scrolling speed or responsiveness.

## Useful ScrollTrigger Properties

- **`trigger`**: The element that triggers the scroll-based animation (usually a DOM element). For example, `trigger: ".my-element"` targets an element with the class `.my-element`.
- **`start` and `end`**: Define the scroll position relative to the trigger element where the animation starts and ends. You can specify values like `"top top"`, `"bottom center"`, or `"top bottom"`, etc.
    - **start**: Defines when the animation should start based on the scroll position of the `trigger` element and the viewport.
    - **end**: Defines when the animation should stop.
- **`scrub`**: Makes the animation progress smoothly with the scroll. It can be a boolean (`true` or `false`) or a number (the higher the number, the smoother it is). Setting it to `true` syncs the animation directly with the scroll.
- **`pin`**: Pins the target element in place while the scroll position is within the `start` and `end` points. This is useful for sticky elements or headers.
- **`markers`**: Used for debugging. It shows markers in the viewport that indicate when the animation starts and ends.
- **`onEnter`, `onLeave`, `onUpdate`**: These are callback functions that are called during specific points in the scroll trigger’s lifecycle. `onEnter` is triggered when the scroll position enters the trigger zone, `onLeave` when it leaves, and `onUpdate` when the trigger updates (e.g., scroll position changes).

You can trigger animations based on the scroll position using `scrollTrigger` options.

```jsx
gsap.to('.box', {
    scrollTrigger: '.box', // start animation when ".box" enters the viewport
    x: 500
});
```

## Useful ScrollTrigger Properties & Methods

[**Properties**](ScrollTrigger%201b2aeacbb29981358b19e468303a2714/Properties%201b2aeacbb29981af9b59f43252754552.md)

[**Methods**](ScrollTrigger%201b2aeacbb29981358b19e468303a2714/Methods%201b2aeacbb29981b1b0a0df562c2792f6.md)