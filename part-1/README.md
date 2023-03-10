# Part 1. Creating and manipulating databases : CRUD I

## Table of Contents

- [Creating and Deleting a Database and a Table](#creating-and-deleting-a-database-and-a-table)
  - [Command to create a new database](#command-to-create-a-new-database)
  - [Command to delete a database](#command-to-delete-a-database)
  - [Command to create a new table](#command-to-create-a-new-table)
  - [Example 1: Creating a new table named person with three columns](#example-1-creating-a-new-table-named-person-with-three-columns)
  - [Command to delete a table](#command-to-delete-a-table)
- [Manage columns in a table](#manage-columns-in-a-table)
  - [Command to create a new column in a table](#command-to-create-a-new-column-in-a-table)
  - [Command to change the data type of a column](#command-to-change-the-data-type-of-a-column)
  - [Command to delete a column](#command-to-delete-a-column)
- [Part 1-2. `CRUD`ing data](#part-1-2--crud-ing-data)
  - [`INSERT` : Command to insert data and copy data from another table](#-insert----command-to-insert-data-and-copy-data-from-another-table)
  - [`SELECT` : Command to see the list of tables](#-select-command-to-see-the-list-of-tables)
    - [Displaying every column of a table](#displaying-every-column-of-a-table)
    - [Displaying a certain column you want to display only](#displaying-a-certain-column-you-want-to-display-only)
    - [Displaying two or more columns is possible..](#displaying-two-or-more-columns-is-possible)
  - [`UPDATE` : Command to update existing data](#-update----command-to-update-existing-data)
  - [`DELETE` : Command to delete existing data](#-delete----command-to-delete-existing-data)
  - [PRO-TIP #1 : Will we want to allow everyone to CRUD data?](#pro-tip--1---will-we-want-to-allow-everyone-to-crud-data-)

## Part 1-1. MySQL Basic Syntax (Data Definition Language)

Commands shown below are called `DDL`, `Data Definition Language`.

MySQL requires a semicolon (`;`) at the end of each SQL statement if you want to execute it. If you don't add a semicolon at the end, SQL will just wait for you, assuming that you will enter additional SQL statements before execution! In this masterbook, I have added a semicolon at the end of every statement as if I were executing SQL statements in a terminal.

If you want to copy and paste statements from this masterbook, you should exclude the trailing semicolon before pasting them into a terminal. If you include the semicolon, SQL will run the statements immediately and may throw errors. Although it should not affect your database in most cases, you should still be careful.

### Creating and Deleting a Database and a Table

> #### Command to create a new database
>
> ```
> CREATE DATABASE your_database_name;
> ```

> #### Command to delete a database
>
> **BE CAREFUL!** You can NOT undo it, which means that this operation is irreversible!
>
> ```
> DROP DATABASE your_database_name;
> ```

> #### Command to create a new table
>
> ```
> CREATE TABLE your_table_name (
>    column1_name DATATYPE,
>    column2_name DATATYPE,
>    column3_name DATATYPE,
>    ...
> );
> ```
>
> The above statement is an example of the SQL syntax used to create a new table in a database. It includes the command `CREATE TABLE` followed by the desired table name (your_table_name) and a list of columns with their respective data types. The data type specifies what kind of data each column will store, such as integers, strings, or dates. We will learn what SQL data types exist in Part 2! The ellipsis (...) is not actually part of SQL statements, and it is to indicate that you can add more columns to the table if needed. Once you execute this command, the new table will be created with the specified columns and data types.
>
> #### Example 1: Creating a new table named person with three columns
>
> Common mistake : **Do NOT add a comma (`,`)** after the last column's data type. There is **NO** comma after `age INT` in the code shown below.
> Some developers write data types in lowercase, but here most of the data types are written in uppercase to clarify that they are part of SQL statements.
>
> ```
> CREATE TABLE person (
>    id INT,
>    name VARCHAR(100),
>    age INT
> );
> ```
>
> The above statement is to create a new table called `person` with three columns: `id`, `name`, and `age`. The `id` and `age` columns have a data type of INT, which stands for integer, while the `name` column has a data type of VARCHAR(100), which stands for variable-length character string with a maximum length of 100 characters.

> #### Command to delete a table
>
> **BE CAREFUL!** This operation is irreversible.
>
> ```
> DROP TABLE your_table_name;
> ```

### Manage columns in a table

> #### Command to create a new column in a table
>
> If there are already some rows in a table, each value for a new column will be `NULL` by default.
>
> ```
> ALTER TABLE your_table_name
> ADD your_new_column_name DATATYPE;
> ```

> #### Command to change the data type of a column
>
> ```
> ALTER TABLE your_table_name
> MODIFY COLUMN your_column_name DATATYPE;
> ```
>
> **BE CAREFUL!** This command does not work for all types of data. For example, let's assume that string values already exist in a certain column named `nickname`. Then, the data type of the `nickname` column cannot be changed to an `INT` type or some number types. So it is more desirable that we do not make any major changes to data types using `MODIFY COLUMN` in SQL. In practice, database engineers create a completely new table with the desired types and copy data appropriately from the table to be changed.

> #### Command to delete a column
>
> ```
> ALTER TABLE your_table_name
> DROP COLUMN your_column_name;
> ```

## Part 1-2. `CRUD`ing data

So far, you have learned how to create and update databases and tables, but you have not yet entered any data into them. In other words, you have created databases and tables and defined what types of data should be stored in each column, but you have not stored any data yet. Therefore, if you list the data stored in the tables, you will see only empty tables. From now on, we will learn how to insert(create) new data into the tables, read stored data, update existing data, and even delete data from the tables.

As a review, let's create a table called `person` with three columns: `id` (integer), `name` (varchar(100)), and `age` (integer). We will use this table to CRUD data. This is the same table as the example shown above. Below is my answer, but make sure to try it out yourself first. SQL is all about practice!

<details><summary><b>Answer</b></summary>

```
CREATE TABLE person (
  id INT,
  name VARCHAR(100),
  age INT
)
```

</details>

### `INSERT` : Command to insert data and copy data from another table

>

### `SELECT` : Command to see the list of tables

`SELECT` will be the first SQL query everyone learns. We will start to learn a lot of SQL statements in Part 3, but here let's learn this basic command to see if the data were really inserted into our `person` table!

> #### Displaying every column of a table
>
> ```
> SELECT * FROM your_table_name
> ```
>
> <details><summary><b>Answer</b></summary>
>
> ```
> CREATE TABLE person (
>   id INT,
>   name VARCHAR(100),
>   age INT
> )
>
> ```

</details>

> #### Displaying a certain column you want to display only
>
> ```
> SELECT column_name_you_want_to_display FROM your_table_name
> ```
>
> What would be the query statement to display `product` column only? Try it for yourself!

> #### Displaying two or more columns is possible..
>
> ```
> SELECT column1, column2 FROM your_table_name
> ```

### `UPDATE` : Command to update existing data

### `DELETE` : Command to delete existing data

### PRO-TIP #1 : Will we want to allow everyone to CRUD data?
