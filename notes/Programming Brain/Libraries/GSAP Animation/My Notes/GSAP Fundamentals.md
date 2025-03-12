# GSAP Fundamentals

`CreateAt- 23 Nov 2024 / RevisedAt-` 

The **`gsap`** object serves as the access point for most of GSAP's functionality. It's just a generic object with various methods and properties that create and control **`Tweens`** and **`Timelines`**, two of the most important concepts to understand.

## What's a Tween?

A **Tween** is what does all the animation work - think of it like a **high-performance property setter**. You feed in targets (the objects you want to animate), a duration, and any properties you want it to animate and then when the Tween's playhead moves to a new position, figures out what the property values should be at that point applies them accordingly.

### Common methods for creating a Tween:

- gsap.to()
- gsap.from()
- gsap.fromTo()

For simple animations (no fancy sequencing), the methods above are all you need! For example:

```jsx
// target the element with a class of "green" - rotate and move TO 100px to the left over the course of 1 second. 
gsap.to(".green", {rotation: 360, x: 100, duration: 1});

// target the element with a class of "purple" - rotate and move FROM 100px to the left over the course of 1 second. 
gsap.from(".purple", {rotation: -360, x: -100, duration: 1});

// target the element with a class of "blue" - rotate and move FROM 100px to the left, TO 100px to the right over the course of 1 second. 
gsap.fromTo(".blue", {x: -100},{rotation: 360, x: 100, duration: 1});
```

You can do basic sequencing by using the **`delay`** special property, but Timelines make sequencing and complex choreography much, much easier.

## What's a Timeline?

A **Timeline** is a **container for Tweens.** It's the ultimate sequencing tool that lets you position animations in time wherever you want and then control the whole sequence easily with methods like `pause()`, `play()`, `progress()`, `reverse()`, `timeScale()`, etc.

Create as many Timelines as you want. You can even **nest them** which is fantastic for modularizing your animation code! Every animation (Tween and Timeline) gets placed onto a parent timeline (the **globalTimeline** by default). Moving a Timeline's playhead cascades down through its children so that the playheads stay aligned. A Timeline is purely about grouping things and coordinating time/playheads - it never actually sets properties on targets (Tweens handle that).

### Method for creating a Timeline:

- gsap.timeline()

GSAP's API lets you control virtually anything on-the-fly, such as the playhead position, the **startTime** of any child, even play/pause/reverse the timeline or alter the timeScale itself.

## Sequencing things in a Timeline

First, create a Timeline:

```jsx
var tl = gsap.timeline();
```

Then add a tween using one of the convenience methods - `to()`, `from()`, or `fromTo()`:

```jsx
tl.to(".box", { duration: 2, x: 100, opacity: 0.5 });
```

Do that as many times as you want. Notice we're calling **`.to()`** **on the timeline instance** (the variable **`tl`** in this case), not the **`gsap`** object. This creates a tween and immediately puts it into that particular Timeline. **`gsap.to()`**, on the other hand, creates a standalone tween. By default, the animations will be sequenced one-after-the-other. You can even use method chaining to simplify your code like this:

```jsx
//sequenced one-after-the-other
tl.to(".box1", { duration: 2, x: 100 }) //notice that there's no semicolon!
  .to(".box2", { duration: 1, y: 200 })
  .to(".box3", { duration: 3, rotation: 360 });
```

**Note:** The whole GSAP platform is object-oriented and you could create individual tween instances with `gsap.to()`, for example, and then `timeline.add()` each one but it's just easier to call `.to()`, `.from()`, or `.fromTo()` directly on the Timeline instance to do the same thing in fewer steps.

## Control placement with the position parameter

Define **exactly** where you want your animations to be placed into the timeline by using the optional position parameter. A number indicates an absolute time (in seconds), or a string with a **`"+="`** or **`"-="`** prefix indicates an offset relative to the END of the timeline. For example, **`"+=2"`** would be 2 seconds after the end, creating a 2-second gap. **`"-=2"`** would create a 2-second overlap.

```jsx
//starts at EXACTLY 1.5 seconds from the start of the Timeline:
tl.to(..., 1.5)
  .to(..., "-=0.75") //overlaps by 0.75 seconds
  .to(..., "+=1") //adds a 1-second gap before
```

## Labels

Use labels to mark certain spots on the timeline so that you can place animations there or navigate there during playback.

```jsx
//add a label at exactly 3 seconds
tl.addLabel("step2", 3)
  .to(..., "step2") //starts at the step2 label
  .to(..., "step2+=0.75") //0.75 seconds after the step2 label

//then later, we can seek() to that spot:
tl.seek("step2");
```

## Controlling Tweens and Timelines

**Tween** and **Timeline** both extend an Animation class that exposes a myriad of useful methods and properties. Here are some of the most frequently used:

- pause()
- play())
- progress()
- restart()
- resume()
- reverse()
- seek()
- time()
- duration()
- **ti**meScale()
- kill()

You can reference the Tween or Timeline instance with a variable, and then control it whenever you want:

```jsx
//you only need to create a variable if you want to control it later...
var tween = gsap.to(...);
var tl = gsap.timeline(); //"tl" short for timeline
tl.to(...).to(...); //add animations.

//now we can control them...
tween.pause();
tween.timeScale(2); //double speed
tl.seek(3); //jump to 3 seconds in
tl.progress(0.5); //halfway through
...
```