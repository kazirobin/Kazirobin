# revokeObjectURL()

The **`URL.revokeObjectURL()`** static method releases an existing object URL which was previously created by calling `URL.createObjectURL()`.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API), except for [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API).

</aside>

Call this method when you've finished using an object URL to let the browser know not to keep the reference to the file any longer.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This method is *not* available in [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API), due to issues with the [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) interface's life cycle and the potential for leaks.

</aside>

## Syntax

```jsx
URL.revokeObjectURL(objectURL)
```

## Parameters

- objectURL: A string representing an object URL that was previously created by calling `createObjectURL()`.

## Return value

None (`undefined`).

## Examples

See [Using object URLs to display images.](createObjectURL()%201b2aeacbb29981a488f9c81145567467.md)