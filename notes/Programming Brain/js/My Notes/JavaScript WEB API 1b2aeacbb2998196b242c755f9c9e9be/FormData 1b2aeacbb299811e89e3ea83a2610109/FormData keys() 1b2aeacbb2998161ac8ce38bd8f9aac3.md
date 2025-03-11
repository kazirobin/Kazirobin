# FormData.keys()

The **`FormData.keys()`** method returns an iterator which iterates through all keys contained in the `FormData`. The keys are strings.

## Syntax

```jsx
keys()
```

## **Parameters**

None.

## Return value

An `iterator` of `FormData`'s keys.

## Examples

```jsx
const formData = new FormData();
formData.append("key1", "value1");
formData.append("key2", "value2");

// Display the keys
for (const key of formData.keys()) {
  console.log(key);
}
```

The result is:

```jsx
key1
key2
```