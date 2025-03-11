# Update Many

`updateMany` updates a batch of existing database records in bulk and returns the number of updated records.

Return updated BatchPayload like: `{ count: 4` }

```jsx
export type BatchPayload = {
  count: number
}
```

Update all `User` records where the `name` is `Alice` to `ALICE`

```jsx
const updatedUserCount = await prisma.user.updateMany({
  where: { name: 'Alice' },
  data: { name: 'ALICE' },
})
```

Update all `User` records where the `email` contains `prisma.io` and at least one related `Post` has more than 10 likes

```jsx
const updatedUserCount = await prisma.user.updateMany({
  where: {
    email: {
      contains: 'prisma.io',
    },
    posts: {
      some: {
        likes: {
          gt: 10,
        },
      },
    },
  },
  data: {
    role: 'USER',
  },
})
```