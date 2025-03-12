# Create Many

`createMany` creates multiple records in a transaction.

## Remarks

- As of Prisma ORM version 5.12.0, `createMany()` is now supported by SQLite.
- The `skipDuplicates` option is not supported by MongoDB, SQLServer, or SQLite.
- You **cannot** create or connect relations by using nested `create`, `createMany`, `connect`, `connectOrCreate` queries inside a top-level `createMany()` query.
- You can use a nested `createMany` query inside an `update()` or `create()` query - for example, add a `User` and two `Post` records with a nested `createMany` at the same time.

**Create several new users**

```jsx
const users = await prisma.user.createMany({
  data: [
    { name: 'Sonali', email: 'sonali@prisma.io' },
    { name: 'Alex', email: 'alex@prisma.io' },
  ],
})
```