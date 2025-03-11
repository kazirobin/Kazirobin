# Aggregate Raw

`<model>.aggregateRaw()` returns aggregated database records. It will perform aggregation operations on the `User` collection:

```jsx
const result = await prisma.user.aggregateRaw({
  pipeline: [
    { $match: { status: 'registered' } },
    { $group: { _id: '$country', total: { $sum: 1 } } },
  ],
})
```

`<model>.aggregateRaw()` returns a `JSON` object whose shape depends on the inputs.