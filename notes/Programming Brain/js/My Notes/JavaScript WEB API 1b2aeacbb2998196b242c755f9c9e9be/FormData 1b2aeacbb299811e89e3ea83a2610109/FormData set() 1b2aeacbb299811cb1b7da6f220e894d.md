# FormData.set()

The **`set()`** method of the `FormData` interface sets a new value for an existing key inside a `FormData` object, or adds the key/value if it does not already exist.

The difference between `set()` and `append()` is that if the specified key does already exist, `set()` will overwrite all existing values with the new one, whereas `append()` will append the new value onto the end of the existing set of values.

## Syntax

```jsx
set(name, value)
set(name, value, filename)
```

## Parameters

- `name`: The name of the field whose data is contained in `value`.
- `name`: The field's value. This can be a string or `Blob` (including subclasses such as `File`). If none of these are specified the value is converted to a string.
- `filename 'Optional'`: The filename reported to the server (a string), when a `Blob` or `File` is passed as the second parameter. The default filename for `Blob` objects is "blob". The default filename for `File` objects is the file's filename.

## Return value

None (`undefined`).

## Examples

```jsx
formData.set("username", "Chris");
```

When the value is a `Blob` (or a `File`), you can specify its name with the `filename` parameter:

```jsx
formData.set("userpic", myFileInput.files[0], "chris.jpg");
```

If the value is not a string or a `Blob`, `set()` will convert it to a string automatically:

```jsx
formData.set("name", 72);
formData.get("name"); // "72"
```