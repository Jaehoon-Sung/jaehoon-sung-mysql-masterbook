# Part 0. Types of Database

## Key-Value Database

While this masterbook primarily focuses on relational databases, it's important to understand non-relational databases as well. A non-relational database is a type of database that does not use tables with a tabular schema of rows and columns. Instead, non-relational databases use different data models such as key-value pairs, documents, or graphs.

One type of non-relational database is the `Key-Value Database`, which uses a simple structure based on key-value pairs to store data (similar to an object in JavaScript). Key-Value Databases are often used to implement simple sub-databases such as caches or session storage. An example of a Key-Value Database is the `Redis` DBMS, which I will introduce below.

```
| KEY          | VALUE        |
| ------------ | ------------ |
| name         | Jaehoon Sung |
| day of birth | March 15th   |
```

`Redis` is a popular open-source DB that supports the key-value database. One important thing to note about Redis is that it is an `in-memory` database, meaning that it stores data in RAM rather than on a hard disk drive (HDD). Since RAM can process data much faster than HDD, Redis can quickly manage its data by processing it in RAM. This is why developers often choose to use Redis, even though it primarily supports a key-value pair. Specifically, Redis is useful for processing frequently-accessed local data quickly (e.g., caches)! However, it's essential to remember that Redis mainly supports the key-value pair. While newer versions of Redis support some other types of DB, they are not as popular.

## Relational Database

You have likely used relational databases before, perhaps by creating a spreadsheet in your daily life! But why is this type of database called `relational`? Despite the name, it has nothing to do with "relationship." Instead, the term derives from the mathematical concept of "Relation," which is a critical concept in matrix and linear algebra. To manage relational databases more efficiently, developers have researched ways to reduce data redundancy, estabilish strong "relationships" between tables, and manage databases using these "relationships". This process is known as `Normalization`, which we will cover in Part 2.

Relational databases are the most popular type of database because they provide a stable environment for data transaction. Many popular relational databases offer functions that ensure safe transactions by satisfying `ACID` properties! ACID refers to a set of properties which a database must have to ensure data validity : `Atomicity`, `Consistency`, `Isolation`, and `Durability`.

Famous relational databases include `Oracle`, `MySQL`, `PostgreSQL`, `MicrosoftSQL Server`, `MariaDB`, `SQLite`, `IBM DB2`, `Google Cloud Spanner`, and more.. According to the StackOverflow 2022 statistics, six of the top nine databases were relational databases.

## Graph Database

If you want to quickly visualize "relationships" among data, consider using a `Graph Database`. For example, when you log into your social media account, you can view your list of friends. Then, when you navigate to one of your friend's profiles, you can view their list of friends. Similarly, if you're managing the departure and arrival status of all airports worldwide, a graph database can help you model the relationships among the data. You can even use the graph database to generate visual representations of the data. The language used to query graph databases is called `Graph Query Language`.

Some examples of famous graph databases include `Neo4j`, `Sparsity`, `OrientDB`, `ArangoDB` and others.. Below is one of the examples which generate visual representations using `Neo4j`.

<p align = "center">
  <img src="https://neo4j.com/developer/_images/graph-examples-movies-example.png" width="70%"></img>
</p>

## Document Database

A `Document Database` looks very similar to the folders you use in Windows or in Finders on Mac. Technically, these folders are called "collections," and within them, there are many "documents". Data in each document is stored in a JSON-type format. But why do we use a document database? It offers more flexibility than a relational database while still maintaining structured and hierarchical properties. For example, with a relational database, you must define what types of data will be stored in each column. However, this is not necessary when using a document database. Furthermore, you can simply add any new set of data with different contexts in existing document databases whenever you want to, which is strictly prohibited in relational databases. To make changes in a relational database, you would have to redefine the whole schema of the database or write commands to let the relational DBMS know that you want to make changes.

Not only do document databases provide more flexibility, but they also allow for distributed processing and horizontal scaling, making them ideal for services that require multiple inputs/outputs. However, this added flexibility means less consistency. Since document databases are easy to update and copy/paste, each document has less consistency with others and has the potential to undermine the ACID rule. (Data in a document database is not normalized.)

Famous document databases include `mongoDB`, `FireStore`, and `CouchDB`.

##
