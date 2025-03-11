# Find Many

The `findMany` query in Prisma is used to retrieve multiple records from a database. It's quite flexible and allows for filtering, ordering, pagination, and selection of specific fields. Below is a detailed breakdown of how to use `findMany` in Prisma.

## Basic Syntax

```jsx
const result = await prisma.modelName.findMany({
  // options here
});
```

### **`Where`** - Filtering records based on conditions.

This will find all active users older than 18.

```jsx
const users = await prisma.user.findMany({
  where: {
    age: { gt: 18 },
    isActive: true,
  },
});
```

### `Select` - Selecting specific fields to return.

Use `select` to control which fields Prisma should return. After adding and selecting, this will return only the ID and name fields for each user.

```jsx
const users = await prisma.user.findMany({
  select: {
    id: true,
    name: true,
  },
});
```

### `Include` - Including related records.

Use `include` to include related records in the result. After adding an `include` field this will consist of the `author` field with each post, pulling in data about the post's author.

```jsx
const posts = await prisma.post.findMany({
  include: {
    author: true, // assumes a relation exists with the model "Author"
  },
});
```

### `OrderBy` - Sorting results.

Use `orderBy` to specify sorting criteria. You can order by one or multiple fields, either ascending (`asc`) or descending (`desc`). After adding the `sort` field this will return users sorted by name in ascending order.

```jsx
const users = await prisma.user.findMany({
  orderBy: {
    name: 'asc',
  },
});
```

### `Skip and Take` - Pagination.

Use `skip` and `take` for pagination. `skip` specifies how many records to skip, while `take` specifies how many to retrieve. After adding `skip` and `take` this will skip the first 10 records and retrieve the next 5.

```jsx
const users = await prisma.user.findMany({
  skip: 10,
  take: 5,
});
```

### `Distinct` - Removing duplicates.

Use `distinct` to return unique records based on one or more fields. After adding `distinct` This will return users with unique names only.

```jsx
const users = await prisma.user.findMany({
  distinct: ['name'],
});
```

## Example Query with Multiple Options

```jsx
const result = await prisma.user.findMany({
  where: {
    isActive: true,
    age: { gte: 21 },
  },
  select: {
    id: true,
    name: true,
    posts: {
      select: {
        title: true,
        createdAt: true,
      },
    },
  },
  orderBy: [
    { name: 'asc' },
    { createdAt: 'desc' },
  ],
  skip: 5,
  take: 10,
});
```

- **`where`**: Filters active users aged 21 or older.
- **`select`**: Retrieves only `id`, `name`, and a nested `posts` selection with specific fields.
- **`orderBy`**: Sorts by `name` ascending, and within names by `createdAt` descending.
- **`skip` and `take`**: Skips the first 5 records, then takes the next 10.

If Prisma's filtering is too limited, you can use raw SQL with `prisma.$queryRaw`. However, this is less safe and doesn’t integrate as well with Prisma’s type safety.

Always use `skip` and `take` for large datasets to avoid loading too many records at once. Use `select` to fetch only required fields and reduce the amount of data processed.