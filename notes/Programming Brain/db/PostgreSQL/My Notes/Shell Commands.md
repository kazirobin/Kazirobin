# Shell Commands

The PostgreSQL cheat sheet provides you with the common PostgreSQL commands and statements that enable you to work with PostgreSQL quickly and effectively.

---

Access the PostgreSQL server from psql with a specific user:

```bash
psql -U [username];
```

For example, the following command uses the `postgres` user to access the PostgreSQL database server:

```bash
psql -U postgres
```

Connect to a specific database:

```bash
\c database_name;
```

For example, the following command connects to the `student` database:

```bash
\c dvdrental;
You are now connected to database "student" as user "postgres".
```

To quit the psql:

```bash
\q
```

List all databases in the PostgreSQL database server

```bash
\l
```

List all schemas:

```bash
\dn
```

List all stored procedures and functions:

```bash
\df
```

List all views:

```bash
\dv
```

Lists all tables in a current database.

```bash
\dt
```

Or to get more information on tables in the current database:

```bash
\dt+
```

Get detailed information on a table.

```bash
\d+ table_name
```

Show a stored procedure or function code:

```bash
\df+ function_name
```

Show query output in the pretty format:

```bash
\x
```

List all users:

```bash
\du
```

Change the database password:

```bash
\password postgres
```

Clear terminal:

```bash
\! cls
```

Create a new role:

```bash
CREATE ROLE role_name;
```

Create a new role with a `username` and `password`:

```bash
CREATE ROLE username NOINHERIT LOGIN PASSWORD password;
```

Change the role for the current session to the `new_role`:

```bash
SET ROLE new_role;
```

Allow `role_1` to set its role as `role_2:`

```bash
GRANT role_2 TO role_1;
```