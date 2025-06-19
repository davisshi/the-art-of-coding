[Wide-column Database](https://www.scylladb.com/glossary/wide-column-database/)
====================

[ Back to Technical Glossary](https://www.scylladb.com/technical-glossary)

Wide-column Database Definition
-------------------------------

A wide-column database is a NoSQL database that organizes data storage into flexible columns that can be spread across multiple servers or database nodes, using multi-dimensional mapping to reference data by column, row, and timestamp.

![Diagram depicting wide column database.](https://www.scylladb.com/wp-content/uploads/Wide-column-Database-diagram.png)

Wide-column Database FAQs

What is a Wide-column Database?
-------------------------------

A wide-column database is a type of [NoSQL database](https://www.scylladb.com/resources/what-is-nosql/) in which the names and format of the columns can vary across rows, even within the same table. Wide-column databases are also known as column family databases.

What Are the Advantages of a Wide-column Database?
--------------------------------------------------

Benefits of a wide-column NoSQL database include speed of querying, scalability, and a flexible [data model](https://www.scylladb.com/glossary/data-model/).

Masterclass: Data Modeling for NoSQL Databases
----------------------------------------------

![](https://www.scylladb.com/wp-content/uploads/Screenshot-2023-09-26-at-17.39.23-300x228.png)Looking for extensive training on about data modeling for NoSQL Databases? Our experts offer a 3-hour masterclass that assists practitioners wanting to migrate from SQL to NoSQL or advance their understanding of NoSQL data modeling. This free, self-paced class covers techniques and best practices on NoSQL data modeling that will help you steer clear of mistakes that could inconvenience any engineering team.

You can access the complete course [here](https://lp.scylladb.com/nosql-data-modeling-masterclass-ondemand-register?siteplacement=resourcecenter).

How Does a Wide-column Store Database Differ from a Relational Database?
------------------------------------------------------------------------

A relational database management system (RDBMS) stores data in a table with rows that all span a number of columns. If one row needs an additional column, that column must be added to the entire table, with null or default values provided for all the other rows. If you need to query that RDBMS table for a value that isn't indexed, the table scan to locate those values will be very slow.

Wide-column NoSQL databases still have the concept of rows, but reading or writing a row of data consists of reading or writing the individual columns. A column is only written if there's a data element for it. Each data element can be referenced by the row key, but querying for a value is optimized like querying an index in a RDBMS, rather than a slow table scan.

![](https://www.scylladb.com/wp-content/uploads/Scylla-Mascot-NoSQL.png)

Learn essential strategies for wide column data modeling with [Apache Cassandra](https://www.scylladb.com/learn/apache-cassandra/introduction-to-apache-cassandra/) and ScyllaDB

[\
Watch Video\
](https://lp.scylladb.com/wbn-sql-nosql-data-modeling-registration)

Are Distributed Databases More Reliable?
----------------------------------------

A distributed key value database can be configured to store the same data in multiple nodes across locations. If a single node fails, the data is still available. You don't have to wait for the database to be restored. A geo-distributed database maintains concurrent nodes across geographical regions for resilience in case of a regional power or communications outage. The ability to store a single database across multiple computers requires an algorithm for replicating data that is transparent to the users.

How Does a Distributed Database Stay in Sync?
---------------------------------------------

ScyllaDB sends all write operations to all nodes, without having to wait for all nodes to report a successful write. The level of data consistency required is configurable. Read operations can query one or multiple nodes, depending on the Consistency Level configured. When the Consistency Level is set to Quorum, for example, a majority of the nodes have to agree on the value returned. The ScyllaDB Repair process runs in the background, updating nodes that are out of sync due to a write failure on that node.

What's the Difference Between Wide-Column and Key Value Store NoSQL databases?
------------------------------------------------------------------------------

NoSQL databases do not store their data in related tables, but NoSQL data stores include four major implementations: Key-Value databases, Wide-column databases, Document databases, and Graph databases. We'll just look at the first two, because they are similar. Key-Value databases are the simplest model and can be thought of as a configuration file or a two-column table of keys with an associated value. Wide-column databases expand that key-value store concept across multiple columns, but only the columns that are needed for that record.

What's the Difference Between a Columnar Database vs. a Wide-column Database?
-----------------------------------------------------------------------------

A columnar database stores each column separately on disk. This allows high compression of "runs" of data --- the same value repeated a number of times in a column can be efficiently stored.

A wide-column database is a row-based data store that supports a complex index comprised of multiple columns used for clustering data for fast querying.

Is a Wide-column Database Highly Scalable?
------------------------------------------

Wide-column databases are highly scalable because the data is stored in individual columns which can be sharded or partitioned across multiple servers.

Can a Wide-column Database Support Different Columns on Some Rows?
------------------------------------------------------------------

Wide-column databases don't have a defined table schema, which leaves them flexible to have certain columns only apply to certain records.

How Do I Add Columns in a Wide-column Database?
-----------------------------------------------

Developers often encounter the need to add an attribute to a data model after deployment. For example, a business might require customer profiles to be augmented with a new attribute in order to support a new service. In a traditional relational database, the developer would add a new column to the entire table, with null or default values taking up space in all the other rows. Even worse, the developer might locate an unused legacy column to repurpose for this piece of data that didn't fit the new schema.

With a wide-column database, developers can simply add elements to a new column, without impacting existing columns or the data they hold.

What are Wide-column Database Use Cases?
----------------------------------------

Wide-column databases are ideal for use cases that require a large dataset that can be distributed across multiple database nodes, especially when the columns are not always the same for every row.

-   Log data
-   IoT (Internet of Things) sensor data
-   Time-series data, such as temperature monitoring or financial trading data
-   Attribute-based data, such as user preferences or equipment features
-   Real-time analytics

What are Wide-column Database Examples?
---------------------------------------

Some common wide-column store database examples include [Apache Cassandra](https://cassandra.apache.org/), [ScyllaDB](https://www.scylladb.com/), [Apache HBase](https://hbase.apache.org/), [Google BigTable](https://cloud.google.com/bigtable), and [Microsoft Azure Cosmos DB](https://azure.microsoft.com/en-us/services/cosmos-db/). When it comes to a wide-column database, [Cassandra](https://www.scylladb.com/resources/introduction-to-apache-cassandra/) is often mentioned first because of its pioneering work. But ScyllaDB is Cassandra rewritten in the C++ programming language, making it faster and more reliable. ScyllaDB has continued to evolve as a notable wide-column database Cassandra.

Does ScyllaDB Offer a Wide-column Database?
-------------------------------------------

Yes, ScyllaDB offers a multi-model database that supports flexibly modeling your data as a wide-column store or a simple key-value store. ScyllaDB enables organizations to scale your data across [distributed database](https://www.scylladb.com/glossary/distributed-database/) nodes for fast performance and high availability. By many estimates, ScyllaDB is the best wide column database on the market today.