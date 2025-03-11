# toJSON()

The **`toJSON()`** method of the `URL` interface returns a string containing a serialized version of the URL, although in practice it seems to have the same effect as `URL.toString()`.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

## Syntax

```jsx
toJSON()
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
url.toJSON(); // should return the URL as a string
```