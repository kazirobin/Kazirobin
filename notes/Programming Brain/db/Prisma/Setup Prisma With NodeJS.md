# Setup Prisma With NodeJS

Prisma is a popular ORM (Object-Relational Mapping) tool that makes it easy to work with databases in a Node.js environment. By providing a simple, intuitive API for querying databases, Prisma helps developers save time and reduce the complexity of their code. we will explore how to use Prisma with Node.js to create a backend for a web application. 

## Setting Up A Prisma Project

The first step in using Prisma with Node.js is to set up a Prisma project. To do this, you will need to install the Prisma CLI, which provides a convenient way to manage your Prisma projects and generate code.

To install the Prisma CLI in your local machine globally, run the following command in your terminal:

```bash
npm install -g prisma
```

or install the Prisma CLI as a dev dependency on your project:

```bash
npm install -D prisma
```

Now that we have prisma installed, we can now initialize it by running the follwing command in the terminal.

```bash
npx prisma init
```

This creates a new `prisma` directory with a `prisma.schema` file. You can use this file to configure your Prisma project and specify the database you want to use.

## Setup A Database

To connect your database, you need to set the `url` field of the `datasource` block in your Prisma schema to your database connection URL:

```jsx
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

In this case, the `url` is set via an environment variable which is defined in `.env`:

```jsx
DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"
```

### If you already have data in your database

- run `npx prisma db pull` if you already have data in your database and you want to generate the Prisma schema and add it to your schema in `schema.prisma`

## Defining A Data Model

Once you have set up your Prisma project, the next step is to define your data model. In Prisma, a data model is a representation of the structure of your data in the database.

The Prisma schema provides an intuitive way to model data. Add the following models to your `Prisma` directory `schema.prisma` file:

```bash
model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
  posts Post[]
}

model Post {
  id        Int     @id @default(autoincrement())
  title     String
  content   String?
  published Boolean @default(false)
  author    User    @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

Models in the Prisma schema have two main purposes:

- Represent the tables in the underlying database
- Serve as foundation for the generated Prisma Client API

## **Initialize Database**

At this point, you have a Prisma schema but no database yet. Run the following command in your terminal to create the database and the `User` and `Post` tables represented by your models:

```bash
npx prisma migrate dev
```

This command did three things:

1. It created a new SQL migration file for this migration in the `prisma/migrations` directory.
2. It executed the SQL migration file against the database.
3. It ran `prisma generate` under the hood (which installed the `@prisma/client` package and generated a tailored Prisma Client API based on your models).

**Note:** Remember to run `npx prisma migrate dev` command after any changes to your schema. if prisma complains, run this command: `npx prisma migrate dev --name init`

## Install Prisma Client

Installing the Prisma Client. Run the following command in the terminal.

```bash
npm install @prisma/client
```

When you install Prisma Client, it automatically generates a client for your defined models, if you need to regenerate the client, run `npx prisma generate`

## Querying The Database

Once you have defined your data model, you can use Prisma to query your database. To do this, you will need to generate a Prisma client, which is a JavaScript library that provides a simple API for querying your database.

To generate a Prisma client, run the following command in your terminal:

```bash
npx prisma generate
```

This will generate a `prisma client` in your project directory, which you can use to query your database.

To query your database, you can use the Prisma client in your Node.js code. For example, you might use the following code to retrieve all the posts in your database:

```jsx
const { PrismaClient } = require("@prisma/client");
const prisma = new PrismaClient();

async function getPosts() {
  const posts = await prisma.post.findMany();
  console.log(posts);
}

getPosts();
```

**Note:** After any changes to your schema push the state of your Prisma schema to the database without using migrations use this command `npx prisma db push` 

## Prisma Studio

Prisma ORM comes with a built-in GUI to view and edit the data in your database. You can open it using the following command:

```jsx
npx prisma studio
```

## Prisma VS Code Extension

Install the [prisma vs-code extension](https://marketplace.visualstudio.com/items?itemName=Prisma.prisma) for syntax highlighting and more
Add the following to your `settings.json` file to enable this extension for `.prisma` files:

```json
"[prisma]": {
  "editor.defaultFormatter": "Prisma.prisma"
}
```