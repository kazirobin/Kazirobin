# Delete Many

`deleteMany` deletes multiple records in a transaction.

Return deleted BatchPayload like: `{ count: 4 }`

```jsx
export type BatchPayload = {
  count: number
}
```

Delete all `User` records

```jsx
const deletedUserCount = await prisma.user.deleteMany({})
```

Delete all `User` records where the `name` is `Alice`

```jsx
const deletedUserCount = await prisma.user.deleteMany({
  where: { name: 'Alice' },
})
```