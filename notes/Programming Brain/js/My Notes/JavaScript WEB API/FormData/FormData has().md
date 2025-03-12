# FormData.has()

The **`has()`** method of the `FormData` interface returns whether a `FormData` object contains a certain key.

## Syntax

```jsx
has(name)
```

## Parameters

- `name`: A string representing the name of the key you want to test for.

## Return value

`true` if a key of `FormData` matches the specified `name`. Otherwise, `false`.

## Examples

The following snippet shows the results of testing for the existence of `username` in a `FormData` object, before and after appending a `username` value to it with `append()`:

```jsx
formData.has("username"); // Returns false
formData.append("username", "Chris");
formData.has("username"); // Returns true
```