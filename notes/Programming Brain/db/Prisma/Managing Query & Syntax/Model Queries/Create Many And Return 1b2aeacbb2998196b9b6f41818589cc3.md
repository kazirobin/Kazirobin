# Create Many And Return

`createManyAndReturn` creates multiple records and returns the resulting objects.

## Remarks

- The `skipDuplicates` option is not supported by SQLite.
- You **cannot** create or connect relations by using nested `create`, `createMany`, `connect`, `connectOrCreate` queries inside a top-level `createManyAndReturn()` query.
- When relations are included via `include`, a separate query is generated per relation.
- `relationLoadStrategy: join` is not supported.

Create and return several new users

```jsx
const users = await prisma.user.createManyAndReturn({
  data: [
    { name: 'Sonali', email: 'sonali@prisma.io' },
    { name: 'Alex', email: 'alex@prisma.io' },
  ],
})
```