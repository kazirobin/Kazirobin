# Find Unique

`CreatedAt- 26 Aug 2024 / RevisedAt-` 

The `findUnique` query is part of Prisma Client and is used to fetch a single record based on a unique field. This field could be a primary key (e.g., `id`) or any other field marked with the `@unique` attribute in your Prisma schema.

Prisma's `findUnique` query is ideal when you're certain there will be only one matching record due to the database's constraints.

## Schema Setup

Here's an example Prisma schema to work with:

```bash
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  username  String   @unique
  name      String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

In this schema:

- `id` is the primary key.
- `email` and `username` are unique fields.

## Basic Query Structure

The `findUnique` query takes an object with a `where` clause. The `where` clause specifies the unique field and the value you want to match.

```jsx
const record = await prisma.modelName.findUnique({
  where: {
    uniqueField: value,
  },
});
```

### Example: Fetch User by ID

```jsx
const user = await prisma.user.findUnique({
  where: {
    id: 1,
  },
});
console.log(user);
```

### Example: Fetch User by Email

```jsx
const user = await prisma.user.findUnique({
  where: {
    email: "example@example.com",
  },
});
console.log(user);
```

## Returning Specific Fields

By default, `findUnique` returns all fields of the record. If you need only specific fields, you can use the `select` clause.

```jsx
const user = await prisma.user.findUnique({
  where: {
    email: "example@example.com",
  },
  select: {
    name: true,
    email: true,
  },
});
console.log(user);
// Output: { name: "John Doe", email: "example@example.com" }
```

## Include Relations

If your model has relations, you can include related records using the `include` clause.

```
model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String
  authorId  Int
  author    User     @relation(fields: [authorId], references: [id])
}

model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  name  String
  posts Post[]
}
```

### Query: Fetch User and Their Posts

```jsx
const user = await prisma.user.findUnique({
  where: {
    email: "example@example.com",
  },
  include: {
    posts: true,
  },
});
console.log(user);
/*
Output:
{
  id: 1,
  email: "example@example.com",
  name: "John Doe",
  posts: [
    { id: 1, title: "First Post", content: "Lorem ipsum" },
    { id: 2, title: "Second Post", content: "Dolor sit amet" },
  ],
}
*/
```

## Error Handling

If no matching record is found, `findUnique` returns `null`. Handling this properly is crucial to avoid runtime errors.

### Example: Handle Missing Records

```jsx
const user = await prisma.user.findUnique({
  where: {
    email: "notfound@example.com",
  },
});

if (!user) {
  console.log("User not found");
} else {
  console.log(user);
}
```

**Throw an Error for Missing Records**

If you want to throw an error when no record is found, you can add your own logic:

```jsx
const getUser = async (email) => {
  const user = await prisma.user.findUnique({
    where: { email },
  });
  if (!user) {
    throw new Error("User not found");
  }
  return user;
};

try {
  const user = await getUser("notfound@example.com");
  console.log(user);
} catch (error) {
  console.error(error.message);
}
```

## Limitations of `findUnique`

- **Works only with unique constraints:** You can’t use it to query non-unique fields (e.g., names).
- **Use `findFirst` for flexible queries:** If you want to fetch the first matching record of a non-unique field, use `findFirst`.

Example: Use `findFirst` Instead

```jsx
const user = await prisma.user.findFirst({
  where: {
    name: "John",
  },
});
console.log(user);
```

## Composite Unique Keys

If your schema uses composite unique keys, you can query with multiple fields

```
model User {
  id        Int    @id @default(autoincrement())
  firstName String
  lastName  String
  email     String @unique
  @@unique([firstName, lastName])
}
```

```jsx
const user = await prisma.user.findUnique({
  where: {
    firstName_lastName: {
      firstName: "John",
      lastName: "Doe",
    },
  },
});
console.log(user);
```

- Since `findUnique` uses the database's unique constraints, it’s optimized for fast lookups. For better performance, ensure indexes are set up correctly.
- Use `findUnique` for fetching records based on unique constraints.
- Combine it with `select` and `include` for custom data retrieval.
- Handle `null` responses to ensure robust error handling.
- If working with non-unique fields, use `findFirst` or `findMany`.