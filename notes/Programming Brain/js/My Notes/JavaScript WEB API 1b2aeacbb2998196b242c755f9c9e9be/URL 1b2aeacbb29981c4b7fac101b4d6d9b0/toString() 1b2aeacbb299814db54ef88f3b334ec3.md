# toString()

The **`toString()`** method of the `URL` interface returns a string containing the whole URL. It is effectively a read-only version of `URL.href`.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

## Syntax

```jsx
toString()
```

## Parameters

None.

## Return value

A string.

## Examples

```jsx
const url = new URL(
  "https://developer.mozilla.org/en-US/docs/Web/API/URL/toString",
);
url.toString(); // should return the URL as a string
```