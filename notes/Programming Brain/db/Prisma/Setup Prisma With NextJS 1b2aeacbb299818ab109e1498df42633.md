# Setup Prisma With NextJS

Every day, new technologies are released, making it easier to build full-stack applications!

Gone are the days when extensive backend knowledge was required to set up everything from simple to quite complex databases. Today, with tools like Prisma, you can get up and running incredibly fast.

Prisma is an Object-Relational Mapping (ORM) tool that is advantageous when building SaaS or full-stack applications, where quick and efficient database interactions are crucial.

## Install Prisma

Once your Next.js application is set up, navigate into your project directory and install Prisma as a development dependency.

Prisma is added as a development dependency because it includes the Prisma CLI, which is used during development and not typically in your production code.

```bash
npm install -D prisma
```

## Install Prisma Client

The Prisma Client is the query engine that lets you interact with your database through Prisma. It translates your queries into actual database queries, so your application must communicate with the database.

```bash
npm install @prisma/client
```

## Initialize Prisma

Once Prisma and the Prisma Client are installed, initialize Prisma in your project by running:

```bash
npx prisma init
```

This command creates a new `prisma` directory in your project root with a `schema.prisma` file inside it. This file is where you define your database schema using Prisma’s modeling language.

## Configure Database Connection

After initializing Prisma, configure the connection to your PostgreSQL database. This involves setting the database URL in the `.env` file that was created in your project directory.

If you use a hosted database service like **Kinsta**, **Neon**, navigate to the **External connections** section of your hosting control panel. Copy the provided connection string and assign it to `DATABASE_URL` in your `.env` file.

If you are connecting to a local PostgreSQL database, you can use the following format for your connection string:

```bash
DATABASE_URL="postgresql://postgres:mysecretpassword@localhost:5143/postgres"
```

Here, `postgres` is the default username, `mysecretpassword` should be replaced with your actual password, `localhost` is the host, `5143` is the port, and `postgres` is the database name.

## Create A Prisma Schema

After setting up and configuring your database connection, the next crucial step is to create a Prisma schema. This schema defines your application's data model and how it maps to your database.

The Prisma schema file, typically named `schema.prisma`, contains the definitions of your database models.

Add the following basic `User` schema to the `schema.prisma` file:

```bash
model User {
    id       Int     @id @default(autoincrement())
    email    String  @unique
    name     String?
    password String
}
```

Once your model is defined in the schema file, you can use Prisma's migration tool to update your database structure.

Run the following command to create a migration file, which Prisma uses to align your database with the new schema:

```bash
npx prisma migrate dev --name init
```

This command also applies the migration to your database, creating the necessary tables and fields as defined in your Prisma schema. In the `prisma` folder, you notice a `migration` folder which contains some SQL commands written for you.

## Seeding Your Database

Before interacting with your database in the Next.js client, it's beneficial to understand how to seed your database.

Seeding is the process of populating your database with initial data, which is especially useful during development and testing. This allows you to work with realistic data sets and perform integrations and functionality tests without starting from scratch.

Prisma makes seeding straightforward. In your project, create a `seed.ts` file in the `prisma` folder for the seeding logic.

In your seed file, import Prisma Client and write the logic to insert the data into your database:

```jsx
// Import Prisma Client
import { PrismaClient } from '@prisma/client';

// Initialize Prisma Client
const prisma = new PrismaClient();

// Define the main function that will handle database operations
async function main() {
	// Create a new user in the database using Prisma Client
	const user1 = await prisma.user.create({
		data: {
			email: 'alice@example.com',
			name: 'Alice',
			password: 'securepassword123', // Note: In a real application, ensure passwords are hashed!
		},
	});

	// Output the email of the newly created user
	console.log(`Created user: ${user1.email}`);
}

// Execute the main function and handle disconnection and errors
main()
	.then(() => prisma.$disconnect()) // Disconnect from the database on successful completion
	.catch(async (e) => {
		console.error(e); // Log any errors
		await prisma.$disconnect(); // Ensure disconnection even if an error occurs
		process.exit(1); // Exit the process with an error code
	});
```

The code above begins by importing and initializing `PrismaClient`. The main function performs the database insertion operation. Here, a new user is created with an email, optional name, and password.

After the `main` function is executed, `.then()` ensures that the database connection is properly closed on success, while `.catch()` handles any errors by logging them, closing the database connection, and exiting the process with an error code.

You can also decide to create an array and then, in the `main` function, loop through and add each `user`:

```jsx
async function main() {
	for (let user of users) {
		await prisma.user.create({
			data: user,
		});
	}
}
```

Next, you need to run the `seed.ts` file. To run this TypeScript file, install the [ts-node](https://www.npmjs.com/ts-node) dependency:

```bash
npm i -D ts-node
```

To execute the seed, you can run:

```bash
npx prisma db seed
```

You now have data in your Postgres database. You can view this data and also manipulate the data with the Prisma Studio. To open the Prisma Studio, run:

```bash
npx prisma studio
```

This opens a browser window where you can view and interact with your database data. You can now use the data in your Next.js application.

## Integrating Prisma data with your Next.js application

Now that you have successfully seeded your database with initial data using Prisma, the next step is interacting with this data from your Next.js client.

However, directly using Prisma Client in various parts of your application, as you did in the seeding script, is not the most efficient or optimal approach, especially for a server-side environment like Next.js.

To manage this more effectively, create a dedicated module that ensures Prisma Client is used as a singleton across your application. This approach is crucial for maintaining efficient and reliable database connections.

To implement this pattern, create a `utils` folder at the root of your project and create a `db.config.ts` file. This file contains the logic to instantiate Prisma Client if it doesn't already exist or use the existing instance if it does.

In the file, paste the following code from [Prisma docs](https://www.prisma.io/docs/orm/more/help-and-troubleshooting/help-articles/nextjs-prisma-client-dev-practices#solution):

```bash
import { PrismaClient } from '@prisma/client';

const prismaClientSingleton = () => {
	return new PrismaClient();
};

declare const globalThis: {
	prismaGlobal: ReturnType<typeof prismaClientSingleton>;
} & typeof global;

const prisma = globalThis.prismaGlobal ?? prismaClientSingleton();

export default prisma;

if (process.env.NODE_ENV !== 'production') globalThis.prismaGlobal = prisma;
```

This code ensures that only one instance of PrismaClient is created and reused across your application, preventing the creation of multiple instances during development hot reloads. It creates a single PrismaClient instance and saves it on the **`globalThis`** object, reusing it if it already exists.

With this, you can now use the Prisma client anywhere in your Next.js application via the App router.

For example, in the `page.tsx` file, pull all the users and display them:

```bash
import prisma from '@/utils/db.config';

const page = async () => {
	const data = await prisma.user.findMany();

	return (
		<div>
			{data.map((user) => (
				<div key={user.id}>{user.name}</div>
			))}
		</div>
	);
};

export default page;
```

In the code above, the Prisma Client is imported from a singleton setup defined in `utils/db.config.ts`. The `page` component then asynchronously fetches user data by calling `prisma.user.findMany()`, which retrieves all user entries from the database.

This data is mapped over in the returned JSX to render each user's name within individual `div` elements.