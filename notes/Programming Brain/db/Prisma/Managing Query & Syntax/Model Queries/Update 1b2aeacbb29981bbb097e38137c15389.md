# Update

`CreatedAt- 26 Aug 2024 / RevisedAt-` 

The `update` query in Prisma allows you to modify an existing record in your database. It requires a unique identifier (like a primary key or a field marked as `@unique`) to locate the record you want to update.

## Basic Syntax

```jsx
const updatedRecord = await prisma.modelName.update({
  where: {
    uniqueField: uniqueValue, // Identifier to locate the record
  },
  data: {
    // Fields to be updated
  },
});
```

- **`where`**: Specifies the unique condition to find the record.
- **`data`**: Contains the field-value pairs for updating the record.

## Example Prisma Schema

```jsx
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  age       Int?
  status    String   @default("active")
  updatedAt DateTime @updatedAt
}
```

### Example: Update a User's Name by ID

```jsx
const updatedUser = await prisma.user.update({
  where: {
    id: 1, // Assuming 1 is the ID of the user
  },
  data: {
    name: "John Updated",
  },
});
console.log(updatedUser);
```

**Output:**

```json
{
  "id": 1,
  "email": "johndoe@example.com",
  "name": "John Updated",
  "age": 30,
  "status": "active",
  "updatedAt": "2024-12-03T12:00:00.000Z"
}
```

## Updating Multiple Fields

You can update multiple fields in one query.

```jsx
const updatedUser = await prisma.user.update({
  where: {
    email: "johndoe@example.com",
  },
  data: {
    name: "John Doe Updated",
    age: 31,
  },
});
console.log(updatedUser);
```

## Updating Relationships

When models have relations, you can update related records using nested `update` queries.

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

```jsx
const updatedUser = await prisma.user.update({
  where: {
    id: 1,
  },
  data: {
    name: "Updated User",
    posts: {
      update: {
        where: { id: 1 }, // ID of the post to update
        data: {
          title: "Updated Post Title",
        },
      },
    },
  },
});
console.log(updatedUser);
```

## Returning Specific Fields

Use the `select` option to limit the fields returned after an update.

```jsx
const updatedUser = await prisma.user.update({
  where: {
    id: 1,
  },
  data: {
    name: "Selective Fields User",
  },
  select: {
    id: true,
    name: true,
  },
});
console.log(updatedUser);
// Output: { id: 1, name: "Selective Fields User" }
```

## Error Handling

Prisma throws an error if no matching record is found. You can handle this using `try-catch`.

```jsx
try {
  const updatedUser = await prisma.user.update({
    where: {
      id: 999, // Non-existent ID
    },
    data: {
      name: "Will Fail",
    },
  });
  console.log(updatedUser);
} catch (error) {
  console.error("Error updating user:", error.message);
}
```

## Combining Updates with Conditions

You can use conditional logic before calling `update` to ensure the operation makes sense.

```jsx
const user = await prisma.user.findUnique({
  where: {
    id: 1,
  },
});

if (user) {
  const updatedUser = await prisma.user.update({
    where: {
      id: 1,
    },
    data: {
      status: "inactive",
    },
  });
  console.log(updatedUser);
} else {
  console.log("User not found");
}
```

## Updates Multiple values with `updateMany`

Use `updateMany` when you want to update multiple records at once.

```jsx
const result = await prisma.user.updateMany({
  where: {
    status: "active",
  },
  data: {
    status: "inactive",
  },
});
console.log(result);
// Output: { count: 5 } (number of records updated)
```

## Updating Records with Composite Keys

If your schema has composite unique keys, you can update records using all key fields.

```
model User {
  firstName String
  lastName  String
  email     String @unique
  @@unique([firstName, lastName])
}
```

```jsx
const updatedUser = await prisma.user.update({
  where: {
    firstName_lastName: {
      firstName: "John",
      lastName: "Doe",
    },
  },
  data: {
    email: "newemail@example.com",
  },
});
console.log(updatedUser);
```

- **`update`** modifies a single record found by a unique identifier.
- Combine it with `select` to control the fields returned.
- Handle errors for records that don't exist using `try-catch`.
- For multiple updates, use `updateMany`.
- Use nested updates for relationships and related records.