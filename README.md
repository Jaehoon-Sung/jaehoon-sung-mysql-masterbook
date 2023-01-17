# jaehoon-sung-mysql-masterbook

**Welcome message from the author**

Hi, thank you for visiting this repository. I created this repository to review important `mySQL` syntax and update some major TIL notes. Any feedback or comments are sincerely appreciated.

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

```
COMING SOON
```

## Part 1-1. Basic Syntax for mySQL (DDL)

Commands shown below are called `DDL`, `Data Definition Language`.

### Create & Delete a database and a table

> #### Command to create a new database
>
> ```
> CREATE DATABASE your_database_name
> ```

> #### Command to delete a database
>
> **BE CAREFUL!** You can NOT undo it.
>
> ```
> DROP DATABASE your_database_name
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
> )
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

## Part 1-2. SQL Data Types

```
COMING SOON!
```

## Part 1-3. Columns with constraints : safe update & easy debug!

We can actually set up constraints to make appropriate values come in our database. To achieve this goal, we can use many keywords introduced below. These keywords will help us set up some customized errors and find bugs more easily. Let's make a full use of them wisely!

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

Let's revisit the `ADD` query statement.

```
ALTER TABLE your_table_name
ADD your_new_column_name DATATYPE;
```

Recall that each value for a new column will be `NULL` by default, if there are already some rows on a table. What should we do to fill each value for a new column using our customized value? (Hint : we just learned it.)

### `NOT NULL` : Don't make the value VOID!

We are already familiar with the definition of `NULL`. The DB does not always let you know whether you fail to enter the whole set of necessary data in your table or not. Sometimes, you can also make some human errors such as entering fewer number of values when adding a new row, and the DB does not still always let you know these errors. Your missing values will be "kindly" filled with `NULL`s, which might occur other errors for your software. `NOT NULL` will help you notice these errors earlier!

```
CREATE TABLE new_table (
    id INT NOT NULL,
    name VARCHAR(100) NOT NULL,
    age INT
)
```

You can see that `id` and `name` marked as `NOT NULL`. Then, if you pass nothing into these columns, the DB will refuse any requested updates and alert you that you don't give any data. It will help you notice `NULL` errors much earlier and prevent you from getting lost when you work on other frontend or backend codes! `NULL` problems are very hard to catch in practice, because you cannot notice them until you literally print them out! Do you agree why constraint keywords are important in SQL now?

### `UNIQUE` : let the value UNIQUE on the column!

```
CREATE TABLE new_table (
    id INT UNIQUE,
    name VARCHAR(100) NOT NULL,
    age INT
)
```

Now, `id` has an `UNIQUE` constraint. As it is an integer type, each value on `id` column will have an **unique** value! So, the table declared above will **NOT** permit the table shown below!

```
| student id | name  | age |
| ---------- | ----- | --- |
| 1          | Jae   | 18  |
| 2          | Grace | 20  |
| 2          | Brian | 17  |

ERROR! Brian's `id` is duplicated with Grace's `id`!
```

Actually, `UNIQUE` is not frequently used, because there is a similar but **more important** keyword `PRIMARY KEY`, which we will meet soon!

### `CHECK()` : for some detailed conditions

`CHECK()` allows us to write some customized conditions.

```
CREATE TABLE new_table (
    id INT,
    name VARCHAR(100),
    age INT CHECK (age > 0)
)
```

`CHECK (age > 0)` makes the DB only get the whole number for `age`. You can use operators such as `AND`, `OR`, `IN`, and `>` with `CHECK()`!

### `PRIMARY KEY` : a value which distinguishes each row data

Assume that you are a college student. Then, what value can be used as an unique key to distingush your information from others? Your name, age, or major cannot be used, because there can be students who have the same name, age, or major. Maybe, your student ID can be. If a college gives each student an unique student ID, it can distinguish each student regardless of other values. Here, the column for student ID is called `PRIMARY KEY`, which helps you distinguish each row data.

TLDR : pick the column which can be used a `PRIMARY KEY` to distinguish each row data from the table shown below!

| student id | name   | age | major            |
| ---------- | ------ | --- | ---------------- |
| 1          | Jay    | 19  | Computer Science |
| 2          | Grace  | 19  | Economics        |
| 3          | Robert | 21  | History          |
| 4          | Jane   | 22  | Computer Science |

Using the only saved data on the table, we can use `student id` and `name` as `PRIMARY KEY`. However, in practice, we must use `student id` only, because any student whose name is Jay, Grace, Robert, or Jane can enroll in this college! Of course, a software engineer at this college must secure that `student id` will be **unique** forever.

Then, how can we give a `PRIMARY KEY` constraint? See the code below.

```
CREATE TABLE new_table (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age > 0)
)
```

Now, `id` has a `PRIMARY KEY` constraint! Giving a `PRIMARY KEY` constraint actually means making the column `NOT NULL` **AND** `UNIQUE`. It makes sense because the value to distinguish each row data must be unique but not void!

**SPOILER ALERT!** We can use two or more columns to designate a `PRIMARY KEY` for the table. It is called a `COMPOSITE PRIMARY KEY`. We will learn it with `NF (Normal Form)`.

### `AUTO_INCREMENT` : gives +1 value automatically. The best friend of `PRIMARY KEY`!

Any data having this `AUTO_INCREMENT` keyword will be filled with a value automatically incremented by 1. The default start value is 1, and you can make the value start with another value using `AUTO_INCREMENT = a_whole_number_you_want_to_start_with`. For example, `AUTO_INCREMENT = 100` means that a value will start from `100`, and each value will be incremented by 1 from 100 one by one. Below is the code example to sho why this `AUTO_INCREMENT` is useful to use.

```
CREATE TABLE new_table (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age > 0)
);
```

Now, we can see that `id` is an auto-incremented primary key for the table. It actually makes sense that `AUTO_INCREMENT` will generate an unique natural number to each row, which can play a role as a primary key. If you use this `AUTO_INCREMENT` keyword, you don't have to "insert" a value into the `id` column, because `AUTO_INCREMENT` already does it for you. The code shown below is a **correct** syntax to insert data into the table created by the query above.

```
INSERT INTO new_table (name, age)
VALUE ('Jaehoon Sung', '26');
```

There is no `id` value in the `INSERT` query shown above. It is fine, because `AUTO_INCREMENT` keyword of `id` column generates the appropriate value for us already.

### `CONSTRAINT()` : easier to read & faster to find errors!

There is actually another way to adding constraints on your table data as shown below!

```
CREATE TABLE new_table (
    id INT,
    name VARCHAR(100),
    age INT,
    PRIMARY KEY (id),
    CHECK(age > 10)
)
```

Can you see that constraints are separately written from columns? Here, you can apply `CONSTRAINT()` to make it much easier to catch each constraint.

```
CREATE TABLE new_table (
    id INT,
    name VARCHAR(100),
    age INT,
    CONSTRAINT constraint1 PRIMARY KEY (id),
    CONSTRAINT constraint2 CHECK(age > 10)
);
```

Let's assume that you try to add an `age` data below 10. Then, you might see an error message saying like "You cannot add this data due to constraint2" on your console or workbench. So, `CONSTRAINT` helps you understand constraints applied in the table by seeing the customized error message. In practice, `constraint2` should have been a text like `age_is_under_10` which helps programmers catch that age must be greater than 10 right away!

### PRO-TIP 1 : How to add constraints to an existing column?

Adding constraints to an existing column means that you want to modify the column's characteristics! So, you should recall `ALTER TABLE`!

```
ALTER TABLE your_table
MODIFY your_column int NOT NULL;
```

The query shown above add a `NOT NULL` constraint to `your_column` in `your_table`!

### PRO-TIP 2 : `AUTO_INCREMENT` is actually not a standard SQL syntax.

A standard syntax for `AUTO_INCREMENT` is shown below. You should write a syntax below, if you want to implement an `AUTO_INCREMENT` function in Oracle, PostgreSQL, and etc.

```
CREATE TABLE new_table (
    id NUMBER GENERATED BY DEFAULT ALWAYS AS IDENTITY
)


Actually, the PostgreSQL syntax for AUTO_INCREMENT should be...

CREATE TABLE new_table (
    id INT GENERATED BY DEFAULT ALWAYS AS IDENTITY
)
```

## Part 2-1. Do you know **EVERYTHING** about `SELECT` for sure? :laughing:

So, what is the purpose to learn SQL language? It's simple. Can you pull, add, delete, and update any data you want? If so, you are done.
Here, we will learn how to display the data you want to see. Below is the table called `inventory` we will use.

| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 4     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |

### Basics of `SELECT`

> #### Displaying every column of a table
>
> ```
> SELECT * FROM your_table_name
> ```

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

### `LIMIT` to show some of the first rows on the table

Let's assume that you want to output the first five rows on the table. Using `LIMIT` achieves this goal.

> #### Displaying the first five rows of the table
>
> ```
> SELECT column1 FROM your_table_name LIMIT 5;
> ```

We will revisit some (simple but) more useful tips to use `LIMIT`. Please see PART 2-4.

P.S. For Oracle DB, you must enter `FETCH FIRST 5 ROWS ONLY` instead of `LIMIT`. Remember that there are small differences in syntax among many SQL DBs!

### `SELECT` with `ORDER BY`

You will have to display the data in a certain order for many cases. `ORDER BY` does it for you.

> #### Ascending order is default
>
> You can omit `ASC`, then SQL will display in ascending order by default.
>
> ```
> SELECT * FROM your_table_name ORDER BY your_column_name ASC;
> ```

> #### Descending order
>
> ```
> SELECT * FROM your_table_name ORDER BY your_column_name DESC;
> ```

> #### You can use `ORDER BY` more than once
>
> ```
> SELECT * FROM your_table_name ORDER BY your_column1 ASC, your_column2 DESC;
> ```
>
> This statement displays data in ascending order by your_column1, and after in descending order by your_column2 for data from the same your_column1 value.

> #### You can pass in the ordinal number of column for `ORDER BY`, instead of column name
>
> ```
>
> | id  | product | category  | price |
> | --- | ------- | --------- | ----- |
> | 1   | shirt   | clothes   | 3     |
> | 2   | pants   | clothes   | 4     |
> | 3   | bed     | furniture | 5     |
> | 4   | chair   | furniture | 6     |
> | 5   | nike    | shoes     | 3     |
>
> SELECT * FROM inventory ORDER BY 3 DESC
>
> ```
>
> It will display the table in descending order by category.
> So, the query statement above is equal to `SELECT * FROM product ORDER BY category DESC`.

## Part 2-2. `WHERE` to filter your data!

You can use `WHERE` to display certain data which meet conditions given after `WHERE`. So,

```
SELECT <your_column FROM your_table> WHERE <conditions_will_go_here>
```

The query statement above will return certain data on `your_column` which meets `conditions_will_go_here` only. Here, `conditions_will_go_here` has the form of syntax as `column_name = column_value_you_want_to_look_for`.

> #### Example 1 : filtering products, each of whose category is in furniture only
>
> ```
> | id  | product | category  | price |
> | --- | ------- | --------- | ----- |
> | 1   | shirt   | clothes   | 3     |
> | 2   | pants   | clothes   | 4     |
> | 3   | bed     | furniture | 5     |
> | 4   | chair   | furniture | 6     |
> | 5   | nike    | shoes     | 3     |
>
> SELECT * FROM inventory WHERE category = 'furniture'
> ```

> #### Example 2 : filtering products, each of whose price is bigger than $4
>
> ```
> | id  | product | category  | price |
> | --- | ------- | --------- | ----- |
> | 1   | shirt   | clothes   | 3     |
> | 2   | pants   | clothes   | 4     |
> | 3   | bed     | furniture | 5     |
> | 4   | chair   | furniture | 6     |
> | 5   | nike    | shoes     | 3     |
>
> SELECT * FROM inventory WHERE price > 4
> ```

You can also use `>`, `<`, `>=`, `<=`, `=`, `!=`

> #### `BETWEEN` is useful
>
> ```
> SELECT * FROM inventory WHERE price BETWEEN 3 AND 6
> ```
>
> `BETWEEN 3 AND 6` is the same expression as `3 ≤ price ≤ 6`. **BE CAREFUL** to remember that `=` sign is included; so, the left and right boundaries are included.

### `AND`, `OR`, and `NOT` for sophiscated conditions

> #### The code below returns data which meet BOTH condition1 AND condition2.
>
> ```
> SELECT * FROM your_table
> WHERE condition1 AND condition2;
> ```

> #### The code below returns data which meet EITHER condition1 OR condition2.
>
> ```
> SELECT * FROM your_table
> WHERE condition1 OR condition2;
> ```

> #### The code below returns data which does NOT meet condition1
>
> Just remember that `NOT` comes directly after `WHERE`
>
> ```
> SELECT * FROM your_table
> WHERE NOT condition1;
> ```

### Parentheses can be used for operator precedence!

> #### You can use parentheses for operation precedence
>
> What will be the result for the query statement shown below?
>
> ```
> | id  | product | category  | price |
> | --- | ------- | --------- | ----- |
> | 1   | shirt   | clothes   | 3     |
> | 2   | pants   | clothes   | 5     |
> | 3   | bed     | furniture | 5     |
> | 4   | chair   | furniture | 6     |
> | 5   | nike    | shoes     | 3     |
>
> SELECT * FROM inventory WHERE (category = 'furniture' OR category = 'clothes') AND price = 5
> ```

## Part 2-3. `OR` VS `IN` / `LIKE` with `%` and `_`

### Multiple `OR`s in the same column? Use `IN`!

| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | shirt   | clothes   | 3     |
| 2   | pants   | clothes   | 5     |
| 3   | bed     | furniture | 5     |
| 4   | chair   | furniture | 6     |
| 5   | nike    | shoes     | 3     |

`SELECT * FROM inventory WHERE category = 'furniture' OR category = 'clothes'` will return data on row 1 through 4.

This query statement is simply and equivalently expressed as  
`SELECT * FROM inventory WHERE category IN ('furniture', 'clothes')`

Imagine the case when you want to pull data related to thousands values of a single column, but NOT the whole values of that column. Then, you might repeat `OR` countlessly. For this case, `IN` will rescue.

Using `IN` will be also easier to read, as we might not want to see heavily repeated `OR column_name = ... OR column_name = ... OR ...`.

You can only use `IN` for values included in the **SAME** column. For example, you cannot simplify the following statement using `IN`.

```
SELECT \* FROM inventory WHERE category = 'clothes' OR price = 3;
```

Spoiler Alert! We can actually use `SELECT` **INSIDE** `IN`. This is one of the examples for SQL subquery. We will look into it on Part 2-5.

### `LIKE` is useful "ONLY" with `%` and `_`

`LIKE` helps you find values **including** certain values you want to filter. Let's learn with the `inventory` table shown below.

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

### `LIKE` with `%`

`%` means any string regardless the number of its characters. Let's dive into the examples.

> #### LIKE 'VALUE%'
>
> ```
> SELECT * FROM inventory WHERE product LIKE 'shirt%'
> ```
>
> This statement allows us to display any values that starts with "shirt". Actually, there is nothing that starts with "shirt" in the example table.

> #### LIKE '%VALUE'
>
> ```
> SELECT * FROM inventory WHERE product LIKE '%shirt'
> ```
>
> This statement allows us to display any values that ends with "shirt". You can find what would be displayed! See the product name which ends with "shirt".

> #### LIKE '%VALUE%'
>
> ```
> SELECT * FROM inventory WHERE product LIKE '%shirt%'
> ```
>
> This statement allows us to display any values that contains "shirt", because `%` is appended before and after "shirt". Guess what will be displayed!

### `LIKE` with `_`

`_` plays a similar role as `%` did, but it **cares** about the number of characters. Let's dive into the examples.

> #### LIKE '\_VALUE'
>
> ```
> SELECT * FROM inventory WHERE product LIKE '_shirt'
> ```
>
> Let's count the number of `_`. There is only **one** \_ , isn't it? So, this statement will return data whose `product` value has a single charactor followed by "shirt". So, it will return a row for product `tshirt`. (**NOT** `tshirt misc`, do you see why? If you want to get a row for `tshirt misc`, what should the query statement look like?)

> #### LIKE 'VALUE\_'
>
> Similarly, the statement below will return data whose `product` value has "shirt" followed by two characters exactly
>
> ```
> SELECT * FROM inventory WHERE product LIKE 'shirt__'
> ```
>
> `LIKE '_VALUE_'` is possible, of course!

### `%` and `_` come together

> #### `%` and `_` can be used together!
>
> You can mix `%` and `_`! The statement below will return data whose `product` value has a single character followed by "shirt" and ends with any string (or
> just ends with no trailing character.)
>
> ```
> SELECT * FROM inventory WHERE product LIKE '_shirt%'
> ```

> #### `%` and `_` can be in-between characters of string!
>
> ```
> SELECT * FROM inventory WHERE product LIKE 'nike%young'
> ```
>
> The statement above is valid. It will return data whose`product` value starts with `nike` and ends with `young`! Remember that `%` and `_` do not have to be at the beginning or end!

### PRO-TIP 1 : **BE CAREFUL** to use `LIKE` for a `CHAR()` data type

I dare say that you might come across the errors shown below, when you use `LIKE` with `%` and `_` for `CHAR()` data.

| id  | product | category  | price |
| --- | ------- | --------- | ----- |
| 1   | nike    | clothes   | 3     |
| 2   | adidas  | clothes   | 5     |
| 3   | tshirt  | clothes   | 5     |
| 4   | chair   | furniture | 4     |

Let's assume that a data type for `product` column is `CHAR(10)`. Then, what will be the result for `LIKE '%chair'`? Using what we have learned so far, I think that most of you would say 'chair', because '%chair' means any string (including no character) followed by `chair`. But actually, it will return **NOTHING**. What happens here?

By declaring a type of `product` column as `CHAR(10)`, if you pass a string `chair` into that column, the table will add trailing spaces to make each string's length 10 **exactly**. So, `'chair'` is actually saved as `'chair_____'`, and this string does not suffice `LIKE '%chair'`, because `%chair` looks for a string which ends with `chair` clearly.

If `LIKE` with `%` and `_` does not work as you intend, it will be always useful to check if you play with a `CHAR` data type! :smile:

### PRO-TIP 2 : Using `%` too many times is actually inefficient.

Using `%` too many times to query the DB is actually not the best. This problem is related to `index` problem, which we will look into later. If you can output the same results with some operators not too complicatedly, I would recommend to go for them without using `%` too much. Well, `%` is the easiest to use, because this is a wild-card! :sweat_smile:

## Part 2-4. Statistics / Some NUMBER statements / Some STRING statements

Below is the `customers` table showing the list of users for JAE Platinum Card.

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

### Statistics with `MAX`, `MIN`, `AVG`, and `SUM`

> This is for a quick review.
> `SELECT total-amount-spent FROM customers` will return the whole data on `total-amount-spent` column.

> #### `MAX(column_name)`
>
> ```
> SELECT MAX(total-amount-spent) FROM customers
> ```
>
> The statement above will return the maximum value of `total-amount-spent` values. **REMEMBER** that this does not return a whole row which contains the corresponding maximum value. It just returns the maximum value of `total-amount-spent` shown as below.
>
> ```
> |  MAX(total-amount-spent) |
> |    ------------------    |
> |          150000          |
> ```

> #### `MIN(column_name)`
>
> ```
> SELECT MIN(total-amount-spent) FROM customers
> ```
>
> Similarly, the statement above will return the minimum value of `total-amount-spent` values shown as below.
>
> ```
> | MIN(total-amount-spent) |
> |   -------------------   |
> |           100           |
> ```

> #### `AVG(column_name)`
>
> ```
> SELECT AVG(num-of-late-payments) FROM customers
> ```
>
> The statement above will return the average value of `num-of-late-payments`.

> #### `SUM(column_name)`
>
> ```
> SELECT SUM(num-of-late-payments) FROM customers
> ```
>
> The statement above will return the sum of `num-of-late-payments`.

### `COUNT()`, `AS`, `DISTINCT`, and `LIMIT`

Let's recall the `customers` table again.

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

> #### `COUNT()` to count the number of rows
>
> ```
> SELECT COUNT(total-amount-spent) FROM customers
> ```
>
> The statement above will return the **number** of rows.
>
> Someone asks me : "Would `SELECT COUNT(*) FROM customers` return the same result above?" YES, it does. The point is that `COUNT` just returns the number of rows.

> #### `AS` to rename a column as an alias.
>
> Let's focus on the column name of the data which is returned by `MAX`, `MIN`, etc...
>
> ```
> SELECT MAX(total-amount-spent) FROM customers
> ```
>
> ```
> |  MAX(total-amount-spent) |
> |--------------------------|
> |          150000          |
> ```
>
> What if we want to use a customized name for `MAX(total-amount-spent)`? Then, we should use an `AS` keyword!
>
> ```
> SELECT MAX(total-amount-spent) AS maximum-spent FROM customers
> ```
>
> See tbat the column name changes!
>
> ```
> |       maximum-spent      |
> |--------------------------|
> |          150000          |
> ```

> #### `DISTINCT` to remove repeated data!
>
> ```
> SELECT DISTINCT num-of-late-payments FROM customers;
> ```
>
> `0` and `1` appear twice on the `num-of-late-payments` column. But, if you add a `DISTINCT` keyword, `0` and `1` will be shown only once on the table as shwon below.
>
> ```
>
> | num-of-late-payments |
> | -------------------- |
> |          0           |
> |          1           |
> |          2           |
> |          3           |
> |          5           |
> |          8           /
> ```

You can generate your own stats based on the results outputted with `DISTINCT`. Sometimes, you might have the chance to make some stats based on data without any redundant data. So, let's just memorize that we can generate many stats using `DISTINCT` data only like `SELECT AVG(DISTINCT your_column) from your_table`

> #### `LIMIT` to find some values
>
> We already learned LIMIT, MAX, and MIN. Even though we can get some maximum/minimum values from the table, it is frequently useful to get them by using LIMIT. In addition, using LIMIT will help you get data like TOP 5 VIP customers, LOWEST 10 users, and etc.
>
> ```
> SELECT * FROM customers ORDER BY total-amount-spent DESC:
> ```
>
> The query above actually returns a maximum value of total-amount-sepnt as `SELECT MAX(total-amount-spent) FROM card;` does.  
> It is still important to know that you can query a set of some maximum/minimum values using LIMIT. MAX and MIN are not always best keywords to get them in some cases.

### Some useful NUMBER statements

We don't have to memorize all the statements shown below. It is just important to know that these functions **exist**. If you forget them, just google "SQL number functions"

> #### Simple calculations are available!
>
> For a `total-amount-spent` column in the `customers` table, we know that each amount includes 10% VAT. How can we calculate the amount except that tax amount (Which is equivalent to 90% of a `total-amount-spent`)?
>
> ```
> SELECT 0.9 * total-amount-spent FROM customers; // it's simple!
> ```
>
> #### We can also do simple calculations using columns
>
> `SELECT (column1 / column2) FROM your_table;` will return a column1 per column2 value for each row! You might also want to use `AS` to give a meaningful name to it!

> #### Some examples for NUMBER statements
>
> You don't have to memorize the queries below. There are also many other NUMBER queries including the queries below.
>
> #### `GREATEST`, `LEAST` : select a max/min value in a single row or a set of numbers
>
> Don't mix up these keywords with `MAX` and `MIN`. `MAX` and `MIN` return a max/min value for a single column!
>
> ```
> SELECT GREATEST(5, 3, 2, 1, 4);
> SELECT LEAST(5, 3, 2, 1, 4);
> ```
>
> #### `FLOOR`, `CEIL` : round up/down to the nearest integer
>
> ```
> SELECT FLOOR(10.1); // 10
> SELECT FLOOR(10.9); // 10
> SELECT CEIL(10.1); // 11
> SELECT CEIL(10.9); // 11
> ```
>
> #### `ROUND`, `TRUNCATE` : more sophiscated round functions
>
> ROUND(number, decimals) : Round to the decimals
>
> ```
> ROUND(9.566, 2); // result : 9.57
> ```
>
> TRUNCATE(number, decimals) : Truncate any number below the decimals (Round down to the decimals)
>
> ```
> TRUNCATE(9.566, 2); // result : 9.56
> ```
>
> #### `POWER` : yes, that "power" function you already know
>
> ```
> SELECT POWER(4,2); // 4 to the 2 = 4^2 = 16
> ```
>
> #### `ABS` : absolute value of the number
>
> ```
> SELECT ABS(-100); // result : 100;
> ```

Again, don't memorize the queries above! It is much more important to remember that many useful NUMBER statements wait for you who want to manipulate some number data more easily!

### Some useful STRING statements

Again, we don't have to memorize all the statements shown below. Let's just remember that they **exist**. We can search by googling "SQL string functions". Let's use a simple table shown below to learn some STRING examples.

| first-name | last-name |
| ---------- | --------- |
| Jaehoon    | Sung      |
| Edward     | Hu        |
| James      | Yoon      |

> #### `CONCAT` : concatenation! adds two or more strings together.
>
> ```
> SELECT CONCAT(first-name, ' ', last-name) AS full-name FROM table
>
> | full-name    |
> | ------------ |
> | Jaehoon Sung |
> | Edward Hu    |
> | James Yoon   |
> ```
>
> Postgres, Oracle use `||` symbol for concatenation. Some DBMSs use `+` symbol.
>
> ```
> SELECT first-name || ' ' || last-name FROM your_table;
> ```
>
> #### `TRIM` : removes leading & trailing space (or other characters if designated)
>
> ```
> SELECT TRIM(column_name) FROM your_table;
> ```
>
> #### `REPLACE` : replace all of matching substrings with a new substring.
>
> REPLACE(whole_string, a_string_you_want_to_erase, a_string_you_want_to_add);
>
> ```
> SELECT REPLACE("Hi, I am from Korea", "Korea", "Canada"); // result : "Hi, I am from Canada"
> ```
>
> search in `REPLACE` is **case-insensitive!**
>
> #### `SUBSTR` : extract a substring from a string as you want
>
> SUBSTR(whole_string, nth_character_where_you_want_to_start_extract, num_of_chracters_you_want_to_extract_from_your_nth_chracter);
>
> ```
> SELECT SUBSTR('abcdef', 3, 2); // starts to extract two chracters from the 3rd chracter. result : "cd"
> ```
>
> #### `INSERT` : a more sophicated `REPLACE` method
>
> See an example below. It is easier to figure out how it works with the example!
>
> ```
> SELECT INSERT('test@email.com', 1, 4, 'Jaehoon')
>
> // The query above says : please take a substring from the 1st to the 4th character, and replace it with "Jaehoon"
> // result : Jaehoon@email.com
> ```

## Part 2-5. `GROUP BY` / `SELECT` in `SELECT` : sub-query!

## Part 3-1. Normal Form : 1NF. 2NF. 3NF. etc...

## Part 3-2. Join / CRUDing data

## Part 5. Procedure / Function / Index / Transaction

## Part 6. DB Hosting / ERD (Entity Relationship Diagram) / SQL Injection

```

```
