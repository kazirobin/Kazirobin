# Group By

Group by `country`/`city` where the average `profileViews` is greater than `200`, and return the `_sum` of `profileViews` for each group

The query also returns a count of `_all` records in each group, and all records with non-`null` `city` field values in each group.

```jsx
const groupUsers = await prisma.user.groupBy({
  by: ['country', 'city'],
  _count: {
    _all: true,
    city: true,
  },
  _sum: {
    profileViews: true,
  },
  orderBy: {
    country: 'desc',
  },
  having: {
    profileViews: {
      _avg: {
        gt: 200,
      },
    },
  },
})
```