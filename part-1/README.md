# Part 1.

## Part 1-1. Basic Syntax for mySQL (DDL)

Commands shown below are called `DDL`, `Data Definition Language`.

MySQL requires a semicolon (;) at the end of each SQL statement if you want to execute it. If you don't add a semicolon at the end, SQL will just waits for you, assuming that you enter additional SQL statements before execution! In this masterbook, I added a semicolon at the end of every statement as if I would execute SQL statements on terminal.

### Create & Delete a database and a table

> #### Command to create a new database
>
> ```
> CREATE DATABASE your_database_name;
> ```

> #### Command to delete a database
>
> **BE CAREFUL!** You can NOT undo it.
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
> #### Example 1 : creating a new table named `person` with three columns
>
> Common Mistake : Do **NOT** add `,` after the last column's data type. See there is **NO** comma after `age INT` in the code shown below.
>
> Some developers write data types in lowercase, but here most of data types have been written in uppercase to clarify that they are part of SQL statements.
>
> ```
> CREATE TABLE person (
>    id INT,
>    name VARCHAR(100),
>    age INT
> );
> ```

> #### Command to delete a table
>
> **BE CAREFUL!** You can NOT undo it.
>
> ```
> DROP TABLE your_table_name
> ```

### Manage columns in a table

> #### Command to create a new column in a table
>
> If there are already some rows on a table, each value for a new column will be `NULL` by default.
>
> ```
> ALTER TABLE your_table_name
> ADD your_new_column_name DATATYPE;
> ```

> #### Command to change a data type of a column
>
> ```
> ALTER TABLE your_table_name
> MODIFY COLUMN your_column_name DATATYPE;
> ```
>
> **BE CAREFUL!** This command does not work for all kinds of types. For example, let's assume that string values already exist in a certain column named `nickname`. Then, the data type of the `nickname` column cannot be changed into an `INT` type or some number types. So it is more desirable that we should not make any major situation where we should change data types using `MODIFY COLUMN` in SQL. In practice, DB managers create a totally new table with desired types, and copy data appropriately from the table to be changed.

> #### Command to delete a column
>
> ```
> ALTER TABLE your_table_name
> DROP COLUMN your_column_name;
> ```

## Part 3-5. CRUDing data
