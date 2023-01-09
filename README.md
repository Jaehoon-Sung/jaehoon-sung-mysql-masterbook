# jaehoon-sung-mysql-masterbook

**Welcome message from the author**

Hi, thank you for visiting this repository. I created this repository to review important `mySQL` syntax and update some major TIL notes.  
Any feedback or comments are sincerely appreciated.

\- Jaehoon Sung (Jae)

## Part 0. Types of Database

### Key-Value Database

Think of an object we use in Javascript. This database has the same structure just shown as below. A `Key-Value Database` is a non-relational database that uses a key-value pair to store data. This `Key-Value Database` is used frequently to implement a simple sub-database. (More practical examples are coming below.)

```
| KEY          | VALUE        |
| ------------ | ------------ |
| name         | Jaehoon Sung |
| day of birth | March 15th   |
```

`Redis` is a famous open-sourced DB which supports this Key-Value database. What you should know about `Redis` is that this is an `in-memory` database, which stores data in a RAM, not a hard disk drive (HDD). A RAM can process data much faster than HDD. So, this `Redis` can manage its data very quickly by processing the data on a RAM. That is why developers use `Redis` even though it supports a key-value pair mainly. Particularly, you might be able to make a good use of `Redis` when you should process some local data very frequently and quickly (i.e. caches)! But still, remember that `Redis` supports a key-value pair only! Newer versions of `Redis` start to support some other types of DB, but they are not popular..

### Relational Database

You already had experiences in relational database. Think of any spreadsheet you made in your daily life. That is an example of relational database. Then, why is this type of database called `relational`? The name itself actually has nothing to do with "relationship". It came from "Relation", a key math terminology in matrix and linear algebra. Apart from this fact, many developers researched how to improve the efficiency of managing this kind of database, and they figured out that it depends on how to reduce data redundancy, create great "relationships" among tables, and manage database using these "relationships". This improvement process is actually called `Normalization`, and we will learn about it soon.

This relational database is the most popular form of database, and I think that is because this form supports a stable environment for data transaction. Many famous relational databases support some functions to secure safe transactions by sufficing `ACID` properties! We will learn about `ACID` properties in this thread, too.

Famous relational database : `Oracle`, `mySQL`, `PostgreSQL`, `MicrosoftSQL Server`, `MariaDB`, `SQLite`, `IBM DB2`, `Google Cloud Spanner`, and etc..

So, what is `ACID`? A set of properties which a database must have to guarantee data validity: `Atomicity`, `Consistency`, `Isolation`, and `Durability`.

### Graph Database

If you really want to see "relationships" among data at a glance, you might want to use `Graph Database`. For example, if you log in your social media account, you can see the list of your friends. Then, if you enter one of your friends' profiles, you might see that friend's list. Or, if you manage departure/arrival status of all airports in the world, you might want to describe it using a graph database. You can even visualize the data you manage using this graph database. The language we are using to manage graph database is called `Graph Query Language`.

Famous graph database : `Neo4j`, `Sparsity`, `OrientDB`, `ArangoDB` and etc..

### There are three more types of databases I think important; will update soon...

## Part 1. Basic Syntax for mySQL (DDL)

Commands shown below are called `DDL`, `Data Definition Language`.

### Command to create a new database

```
CREATE DATABASE your_database_name
```

### Command to delete a database

**BE CAREFUL!** You can NOT undo it.

```
DROP DATABASE your_database_name
```

### Command to create a new table

```
CREATE TABLE your_table_name (
    column1_name DATATYPE,
    column2_name DATATYPE,
    column3_name DATATYPE,
    ...
);
```

### Example 1 : creating a new table named `person` with three columns

Common Mistake : Do **NOT** add `,` after the last column's data type. See there is **NO** comma after `age INT` in the code shown below.

Some developers write data types in lowercase, but here most of data types have been written in uppercase to clarify that they are part of SQL statements.

```
CREATE TABLE person (
    id INT,
    name VARCHAR(100),
    age INT
)
```

### Create a new table with a `DEFAULT` value

You can declare each column's default value, which will be used to fill in when there is no input for that column.  
What would happen if there is no input value for `name` column in the `person` table below?

```
CREATE TABLE person (
    id INT,
    name VARCHAR(100) DEFAULT 'Jaehoon Sung',
    age INT
)
```

### Command to delete a table

**BE CAREFUL!** You can NOT undo it.

```
DROP TABLE your_table_name
```

### Command to manage columns in a table

#### Command to create a new column in a table

If there are already some rows on a table, each value for a new column will be `NULL` by default.  
What should we do if we want to pass another default value? (Hint : we already learned this above.)

```
ALTER TABLE your_table_name
ADD your_new_column_name VARCHAR(100);
```

#### Command to change a data type of a column

**BE CAREFUL!** Let's assume that string values already exist in a certain column named `nickname`. Then, the data type of the `nickname` column cannot be changed into a `INT` type or some number types. So it is more desirable that we should not make any major situation where we change data types in SQL. In practice, DB managers create a totally new table with desired types, and copy data appropriately from the table to be changed.

```
ALTER TABLE your_table_name
MODIFY COLUMN your_column_name DATATYPE;
```

#### Command to delete a column

```
ALTER TABLE your_table_name
DROP COLUMN your_column_name;
```

### SQL Data Types; will update soon...

## Part 2-1. Do you know **EVERYTHING** about `SELECT` for sure? :laughing:

So, what is the purpose to learn SQL language? It's simple. Can you pull, add, delete, and update any data you want? If so, you are done.  
Here, we will learn how to display the data you want to see. Below is the table called `inventory` we will use.

```
| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 4     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |
```

### Basics of `SELECT`

#### Displaying every column of a table

```
SELECT * FROM your_table_name
```

#### Displaying a certain column you want to display only

```
SELECT column_name_you_want_to_display FROM your_table_name
```

What would be the query statement to display `product` column only? Try it for yourself!

#### Displaying two or more columns is possible..

```
SELECT column1, column2 FROM your_table_name
```

### `SELECT` with `ORDER BY`

You will have to display the data in a certain order for many cases. `ORDER BY` does it for you.

#### Ascending order is default

You can omit `ASC`, then SQL will display in ascending order by default.

```
SELECT * FROM your_table_name ORDER BY your_column_name ASC;
```

#### Descending order

```
SELECT * FROM your_table_name ORDER BY your_column_name DESC;
```

#### You can use `ORDER BY` more than once

```
SELECT * FROM your_table_name ORDER BY your_column1 ASC, your_column2 DESC;
```

This statement displays data in ascending order by your_column1, and after in descending order by your_column2 for data from the same your_column1 value.

#### You can pass in the ordinal number of column for `ORDER BY`, not column name

```
| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 4     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |

SELECT * FROM inventory ORDER BY 3 DESC
```

It will display the table in descending order by category.  
So, the query statement above is equal to `SELECT * FROM product ORDER BY category DESC`

## Part 2-2. `WHERE` to filter your data!

You can use `WHERE` to display certain data which meet conditions given after `WHERE`. So,

```
SELECT your_column FROM your_table WHERE conditions_will_go_here
```

The query statement above will return certain data on `your_column` which meets `conditions_will_go_here` only. Here, `conditions_will_go_here` has the form of syntax as `column_name = column_value_you_want_to_look_for`.

#### Example 1 : filtering products, each of whose category is in furniture only

```
| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 4     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |

SELECT * FROM inventory WHERE category = 'furniture'
```

#### Example 2 : filtering products, each of whose price is bigger than $4

```
| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 4     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |

SELECT * FROM inventory WHERE price > 4
```

You can also use `>`, `<`, `>=`, `<=`, `=`, `!=`

#### `BETWEEN` is useful

```
SELECT * FROM inventory WHERE price BETWEEN 3 AND 6
```

`BETWEEN 3 AND 6` is the same expression as `3 ≤ price ≤ 6`. **BE CAREFUL** to remember that `=` sign is included; so, the left and right boundaries are included.

### `AND`, `OR`, and `NOT` for sophiscated conditions / Parentheses can be used for operator precedence!

#### The code below returns data which meet BOTH condition1 AND condition2.

```
SELECT * FROM your_table
WHERE condition1 AND condition2;
```

#### The code below returns data which meet EITHER condition1 OR condition2.

```
SELECT * FROM your_table
WHERE condition1 OR condition2;
```

#### The code below returns data which does NOT meet condition1

Just remember that `NOT` comes directly after `WHERE`

```
SELECT * FROM your_table
WHERE NOT condition1;
```

#### You can use parentheses for operation precedence

What will be the result for the query statement shown below?

```
| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 5     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |

SELECT * FROM inventory
WHERE (category = 'furniture' OR category = 'clothes') AND price = 5
```

## Part 2-3. `OR` VS `IN` / `LIKE` with `%` and `_`

### Multiple `OR`s in the same column? Use `IN`!

```
| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 5     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |

SELECT * FROM inventory WHERE category = 'furniture' OR category = 'clothes'
```

The query statement above is the equal statement as

```
SELECT * FROM inventory WHERE category IN ('furniture', 'clothes')
```

Imagine the case when you want to pull data in thousand kinds of category, but NOT every category. Then, you might repeat `OR` countlessly. Then, `IN` will rescue. Using `IN` will be also easier to read! We don't want to see heavily repeated `OR column_name = ... OR column_name = ... OR ...`.

You can only use `IN` for values included in the **SAME** column. For example, you cannot simplify the following statement using `IN`

```
SELECT * FROM inventory WHERE category = 'clothes' OR price = 3;
```

We can actually use `SELECT` **INSIDE** `IN`. This is one of the examples for SQL subquery. We will look into it, soon.

### `LIKE` with `%` and `_`

`LIKE` helps you find values **containing** values after `LIKE`. Let's learn with the `inventory` table shown below.

| id  | product          | category  | price |
| --- | ---------------- | --------- | ----- |
| 1   | nike shirt       | clothes   | 3     |
| 2   | adidas shirt     | clothes   | 5     |
| 3   | tshirt misc      | clothes   | 5     |
| 4   | chair            | furniture | 4     |
| 5   | wood chair       | furniture | 3     |
| 6   | chair acces      | furniture | 2     |
| 7   | nike shirt young | clothes   | 3     |
| 8   | adidas shirt new | clothes   | 5     |
| 9   | tshirt           | clothes   | 4     |
| 10  | steel chair      | furniture | 6     |
| 11  | chair repair     | furniture | 3     |

`SELECT * FROM inventory WHERE product = 'shirt'` won't give you any data. It is because there is no data whose `product` value is exactly **shirt**.  
How about `SELECT * FROM inventory WHERE product LIKE 'shirt'`? This also returns **NO** data. `Like 'shirt'` is actually same as `= 'shirt'`. To make use of `LIKE`, you must use wild-card characters such as `%` and `_`!

#### `LIKE` with `%`

`%` means any string regardless the number of its characters. Let's dive into the examples.

> ```
> SELECT * FROM inventory WHERE product LIKE 'shirt%'
> ```
>
> This statement allows us to display any values that starts with "shirt". Actually, there is nothing that starts with "shirt" in the example table.

> ```
> SELECT * FROM inventory WHERE product LIKE '%shirt'
> ```
>
> This statement allows us to display any values that ends with "shirt". You can find what would be displayed! See the product name which ends with "shirt".

> ```
> SELECT * FROM inventory WHERE product LIKE '%shirt%'
> ```
>
> This statement allows us to display any values that contains "shirt", because `%` is appended before and after "shirt". Guess what will be displayed!

#### `LIKE` with `_`

`_` plays a similar role as `%` did, but it **cares** about the number of characters. Let's dive into the examples.

> ```
> SELECT * FROM inventory WHERE product LIKE '_shirt'
> ```
>
> Let's count the number of `_`. There is only **one** \_ , isn't it? So, this statement will return data whose `product` value has a single charactor followed by "shirt". So, it will return a row for product `tshirt`. (**NOT** `tshirt misc`, do you see why? If you want to get a row for `tshirt misc`, what should the query statement look like?)

> Similarly, the statement below will return data whose `product` value has "shirt" followed by two characters exactly
>
> ```
> SELECT * FROM inventory WHERE product LIKE 'shirt__'
> ```

> You can mix `%` and `_`! The statement below will return data whose `product` value has a single character followed by "shirt" and ends with any string (or > just ends with no trailing character.)
>
> ```
> SELECT * FROM inventory WHERE product LIKE '_shirt%'
> ```

## Part 2-4. Statistics / Some NUMBER statements / Some STRING statements

Welcome to JAE Credit Card. Below is the `customers` table showing the list of users for JAE Platinum Card.

| id  | name     | num-of-checkouts | total-amount-spent | membership-rank | num-of-late-payments |
| --- | -------- | ---------------- | ------------------ | --------------- | -------------------- |
| 1   | Jay      | 3                | 250                | family          | 0                    |
| 2   | Robert   | 45               | 150000             | vip             | 0                    |
| 3   | Mitchell | 52               | 3200               | royal           | 8                    |
| 4   | Jane     | 121              | 25000              | vip             | 5                    |
| 5   | Mickey   | 21               | 1250               | family          | 1                    |
| 6   | Grace    | 63               | 100                | family          | 1                    |
| 7   | Harry    | 87               | 16500              | vip             | 2                    |
| 8   | Alex     | 17               | 2500               | royal           | 3                    |

### Statistics with `MIN`, `MAX`, `AVG`, and `SUM`

> This is for a quick review.
> `SELECT total-amount-spent FROM customers` will return the whole data on `total-amount-spent` column.

> ```
> SELECT MAX(total-amount-spent) FROM customers`
> ```
>
> The statement above will return the maximum value of `total-amount-spent` values. **REMEMBER** that this does not return a whole row which contains the corresponding maximum value. It just returns the maximum value of `total-amount-spent` shown as below.
> | total-amount-spent |
> |150000|

> ```
> SELECT MIN(total-amount-spent) FROM customers`
> ```
>
> Similarly, the statement above will return the minimum value of `total-amount-spent` values shown as below.
> | total-amount-spent |
> |100|

### Some useful NUMBER statements

### Some useful STRING statements

## Part 2-5. `GROUP BY` / `SELECT` in `SELECT` : sub-query!

## Part 3-1. Normal Form : 1NF. 2NF. 3NF. etc...

## Part 3-2. Join / CRUDing data

## Part 5. Procedure / Function / Index / Transaction

## Part 6. DB Hosting / ERD (Entity Relationship Diagram) / SQL Injection
