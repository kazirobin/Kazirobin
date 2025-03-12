# Upsert

`upsert` does the following

- If an existing database record satisfies the `where` condition, it updates that record
- If no database record satisfies the `where` condition, it creates a new database record

## Remarks

- To perform arithmetic operations on update (add, subtract, multiply, divide), use atomic updates to prevent race conditions.
- If two or more upsert operations happen at the same time and the record doesn't already exist, then a race condition might happen. As a result, one or more of the upsert operations might throw a unique key constraint error. Your application code can catch this error and retry the operation.
- From version 4.6.0, Prisma ORM hands over upsert queries to the database where possible.

Update (if exists) or create a new `User` record with an `email` of `alice@prisma.io`

```jsx
const user = await prisma.user.upsert({
  where: { id: 1 },
  update: { email: 'alice@prisma.io' },
  create: { email: 'alice@prisma.io' },
})
```