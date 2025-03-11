# PostgreSQL INITCAP()

The `INITCAP()` function converts the first letter of each word in a string to uppercase and the rest to lowercase. In other words, the `INITCAP()` function converts a string to a proper case.

Technically, words are defined as sequences of alphanumeric characters separated by non-alphanumeric characters.

Here’s the basic syntax of the `INITCAP()` function:

```bash
INITCAP(text)
```

In this syntax, the `text` is a string you want to convert to a proper case. Its type can be `CHAR`, `VARCHAR`, or `TEXT`.

The `INITCAP()` returns the text in a proper case. It returns `NULL` if the `text` is `NULL`.

Let’s explore some examples of using the `INITCAP()` function.

The following example uses the INITCAP() to convert the string ‘hello john’ to the proper case:

```bash
SELECT INITCAP('hello john');
```

Output:

```bash
  initcap
------------
 Hello John
(1 row)
```

## INITCAP() With Table Data

In practice, you often use the `INITCAP()` function to format blog titles, author names, and so on. For example:

First, create a new table called `blog_posts` and insert some rows into it:

```bash
CREATE TABLE blog_posts(
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL
);

INSERT INTO blog_posts(title) 
VALUES
    ('getting started with postgresql'),
    ('advanced postgresql queries'),
    ('postgresql performance optimization'),
    ('postgresql data modeling techniques'),
    ('using postgresql in web development')
RETURNING *;
```

Output:

```bash
 id |                title
----+-------------------------------------
  1 | getting started with postgresql
  2 | advanced postgresql queries
  3 | postgresql performance optimization
  4 | postgresql data modeling techniques
  5 | using postgresql in web development
(5 rows)
```

Second, use the `INITCAP()` function to update the titles in the `blog_posts` table to the proper case:

```bash
UPDATE blog_posts
SET title = INITCAP(title)
RETURNING *;
```

Output:

```bash
 id |                title
----+-------------------------------------
  1 | Getting Started With Postgresql
  2 | Advanced Postgresql Queries
  3 | Postgresql Performance Optimization
  4 | Postgresql Data Modeling Techniques
  5 | Using Postgresql In Web Development
(5 rows)

UPDATE 5
```