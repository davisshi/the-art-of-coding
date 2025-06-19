[Wide Column Store Definition](https://www.scylladb.com/glossary/wide-column-store/)
----------------------------

A Wide Column Store, also known as a column store, column family store, columnar data store, or column store database, is a type of [NoSQL database](https://www.scylladb.com/resources/what-is-nosql/) that organizes related data in column families rather than traditional rows, allowing large amounts of data to be stored across a distributed column store architecture.

![Diagram depicting data organized in column families rather than traditional rows.](https://www.scylladb.com/wp-content/uploads/Wide-column-store-diagram.png)

Wide Column Store FAQs

What's the Difference Between a Row Store vs. Column Store?
-----------------------------------------------------------

The difference between row store and column store databases lies in their data structures, which are organized in fundamentally different ways. A relational database stores data in tables, where data is queried by row, and where all rows have the same columns. A NoSQL wide column store permits rows to have differing columns, resulting in a more flexible data model that provides the ability to evolve and adapt over time. In a wide column store, each column is stored separately, enabling data to be partitioned more easily across [distributed database](https://www.scylladb.com/glossary/distributed-database/) systems.

What's the Difference Between a Document Store vs. Column Store?
----------------------------------------------------------------

To understand the difference between a wide column versus document store database, let's first clarify what a document store does. In a document store, the key is associated with a complex object, typically stored in Javascript Object Notation (JSON) format. Examples of document databases include MongoDB and Azure DocumentDB. In contrast to a document store, a wide column store is less specialized. A Cassandra wide column store, for example, supports simple numeric and string data types, but it can also use a collection or list as a column data type for storing multiple values or even nested values.

What are the Advantages of Column Store Databases?
--------------------------------------------------

Every type of database has benefits and limitations. Relational row-structured databases are ideal for querying a few rows with multiple columns. A wide column store is better for aggregated data from a single column over millions of rows. Column stores are also easily partitioned, enabling the distribution of large datasets across multiple nodes for high availability and low-latency.

Explain How to Create a Column Store Index
------------------------------------------

Indexed appropriately, a column store [NoSQL database](https://www.scylladb.com/learn/nosql/) can be very efficient for searching data. An important consideration is when a column benefits from being indexed. In general, a column should be indexed when it has low cardinality, that is, when it has significantly fewer unique values than rows, when it is not a counter data type, and when it is not frequently updated or deleted. The overhead of frequent deletions and updates or scans of the entire index can impact index performance.

The CQL syntax to create an index on an Apache Cassandra column store is like this:

CREATE INDEX [IF NOT EXISTS] [indexName] ON [keySpaceName.]tableName (KEYS (columnName))

Let's look at a simple NoSQL wide column store database example of a column index:

CREATE INDEX employeeStateIndex ON Employees (KEYS (State))

What's the Best Open Source Column Store Database?
--------------------------------------------------

One of the best-known open source column store NoSQL databases is [Apache Cassandra](https://www.scylladb.com/resources/introduction-to-apache-cassandra/), which is a distributed wide column store database. ScyllaDB's [open source](https://www.scylladb.com/learn/open-source-database/) NoSQL wide column store database, ScyllaDB, is fully compatible with Cassandra, while also delivering higher performance, predictable low latencies, and lower operational overhead. ScyllaDB strives to be the best columnar store database.

Does ScyllaDB Offer Solutions for Wide Column Store?
----------------------------------------------------

ScyllaDB offers [ScyllaDB as a high-performance](https://www.scylladb.com/product/), distributed NoSQL wide column store database. In industry-standard performance benchmarks, ScyllaDB demonstrates [high performance](https://www.scylladb.com/product/), along with the ability to scale across distributed nodes for predictable [low latency](https://www.scylladb.com/glossary/low-latency-database/) and high availability. Implemented in C++ instead of Java, ScyllaDB is built on an advanced, open-source, cloud-native framework for high-performance server applications on modern hardware.
