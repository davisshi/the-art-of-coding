1.  [Designgurus](https://www.designgurus.io/home) / [Blogs](https://www.designgurus.io/blog) / system-design-interview-basics-cap-vs-pacelc

![Image](https://www.designgurus.io/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Farslan.0d4d8810.jpeg&w=128&q=75)

Arslan Ahmad

February 23rd, 2023

[System Design Interview Basics: CAP vs. PACELC](https://www.designgurus.io/blog/system-design-interview-basics-cap-vs-pacelc)
==============================================

What is CAP theorem and how PACELC extends it?

![Image](https://www.designgurus.io/_next/image?url=https%3A%2F%2Fstorage.googleapis.com%2Fdownload%2Fstorage%2Fv1%2Fb%2Fdesigngurus-prod.appspot.com%2Fo%2F0ed20d9512730e413bd876601%3Fgeneration%3D1714367358048205%26alt%3Dmedia&w=3840&q=75)

In distributed systems, different types of failures can occur, e.g., servers can crash or fail permanently, disks can go bad resulting in data losses, or network connection can be lost, making a part of the system inaccessible. How can a distributed system model itself to get the maximum benefits out of different resources available? What are the guiding principles to help distributed systems choose a desirable balance between various distributed characteristics?

> Check [Grokking the System Design Interview](https://www.designgurus.org/course/grokking-the-system-design-interview) to learn about important distributed system concepts.

CAP theorem to the rescue
-------------------------

CAP theorem states that it is impossible for a distributed system to simultaneously provide all three of the following desirable properties:

Consistency ( C ): All nodes see the same data at the same time. This means users can read or write from/to any node in the system and will receive the same data. It is equivalent to having a single up-to-date copy of the data.

Availability ( A ): Availability means every request received by a non-failing node in the system must result in a response. Even when severe network failures occur, every request must terminate. In simple terms, availability refers to a system's ability to remain accessible even if one or more nodes in the system go down.

Partition tolerance ( P ): A partition is a communication break (or a network failure) between any two nodes in the system, i.e., both nodes are up but cannot communicate with each other. A partition-tolerant system continues to operate even if there are partitions in the system. Such a system can sustain any network failure that does not result in the failure of the entire network. Data is sufficiently replicated across combinations of nodes and networks to keep the system up through intermittent outages.

According to the CAP theorem, any distributed system needs to pick two out of the three properties. The three options are CA, CP, and AP. However, CA is not really a coherent option, as a system that is not partition-tolerant will be forced to give up either Consistency or Availability in the case of a network partition. Therefore, the theorem can really be stated as: In the presence of a network partition, a distributed system must choose either Consistency or Availability.

![Image](https://storage.googleapis.com/download/storage/v1/b/designgurus-prod.appspot.com/o/docImages%2F63f7c3824890332fa0e7c691%2Fimg:702caa-0f-367-d57d-7640637d7e60.svg?generation=1677182403493045&alt=media)

CAP Theorem

Justification for the CAP theorem
---------------------------------

We cannot build a general data store that is continually available, sequentially consistent, and tolerant to any partition failures. We can only build a system that has any two of these three properties. Because, to be consistent, all nodes should see the same set of updates in the same order. But if the network loses a partition, updates in one partition might not make it to the other partitions before a client reads from the out-of-date partition after reading from the up-to-date one. The only thing that can be done to cope with this possibility is to stop serving requests from the out-of-date partition, but then the service is no longer 100% available.

What is missing in the CAP theorem?
-----------------------------------

We cannot avoid partition in a distributed system, therefore, according to the CAP theorem, a distributed system should choose between consistency or availability. ACID (Atomicity, Consistency, Isolation, Durability) databases, such as RDBMSs like MySQL, Oracle, and Microsoft SQL Server, chose consistency (refuse response if it cannot check with peers), while BASE (Basically Available, Soft-state, Eventually consistent) databases, such as NoSQL databases like MongoDB, Cassandra, and Redis, chose availability (respond with local data without ensuring it is the latest with its peers).

One place where the CAP theorem is silent is what happens when there is no network partition? What choices does a distributed system have when there is no partition?

PACELC theorem to the rescue
----------------------------

The PACELC theorem states that in a system that replicates data:

-   if there is a partition ('P'), a distributed system can tradeoff between availability and consistency (i.e., 'A' and 'C');
-   else ('E'), when the system is running normally in the absence of partitions, the system can tradeoff between latency ('L') and consistency ('C').

![Image](https://storage.googleapis.com/download/storage/v1/b/designgurus-prod.appspot.com/o/docImages%2F63f7c3824890332fa0e7c691%2Fimg:554083-b7bf-0fb-501a-71a7bc8ce4cf.svg?generation=1677182345624388&alt=media)

PACELC Theorem

The first part of the theorem (PAC) is the same as the CAP theorem, and the ELC is the extension. The whole thesis is assuming we maintain high availability by replication. So, when there is a failure, CAP theorem prevails. But if not, we still have to consider the tradeoff between consistency and latency of a replicated system.

Examples
--------

-   Dynamo and Cassandra are PA/EL systems: They choose availability over consistency when a partition occurs; otherwise, they choose lower latency.
-   BigTable and HBase are PC/EC systems: They will always choose consistency, giving up availability and lower latency.
-   MongoDB can be considered PA/EC (default configuration): MongoDB works in a primary/secondaries configuration. In the default configuration, all writes and reads are performed on the primary. As all replication is done asynchronously (from primary to secondaries), when there is a network partition in which primary is lost or becomes isolated on the minority side, there is a chance of losing data that is unreplicated to secondaries, hence there is a loss of consistency during partitions. Therefore it can be concluded that in the case of a network partition, MongoDB chooses availability, but otherwise guarantees consistency. Alternately, when MongoDB is configured to write on majority replicas and read from the primary, it could be categorized as PC/EC.

Conclusion
----------

The PACELC theorem states that in a system that replicates data: CAP and PACELC theorems help distributed systems choose a desirable balance between various distributed characteristics like Consistency, Availability, Partition Tolerance, and Latency. Please take a look at [Grokking the System Design Interview](https://www.designgurus.io/course/grokking-the-system-design-interview) and [Grokking the Advanced System Design Interview](https://www.designgurus.io/course/grokking-the-advanced-system-design-interview) for some good examples of system design basics.

Want to learn more about system design interviews, check the following posts from [Design Gurus](https://www.designgurus.io/):\
[1] [System Design Interviews: A Step-By-Step Guide](https://www.designgurus.io/blog/step-by-step-guide)\
[2] [System Design Interview Question: Designing a URL Shortening Service](https://www.designgurus.io/blog/url-shortening)

CAP Theorem

System Design Fundamentals

System Design Interview

Scalability