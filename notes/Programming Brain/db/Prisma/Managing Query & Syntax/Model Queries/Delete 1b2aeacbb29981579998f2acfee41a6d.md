# Delete

`CreatedAt- 26 Aug 2024 / RevisedAt-` 

The `delete` query in Prisma allows you to remove a single record from the database. It requires a unique identifier (like a primary key or a field marked as `@unique`) to locate the record you want to delete.

## Basic Syntax

```jsx
const deletedRecord = await prisma.modelName.delete({
  where: {
    uniqueField: uniqueValue, // Identifier to locate the record
  },
});
```

**`where`**: Specifies the unique condition to find and delete the record.

## Example Prisma Schema

```
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  age       Int?
  status    String   @default("active")
}
```

### Example: Delete a User by ID

```jsx
const deletedUser = await prisma.user.delete({
  where: {
    id: 1, // Assuming 1 is the ID of the user
  },
});
console.log(deletedUser);
```

**Output:**
The query will return the deleted record

```jsx
{
  "id": 1,
  "email": "johndoe@example.com",
  "name": "John Doe",
  "age": 30,
  "status": "active"
}
```

## Deleting by Unique Fields

If you have a unique field (e.g., `email`), you can use it to delete the record.

```jsx
const deletedUser = await prisma.user.delete({
  where: {
    email: "johndoe@example.com",
  },
});
console.log(deletedUser);
```

## Error Handling

If no record matches the condition in `where`, Prisma will throw an error. Use `try-catch` to handle this gracefully.

```jsx
try {
  const deletedUser = await prisma.user.delete({
    where: {
      id: 999, // Non-existent ID
    },
  });
  console.log(deletedUser);
} catch (error) {
  console.error("Error deleting user:", error.message);
}
```

## Deleting Related Records

If the record you are deleting has related records (e.g., `User` has related `Post` entries), you need to handle the relationship. You can use cascading deletes or manually delete related records.

```
model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String
  authorId  Int
  author    User     @relation(fields: [authorId], references: [id], onDelete: Cascade)
}

model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  name  String
  posts Post[]
}
```

If the `onDelete: Cascade` is set in the schema, deleting a `User` will automatically delete their related `Post` records.

**Delete a User with Related Posts**

```jsx
const deletedUser = await prisma.user.delete({
  where: {
    id: 1,
  },
});
console.log(deletedUser);
```

## Using `deleteMany` for Multiple Records

If you need to delete multiple records that match certain conditions, use `deleteMany`.

```jsx
const result = await prisma.user.deleteMany({
  where: {
    status: "inactive",
  },
});
console.log(result);
// Output: { count: 5 } (number of records deleted)
```

## Returning Specific Fields

If you only want specific fields returned after deleting, use the `select` option.

```jsx
const deletedUser = await prisma.user.delete({
  where: {
    id: 1,
  },
  select: {
    id: true,
    name: true,
  },
});
console.log(deletedUser);
// Output: { id: 1, name: "John Doe" }
```

## Check Before Deleting

Sometimes, you may want to check if a record exists before attempting to delete it.

```jsx
const user = await prisma.user.findUnique({
  where: {
    id: 1,
  },
});

if (user) {
  const deletedUser = await prisma.user.delete({
    where: {
      id: 1,
    },
  });
  console.log(deletedUser);
} else {
  console.log("User not found");
}
```

## Soft Deletes

If you want to keep records in the database but mark them as "deleted," implement a soft delete pattern by adding a `deletedAt` or `isDeleted` field to your model.

```
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  isDeleted Boolean  @default(false)
}
```

```jsx
const softDeletedUser = await prisma.user.update({
  where: {
    id: 1,
  },
  data: {
    isDeleted: true,
  },
});
console.log(softDeletedUser);
```

- Use `delete` for removing a single record based on unique fields.
- Handle errors using `try-catch`.
- For bulk deletions, use `deleteMany`.
- Consider cascading deletes for related records.
- Implement soft deletes for retaining data while marking it as "deleted."