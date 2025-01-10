[ByteByteGo Newsletter](https://blog.bytebytego.com/)
=====================================================

Upgrade to paidSign in

[Understanding Message Queues](https://blog.bytebytego.com/p/understanding-message-queues)
============================

[![](https://substackcdn.com/image/fetch/w_36,h_36,c_fill,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc9941c68-e5b7-4b93-be75-df7cc4ffef02_504x540.png)](https://substack.com/@bytebytego399569)

[ByteByteGo](https://substack.com/@bytebytego399569)

Jan 09, 2025

Asynchronous communication has become an important strategy for modern software systems, particularly in distributed and large-scale applications. 

Unlike synchronous communication, where a sender waits for a response before proceeding, asynchronous communication allows processes to continue without waiting. This has a significant impact on the system's performance, scalability, and resilience.

Some real-world scenarios where async communication shines are as follows:

-   An online store where an order placement triggers real-time calls to inventory, payment, and shipping services. If any of these services experience latency or downtime, the order process stalls, leading to poor user experience and lost revenue. Using a message queue, the order service can immediately enqueue messages for inventory, payment, and shipping.

-   IoT systems like smart home devices often involve thousands of sensors sending data to central servers. A synchronous approach can overwhelm the server during peak activity, leading to data loss or delayed responses. Message queues allow sensors to send data without waiting for processing.

-   In a microservices architecture, tightly coupled services communicating synchronously can create cascading failures. With message queues, services communicate indirectly, reducing dependency and allowing independent scaling.

These are just a few examples. There are several potential scenarios where async communication is important. But what makes async communication possible?

This is where message queues come into the picture.

Message queues act as intermediaries, enabling asynchronous between producers (senders) and consumers (receivers). In this article, we'll look at understanding how message queues work, the various terminologies involved, and the patterns that can be implemented using them.

[![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ae8b491-b794-446b-8ca5-25ac552161be_1417x1600.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2ae8b491-b794-446b-8ca5-25ac552161be_1417x1600.png)

What is a Message Queue?
------------------------

![](https://substackcdn.com/image/fetch/w_64,h_64,c_fill,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F10cd1afb-9a92-433e-bbf4-f726eb8ffdb3_375x375.jpeg)

Continue reading this post for free, courtesy of Alex Xu.
---------------------------------------------------------

|  |  | Claim my free post |

[Or upgrade your subscription. **Upgrade to paid**](https://blog.bytebytego.com/subscribe?simple=true&next=https%3A%2F%2Fblog.bytebytego.com%2Fp%2Funderstanding-message-queues&utm_source=paywall&utm_medium=web&utm_content=154385514&just_signed_up=falsesimple=true&utm_source=paywall&utm_medium=email&utm_content=154385514&next=https://blog.bytebytego.com/p/understanding-message-queues)