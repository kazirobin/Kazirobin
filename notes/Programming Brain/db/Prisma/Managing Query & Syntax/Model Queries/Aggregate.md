# Aggregate

Return `_min`, `_max`, and `_count` of `profileViews` of all `User` records

```jsx
const minMaxAge = await prisma.user.aggregate({
  _count: {
    _all: true,
  },
  _max: {
    profileViews: true,
  },
  _min: {
    profileViews: true,
  },
})
```

Return `_sum` of all `profileViews` for all `User` records

```jsx
const setValue = await prisma.user.aggregate({
  _sum: {
    profileViews: true,
  },
})
```