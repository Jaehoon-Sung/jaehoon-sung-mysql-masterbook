# Part 0. Types of Database

## Key-Value Database

Think of an object we use in Javascript. This database has the same structure just shown as below. A `Key-Value Database` is a non-relational database that uses a key-value pair to store data. This `Key-Value Database` is used frequently to implement a simple sub-database. (More practical examples are coming below.)

```
| KEY          | VALUE        |
| ------------ | ------------ |
| name         | Jaehoon Sung |
| day of birth | March 15th   |
```

`Redis` is a popular open-source DB that supports the key-value database. One important thing to note about Redis is that it is an `in-memory` database, meaning that it stores data in RAM rather than on a hard disk drive (HDD). Since RAM can process data much faster than HDD, Redis can quickly manage its data by processing it in RAM. This is why developers often choose to use Redis, even though it primarily supports a key-value pair. Specifically, Redis is useful for processing frequently-accessed local data quickly (e.g., caches)! However, it's essential to remember that Redis mainly supports the key-value pair. While newer versions of Redis support some other types of DB, they are not as popular.

## Relational Database

You've likely had experience using relational databases. That's exactly any spreadsheet you created and made in your daily life. But why is this type of database called `relational`? Contrary to what the name might suggest, it has nothing to do with "relationship". It derives from the mathematical term "Relation," a key concept in matrix and linear algebra. In order to improve the effciency of managing relational databases, developers have researched how to reduce data redundancy, estabilish strong "relationships" between tables, and manage databases using these "relationships". This process is actually called `Normalization`, which we will cover in Part 2.

Relational databases are the most popular type of database because I think they provide a stable environment for data transaction. Many popular relational databases offer functions to secure safe transactions by satisfying `ACID` properties! ACID refers to a set of properties which a database must have to ensure data validity : `Atomicity`, `Consistency`, `Isolation`, and `Durability`.

Famous relational databases include `Oracle`, `MySQL`, `PostgreSQL`, `MicrosoftSQL Server`, `MariaDB`, `SQLite`, `IBM DB2`, `Google Cloud Spanner`, and more..

## Graph Database

If you really want to see "relationships" among data at a glance, you might want to use `Graph Database`. For example, if you log in your social media account, you can see the list of your friends. Then, if you enter one of your friends' profiles, you might see that friend's list. Or, if you manage departure/arrival status of all airports in the world, you might want to describe it using a graph database. You can even visualize the data you manage using this graph database. The language we are using to manage graph database is called `Graph Query Language`.

Famous graph database : `Neo4j`, `Sparsity`, `OrientDB`, `ArangoDB` and etc..

## There are three more types of databases I think important; will update soon...

```
COMING SOON
```
