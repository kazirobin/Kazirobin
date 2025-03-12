# Prisma Migrate

`CreatedAt- 30 Nov 2024 / RevisedAt-` 

In Prisma, **migrate** is a feature used to manage your database schema through a process called **migrations**. It enables you to define your database schema in a **Prisma schema file** (`schema.prisma`) and then apply changes to your database in a controlled and versioned manner.

## What is Prisma Migrate?

Prisma Migrate is a tool that synchronizes changes made to your data model in the Prisma schema file (`schema.prisma`) with your actual database schema. It generates **migration files**, which contain SQL instructions to apply these changes to your database.

This process ensures that the database schema stays consistent with the application logic.

## Prisma Migration Commands

### `prisma migrate dev`

Used in development to:

- Detect changes in the Prisma schema file.
- Create a new migration file in `prisma/migrations/`.
- Apply the migration to your database.

```bash
npx prisma migrate dev
```

1. Prisma compares the existing database schema with the schema in `schema.prisma`.
2. A new migration file is generated if there are changes.
3. The migration is applied to the database.

### `prisma migrate deploy`

Used in production to:

- Apply all pending migrations in the `prisma/migrations/` directory to the database.

```bash
npx prisma migrate deploy
```

This ensures that the database schema in production is updated without generating new migration files.

### `prisma migrate reset`

Resets the database by:

- Dropping all tables.
- Reapplying all migrations.

```bash
npx prisma migrate reset
```

This is useful in local development for testing schema changes. **`Do not use in production`**, as it erases all data.

### `prisma migrate status`

Displays the current status of migrations, showing

- Applied migrations.
- Pending migrations.
- Whether the database is up-to-date.

```bash
npx prisma migrate status
```

## How Migrations Work

- **Versioning**: Each migration is stored in a folder named with a timestamp and a descriptive name (e.g., `20231130123045_initial_migration`).
- **SQL Files**: Migration files contain raw SQL statements that Prisma generates to update the database schema.
- **History Table**: Prisma uses a `_prisma_migrations` table in your database to track applied migrations.
- **Consistency**: The migration process ensures that your database schema matches the `schema.prisma` definition, even across environments.

## Example Workflow

1. Define your initial schema in `schema.prisma`

```bash
model User {
  id    Int    @id @default(autoincrement())
  name  String
  email String @unique
}
```

1. Run

```bash
npx prisma migrate dev --name initial_migration
```

This creates and applies the migration.

1. Add a new field to the `User` model:

```
model User {
  id        Int    @id @default(autoincrement())
  name      String
  email     String @unique
  age       Int?   // New field
}
```

1. Run

```bash
npx prisma migrate dev --name add_age_field
```

1. In production, deploy all migrations

```bash
npx prisma migrate deploy
```

## Handling Required Fields in Existing Tables

If you add a **required** column to an existing table, Prisma may give an error like:

**Error:** The required column `address` was added to the `user` table without a default value.

### Solution 1: Provide a Default Value

Added a default value

```
model User {
  id        Int    @id @default(autoincrement())
  name      String
  email     String @unique
  address   String @default("Unknown")  // Default value added
}
```

Then, run:

```bash
npx prisma migrate dev --name add_address_column
```

### Solution 2: Make the Column Optional

Make the column value optional

```
model User {
  id        Int    @id @default(autoincrement())
  name      String
  email     String @unique
  address   String? // Made optional
}
```

Then, run:

```bash
npx prisma migrate dev --name add_address_column
```

### Solution 3: Manually Handle Migration

1. Create a migration without applying it:

```bash
npx prisma migrate dev --create-only --name add_address_column
```

1. Open the generated SQL file in `prisma/migrations/.../migration.sql` and modify it:

```bash
ALTER TABLE "User" ADD COLUMN "address" TEXT NOT NULL DEFAULT 'Unknown';
```

1. Apply the migration:

```bash
npx prisma migrate dev
```

## Different Migrate & Push

The main difference between **`prisma migrate`** and **`prisma db push`** lies in **how they handle database schema changes** and their use cases.

### `prisma migrate`

- **Purpose**:
    
    `prisma migrate` is used for **managing migrations** and applying schema changes in a version-controlled and systematic way. It creates migration files and applies them to the database.
    
- **Key Features**:
    - **Migration Files**: Creates SQL-based migration files stored in the `prisma/migrations/` folder. These files document schema changes and allow collaboration and versioning.
    - **Environment Compatibility**: Ideal for production and team collaboration, ensuring consistent schema changes across environments.
    - **Database State Tracking**: Tracks applied migrations in the `_prisma_migrations` table in the database.
- **Commands**:
    - `prisma migrate dev`: Generates migrations and applies them in development.
    - `prisma migrate deploy`: Applies pending migrations in production.
    - `prisma migrate reset`: Resets the database and reapplies all migrations.
- **Use Case**:
    - Use when you need **version-controlled migrations**, especially for production or team projects.
    - Ensures that every change is properly recorded and can be reproduced in other environments.

### `prisma db push`

- **Purpose**:
    
    `prisma db push` is a **lightweight command** that synchronizes the Prisma schema (`schema.prisma`) directly with the database schema **without creating migration files**.
    
- **Key Features**:
    - **No Migration Files**: Changes are directly applied to the database, and no migration files are generated.
    - **Quick Updates**: Useful for prototyping or quickly syncing the schema with the database in development.
    - **No Tracking**: Changes made with `db push` are not tracked in the `_prisma_migrations` table.
- **Commands**:
    - `prisma db push`
- **Use Case**:
    - Use during **rapid prototyping** or **local development** when you don’t need to keep a history of schema changes.
    - Not suitable for production because changes aren't tracked, making them difficult to reproduce or roll back.

## Comparison Table

| Feature | prisma migrate | prisma db push |
| --- | --- | --- |
| Purpose | Versioned schema migrations | Direct schema synchronization |
| Migration Files | Creates SQL migration files | Does not create migration files |
| Tracking | Tracks applied changes in `_prisma_migrations` | Does not track changes |
| Use Case | Production and collaboration | Prototyping or quick local changes |
| Environment | Suitable for all environments (dev/prod) | Suitable for development only |
| Rollback Support | Supports rollbacks with migrations | No rollback support |
| Command | `npx prisma migrate dev` | `npx prisma db push` |