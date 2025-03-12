# FormData.entries()

The **`FormData.entries()`** method returns an iterator which iterates through all key/value pairs contained in the `FormData`. The key of each pair is a string object, and the value is either a string or a `Blob`.

## **Syntax**

```jsx
entries()
```

## **Parameters**

None.

## **Return value**

An iterator of `FormData`'s key/value pairs.

## Examples

```jsx
formData.append("key1", "value1");
formData.append("key2", "value2");

// Display the key/value pairs
for (const pair of formData.entries()) {
  console.log(pair[0], pair[1]);
}
```

The result is:

```jsx
key1 value1
key2 value2
```