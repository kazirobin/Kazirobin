# searchParams Property

The **`searchParams`** read-only property of the `URL` interface returns a `URLSearchParams` object allowing access to the `GET` decoded query arguments contained in the URL.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

## Value

A `URLSearchParams` object.

## Examples

If the URL of your page is `https://example.com/?name=Jonathan%20Smith&age=18` you could parse out the `name` and `age` parameters using:

```jsx
let params = new URL(document.location).searchParams;
let name = params.get("name"); // is the string "Jonathan Smith".
let age = parseInt(params.get("age")); // is the number 18
```