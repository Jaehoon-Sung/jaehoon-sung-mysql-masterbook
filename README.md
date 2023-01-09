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

## Part 1. Basic Syntax for mySQL

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

Commands shown above are called `DDL`, `Data Definition Language`, because these commands are used to define data we want to manage.

### SQL Data Types; will update soon...

## Part 2. Do you know **EVERYTHING** about `SELECT` for sure? :D

## Part 3. Normal Form : 1NF. 2NF. 3NF. etc...

## Part 4. Join / CRUDing data

## Part 5. Procedure / Function / Index / Transaction

## Part 6. DB Hosting / ERD (Entity Relationship Diagram) / SQL Injection
