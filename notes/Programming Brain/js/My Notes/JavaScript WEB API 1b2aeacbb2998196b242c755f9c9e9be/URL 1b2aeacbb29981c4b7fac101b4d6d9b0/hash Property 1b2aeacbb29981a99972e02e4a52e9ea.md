# hash Property

The **`hash`** property of the `URL` interface is a string containing a `'#'` followed by the fragment identifier of the URL.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

The fragment is not URL decoded. If the URL does not have a fragment identifier, this property contains an empty string — `""`.

## Value

A string.

## Examples

```jsx
const url = new URL(
  "https://developer.mozilla.org/en-US/docs/Web/API/URL/href#Examples",
);
console.log(url.hash); // Logs: '#Examples'

```