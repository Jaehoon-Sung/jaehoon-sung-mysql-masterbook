# Part 0. Types of Database

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
