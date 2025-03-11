# search Property

The **`search`** property of the [`URL`](https://developer.mozilla.org/en-US/docs/Web/API/URL) interface is a search string, also called a *query string*, that is a string containing a `'?'` followed by the parameters of the URL.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

Modern browsers provide the `URL.searchParams` property to make it easy to parse out the parameters from the query string.

## Value

A string.

## Examples

```jsx
const url = new URL(
  "https://developer.mozilla.org/en-US/docs/Web/API/URL/search?q=123",
);
console.log(url.search); // Logs "?q=123"
```