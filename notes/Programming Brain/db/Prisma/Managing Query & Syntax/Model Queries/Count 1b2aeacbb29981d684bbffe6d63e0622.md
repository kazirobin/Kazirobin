# Count

**Count all `User` records**

```jsx
const result = await prisma.user.count()
```

Count all `User` records with at least one published `Post`

```jsx
const result = await prisma.user.count({
  where: {
    post: {
      some: {
        published: true,
      },
    },
  },
})
```

Use `select` to perform three separate counts

The following query returns:

- A count of all records (`_all`)
- A count of all records with non-`null` `name` fields
- A count of all records with non-`null` `city` fields

```jsx
const c = await prisma.user.count({
  select: {
    _all: true,
    city: true,
    name: true,
  },
})
```