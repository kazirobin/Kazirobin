# Relations

A relation is a *connection* between two models in the Prisma schema. For example, there is a one-to-many relation between `User` and `Post` because one user can have many blog posts.

The following Prisma schema defines a one-to-many relation between the `User` and `Post` models. The fields involved in defining the relation are highlighted:

### Relational databases

```jsx
model User {
  id    Int    @id @default(autoincrement())
  posts Post[]
}

model Post {
  id       Int  @id @default(autoincrement())
  author   User @relation(fields: [authorId], references: [id])
  authorId Int // relation scalar field  (used in the `@relation` attribute above)
}
```

### MongoDB

```jsx
model User {
  id    String @id @default(auto()) @map("_id") @db.ObjectId
  posts Post[]
}

model Post {
  id       String @id @default(auto()) @map("_id") @db.ObjectId
  author   User   @relation(fields: [authorId], references: [id])
  authorId String @db.ObjectId // relation scalar field  (used in the `@relation` attribute above)
}
```

At a Prisma ORM level, the `User` / `Post` relation is made up of:

- Two relation fields: `author` and `posts`. Relation fields define connections between models at the Prisma ORM level and **do not exist in the database**. These fields are used to generate Prisma Client.
- The scalar `authorId` field, which is referenced by the `@relation` attribute. This field **does exist in the database** - it is the foreign key that connects `Post` and `User`.

At a Prisma ORM level, a connection between two models is **always** represented by a relation field on **each side** of the relation.

## Relations in the database

### For Relational databases

The following entity relationship diagram defines the same one-to-many relation between the `User` and `Post` tables in a **relational database**:

![one-to-many-9fd7879c7dbeeb3a0409b55ba7f8ccd9.png](Relations%201b2aeacbb29981ef8e73d60c57e6a6a2/one-to-many-9fd7879c7dbeeb3a0409b55ba7f8ccd9.png)

In SQL, you use a *foreign key* to create a relation between two tables. Foreign keys are stored on **one side** of the relation. Our example is made up of:

- A foreign key column in the `Post` table named `authorId`.
- A primary key column in the `User` table named `id`. The `authorId` column in the `Post` table references the `id` column in the `User` table.

In the Prisma schema, the foreign key / primary key relationship is represented by the `@relation` attribute on the `author` field:

```jsx
author     User        @relation(fields: [authorId], references: [id])
```

**Note:** Relations in the Prisma schema represent relationships that exist between tables in the database. If the relationship does not exist in the database, it does not exist in the Prisma schema.

### For **MongoDB**

For MongoDB, Prisma ORM currently uses a normalized data model design, which means that documents reference each other by ID in a similar way to relational databases.

The following document represents a `User` (in the `User` collection):

```jsx
{ "_id": { "$oid": "60d5922d00581b8f0062e3a8" }, "name": "Ella" }
```

The following list of `Post` documents (in the `Post` collection) each have a `authorId` field which reference the same user:

```jsx
[
  {
    "_id": { "$oid": "60d5922e00581b8f0062e3a9" },
    "title": "How to make sushi",
    "authorId": { "$oid": "60d5922d00581b8f0062e3a8" }
  },
  {
    "_id": { "$oid": "60d5922e00581b8f0062e3aa" },
    "title": "How to re-install Windows",
    "authorId": { "$oid": "60d5922d00581b8f0062e3a8" }
  }
]
```

This data structure represents a one-to-many relation because multiple `Post` documents refer to the same `User` document.

### `@db.ObjectId` on IDs and relation scalar fields

If your model's ID is an `ObjectId` (represented by a `String` field), you must add `@db.ObjectId` to the model's ID *and* the relation scalar field on the other side of the relation:

```jsx
model User {
  id    String @id @default(auto()) @map("_id") @db.ObjectId
  posts Post[]
}

model Post {
  id       String @id @default(auto()) @map("_id") @db.ObjectId
  author   User   @relation(fields: [authorId], references: [id])
  authorId String @db.ObjectId // relation scalar field  (used in the `@relation` attribute above)
}
```

## Relations in Prisma Client

Prisma Client is generated from the Prisma schema. The following examples demonstrate how relations manifest when you use Prisma Client to get, create, and update records.

### Create a record and nested records

The following query creates a `User` record and two connected `Post` records:

```jsx
const userAndPosts = await prisma.user.create({
  data: {
    posts: {
      create: [
        { title: 'Prisma Day 2020' }, // Populates authorId with user's id
        { title: 'How to write a Prisma schema' }, // Populates authorId with user's id
      ],
    },
  },
})
```

In the underlying database, this query:

1. Creates a `User` with an auto-generated `id` (for example, `20`)
2. Creates two new `Post` records and sets the `authorId` of both records to `20`

### Retrieve a record and include related records

The following query retrieves a `User` by `id` and includes any related `Post` records:

```jsx
const getAuthor = await prisma.user.findUnique({
  where: {
    id: "20",
  },
  include: {
    posts: true, // All posts where authorId == 20
  },
});
```

In the underlying database, this query:

1. Retrieves the `User` record with an `id` of `20`
2. Retrieves all `Post` records with an `authorId` of `20`

### Associate an existing record to another existing record

The following query associates an existing `Post` record with an existing `User` record:

```jsx
const updateAuthor = await prisma.user.update({
  where: {
    id: 20,
  },
  data: {
    posts: {
      connect: {
        id: 4,
      },
    },
  },
})
```

In the underlying database, this query uses a nested `connect` query to link the post with an `id` of 4 to the user with an `id` of 20. The query does this with the following steps:

- The query first looks for the user with an `id` of `20`.
- The query then sets the `authorID` foreign key to `20`. This links the post with an `id` of `4` to the user with an `id` of `20`.

In this query, the current value of `authorID` does not matter. The query changes `authorID` to `20`, no matter its current value.

## Types of relations

There are three different types of relations in Prisma ORM:

- One-to-one (also called 1-1 relations)
- One-to-many (also called 1-n relations)
- Many-to-many (also called m-n relations)

The following Prisma schema includes every type of relation:

- one-to-one: `User` ↔ `Profile`
- one-to-many: `User` ↔ `Post`
- many-to-many: `Post` ↔ `Category`

### For Relational Databases

```jsx
model User {
  id      Int      @id @default(autoincrement())
  posts   Post[]
  profile Profile?
}

model Profile {
  id     Int  @id @default(autoincrement())
  user   User @relation(fields: [userId], references: [id])
  userId Int  @unique // relation scalar field (used in the `@relation` attribute above)
}

model Post {
  id         Int        @id @default(autoincrement())
  author     User       @relation(fields: [authorId], references: [id])
  authorId   Int // relation scalar field  (used in the `@relation` attribute above)
  categories Category[]
}

model Category {
  id    Int    @id @default(autoincrement())
  posts Post[]
}
```

### For MongoDB

```jsx
model User {
  id      String   @id @default(auto()) @map("_id") @db.ObjectId
  posts   Post[]
  profile Profile?
}

model Profile {
  id     String @id @default(auto()) @map("_id") @db.ObjectId
  user   User   @relation(fields: [userId], references: [id])
  userId String @unique @db.ObjectId // relation scalar field (used in the `@relation` attribute above)
}

model Post {
  id          String     @id @default(auto()) @map("_id") @db.ObjectId
  author      User       @relation(fields: [authorId], references: [id])
  authorId    String     @db.ObjectId // relation scalar field  (used in the `@relation` attribute above)
  categories  Category[] @relation(fields: [categoryIds], references: [id])
  categoryIds String[]   @db.ObjectId
}

model Category {
  id      String   @id @default(auto()) @map("_id") @db.ObjectId
  posts   Post[]   @relation(fields: [postIds], references: [id])
  postIds String[] @db.ObjectId
}
```

Notice that the syntax is slightly different between relational databases and MongoDB - particularly for many-to-many relations.

For relational databases, the following entity relationship diagram represents the database that corresponds to the sample Prisma schema:

![sample-schema-bb495abfe60492352874c8d62ceb36bc.png](Relations%201b2aeacbb29981ef8e73d60c57e6a6a2/sample-schema-bb495abfe60492352874c8d62ceb36bc.png)

For MongoDB, Prisma ORM uses a normalized data model design, which means that documents reference each other by ID in a similar way to relational databases.

### Implicit and explicit many-to-many relations

- explicit many-to-many relations, where the relation table is represented as an explicit model in your Prisma schema
- implicit many-to-many relations, where Prisma ORM manages the relation table and it does not appear in the Prisma schema.

Implicit many-to-many relations require both models to have a single `@id`. Be aware of the following:

- You cannot use a multi-field ID
- You cannot use a `@unique` in place of an `@id`

To use either of these features, you must set up an explicit many-to-many instead.

The implicit many-to-many relation still manifests in a relation table in the underlying database. However, Prisma ORM manages this relation table.

## Relation fields

Relation fields are fields on a Prisma model that do *not* have a scalar type. Instead, their type is another model.

Every relation must have exactly two relation fields, one on each model. In the case of one-to-one and one-to-many relations, an additional *relation scalar field* is required which gets linked by one of the two relation fields in the `@relation` attribute. This relation scalar field is the direct representation of the *foreign key* in the underlying database.

### For Relational Databases

```jsx
model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  role  Role   @default(USER)
  posts Post[] // relation field (defined only at the Prisma ORM level)
}

model Post {
  id       Int    @id @default(autoincrement())
  title    String
  author   User   @relation(fields: [authorId], references: [id]) // relation field (uses the relation scalar field `authorId` below)
  authorId Int // relation scalar field (used in the `@relation` attribute above)
}
```

### For MongoDB

```jsx
model User {
  id    String @id @default(auto()) @map("_id") @db.ObjectId
  email String @unique
  role  Role   @default(USER)
  posts Post[] // relation field (defined only at the Prisma ORM level)
}

model Post {
  id       String @id @default(auto()) @map("_id") @db.ObjectId
  title    String
  author   User   @relation(fields: [authorId], references: [id]) // relation field (uses the relation scalar field `authorId` below)
  authorId String @db.ObjectId // relation scalar field (used in the `@relation` attribute above)
}
```

Both `posts` and `author` are relation fields because their types are not scalar types but other models.

Also, note that the annotated relation field `author` needs to link the relation scalar field `authorId` on the `Post` model inside the `@relation` attribute. The relation scalar field represents the foreign key in the underlying database.

The other relation field called `posts` is defined purely on a Prisma ORM-level, it doesn't manifest in the database.

### Annotated Relation Fields

Relations that require one side of the relation to be *annotated* with the `@relation` attribute are referred to as *annotated relation fields*. This includes:

- one-to-one relations
- one-to-many relations
- many-to-many relations for MongoDB only

The side of the relation which is annotated with the `@relation` attribute represents the side that **stores the foreign key in the underlying database**. The "actual" field that represents the foreign key is required on that side of the relation as well, it's called *relation scalar field*, and is referenced inside `@relation` attribute:

### For Relational Databases

```jsx
author     User    @relation(fields: [authorId], references: [id])
authorId   Int
```

### For MongoDB

```jsx
author     User    @relation(fields: [authorId], references: [id])
authorId   String  @db.ObjectId
```

A scalar field *becomes* a relation scalar field when it's used in the `fields` of a `@relation` attribute.

### Relation scalar fields

Relation scalar field naming conventions

Because a relation scalar field always *belongs* to a relation field, the following naming convention is common:

- Relation field: `author`
- Relation scalar field: `authorId` (relation field name + `Id`)

## The `@relation` Attribute

The `@relation` attribute can only be applied to the relation fields, not to scalar fields.

The `@relation` attribute is required when:

- you define a one-to-one or one-to-many relation, it is required on *one side* of the relation (with the corresponding relation scalar field)
- you need to disambiguate a relation (that's e.g. the case when you have two relations between the same models)
- you define a self-relation
- you define a many-to-many relation for MongoDB
- you need to control how the relation table is represented in the underlying database (e.g. use a specific name for a relation table)

## Disambiguating Relations

When you define two relations between the same two models, you need to add the `name` argument in the `@relation` attribute to disambiguate them. As an example for why that's needed, consider the following models:

### For Relational Databases

```jsx
// NOTE: This schema is intentionally incorrect. See below for a working solution.

model User {
  id           Int     @id @default(autoincrement())
  name         String?
  writtenPosts Post[]
  pinnedPost   Post?
}

model Post {
  id         Int     @id @default(autoincrement())
  title      String?
  author     User    @relation(fields: [authorId], references: [id])
  authorId   Int
  pinnedBy   User?   @relation(fields: [pinnedById], references: [id])
  pinnedById Int?
}
```

### For MongoDB

```jsx
// NOTE: This schema is intentionally incorrect. See below for a working solution.

model User {
  id           String  @id @default(auto()) @map("_id") @db.ObjectId
  name         String?
  writtenPosts Post[]
  pinnedPost   Post?
}

model Post {
  id         String  @id @default(auto()) @map("_id") @db.ObjectId
  title      String?
  author     User    @relation(fields: [authorId], references: [id])
  authorId   String  @db.ObjectId
  pinnedBy   User?   @relation(fields: [pinnedById], references: [id])
  pinnedById String? @db.ObjectId
}
```

In that case, the relations are ambiguous, there are four different ways to interpret them:

- `User.writtenPosts` ↔ `Post.author` + `Post.authorId`
- `User.writtenPosts` ↔ `Post.pinnedBy` + `Post.pinnedById`
- `User.pinnedPost` ↔ `Post.author` + `Post.authorId`
- `User.pinnedPost` ↔ `Post.pinnedBy` + `Post.pinnedById`

To disambiguate these relations, you need to annotate the relation fields with the `@relation` attribute and provide the `name` argument. You can set any `name` (except for the empty string `""`), but it must be the same on both sides of the relation:

### For **Relational Databases**

```jsx
model User {
  id           Int     @id @default(autoincrement())
  name         String?
  writtenPosts Post[]  @relation("WrittenPosts")
  pinnedPost   Post?   @relation("PinnedPost")
}

model Post {
  id         Int     @id @default(autoincrement())
  title      String?
  author     User    @relation("WrittenPosts", fields: [authorId], references: [id])
  authorId   Int
  pinnedBy   User?   @relation("PinnedPost", fields: [pinnedById], references: [id])
  pinnedById Int?    @unique
}
```

### For MongoDB

```jsx
model User {
  id           String  @id @default(auto()) @map("_id") @db.ObjectId
  name         String?
  writtenPosts Post[]  @relation("WrittenPosts")
  pinnedPost   Post?   @relation("PinnedPost")
}

model Post {
  id         String  @id @default(auto()) @map("_id") @db.ObjectId
  title      String?
  author     User    @relation("WrittenPosts", fields: [authorId], references: [id])
  authorId   String  @db.ObjectId
  pinnedBy   User?   @relation("PinnedPost", fields: [pinnedById], references: [id])
  pinnedById String? @unique @db.ObjectId
}
```

[One To One Relations](Relations%201b2aeacbb29981ef8e73d60c57e6a6a2/One%20To%20One%20Relations%201b2aeacbb2998137afebc9167c8e619a.md)

[One To Many Relations](Relations%201b2aeacbb29981ef8e73d60c57e6a6a2/One%20To%20Many%20Relations%201b2aeacbb29981a982bae1cda9169b29.md)

[Many To Many Relations](Relations%201b2aeacbb29981ef8e73d60c57e6a6a2/Many%20To%20Many%20Relations%201b2aeacbb29981ef8a8ac076c21af7eb.md)

[Self Relations](Relations%201b2aeacbb29981ef8e73d60c57e6a6a2/Self%20Relations%201b2aeacbb299813a819bf319ddb81582.md)