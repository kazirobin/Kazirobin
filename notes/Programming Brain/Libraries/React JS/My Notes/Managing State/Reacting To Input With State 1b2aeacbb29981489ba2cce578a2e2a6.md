# Reacting To Input With State

`CreatedAt- 21 Jan 2024 / RevisedAt-`

React provides a declarative way to manipulate the UI. Instead of manipulating individual pieces of the UI directly, you describe the different states that your component can be in, and switch between them in response to the user input. This is similar to how designers think about the UI.

---

## How declarative UI compares to imperative

When you design UI interactions, you probably think about how the UI changes in response to user actions. Consider a form that lets the user submit an answer:

- When you type something into the form, the “Submit” button **becomes enabled.**
- When you press “Submit”, both the form and the button **become disabled,** and a spinner **appears.**
- If the network request succeeds, the form **gets hidden,** and the “Thank you” message **appears.**
- If the network request fails, an error message **appears,** and the form **becomes enabled** again.

In **imperative programming,** the above corresponds directly to how you implement interaction. You have to write the exact instructions to manipulate the UI depending on what just happened. Here’s another way to think about this: imagine riding next to someone in a car and telling them turn by turn where to go.

![i_imperative-ui-programming.png](Reacting%20To%20Input%20With%20State%201b2aeacbb29981489ba2cce578a2e2a6/i_imperative-ui-programming.png)

They don’t know where you want to go, they just follow your commands. (And if you get the directions wrong, you end up in the wrong place!) It’s called *imperative* because you have to “command” each element, from the spinner to the button, telling the computer *how* to update the UI.

In this example of imperative UI programming, the form is built *without* React. It only uses the browser DOM:

create a file named **index.js**

```jsx
async function handleFormSubmit(e) {
  e.preventDefault();
  disable(textarea);
  disable(button);
  show(loadingMessage);
  hide(errorMessage);
  try {
    await submitForm(textarea.value);
    show(successMessage);
    hide(form);
  } catch (err) {
    show(errorMessage);
    errorMessage.textContent = err.message;
  } finally {
    hide(loadingMessage);
    enable(textarea);
    enable(button);
  }
}

function handleTextareaChange() {
  if (textarea.value.length === 0) {
    disable(button);
  } else {
    enable(button);
  }
}

function hide(el) {
  el.style.display = 'none';
}

function show(el) {
  el.style.display = '';
}

function enable(el) {
  el.disabled = false;
}

function disable(el) {
  el.disabled = true;
}

function submitForm(answer) {
  // Pretend it's hitting the network.
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (answer.toLowerCase() === 'istanbul') {
        resolve();
      } else {
        reject(new Error('Good guess but a wrong answer. Try again!'));
      }
    }, 1500);
  });
}

let form = document.getElementById('form');
let textarea = document.getElementById('textarea');
let button = document.getElementById('button');
let loadingMessage = document.getElementById('loading');
let errorMessage = document.getElementById('error');
let successMessage = document.getElementById('success');
form.onsubmit = handleFormSubmit;
textarea.oninput = handleTextareaChange;
```

create a file named **index.html**

```html
<form id="form">
  <h2>City quiz</h2>
  <p>
    What city is located on two continents?
  </p>
  <textarea id="textarea"></textarea>
  <br />
  <button id="button" disabled>Submit</button>
  <p id="loading" style="display: none">Loading...</p>
  <p id="error" style="display: none; color: red;"></p>
</form>
<h1 id="success" style="display: none">That's right!</h1>

<style>
* { box-sizing: border-box; }
body { font-family: sans-serif; margin: 20px; padding: 0; }
</style>
```

Manipulating the UI imperatively works well enough for isolated examples, but it gets exponentially more difficult to manage in more complex systems. Imagine updating a page full of different forms like this one. Adding a new UI element or a new interaction would require carefully checking all existing code to make sure you haven’t introduced a bug (for example, forgetting to show or hide something).

React was built to solve this problem.

In React, you don’t directly manipulate the UI—meaning you don’t enable, disable, show, or hide components directly. Instead, you **declare what you want to show,** and React figures out how to update the UI. Think of getting into a taxi and telling the driver where you want to go instead of telling them exactly where to turn. It’s the driver’s job to get you there, and they might even know some shortcuts you haven’t considered!

![i_declarative-ui-programming.png](Reacting%20To%20Input%20With%20State%201b2aeacbb29981489ba2cce578a2e2a6/i_declarative-ui-programming.png)

## Thinking about UI declaratively

You’ve seen how to implement a form imperatively above. To better understand how to think in React, you’ll walk through reimplementing this UI in React below:

1. **Identify** your component’s different visual states
2. **Determine** what triggers those state changes
3. **Represent** the state in memory using `useState`
4. **Remove** any non-essential state variables
5. **Connect** the event handlers to set the state

[**Step 1: Identify your component’s different visual states**](Reacting%20To%20Input%20With%20State%201b2aeacbb29981489ba2cce578a2e2a6/Step%201%20Identify%20your%20component%E2%80%99s%20different%20visual%20%201b2aeacbb299810793b6f2397d68b53e.md)

[**Step 2: Determine what triggers those state changes**](Reacting%20To%20Input%20With%20State%201b2aeacbb29981489ba2cce578a2e2a6/Step%202%20Determine%20what%20triggers%20those%20state%20changes%201b2aeacbb299814aba6be9935cf0d47a.md)

[**Step 3: Represent the state in memory with `useState`**](Reacting%20To%20Input%20With%20State%201b2aeacbb29981489ba2cce578a2e2a6/Step%203%20Represent%20the%20state%20in%20memory%20with%20useState%201b2aeacbb29981c3a632c4d25d0d5e9c.md)

[**Step 4: Remove any non-essential state variables**](Reacting%20To%20Input%20With%20State%201b2aeacbb29981489ba2cce578a2e2a6/Step%204%20Remove%20any%20non-essential%20state%20variables%201b2aeacbb299813ba16ff24bba7c7f42.md)

[**Step 5: Connect the event handlers to set state**](Reacting%20To%20Input%20With%20State%201b2aeacbb29981489ba2cce578a2e2a6/Step%205%20Connect%20the%20event%20handlers%20to%20set%20state%201b2aeacbb29981c68f56ce31b2a2a381.md)