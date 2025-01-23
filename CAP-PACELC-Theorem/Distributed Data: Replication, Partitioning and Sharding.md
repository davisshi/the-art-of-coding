[Distributed Data: Replication, Partitioning and Sharding](https://medium.com/@nishantparmar/distribute-data-replication-partitioning-and-sharding-920a71481c1c)
========================================================

[![Nishant](https://miro.medium.com/v2/resize:fill:88:88/1*wRZfXfEA5wlAy_y6QXvT_A.jpeg)](https://medium.com/@nishantparmar?source=post_page-----920a71481c1c--------------------------------)

[Nishant](https://medium.com/@nishantparmar?source=post_page-----920a71481c1c--------------------------------)

Follow 76

There are two common ways data is distributed across multiple nodes.

Replication and Partitioning (Sharding, when assigned to different nodes)
-------------------------------------------------------------------------

![](https://miro.medium.com/v2/resize:fit:460/1*zIdOtye14qYFRwFqMWmZRQ.png)

Patterns for Distribute Data

![](https://miro.medium.com/v2/resize:fit:128/0*hCAaJKDD3TtPRunL.png)

Replication

**Replication** (Copying data)--- Keeping a copy of same data on multiple servers that are connected via a network.

![](https://miro.medium.com/v2/resize:fit:200/1*fqCMuxG46YTjDcJeqo0W3g.jpeg)

Partitioning

**Partitioning** --- Splitting up a large monolithic database into multiple smaller databases based on data cohesion. e.g. Horizontal (sharding) and Vertical (increase server size) partitioning.

![](https://miro.medium.com/v2/resize:fit:200/1*mARssEbh6DcyDegq224tGg.jpeg)

Sharding

> In this blog I will focus more on Sharding (Horizontal Partitioning) Vertical partitioning.

**Sharding** (Horizontal Partitioning)--- A type of horizontal partitioning that splits large databases into smaller components, which are faster and easier to manage. In other words --- Splitting up a large table of data horizontally i.e. row-wise.

Why to Shard a table?
=====================

A shard is an individual partition that exists on separate database server instance to spread load. It is needed when a dataset is too big to be stored in a single database.

As both the database size and number of transactions increase, so does the response time for querying the database. Costs associated with maintaining a huge database can also skyrocket due to the number and quality of computers you need to manage your workload. Data shards, on the other hand, have fewer hardware and software requirements and can be managed on less expensive servers.

Advantages of Sharding
======================

-   Solve Scalability Issue: With a single database server architecture any application experiences performance degradation. At some point, you will be running out of disk space. Database sharding fixes all these issues by partitioning the data across multiple machines.
-   High Availability: If an outage happens in sharded architecture, then only some specific shards will be down. All the other shards will continue the operation and the entire application won't be unavailable for the users.
-   Speed Up Query Response Time: In a sharded database a query has to go through fewer rows, and you receive the response in less time.
-   More Write Bandwidth: For many applications writings is a major bottleneck. With no master database serializing writes sharded architecture allows you to write in parallel and increase your write throughput.
-   Scaling Out: Sharding a database facilitates *horizontal scaling*, known as *scaling out*. In horizontal scaling, you add more machines in the network and distribute the load on these machines for faster processing and response.

Disadvantages of Sharding
=========================

-   Adds Complexity in the System: It's a complicated task and if it's not implemented properly then you may lose the data or get corrupt tables in your database. You also need to manage the data from multiple shard locations instead of managing and accessing it from a single-entry point. This may affect the workflow of your team which can be potentially disruptive to some teams.
-   Rebalancing Data: In a sharded database architecture, sometimes shards become unbalanced (when a shard outgrows other shards) and may create *database hotspot*. To overcome this problem and to rebalance the data you need to do re-sharding for even data distribution. Moving data from one shard to another shard is not a good idea because it requires a lot of downtime.
-   Joining Data from Multiple Shards is Expensive: In sharded architecture, you need to pull the data from different shards, and you need to perform joins across multiple networked servers. You can pull out the data and join the data across the network. This is going to be an expensive and time-consuming process. It adds latency to your system.
-   No Native Support: Sharding is not natively supported by every database engine.

Why to do data Replication?
===========================

Data Replication is the process of storing data in more than one site or node.

Advantages of full Replication
==============================

-   Keep data geographically close to users (and thus reduce latency)
-   Allow the system to continue working even if some of its parts have failed (and thus increase availability).
-   Scale out the number of servers that can serve read queries (and thus increase read thruputs).

Disadvantages of full Replication
=================================

-   Concurrency is difficult to achieve in full replication.
-   Slow update process as a single update must be performed at different databases to keep the copies consistent