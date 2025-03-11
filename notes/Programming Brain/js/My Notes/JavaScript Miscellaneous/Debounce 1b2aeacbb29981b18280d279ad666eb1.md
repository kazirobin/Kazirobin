# Debounce

In JavaScript, a debounce function makes sure that your code is only triggered once per user input. Search box suggestions, text-field auto-saves, and eliminating double-button clicks are all use cases for debounce.

---

## What is debounce?

The term **debounce** comes from electronics. When you’re pressing a button, let’s say on your TV remote, the signal travels to the microchip of the remote so quickly that before you manage to release the button, it bounces, and the microchip registers your “click” multiple times.

![debounce-button.png](Debounce%201b2aeacbb29981b18280d279ad666eb1/debounce-button.png)

To mitigate this, once a signal from the button is received, the microchip stops processing signals from the button for a few microseconds while it’s physically impossible for you to press it again.

## Debounce in JavaScript

In JavaScript, the use case is similar. We want to trigger a function, but only once per use case.

Let's say that we want to show suggestions for a search query, but only after a visitor has finished typing it.

Or we want to save changes on a form, but only when the user is not actively working on those changes, as every "save" costs us a database trip.

And my favorite—some people got really used to Windows 95 and now double click everything 😁.

```jsx
function debounce(func, timeout = 300){
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => { func.apply(this, args); }, timeout);
  };
}
function saveInput(){
  console.log('Saving data');
}
const processChange = debounce(() => saveInput());
```

It can be used on an input:

```jsx
<input type="text" onkeyup="processChange()" />
```

Or a button:

```jsx
<button onclick="processChange()">Click me</button>
```

Or a window event:

```jsx
window.addEventListener("scroll", processChange);
```

And on other elements like a simple JS function.

So what’s happening here? The `debounce` is a special function that handles two tasks:

- Allocating a scope for the *timer* variable
- Scheduling your function to be triggered at a specific time

Let’s explain how this works in the first use case with text input.

When a visitor writes the first letter and releases the key, the `debounce` first resets the timer with `clearTimeout(timer)`. At this point, the step is not necessary as there is nothing scheduled yet. Then it schedules the provided function—`saveInput()`—to be invoked in 300 ms.

But let's say that the visitor keeps writing, so each key release triggers the `debounce` again. Every invocation needs to reset the timer, or, in other words, cancel the previous plans with `saveInput()`, and reschedule it for a new time—300 ms in the future. This goes on as long as the visitor keeps hitting the keys under 300 ms.

The last schedule won’t get cleared, so the `saveInput()` will finally be called.