# FormData.get()

The **`get()`** method of the `FormData` interface returns the first value associated with a given key from within a `FormData` object. If you expect multiple values and want all of them, use the `getAll()` method instead.

## Syntax

```jsx
get(name)
```

## Parameters

- `name`: A string representing the name of the key you want to retrieve.

## Return value

A value whose key matches the specified `name`. Otherwise, `null`.

## Examples

If we add two `username` values to a `FormData` using `append()`:

```jsx
formData.append("username", "Chris");
formData.append("username", "Bob");
```

The following `get()` method will only return the first `username` value:

```jsx
formData.get("username"); // Returns "Chris"
```