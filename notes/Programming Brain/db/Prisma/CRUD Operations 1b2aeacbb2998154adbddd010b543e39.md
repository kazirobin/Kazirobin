# CRUD Operations

Before moving forward let's understand what is Prisma. So, Prisma is a next-generation ORM (Object Relational Mapping) tool that provides several components for database management and access.

It is a server-side library that helps developers read and write data to the database in an intuitive, efficient and safe way.

It is a server-side library that helps developers read and write data to the database in an intuitive, efficient and safe way.

## Project Setup

To start off, we'll initialize our Node project with:

```bash
npm init -y
```

Next We will install the required dependencies:

```bash
npm i --save-dev prisma typescript ts-node @types/node nodemon
```

For TypeScript configuration,we'll create a `tsconfig.json` file and add the following settings:

```bash
{
  "compilerOptions": {
    "sourceMap": true,
    "outDir": "dist",
    "strict": true,
    "lib": ["esnext"],
    "esModuleInterop": true
  }
}
```

Now, We'll Initialize our Prisma! For that execute the command:

```bash
npx prisma init
```

We can also specify the database during Prisma initialization. For this Project, We are using PostgreSQL so the Command will be:

```bash
npx prisma init --datasource-provider postgresql
```

These steps will generate essential configuration and setup files for our project. Like `prisma/schema.prisma`

Now that we've set up our project environment, let's move on to defining our Prisma models.

## Prisma Model Setup:

Here, we'll define the User Model for our application in the `schema.prisma` file.

```bash
model User {
  id        String   @id @default(uuid())
  email     String   @unique
  name      String?
  password  String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

So, we have created our User model but our database is not yet connected. Before utilizing these models to interact with our database We need to establish a proper database connection.

## Prisma Migration:

Till now Prisma and our database is completely separate! They are able to interact with each other but defining something in prisma won't do anything in the database!

Suppose We made changes to our schema, To reflect those changes in our DB, we have to migrate our new schema! For that we have to use a command:

```bash
npx prisma migrate dev --name init
```

**Note:** Here the --name is optional

Before Migration, Don't forget to change the `DATABASE_URL` to according to your DB.

So This command will do something like this:

![c66f9096-a174-44f7-adef-5fa974d79362.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/c66f9096-a174-44f7-adef-5fa974d79362.png)

After that, It will create a migration file. This migration file will communicate with our postgres database.

This file contains nothing but the SQL commands of our schema. It looks something like this:

![6720fd2d-e795-4d32-b9eb-cf8bd9ef5370.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/6720fd2d-e795-4d32-b9eb-cf8bd9ef5370.png)

## Prisma Client:

The Client is essentially all of the code for interacting to our database. Now, if we see the console , we'll find something interesting!

![e7f5d902-d36d-43c6-bcd4-8a488fc8a89f.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/e7f5d902-d36d-43c6-bcd4-8a488fc8a89f.png)

So, As we can see here, after the migration it has created a brand new prisma client and pushed that into the node-modules!

That's what it does every time we make a migration or changes to our database it creates a new prisma client.

But We don't have the client yet as we haven't installed the client library! To install that run this:

```bash
npm i @prisma/client
```

By doing this migration we have already generated the prisma client but if we want to generate/regenerate the Prisma client manually, We have to use the following command:

```bash
npx prisma generate
```

Now to use the Prisma Client, We have to add the following code:

```bash
import { PrismaClient } from '@prisma/client'
const prisma = new PrismaClient()
```

And with this we can perform our desired operations (like Create, Read, Update & Delete).

## CRUD Operations with Prisma Client:

Now We'll perform CRUD operations with the prisma client that we have created in the previous section.

For that, We'll create a new file script.ts. And start Implementing CRUD!

```jsx
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

async function main() {
  // ... We will write our Prisma Client queries here
}

main()
  .catch((e) => {
    throw e;
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
```

Here, We have created an async function as almost all the operations in Prisma are asynchronous!

We are also catching our errors with the .catch method and in the end we are disconnecting from the Prisma database.

Now in side main we'll write our functions!

## CREATE Operation:

Now, Let's Create our first user.

```jsx
async function main() {
  const user = await prisma.user.create({
    data: {
      email: "arindammajumder2020@gmail.com",
      name: "Arindam Majumder",
      password: "12345678",
    },
  });
  console.log(user);
}
```

Here We are creating our first user using the `prisma.user.create` method.

Before that We will add one script to the `package.json` file in order to run the code.

```jsx
// package.json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon script.ts"
  },
```

Let's start the app and see if it works or not!

![552e0751-384a-4659-8fb3-f825db42cd13.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/552e0751-384a-4659-8fb3-f825db42cd13.png)

Great! We have created our first user!

And if We want to add multiple users at time then the code will belike this:

```jsx
const usersToCreate = [
    {
      email: "john.doe@example.com",
      name: "John Doe",
      password: "password123",
    },
    {
      email: "jane.smith@example.com",
      name: "Jane Smith",
      password: "pass@123",
    },
    {
      email: "robert.brown@example.com",
      name: "Robert Brown",
      password: "securepwd",
    },
    // Add more user objects as needed
  ];
async function main() {
  // ...other functions

  const createdUsers = await prisma.user.createMany({
    data: usersToCreate,
    skipDuplicates: true, // Optional: Skip duplicate entries if any
  });
  console.log(createdUsers);
}
```

This will create multiple users.

**Note:** It's better to add `skipDuplicates: true` to ignore the duplicate values

## READ Operation

Till now, We have created many users.So, It's time to check those data!

To, View all records add the following code to the main function:

```jsx
const allUsers = await prisma.user.findMany();
  console.log(allUsers);
```

Let's Run this and see the results:

![662be8a1-77b0-494f-8af0-330dcefda52d.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/662be8a1-77b0-494f-8af0-330dcefda52d.png)

Great! So we got all the records!

We can also retrieve a single data with unique identifier! Suppose We want to get the user Arindam, We'll use the id and retrive Arindam's data! Here's the code for that:

```jsx
const userById = await prisma.user.findUnique({
    where: {
      id: "84e37ff7-0f7e-41c6-9cad-d35ceb002991",
    },
  });
  console.log(userById);
```

And The Output is as expected :

![a9998cb8-9e3d-4637-9849-f978c407b4ee.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/a9998cb8-9e3d-4637-9849-f978c407b4ee.png)

## UPDATE Operation

This operation is quite similar to the read operations. Previously We are only reading the data, here we'll read and manipulate the data using the queries.

Suppose We want to change the Name to "Arindam" , the code will be:

```jsx
  const updatedUser = await prisma.user.update({
      where: {
        id: "84e37ff7-0f7e-41c6-9cad-d35ceb002991",
      },
      data: {
        name: "Arindam",
      },
    });
```

And See the Console! The name is changed!

![0763a115-6ae7-4068-ad4e-e83025375db0.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/0763a115-6ae7-4068-ad4e-e83025375db0.png)

## DELETE Operation

Okay, Now we will delete a user using it's id!

Here's the code for that:

```jsx
const deletedUser = await prisma.user.delete({
    where: {
      id: "84e37ff7-0f7e-41c6-9cad-d35ceb002991",
    },
});
```

This will Delete the user named Arindam! To verify that if we check allUsers again!

![040f5b35-1a75-4a55-8d8e-9995bc837224.png](CRUD%20Operations%201b2aeacbb2998154adbddd010b543e39/040f5b35-1a75-4a55-8d8e-9995bc837224.png)

And, There's no user named Arindam! We have successfully deleted the user!