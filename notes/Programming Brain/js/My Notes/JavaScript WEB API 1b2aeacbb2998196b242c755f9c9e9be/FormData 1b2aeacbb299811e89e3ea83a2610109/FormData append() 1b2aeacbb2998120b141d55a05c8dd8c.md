# FormData.append()

The **`append()`** method of the `FormData` interface appends a new value onto an existing key inside a `FormData` object, or adds the key if it does not already exist.

The difference between [`set()`](https://developer.mozilla.org/en-US/docs/Web/API/FormData/set) and `append()` is that if the specified key already exists, `set()` will overwrite all existing values with the new one, whereas `append()` will append the new value onto the end of the existing set of values.

## Syntax

```jsx
append(name, value)
append(name, value, filename)
```

## **Parameters**

- `name`: The name of the field whose data is contained in value.
- `value`: The field's value. This can be a string or `Blob` (including subclasses such as `File`). If none of these are specified the value is converted to a string.
- `filename 'Optional'`: The filename reported to the server (a string), when a `Blob` or `File` is passed as the second parameter. The default filename for `Blob` objects is "blob". The default filename for `File` objects is the file's filename.

## Return value

None (`undefined`).

## Examples

```jsx
formData.append("username", "Chris");
```

When the value is a `Blob` (or a `File`), you can specify its name with the `filename` parameter:

```jsx
formData.append("userpic", myFileInput.files[0], "chris.jpg");
```

As with regular form data, you can append multiple values with the same name:

```jsx
formData.append("userpic", myFileInput.files[0], "chris1.jpg");
formData.append("userpic", myFileInput.files[1], "chris2.jpg");
```

If the value is not a string or a `Blob`, `append()` will convert it to a string automatically:

```jsx
formData.append("name", true);
formData.append("name", 72);
formData.getAll("name"); // ["true", "72"]
```