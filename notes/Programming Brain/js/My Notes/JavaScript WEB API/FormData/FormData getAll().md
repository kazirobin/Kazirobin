# FormData.getAll()

The **`getAll()`** method of the `FormData` interface returns all the values associated with a given key from within a `FormData` object.

## **Syntax**

```jsx
getAll(name)
```

## **Parameters**

- `name`: A string representing the name of the key you want to retrieve.

## Return value

An array of values whose key matches the specified `name`. Otherwise, an empty list.

## Examples

If we add two `username` values to a `FormData` using `append()`:

```jsx
formData.append("username", "Chris");
formData.append("username", "Bob");
```

The following `getAll()` method will return both `username` values in an array:

```jsx
formData.getAll("username"); // Returns ["Chris", "Bob"]
```