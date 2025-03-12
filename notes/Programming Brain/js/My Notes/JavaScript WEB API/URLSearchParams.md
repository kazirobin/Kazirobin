# URLSearchParams

he **`URLSearchParams`** interface defines utility methods to work with the query string of a URL.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

</aside>

An object implementing `URLSearchParams` can directly be used in a `for...of` structure to iterate over key/value pairs in the same order as they appear in the query string, for example the following two lines are equivalent:

```jsx
for (const [key, value] of mySearchParams) {
}
for (const [key, value] of mySearchParams.entries()) {
}
```

## Constructor