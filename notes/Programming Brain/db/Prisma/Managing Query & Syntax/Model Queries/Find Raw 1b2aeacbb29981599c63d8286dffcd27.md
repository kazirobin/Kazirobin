# Find Raw

`<model>.findRaw()` returns actual database records. It will find zero or more documents that match the filter on the `User` collection:

```jsx
const result = await prisma.user.findRaw({
  filter: { age: { $gt: 25 } },
  options: { projection: { _id: false } },
})
```

`<model>.findRaw()` returns a `JSON` object whose shape depends on the inputs.