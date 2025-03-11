# FormData.values()

The **`FormData.values()`** method returns an iterator which iterates through all values contained in the `FormData`. The values are strings or `Blob` objects.

## Syntax

```jsx
values()
```

## Parameters

None.

## Return value

An `iterator` of `FormData`'s values.

## Examples

```jsx
const formData = new FormData();
formData.append("key1", "value1");
formData.append("key2", "value2");

// Display the values
for (const value of formData.values()) {
  console.log(value);
}
```

The result is:

```jsx
value1
value2
```