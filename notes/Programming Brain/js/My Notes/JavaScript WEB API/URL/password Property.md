# password Property

The **`password`** property of the `URL` interface is a string containing the password specified before the domain name.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

If it is set without first setting the `username` property, it silently fails.

## Value

A string.

## Examples

```jsx
const url = new URL(
  "https://anonymous:flabada@developer.mozilla.org/en-US/docs/Web/API/URL/password",
);
console.log(url.password); // Logs "flabada"
```