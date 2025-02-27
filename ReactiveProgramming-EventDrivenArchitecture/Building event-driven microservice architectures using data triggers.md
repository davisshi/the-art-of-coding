[Microservices and data in cloud-native architectures](https://aws.amazon.com/marketplace/build-learn/data-analytics/event-based-architecture?trk=12cbccd7-a7a4-43db-9606-44451613641c&sc_channel=em&mkt_tok=MTEyLVRaTS03NjYAAAGY5pJctLa1Evgf0K4qeiQIOygZNfNnlblanNOvKttDAZp77AghPJZque3Rcyw06ZRdALL_QDqFoQr1QmRJkHCaaeot-TZddNX3lzss_AHmSppY-1KfJzdNjw)
----------------------------------------------------

The architecture of our applications has dramatically evolved. Today microservices and containerized workloads have taken the lead, leaving monolithic applications behind. This change in application architecture has also impacted the way in which we store and structure data.

Just as services are now distributed and built using the stack that is best suited for the features, the data they aim to deliver is also distributed and lives in service-specific databases that own the data specific to their scope.

To fully extract the value of all this data, it is necessary to make it available to a large network of consumers over a consolidated, simple, and consistent interface. Traditionally, this has meant a layer that requires considerable effort in maintaining.

In this article you will see how MongoDB Atlas Data API can provide this type of central, intuitive access to all your data without the complexity of moving data around or relying on individual service endpoints while benefiting from the efficiency, performance, and flexibility of a data-driven, event-based architecture.

[You can try MongoDB Atlas for free in AWS Marketplace.](https://aws.amazon.com/marketplace/pp/prodview-pp445qepfdy34?trk=5e006c7e-82a4-4115-8346-688a232479d2&sc_channel=el)

Let's dig in!

The architecture of systems today
---------------------------------

The cloud and container orchestration have dramatically helped in maturing today's microservice architectures across most complex enterprise landscapes with many solid reasons:

-   Horizontal scalability becomes easier to achieve
-   Faults are easier to isolate
-   Teams can move faster thanks to services being decoupled
-   Smaller releases are easier to test and faster to deploy

To achieve these benefits though, it is important that each microservice does indeed follow best practices and therefore owns its own data.

This principle has given freedom to application and infrastructure architects to structure their data and deployment needs efficiently and securely by being able to provide some teams with dedicated Amazon Web Services (AWS) accounts and clusters for their demanding data requirements while others can own databases within larger shared clusters in shared AWS accounts.

In traditional architectures, each RESTful service exposes an API and requests from users are routed to the appropriate service through an API gateway configured to send requests to the right service given the request URI or other parameters.

![AWS Cloud MongoDB Atlas Cluster archietecture map](https://d1.awsstatic.com/awsmp/solutions/awsmp_mss-impguide-mongodb-aws_cloud-aws_account-services.51094886eb6f095e1d5b50e441dc5ac62c76075e.jpg)

This architecture has been widely battle tested and offers a solid foundation for most use cases, but in some scenarios, there are areas where it can be simplified.

Let's look at some of the complexities of this traditional approach

### Many moving pieces

As you can see from the scenario above, there are a lot of moving pieces: load balancers and VPC endpoints across accounts, plus API gateway configurations that must be updated whenever new services are added. Not to mention each microservice is itself running in some compute environment.

The number of components that require monitoring and the many steps for a request to get data back to the user is not trivial.

### Client drivers are always required

Every microservice must include client drivers to connect to its corresponding database and security and network controls must be in place to ensure those connections are possible and secure.

This may not always be possible depending on your service requirements, for example, when your services must live outside of the cloud in Internet of Things (IoT) scenarios.

The need for client libraries also produces larger builds and a more complex software supply chain.

### APIs matching data schemas

Each microservice effectively offers a REST API to some underlying data stored in the service's own database. Changes to underlying data schemas must then be reflected in the REST API that the service exposes, otherwise as it usually happens, the REST API starts to become a data translation layer, simply looking to transform and match the underlying data structures without impacting REST API consumers.

Building a data-centric, event-driven architecture
--------------------------------------------------

Let us now look at how this architecture could be dramatically simplified by building a solution that uses a MongoDB Atlas on AWS using Amazon API Gateway & AWS Lambda as the single interface for all entities that require access to data and a fully decoupled event-driven computations triggered using MongoDB Atlas Event Triggers together with Amazon EventBridge to perform all actions that must take place with data once a request has been made by a user.

![AWS Cloud MongoDB Atlas cluster Amazon API Gateway AWS Lambda architecture map](https://d1.awsstatic.com/awsmp/solutions/awsmp_mss-impguide-mongodb-aws_cloud-atlas_cluster-architecture.c5c5ed37ddf7eaa3199f145cac932b06055e1393.jpg)

Architecture Walkthrough
------------------------

The first thing you can see from the architecture above is the rather simplified structure that is required and, therefore, the corresponding surface to support and configuration to manage also sees a meaningful improvement.

At a high level, the primary optimizations we've achieved with this new design are:

-   There is no longer a need for network and load balancing components to receive and route requests since all requests will be handled by the top-level Amazon API Gateway connected to MongoDB Atlas on AWS through AWS Lambda, which will have access to all applicable databases.
-   Both users as well as backend services use a common HTTPS interface to interact with the data without the need for client libraries to be bundled in releases or available across diverse devices.
-   Complex queries can be fully orchestrated in the backend using data as trigger. The combination of MongoDB Atlas Triggers and Amazon EventBridge together with the huge diversity of AWS services that can be integrated effortlessly with this approach makes this solution extremely extensible.

Let's look at some of the components in more detail:

### Amazon API Gateway & Lambda to MongoDB Atlas

We use Amazon API Gateway to provide the top-level interface to interact with MongoDB Atlas on AWS through the use of Lambda functions. Amazon API Gateway provides the HTTP/HTTPS interface that can be used to read and modify all connected databases. The AWS Lambda function performs the operation based on the type of request and the request body.

![Amazon API Gateway accesses AWS Lambda to MongoDB with CRUD access to MongoDB Atlas on AWS](https://d1.awsstatic.com/awsmp/solutions/awsmp_mss-impguide-mongodb-amazon_api-gateway-Lambda-Mongodb_atlas.a78af852e08d25c86b84845661e3f3c9d163ef1a.jpg)

This works well for basic read/write operations and more advanced reactive features can be handled using event-based processing.

### MongoDB Atlas Triggers and Amazon EventBridge

MongoDB Atlas Triggers respond to some event and execute some processing action when the event "fires." This MongoDB Atlas Triggers capability, a feature of Data Services, becomes incredibly powerful when paired with the native support for Amazon EventBridge.

Amazon EventBridge enables the development of loosely coupled, event-driven architectures, integrating a huge variety of AWS solutions as targets when events occur. This allows for complex workflows to be built that provide a very streamlined and highly available mechanism to perform compute and other operations.

![Amazon Eventbrdgie Saas app Namespace EventBridge architecture map](https://d1.awsstatic.com/awsmp/solutions/awsmp_mss-impguide-mongodb-saas_eventbridge_conceptual.c2b7c588c9a77466dedc5dc41ed8bcf426f1fdf0.jpg)

MongoDB Atlas Triggers can fire when specific database operations occur, such as inserts or changes to some collection, whenever user-related activities take place (login, user deletion, etc.), and also on some pre-defined schedule.

![MongoDB Atlas Add Trigger settings](https://d1.awsstatic.com/awsmp/solutions/awsmp_mss-impguide-mongodb-org-add-trigger-details.087942087da9cdea618a9c4a8236db8cc2d2505d.jpg)

### How would this look in action?

The flow of requests will be very simple and consistent regardless of the underlying service that is involved in delivering the desired business logic. Let's look at a sample flow:

1.  An end user, using a standard HTTPS request, requests some data such as a list of products from a store. This request will be served by Amazon API Gateway by fetching data directly from the database using an AWS Lambda function and returning a JSON payload.
2.  The user selects multiple products and now chooses to make an order. This order is effectively a single insert in the orders collection, which is also made by a simple HTTPS request to the API. This action, however, as opposed to a simple product listing, requires various different services in the backend to perform some operation.
    1.  A MongoDB Atlas Trigger is configured to produce an event every time an insert happens on the orders collection.
    2.  An Amazon EventBridge is configured using partner event source to consume those events and trigger multiple services: the billing service will handle processing payment for the order, while the shipping service handles scheduling the package pick-up and delivery.
    3.  Each service handles its side of the operation and uses the Amazon API Gateway to MongoDB Atlas to make any necessary changes to the corresponding data in the database, again using standard, authenticated HTTPS requests.
    4.  Each service sends push notifications using Amazon Simple Notification Service (Amazon SNS) to the end user that made the request, providing real-time updates as each step in the order fulfillment process takes place.

What do we get with this solution?
----------------------------------

What we have is a radically simple, elegant, secure, and scalable solution that allows all entities that require data from your services to use a common HTTPS interface without any specific client libraries, a complex network, or request routing mechanisms, all while providing efficient request orchestration capabilities and real-time consumer updates.

[You can try MongoDB Atlas for free in AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-pp445qepfdy34?trk=5e006c7e-82a4-4115-8346-688a232479d2&sc_channel=el) and by doing so dramatically simplify the integration of your MongoDB Atlas and AWS accounts.

Be on the lookout for an upcoming lab where I'll show you step-by-step how to build this very solution in your own AWS account!