# Timeline

`CreatedAt- 24 Nov 2024 / RevisedAt-` 

A Timeline is a powerful sequencing tool that acts as a container for tweens and other timelines, making it simple to control them as a whole and precisely manage their timing. Without Timelines, building complex sequences would be far more cumbersome because you'd need to use a `delay` for every animation. For example:

```jsx
// WITHOUT Timelines (only using tweens with delays):
gsap.to("#id", { x: 100, duration: 1 });
gsap.to("#id", { y: 50, duration: 1, delay: 1 }); //wait 1 second
gsap.to("#id", { opacity: 0, duration: 1, delay: 2 }); //wait 2 seconds
```

What if you wanted to make the first animation longer? You'd need to adjust *every* delay thereafter. And what if you want to **`pause()`** the whole sequence or **`restart()`** it or **`reverse()`** it on-the-fly or repeat it twice? This could become quite messy, but GSAP's Timelines make it incredibly simple:

```jsx
//WITH Timelines (cleaner, more versatile)
var tl = gsap.timeline({repeat: 2, repeatDelay: 1});
tl.to("#id", {x: 100, duration: 1});
tl.to("#id", {y: 50, duration: 1});
tl.to("#id", {opacity: 0, duration: 1});

// then we can control the whole thing easily...
tl.pause();
tl.resume();
tl.seek(1.5);
tl.reverse();
...
```

Now we can adjust the timing without worrying about trickle-down changes to delays! Increase the duration of that first tween and everything automatically adjusts.

## Positioning animations in a timeline

By default, animations are added to the **end** of the timeline so that they're sequenced one-after-the-other but you can use the **position parameter** to control precisely where things are placed. It typically comes after the **vars** parameter and it uses a flexible syntax with the following options:

**Absolute time** (in seconds) measured from the start of the timeline, as a **number** like **`3`**

```jsx
// insert exactly 3 seconds from the start of the timeline
tl.to(".class", { x: 100 }, 3);
```

**Label**, like **`"someLabel"`**. If the label doesn't exist, it'll be added to the end of the timeline.

```jsx
// insert at the "someLabel" label
tl.to(".class", { x: 100 }, "someLabel");
```

**`"<"`** The **start** of previous animation**. Think of **`<`** as a pointer back to the start of the previous animation

```jsx
// insert at the START of the  previous animation
tl.to(".class", { x: 100 }, "<");
```

**`">"`** - The **end** of the previous animation**. Think of **`>`** as a pointer to the end of the previous animation.

```jsx
// insert at the END of the previous animation
tl.to(".class", { x: 100 }, ">");
```

A complex string where **`"+="`** and **`"-="`** prefixes indicate **relative** values. *When a number follows **`"<"`** or **`">"`**, it is interpreted as relative so **`"<2"`** is the same as **`"<+=2"`**.* Examples:

- **`"+=1"`** - 1 second past the end of the timeline (creates a gap)
- **`"-=1"`** - 1 second before the end of the timeline (overlaps)
- **`"myLabel+=2"`** - 2 seconds past the label **`"myLabel"`**
- **`"<+=3"`** - 3 seconds past the start of the previous animation
- **`"<3"`** - same as **`"<+=3"`** (see above) (**`"+="`** is implied when following **`"<"`** or **`">"`**)
- **`">-0.5"`** - 0.5 seconds before the end of the previous animation. It's like saying *"the end of the previous animation plus -0.5"*

A complex string based on a **percentage**. When immediately following a **`"+="`** or **`"-="`** prefix, the percentage is based on **total duration** of the **animation being inserted**. When immediately following **`"<"`** or **`">"`**, it's based on the **total duration** of the **previous animation**. *Note: total duration includes repeats/yoyos*. Examples:

- **`"-=25%"`** - overlap with the end of the timeline by 25% of the inserting animation's total duration
- **`"+=50%"`** - beyond the end of the timeline by 50% of the inserting animation's total duration, creating a gap
- **`"<25%"`** - 25% into the previous animation (from its start). Same as **`">-75%"`** which is negative 75% from the **end** of the previous animation.
- **`"<+=25%"`** - 25% of the inserting animation's total duration past the start of the previous animation. Different than **`"<25%"`** whose percentage is based on the **previous animation's** total duration whereas anything immediately following **`"+="`** or **`"-="`** is based on the **inserting animation's** total duration.
- **`"myLabel+=30%"`** - 30% of the inserting animation's total duration past the label **`"myLabel"`**.

## Special Properties and Callbacks

Add any of these to your vars object to give your animation special powers