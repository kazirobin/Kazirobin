# Create

`CreatedAt- 26 Aug 2024 / RevisedAt-` 

The `create` query in Prisma is used to insert a new record into the database. This is one of the most commonly used operations when working with a database.

## Basic Syntax

```jsx
const record = await prisma.modelName.create({
  data: {
    // Field-value pairs for the new record
  },
});
```

**`data`**: This is where you specify the fields and their values for the new record.

## Example Prisma Schema

Let's consider the following schema

```jsx
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  age       Int?
  createdAt DateTime @default(now())
}
```

## Basic `create` Query

```jsx
const newUser = await prisma.user.create({
  data: {
    email: "johndoe@example.com",
    name: "John Doe",
    age: 30,
  },
});
console.log(newUser);
```

**Output:**

```json
{
  id: 1,
  email: "johndoe@example.com",
  name: "John Doe",
  age: 30,
  createdAt: "2024-12-03T12:00:00.000Z"
}
```

## Optional Fields

If a field is optional (e.g., `age`), you can omit it from the `data` object.

```json
const newUser = await prisma.user.create({
  data: {
    email: "janedoe@example.com",
    name: "Jane Doe",
  },
});
console.log(newUser);
```

## Default Values

Fields with default values (e.g., `createdAt` in the schema above) will automatically be populated if you don't specify them in the `data`.

## Creating Related Records

When models are related, you can create related records at the same time using nested `create` queries.

```json
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
const newUser = await prisma.user.create({
  data: {
    email: "author@example.com",
    name: "Author Name",
    posts: {
      create: [
        {
          title: "First Post",
          content: "This is the content of the first post.",
        },
      ],
    },
  },
});
console.log(newUser);
```

This query creates a new user and a related post in the `Post` model.

## Handling Unique Constraints

If you attempt to create a record with a unique field that already exists, Prisma will throw an error. You can handle this using `try-catch`.

```jsx
try {
  const newUser = await prisma.user.create({
    data: {
      email: "duplicate@example.com", // Assume this email already exists
      name: "Duplicate User",
    },
  });
  console.log(newUser);
} catch (error) {
  console.error("Error creating user:", error.message);
}
```

## Returning Specific Fields

You can use the `select` clause to return only specific fields after creating a record.

```jsx
const newUser = await prisma.user.create({
  data: {
    email: "minimal@example.com",
    name: "Minimal User",
    age: 25,
  },
  select: {
    id: true,
    email: true,
  },
});
console.log(newUser);
// Output: { id: 1, email: "minimal@example.com" }
```

## Upserting Records

Sometimes, you may want to create a record if it doesn't exist or update it if it does. Prisma provides the `upsert` method for this.

```jsx
const user = await prisma.user.upsert({
  where: { email: "upsert@example.com" },
  update: { name: "Updated Name" },
  create: {
    email: "upsert@example.com",
    name: "New User",
    age: 35,
  },
});
console.log(user);
```

- Use `create` to insert new records into your database.
- Optional fields can be omitted.
- Default values are automatically applied.
- Related records can be created using nested `create` queries.
- Handle unique constraints using `try-catch`.
- Use `select` to return specific fields after creation.
- For create-or-update functionality, consider using `upsert`.