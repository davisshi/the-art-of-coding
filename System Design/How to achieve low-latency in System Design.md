How to achieve low-latency in System Design
================================================

Low latency can make or break your user experience --- I've seen it firsthand.

While working on Meta's distributed data store, battling latency was my biggest challenge. Even tiny delays caused system reliability issues and left users (and my team) frustrated.

So we pushed ourselves to find out: How do we build a system architecture so fast that users never feel a lag?

The good news is that I've got 5 proven solutions for latency.

Today, I'm sharing those techniques to help you design low-latency systems that keep things running smoothly -- and users happy.

In addition to 1200+ AI-powered courses & projects, access popular interview prep resources, including:

- **![💼](https://fonts.gstatic.com/s/e/notoemoji/15.1/1f4bc/32.png) **[AI Mock Interviews](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5rbg3qgyTW8wLKSR6lZ3lrW5_-qsr3nc085W5sXdyX3vKKqTVSPj5R4Lc7D-N3f8jxsbC4bRW367yQJ1gkn1MW63TmXk5lXb5LW2Vz7xH2tX_JBDTFLqMG9SHN7Rw_wj-lydxVGSJHx2hz-R_W927nqV49RdmMW3qPbDv6VL0htVyrR575xR599W7pSFYj8RH9XBW6JHcMv88cMBrW76xbHZ4XG03DW1C0zLb4sylcnW1vBpk65vCMbWW14dy253nV6PSW7pnvmW1Ss3JRN4zzx9CZds7pW5mFYY-7sWPGCW5d3pG61wNswnW4D6-Py4N3syqW1__ffW1tt_QsW6JzBGc1GXXWZW6gFSrd2xPtxWM9QZ4rHPt2kf9hYTgn04) (coding interviews, System Design, and more)
- **![🌐](https://fonts.gstatic.com/s/e/notoemoji/15.1/1f310/32.png) **[Grokking Modern System Design for Engineers & Managers](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5r8P5nR32W5BWr2F6lZ3lnW1qZyDz1P3ZDWVRKWCg7NtCVZN1CvxfM6d5TyV3zKFj5gqS8nW4LH3qw1dMYJmW6Lkb0K73Y3Y1W4Q1dfc99H0QpV9QJDR5Hnd1rW72SQ5m5L8tGyW3mlhf92VG1kFW1Hg4LM39hLyNW6Wjys88-K6brW2WLfKJ3VB5cGV2PdXR8nNv-nW3Gghwd4WjGx0W6j7Fb1475HVlW8gRRmN35X4PbW6k9sqj7NHDRtW1HZlTk7LCQVpW4ysMW67qyxnkVg5qgY4_kt46N2B4bY7GvtM_W7MzQz_1BdfXQW3gBcbb55-5wmW5RSnNZ5DDfJxW4bj6fY1-Wcf_N1mb_z3g4xjXW9gZkgg5YQ-wyW1byhhy7kp9yDW1lHKmK56VtD9W3_YK3S3Gv0q2VdZKfp66vS7nW1BcNwx8sjz9DW3xKQlc8Ms0slf4fxP7T04)
- **![🏃](https://fonts.gstatic.com/s/e/notoemoji/15.1/1f3c3/32.png) Speedrun the Coding Interview** (available for [Google](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5r8P5nR32W5BWr2F6lZ3pmW2f7NRM5jpbkFW59q7XH8Z0JyLW4fs_Mg7J0lypW2n_tqx1stLZ4W2X427-1vYcGKW94zg5V3Q-zDTW8MYV-q1Jy0tRW2Lp7WP7JJjftW2rKMPl6yPx_3W68rmHw87CwZYW5tPQFV6qv7bvW7Sdk5C7VYhXrW6JJfDv2SZwdnW8dmLH42RXYdgW7sL3336_QR25W7TQR2w3S1rBwW8616J86RPMr5W6RTN867mTBfkW1PQdSl2wYxV3W7zNhn_5yqLDMW6f6dNy2BvyW7W8mhVPj57-8MgVDnjQZ6XhqlsW3lqrWy8-nJbKW55TXrG5mTSjqW6dgjzz6NwhlMW4RL-QL7Ct4TRW2VcmnN7Hf06rW1SRYvT4rZMJNW420lpf51BzwjW5BYWb_8THnmLW5MQDL58J00P3N1qLm2jBJDlpW8TjV_r21Ttntf4vG9ml04), [Meta](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5r8P5nR32W5BWr2F6lZ3ksW1WkHVH5HdV9kW7_8vzZ7ScD_4W65fsfD5qQPBdW5GsTbs2tqjR_W8S28rM32tmF_W10CQNb418hvLW8dktRq2nRDzDVSkNR97P0vd9W1XCSDp4SfVsmVpv9_56lJRynW14B-CF5n0p4gW6ZzV8c16P-YfW5qhcLH4vQtXwN7wfCMLDlkPGN4tfv794VCgGW8Lldmg1QD9nKN3KvlsW_5k21W6LWMLH7cZqjpW96rXQN8zgsWbW8H35x46dP6dpW3dnfhG7bXWlZVjdG6X7mdRfMW4xMrgT4gPfV7W7LPd762g05D2W2qBmyW3hs7MJW8N_qh-1r6yHgW81zxgX5T891wW5HTCC76-8_l8W1mzSwn3JXKXGW3XMg5B3D62XMN6LTT07d9qt8W8F3hm11rndW7W979hVS12v7TlW35QP_M52V_D4f7y_mmP04), and more)
- **![✅](https://fonts.gstatic.com/s/e/notoemoji/15.1/2705/32.png) **[Educative-99](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5r8P5nR32W5BWr2F6lZ3kXW3wZMsK2cYD5mW94Wrdy7tXWS6W4QGtZ-2rgGQGW117flN75trXQW8krfVq8PzrbjW47P3l384H6kxW4tsz8K2KmxG2W4gXXD76-4VXfW19YhTR5WgcWLW6VggWq7QKKcgW9gLr4_5GH0wzW2Vxd9B6l4Q38W68_ZYR2y0y8yW8Bk9xc32GGDgN7sRhH7TMpTlMc4dLmxQ5YyW5LWcr65mwR0-W25nRZD6v8gfpN5DjW4hPKsdpVbhlwW71HDzMW8Pj2KS2yZ_9LW6Wm8TS3N1ftDW6QBz1L6mk0VSW8TC0w95J338jN2Mj0yZlNGQJW72QF6V2s9rXKW1PFLqB2lRYs8W8gTZ_y60xKWbVCVFs45vz-N4W8MvcV12Zsy_mW8j8qL28zTLFrW684z6V5bsjRyW1c46LD5ClkX_N22stM2Yxk0Cf7gX5xd04)(LeetCode-style crash course)

*Join 2M+ developers leveling up with Educative*

### Every millisecond counts

Latency is the delay between a request and a response -- and it can make or break your system's performance. Whether it's **network latency** (data travel time), **application latency** (server processing time), or **read/write latency** (storage access delays), every millisecond counts.

In fact, Google found that a 200 ms delay results in user drop-offs. What's more, Amazon loses 1% in sales for every 100 ms of latency. So latency *really* matters.

![Abe Simpson walking into and out of a door on loop.](https://ci3.googleusercontent.com/meips/ADKq_NY9ctwxQyxNAjcne-Qb6HPZibjjSNay0eKMq5qfn03xhSrDQzeqmdlDTJBGv9A47m4mGhdWCRhzGYxPXRWs5sFyRGfK5RaoMn2615UuH80q_ajhiU-NIfshD-zudrH4meXV9KqoSIfSY-Fily2ctNLCklI27QRU7w=s0-d-e1-ft#https://learn.educative.io/hs-fs/hubfs/abesimpson.webp?width=712&upscale=true&name=abesimpson.webp)

*The typical user when confronted with a > 200 ms delay*

Luckily, reducing latency comes down to 3 key areas:

-   **Minimize data processing time:** Use efficient algorithms and parallel processing to speed things up.

-   **Reduce network delays:** Cut down on hops, use event-driven architectures, and optimize communication protocols.

-   **Manage resources effectively:** Balance loads, shard databases, and cache smartly to keep things running smoothly.

Now that we know why latency matters, we're ready to talk about the strategies that can help you reduce it. Let's go.

5 best practices for achieving low latency
------------------------------------------

### 1\. Refine your system architecture 

Think of your system architecture as a pizza restaurant. You can either operate from one centralized location (monolithic architecture) or open smaller, independent shops everywhere across town (microservices).

Which one is getting pizza to more customers before it gets cold?

Monolithic systems are more straightforward to manage, but they don't scale with demand as well because of interdependencies. Microservices, though, work like the distributed pizza chain: modular, scalable, and more responsive.

And for real-time apps (like gaming or financial platforms), **event-driven architecture** further reduces latency by only sending data when events are triggered, eliminating unnecessary back-and-forth.

(And nobody's left hanging ... or hungry).

![Screenshot 2024-09-16 at 1.56.24 PM](https://ci3.googleusercontent.com/meips/ADKq_NaFW5ZSsQtKvZ0L9M4u3BCR_SPaId02s_RPx2DR2MmwZ50k4sewNCiylrb6kmk3MPrxN2EeLrqvolCtZoLyUYGwn3-Ka_OGhF7kK9smy6cIp0OciKGh2SsTZjbqlQZRrRtH52zZg9xWjgLLnvdn8vYhow_HSrXOIN6o1ooJiAj8ZGhSpXbBdfEmeVtadPmpKgTNLNaDOY6jBNz2_6SthU6AzuwHpRPc2d1leRH1ecOcgdeiqmpB8kPBUw=s0-d-e1-ft#https://learn.educative.io/hs-fs/hubfs/Screenshot%202024-09-16%20at%201.56.24%20PM.png?width=1120&upscale=true&name=Screenshot%202024-09-16%20at%201.56.24%20PM.png) |

*The difference between a monolithic system (left) and a microservices system (right)*

### 2. Optimize your network design

Network design helps reduce latency because it directly impacts how fast data travels between systems and users. Here's what you can do to keep data moving:

-   **Minimize network hops:** The fewer stops your data has to make, the faster it arrives -- like a direct flight versus one with multiple layovers. Use peering agreements, private network links, and optimized routing to cut down on hops.

-   **Leverage CDNs:** A content delivery network (CDN) brings data closer to users, reducing the time content takes to load. Instead of a New York user accessing a California server, serve the data from a CDN node in New York for faster results. (Kind of like our pizzeria example above.)

-   **Use geographical distribution and edge caching:** Spread CDN servers across different regions and store frequently accessed content at the edge of the network, right where your users are.

-   **Balance the load:** Avoid taxing servers by using load balancers. Whether it's round-robin, geographic, or session-based, load balancing ensures traffic is distributed, preventing delays and improving responsiveness.

![cdnwithloadbalancer](https://ci3.googleusercontent.com/meips/ADKq_NYxIG5ctI9e-JpwPTVu9LOr8_bV0s5kkulY7B52qwJW_PcOt42xR1fRkWaKozIVniZ9-G1oNa-z6nwOVHejB08mHpqBJ8U6FPqGbtANcTOqgY8hP6mMeoBGyULsr-XAZZWMF5gI1yH3lfMzplQ5qJgC_ZwdDwEOtHosWUjDDzU2YSBnU1xxQ5Y=s0-d-e1-ft#https://learn.educative.io/hs-fs/hubfs/cdnwithloadbalancer.jpg?width=600&upscale=true&name=cdnwithloadbalancer.jpg) |

*A load balancer and a CDN in a system*

### 3\. Improve data management and optimization

Your database setup is crucial for reducing latency because it determines how quickly your system retrieves and processes data. Here's how to make sure your data moves quickly:

- **Choose the right database:** Use SQL for structured data (like customer details) and NoSQL for flexible data models (like social media posts or real-time analytics).

- **Speed up retrieval:** Index your data and optimize queries for quicker execution. For large systems, shard your database (split it across servers) to handle more requests and replicate it to ensure fast, local access.

- **Go faster with in-memory databases:** Tools like Redis or Memcache store frequently accessed data in memory, cutting down on time spent fetching data from disk.

![datamanagementandoptimization](https://ci3.googleusercontent.com/meips/ADKq_NY23UdtjF-VPRlp2SLbS2J0GmEupO9LouzWWAU4Yl_tEajCj94pIWFGevIIa1NGcp2FlVe6lvA0sNyRZcGD5bJda5sdrSlFiw9QWaN-58hHvNi6vlIM0lBqsjn4KX7CyvLUEcpJ--s8feAZJjLIts4IkAOb7ezGHt5-46K6mZqtKsSHk3DrRzuc4K3xbxIuIFo7OeooUkK1uglFP0Bh=s0-d-e1-ft#https://learn.educative.io/hs-fs/hubfs/datamanagementandoptimization.jpg?width=1100&upscale=true&name=datamanagementandoptimization.jpg) |

*Database sharding (left) and database replication (right)*

### 4\. Use effective caching strategies

Smart caching can make a big difference in latency. By storing frequently accessed data in memory, you can deliver faster responses without hitting the database every time. Keep these tips in mind:

-   **Use caching at multiple layers**: Whether it's at the server, application, or database level, caching reduces the time it takes to serve data. This way, your system can respond quickly without unnecessary round trips.

-   **Eviction policies are key**: When the cache gets full, you need a strategy to decide what stays and what doesn't. The most common ones are Least Recently Used (LRU) and Least Frequently Used (LFU), which help ensure that the least relevant data clears first.

-   **Keep data fresh**: A stale cache can frustrate users. If the data in the backend is updated, make sure your cache is synced up so users get the most up-to-date, accurate information.

![effectivecaching](https://ci3.googleusercontent.com/meips/ADKq_NZ7mTKiZvD0sQiI8r0AGVJMDrhjiNqwxxo5szLmHJL6AT4Egvb-GrWfAHkBziBIjNMosVHDPZMLNGILROAaX8LkcKPiQ2ryqEdwOAqxvqyzEvOFcqGuIhUycHpy3xFnSwxJBPyCAQPU0sYAyESPpKDvgMf5vZVnjDkSiotuF_O5L40=s0-d-e1-ft#https://learn.educative.io/hs-fs/hubfs/effectivecaching.jpg?width=900&upscale=true&name=effectivecaching.jpg) |

*Serving clients' requests from cached data*

### 5\. Optimize your hardware and infrastructure

Reducing latency isn't just about software --- hardware and infrastructure are just as important. Try these strategies:

-   **Upgrade your hardware:** Choose **SSDs** over HDDs. SSDs significantly speed up data access, which can shave valuable milliseconds off response times.

-   **Leverage low-latency cloud services:** Platforms like AWS, Google Cloud, and Azure offer tools designed to reduce latency. Services like **AWS Global Accelerator** route traffic to the optimal endpoint based on latency, ensuring faster response times.

-   **Monitor and test regularly:** Setting up **real-time monitoring and alerts** is crucial. Regularly test your system's load and performance so you can spot any latency issues early and keep your system running smoothly.

💡This newsletter is adapted from my new blog, [Best Practices for Achieving Low Latency System Design](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5rbz3qgyTW95jsWP6lZ3m5W50BfJb4kpHJPW1p1vMX6sv9jPW5121FJ8xPjDLW5lHh9M4m81CkW779mq95Qf31wW1XCD3z3_4VwPVKqwW414b_5nW6x9WGY5FzTnHW3VhXRz11qHsRW4h3hpF5QhcPtV6tRyn4NnZ9BW4V4hR_3rN2zfW78z8sm6ZFRrnW6Wr9gY7XJnR6VCPsdD9fCxQBN1x0QFHk_CrsW2wyTJg6RvQVDW5yFVT74vQSRpW15C4RM372h27W6XZ81744QhVnW7wj1Jt748ZdjW8JdD1c9cTZ3GW57Hmm_8RPSYKF77sTbCHs9vW7GKj0P4hXfGZF3ggsN1GgxlW8Ss7WR4TBH8WW8_ZzNL30kgR0VBqwLh6lZS-GW2y97FX643gvhf5cTJN604). Read the full post for a deeper dive into each practice --- and for two more of my favorite pro tips.*

Don't let latency slow you down

There's no single fix for latency, but by making smart choices at every stage of your System Design, you can minimize it. Just make sure to keep user experience top of mind with each decision.

Latency is a challenge you'll face throughout your career, but with these tips, you'll master low-latency design ... maybe almost as fast as your applications respond.

As always, Educative's course [Grokking Modern System Design Interview](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5r8P5nR32W5BWr2F6lZ3kKW8h4tnD98WbJqVt2knw3f4s73W91NP2n22-5b3W3-9-vH6RpX1SW2ylmhx7jgJf4N6Qnx5GbmN5BW6SH1td3zgd-cW3F6PJ82TvFKrW7Kkhvt3GB3VYN2kWytgHyX4yVqXLPG8ZgkQnN7n589S_Jy1hW61D5M58T-cG_W2KZRHH95MBjFW7cqK-Z1hHqvwW84p1c_382d31W5gPDkZ1j2fthW7DJN3X6NZDdyVGphpd5_lHtBW277TB22__ZRNW9cwt0L2bc_Y7N4BC9pHNFCkGN2gZBlnb50FsW2ZcTNn65Yvj8W7tbF-Q3dtxGQW68hMk85TsyvHW3RW43v3tBt_cW8d_4qB1SlRVkW3dhGdh7Fkj8rW2pHMGq6t9LJXW6PpSrH7XYrQqW7jnVxk2G3qFFW6gmLch7YkCNwW2png1f1vlLfbd63k3l04) is a great place to get hands-on with essential System Design techniques for interviews and beyond. Today you can even get 50% off your subscription to access this popular course --- and 1200+ more.

Give it a shot and let me know you're able to apply what you learn to your own systems and products.

*Happy learning!*

![Fahim_Headshot](https://ci3.googleusercontent.com/meips/ADKq_NYHUYNwDdv45OSbM73USH7VBSuVL0Ihs6qv06bOOAcPuOzRoPRvoR7b_Np-1z_TyX7IP0ccyQjYMHG2YLpfPdyP_Sl9OZqKI3PElfjzEIPrUJeM0DKXQJj_Oijs6a45binXAerRjoZYpGjTFXte7PyieztbpbCNf6gJDYc2vg=s0-d-e1-ft#https://learn.educative.io/hs-fs/hubfs/Fahim_Headshot.png?width=220&upscale=true&name=Fahim_Headshot.png) |

Fahim ul Haq\
CEO & Cofounder\
[educative.io](https://learn.educative.io/e3t/Ctc/RG+113/cz5H404/VWQ76s93nXqfW89pPT31H9bKxW6J3_6X5l4CqrN3Z5r9-3qgyTW7Y8-PT6lZ3q3W1gghG_6jKXVVW8Bwdbg4gVZ35N7z4Ps6YMs9FW3jHM5l37fYJLW7mVN_Z41R1wdV39RnF3GGVNFW2y5BTj7jjQ8RW698VJS1m_d6fN5m3NdsrTZK4W8chMZM94C3z3W4MJKb18TD4n3W82vzxP2r0_9MW1DGJsv6Gns0nVX4zNB1xYjBrW8lPrBb6Jp0ZnW629ghS8LVlpsW58X3By8KHCsnW6F_nBk6cbwTVW7yLRT815TYqbW51jXBW1JDF8RVWR43X6Y_5d4W7Hk5Vp5RGc-qW8l8rVb2b3QSxVG7Gdw3vZ0GcW6N_jVV5h_rCJW47qZb34-b4m2f1yNgS204)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

|