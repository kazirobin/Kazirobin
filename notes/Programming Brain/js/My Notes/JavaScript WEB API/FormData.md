# FormData

The JavaScript FormData interface provides a method to create an object having key-value pairs. These objects can be shared over the internet using fetch() or XMLHttpRequest.send() method. It uses the HTML form element's functionality. It will use the same format that will be used by a form of the encoding type is set to "multipart/form-data".

We can also pass it directly to the URLSearchParams constructor to get the query parameters just like in the <form> tag behaviour on the GET request submission.

Suppose you have a subscription form with two fields name and email.

```html
<form id="subscription">
    <h1>Subscribe</h1>
    <div id="message"></div>
    <div class="field">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" placeholder="Enter your fullname" required />
        <small></small>
    </div>
    <div class="field">
        <label for="email">Email:</label>
        <input type="text" id="email" name="email" placeholder="Enter your email address" required />
        <small></small>
    </div>
    <div class="field">
        <button type="submit" class="full" id="submit">Subscribe</button>
    </div>
</form>
```

When you click the submit button, the web browser submits the values of the name and email fields in the form to the server.

Similarly, the `FormData` interface allows you to construct a set of key/value pairs representing form fields and their values in JavaScript.

Once having a `FormData` object, you can post it to the server using the fetch API. If you want to submit the form as if it were like the GET request, you can pass the `FormData` object to the `URLSearchParams` constructor.

## Create a FormData object

The following creates a new `FormData` object from an HTML form element:

```jsx
const formData = new FormData(form);
```

The following script shows the values of a `FormData` object:

```jsx
const btn = document.querySelector('#submit');
const form = document.querySelector('#subscription');

btn.addEventListener('click', (e) => {
    // prevent the form from submitting
    e.preventDefault();

    // show the form values
    const formData = new FormData(form);
    const values = [...formData.entries()];
    console.log(values);
});
```

How it works.

- First, select the submit button using the [`querySelector()`](https://www.javascripttutorial.net/javascript-dom/javascript-queryselector/) method of the `document` object.
- Next, add an event handler to handle the click event of the submit button.
- Then, call the [`preventDefault()`](https://www.javascripttutorial.net/dom/events/prevent-default-action-of-events/) method of the event object to avoid form submission.
- After that, create a new `FormData` object from the form element.
- Finally, call the entries() method of the FormData object. Since the entries() method returns an iterator, you must use the [spread operator](https://www.javascripttutorial.net/es6/javascript-spread/) (`...`).

## FormData Methods

The `FormData` object has the following methods:

[`FormData.append()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20append()%201b2aeacbb2998120b141d55a05c8dd8c.md)

[`FormData.delete()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20delete()%201b2aeacbb29981d79aebf6ea72291956.md)

[`FormData.entries()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20entries()%201b2aeacbb299816ba58cc8358d4a5154.md)

[`FormData.get()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20get()%201b2aeacbb2998186af30f509b4dd7503.md)

[`FormData.getAll()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20getAll()%201b2aeacbb2998198bf79e11d258b423b.md)

[`FormData.has()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20has()%201b2aeacbb299818493c1d97a0fb60d39.md)

[`FormData.keys()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20keys()%201b2aeacbb2998161ac8ce38bd8f9aac3.md)

[`FormData.set()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20set()%201b2aeacbb299811cb1b7da6f220e894d.md)

[`FormData.values()`](FormData%201b2aeacbb299811e89e3ea83a2610109/FormData%20values()%201b2aeacbb299814fb4abc3c2d41ddb66.md)

## Submit the FormData using fetch API

We’ll build a simple subscription form that uses the FetchAPI to post a FormData object to the server. The following illustrates how to submit `FormData` using the fetch API:

```jsx
const btn = document.querySelector('#submit');
const form = document.querySelector('#subscription');
const messageEl = document.querySelector('#message');

btn.addEventListener('click', (e) => {
    e.preventDefault();
    subscribe();
});

const subscribe = async () => {
    try {
        let response = await fetch('subscribe.php', {
        method: 'POST',
        body: new FormData(form),
        });
        const result = await response.json();

        showMessage(result.message, response.status == 200 ? 'success' : 'error');
    } catch (error) {
        showMessage(error.message, 'error');
    }
};

const showMessage = (message, type = 'success') => {
    messageEl.innerHTML = `
        <div class="alert alert-${type}">
        ${message}
        </div>
    `;
};
```

In this example, we define a function named subscribe() and call it in the submit button’s click event listener. The `subscribe()` function is an async function because it uses the `await` keyword.

Inside the `subscribe()` function:

First, post the form data to the subscribe.php script using the `fetch()` method:

```jsx
let response = await fetch('subscribe.php', {
    method: 'POST',
    body: new FormData(form),
});
```

Second, get the JSON response by calling the `json()` method of the `response` object:

```jsx
const result = await response.json();
```

Third, show a success message if the HTTP status code is 200. Otherwise, display an error message. The `message` property of the `result` stores the success or error message.

```jsx
showMessage(result.message, response.status == 200 ? 'success' : 'error');
```

Finally, define the `showMessage()` function that displays a success or error message:

```jsx
const showMessage = (message, type = 'success') => {
    messageEl.innerHTML = `
        <div class="alert alert-${type}">
        ${message}
        </div>
    `;
};
```

## Put it all together.

Create a file named **index.html**

```html
<!DOCTYPE html>
<html lang="en">

    <head>
        <title>JavaScript Form Demo</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <link rel="stylesheet" href="css/style.css" />
    </head>

    <body>
        <div class="container">
            <form id="subscription">
                <h1>Subscribe</h1>
                <div id="message"></div>
                <div class="field">
                    <label for="name">Name:</label>
                    <input type="text" id="name" name="name" placeholder="Enter your fullname" required />
                    <small></small>
                </div>
                <div class="field">
                    <label for="email">Email:</label>
                    <input type="text" id="email" name="email" placeholder="Enter your email address" required />
                    <small></small>
                </div>
                <div class="field">
                    <button type="submit" class="full" id="submit">Subscribe</button>
                </div>
            </form>
        </div>
        <script src="app.js"></script>
    </body>

</html>
```

Create a file named **app.js**

```jsx
const btn = document.querySelector('#submit');
const form = document.querySelector('#subscription');
const messageEl = document.querySelector('#message');

btn.addEventListener('click', (e) => {
    e.preventDefault();
    subscribe();
});

const subscribe = async () => {
    try {
        let response = await fetch('subscribe.php', {
            method: 'POST',
            body: new FormData(form),
        });
        const result = await response.json();

        showMessage(result.message, response.status == 200 ? 'success' : 'error');

    } catch (error) {
        showMessage(error.message, 'error');
    }
};

const showMessage = (message, type = 'success') => {
    messageEl.innerHTML = `
        <div class="alert alert-${type}">
        ${message}
        </div>
    `;
};
```

- Use the JavaScript FormData API to capture the HTML form values.
- Use the Fetch API to submit the `FormData` to the server.