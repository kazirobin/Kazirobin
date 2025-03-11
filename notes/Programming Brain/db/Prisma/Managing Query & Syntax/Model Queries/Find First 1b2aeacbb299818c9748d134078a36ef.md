# Find First

`CreatedAt- 26 Aug 2024 / RevisedAt-` 

The `findFirst` query in Prisma is used when you want to fetch the **first** record that matches a set of conditions, without needing a unique constraint. This is ideal for querying multiple records based on some conditions but retrieving just the first one that matches.

## Basic Syntax

```jsx
const record = await prisma.modelName.findFirst({
  where: {
    // Conditions
  },
  orderBy: {
    // Optional: Specifies the sorting order
  },
  select: {
    // Optional: Specifies the fields to be returned
  },
});
```

- **`where`**: The conditions for filtering records.
- **`orderBy`**: Optional. Allows sorting the results. This is often used to get the "first" record based on a particular column (e.g., `createdAt`).
- **`select`**: Optional. Specifies which fields to include in the result.

## Use Cases for Find First

If you need to find the first user who signed up, you can query based on the `createdAt` field.

### Example: Find First User by Name

```jsx
const user = await prisma.user.findFirst({
  where: {
    name: "John Doe",
  },
});
console.log(user);
```

This query finds the **first** user with the name "John Doe" from the `User` model. It returns only the first matching record.

### Example: Find the First User by `createdAt` (Earliest Sign Up)

Often, you may want to find the most recent or earliest record based on a timestamp field.

```jsx
const user = await prisma.user.findFirst({
  where: {
    email: {
      contains: "@example.com",
    },
  },
  orderBy: {
    createdAt: 'asc',  // 'asc' for oldest, 'desc' for newest
  },
});
console.log(user);
```

In this example, the query filters users with an email containing `@example.com` and then sorts them by `createdAt` in ascending order (`asc`), returning the **earliest** one.

### Example: Find the First User with a Specific Email and Status

You can combine conditions to search for records with multiple filters.

```jsx
const user = await prisma.user.findFirst({
  where: {
    email: "user@example.com",
    status: "active",
  },
});
console.log(user);
```

Here, the query searches for the first user with the email `"user@example.com"` and status `"active"`.

### Example: Find the First User with Specific Fields

Just like `findUnique`, you can use `select` to specify which fields you want to retrieve.

```jsx
const user = await prisma.user.findFirst({
  where: {
    name: "John Doe",
  },
  select: {
    id: true,
    email: true,
  },
});
console.log(user);
// Output: { id: 1, email: "johndoe@example.com" }
```

## Using `findFirst` with Pagination

When querying multiple records, `findFirst` is often used to get the first record in a paginated set. You can combine `skip` and `take` to implement pagination.

```jsx
const users = await prisma.user.findFirst({
  take: 10,
  skip: 0,  // This will return the first 10 users
});
console.log(users);
```

## Combining `findFirst` with `orderBy`

In scenarios where you want to sort the results and get just the first matching record, `orderBy` can be helpful.

```jsx
const post = await prisma.post.findFirst({
  orderBy: {
    createdAt: 'desc', // 'desc' will return the most recent post
  },
});
console.log(post);
```

This query retrieves the **most recent** post, sorted by `createdAt` in descending order (`desc`).

## Error Handling

Since `findFirst` returns the first matching record, it might return `null` if no records match the conditions. Make sure to handle this case to avoid errors.

```jsx
const user = await prisma.user.findFirst({
  where: {
    email: "notfound@example.com",
  },
});

if (!user) {
  console.log("No user found");
} else {
  console.log(user);
}
```

- **Use `findFirst`** when you need to fetch the **first matching record** based on conditions and optionally order the results.
- It's useful for querying non-unique fields or retrieving the first record in a sorted list.
- Combine `where`, `orderBy`, and `select` for complex queries.
- **`findFirst`** is more flexible than `findUnique`, as it doesn’t require unique fields and can return the first match based on multiple conditions.