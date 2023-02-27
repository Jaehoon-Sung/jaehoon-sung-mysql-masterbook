# Part 2.

## Part 2-1. SQL Data Types

```
COMING SOON!
```

## Part 2-2. Columns with constraints : safe update & easy debug!

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

Assume that you are a college student. Then, what value can be used as an unique key to distinguish your information from others? Your name, age, or major cannot be used, because there can be students who have the same name, age, or major. Maybe, your student ID can be. If a college gives each student an unique student ID, it can distinguish each student regardless of other values. Here, the column for student ID is called `PRIMARY KEY`, which helps you distinguish each row data.

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
