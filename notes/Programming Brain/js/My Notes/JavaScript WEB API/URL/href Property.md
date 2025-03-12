# href Property

The **`href`** property of the `URL` interface is a string containing the whole URL.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

## Value

A string.

## Examples

```jsx
const url = new URL(
  "https://developer.mozilla.org/en-US/docs/Web/API/URL/href",
);
console.log(url.href); // Logs: 'https://developer.mozilla.org/en-US/docs/Web/API/URL/href'
```