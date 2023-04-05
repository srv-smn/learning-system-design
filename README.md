# System Design

 ## Vertical VS Horizontal Scaling
 `Scablity` : The scalability of an application can be measured by the number of requests it can effectively support simultaneously. The point at which an application can no longer handle additional requests effectively is the limit of its scalability. This limit is reached when a critical hardware resource runs out, requiring different or more machines.

 Scaling horizontally and scaling vertically are similar in that they both involve adding computing resources to your infrastructure. There are distinct differences between the two in terms of implementation and performance.

 `Horizontal scaling` means scaling by adding more machines to your pool of resources (also described as “scaling out”), whereas `vertical scaling` refers to scaling by adding more power (e.g. CPU, RAM) to an existing machine (also described as “scaling up”).

 One of the fundamental differences between the two is that horizontal scaling requires breaking a sequential piece of logic into smaller pieces so that they can be executed in parallel across multiple machines. In many respects, vertical scaling is easier because the logic really doesn’t need to change. Rather, you’re just running the same code on higher-spec machines. However, there are many other factors to consider when determining the appropriate approach.

<img width="678" alt="image" src="https://user-images.githubusercontent.com/86356248/229762493-86f3f2b2-bb9e-4bfa-89bb-72f1b3b6b4d6.png">


| Horizontal Scaling                           	| Vertical Scaling            	|
|----------------------------------------------	|-----------------------------	|
| load balancing is req.                       	| NA                          	|
| Resilient                                    	| Single point of failure     	|
| Network Calls (Remote Procedure Calls - RPC) 	| Inter process communication 	|
| Data Inconsistent                            	| Consistent                  	|
| Scales well as user increases                	| Hardware Limit              	|


Factors while considering scaling solution
1. Performance
2. Flexibility
3. Regularity of Upgrades
4. Redundancy
5. Geographical Distribution
6. Cost

`Conclusion`:
It doesn’t always make sense to choose between horizontal and vertical scaling. Moving between the two models is often a better choice. For instance, in storage, we often want to switch between a single local disk to a distributed storage system.
Building flexibility into the system, where some layers of the application run on vertically scaled machines and other layers on horizontally scaled infrastructure remains a matter of designing for parallelization.

Resources:
1. [Youtube](https://youtu.be/xpDnVSmNFX0)
2. [Article](https://www.section.io/blog/scaling-horizontally-vs-vertically/)

## HLD and LLD
HLD and LLD are two different stages in the software development life cycle that represent different levels of detail in system design.

HLD, or High-Level Design, is the first stage of the system design process. It focuses on defining the overall architecture of the system at a high level. HLD includes identifying the major components of the system and their interactions, as well as defining the data flow and control flow within the system. HLD is typically represented using diagrams such as flowcharts, block diagrams, or UML diagrams.

LLD, or Low-Level Design, is the next stage in the system design process. It provides a more detailed design of the system components that were identified during HLD. LLD focuses on defining the functionality of each component, including algorithms, data structures, and interface specifications. LLD is typically represented using diagrams such as class diagrams, sequence diagrams, or state transition diagrams.

In summary, HLD provides an overall architecture of the system while LLD provides detailed designs for individual components of the system. HLD is concerned with the system's structure and interactions while LLD is focused on the implementation details of each component.

Few concepts of HLD

1. `Vertical scaling`: This refers to adding more resources, such as CPU, memory, or storage, to a single server or instance to improve its performance or capacity.

2. `Pre-processing`: This is the manipulation of data or information before it is used by a system or application. Pre-processing can include tasks such as cleaning, filtering, formatting, or transforming data to make it more suitable for the application's needs.

3. `Backups`: This refers to creating copies of data or system configurations to protect against data loss or system failure. Backups can be performed on a regular schedule and stored in a secure location.

4. `Horizontal scaling`: This refers to adding more servers or instances to a system to improve its performance or capacity. Horizontal scaling can improve the system's reliability and availability by distributing the workload across multiple servers.

5. `Microservice architecture`: This is an architectural pattern in which a system is broken down into small, independent services that can be developed, deployed, and scaled independently. Microservices can improve the system's flexibility, maintainability, and scalability.

6. `Distributed System`: This refers to a system that is composed of multiple independent components that are connected and coordinated by a communication network. Distributed systems can improve the system's performance, scalability, and fault tolerance.

7. `Load balancing`: This is the process of distributing incoming network traffic across multiple servers or instances to improve the system's performance and reliability. Load balancing can improve the system's scalability, availability, and responsiveness.

8. `Decoupling`: This refers to designing a system so that its components are loosely coupled and can be developed, deployed, and maintained independently. Decoupling can improve the system's flexibility, maintainability, and scalability.

9. `Logging and Metrics calculation`: This refers to the process of capturing and analyzing system logs and performance metrics to monitor and troubleshoot the system's behavior. Logging and metrics calculation can improve the system's reliability, availability, and performance.

10. `Extensible`: This refers to designing a system so that it can be easily extended or modified to meet changing requirements or accommodate new features. Extensibility can improve the system's flexibility, maintainability, and scalability.


## Consistent hashing and Load balancing
Consistent hashing and load balancing are two concepts that are often used together in distributed computing to improve the scalability and reliability of systems.

Consistent hashing is a technique used to distribute data and workload across multiple servers in a consistent and efficient manner. It is based on the idea of mapping data items and servers onto a fixed set of hash values, which are used to determine the server responsible for handling a particular data item. By using a hash function to map data items onto servers, consistent hashing ensures that the distribution of data is balanced across the servers, and that the addition or removal of servers from the cluster does not require a complete remapping of data items.

Load balancing, on the other hand, is a technique used to distribute incoming traffic across multiple servers to ensure that no single server is overloaded with requests. Load balancing can be implemented using different algorithms, such as round-robin, random, or least connections, to distribute the traffic across the servers. Load balancing also involves monitoring the servers to detect any failures or performance issues and redirecting traffic to healthy servers.

When used together, consistent hashing and load balancing can improve the scalability and reliability of distributed systems by distributing workload and traffic across multiple servers in a consistent and efficient manner. By using consistent hashing to distribute data and load balancing to distribute traffic, the system can handle large amounts of data and traffic while ensuring that no single server is overloaded with requests. Additionally, if a server fails, the consistent hashing algorithm can route the affected data to another server in the cluster, while the load balancer can redirect traffic to healthy servers. This makes the system more resilient to failures and improves the overall performance and availability of the system.

what will happen if server fails ?

1. If a server fails in a distributed system that uses consistent hashing and load balancing, the system should be able to continue functioning without any interruption or loss of data. Here's what typically happens when a server fails:

2. When a server fails, it becomes unavailable and stops responding to requests. This may be due to hardware failure, network issues, or software bugs.

3. The load balancer detects that the failed server is unresponsive and removes it from the list of active servers.

4. The consistent hashing algorithm maps the data items that were previously assigned to the failed server to the next available server in the ring. This ensures that the data items remain available and are not lost.

5. Any incoming requests that were previously directed to the failed server are now redirected by the load balancer to another available server.

6. If the failed server is replaced by a new server, the consistent hashing algorithm will assign some of the data items that were previously assigned to the failed server to the new server, and the load balancer will start directing incoming requests to the new server.

7. As the system continues to operate, the consistent hashing algorithm may need to rebalance the distribution of data across the servers to ensure that the workload is evenly distributed.

In summary, a distributed system that uses consistent hashing and load balancing is designed to be resilient to server failures. The system can continue to function and serve requests even if a server fails, by redistributing the workload and data to other available servers. This makes the system more reliable and helps to minimize downtime and data loss.

Resources
[Video 1](https://youtu.be/K0Ta65OqQkY)


[Video 2](https://youtu.be/zaRkONvyGr8)


[java code](https://github.com/coding-parrot/Low-Level-Design/blob/master/service-orchestrator/src/main/java/algorithms/ConsistentHashing.java)

## Message/Task Queue
A message/task queue that includes load balancing, notifier, and heartbeat check functionality is a powerful tool for building scalable and reliable distributed systems.

Load balancing functionality in a message/task queue can help distribute workloads across multiple nodes or servers. With load balancing, tasks or messages can be distributed to different nodes in a way that balances the load and maximizes throughput. This can help to ensure that the system is scalable and can handle increased traffic or workload without becoming overloaded.

Notifier functionality in a message/task queue can help to keep track of the status of tasks or messages. A notifier can be used to notify users or other systems when tasks are completed or when certain events occur. This can help to improve the overall reliability of the system and reduce the risk of errors or delays.

Heartbeat check functionality in a message/task queue can help to detect failures or issues in the system. By periodically sending heartbeat messages, a node or server can notify other nodes in the system that it is still functioning properly. If a node fails to respond to heartbeat messages, it can be assumed that the node has failed or become unavailable. This can trigger a failover or recovery process to ensure that the system remains available and operational.

By combining load balancing, notifier, and heartbeat check functionality, a message/task queue can provide a powerful platform for building scalable and reliable distributed systems. This type of system can help to ensure that tasks are distributed efficiently, notifications are delivered reliably, and failures are detected and handled quickly. This can improve the overall performance and availability of the system and help to ensure that it can handle increased traffic or workload as needed.

reference: [video](https://youtu.be/oUJbuFMyBDk)

## Monolithic VS Microservice
Monolithic Architecture:
Monolithic architecture is a traditional software development approach where the entire application is built as a single, self-contained unit. All the modules of the application are tightly coupled, and a change in one module affects the entire application. The monolithic application is deployed on a single server or a cluster of servers.

Pros:

Simple to develop and test.
Easy to deploy and manage since it is a single unit.
All modules have access to the same data, so there is no need to handle distributed transactions.
Good for small applications with limited scalability requirements.
Cons:

Monolithic applications can become large and complex over time, making them difficult to maintain.
Scaling up can be a challenge, as adding more resources means scaling the entire application, even the parts that don't need scaling.
A bug in one module can bring down the entire application.
Deployment and updates require downtime, which can disrupt service.
Example:
An example of a monolithic application could be a web-based e-commerce platform, where all the functionalities are part of a single application. All the components such as customer service, inventory management, order management, and payment processing are combined in one application.

Microservice Architecture:
Microservices are a modern software development approach where the application is divided into independent services, each running in its process and communicating with other services through lightweight mechanisms. Each microservice is developed, deployed, and maintained independently, enabling teams to work on different parts of the application without interfering with each other.

Pros:

Microservices are more flexible and adaptable to change since each service can be updated and deployed independently.
Scaling up is easier, as only the services that need scaling can be scaled, avoiding the need to scale the entire application.
Services can be developed using different languages and technologies, allowing developers to use the best tool for each job.
Faults are isolated to individual services, making it easier to locate and fix issues.
Updates can be made without downtime, as only the services being updated are affected.
Cons:

Microservices are more complex to develop and test, as each service needs to be tested individually as well as integrated with other services.
Managing distributed data can be challenging, as each service may have its database or cache, requiring a strategy for data consistency and synchronization.
Network latency can affect the overall performance of the application, as each service communication adds an overhead.
Security can be more challenging as there are more points of entry.
Example:
An example of a microservice architecture could be a travel booking platform where each service handles a specific functionality such as hotel booking, flight booking, car rental, and payment processing. Each service can be independently scaled, updated, and deployed, providing a more flexible and adaptable system.

In summary, monolithic architecture and microservice architecture are two different software development approaches, each with its pros and cons. Monolithic architecture is simpler to develop and manage, but it can become complex and difficult to maintain as the application grows. Microservice architecture is more flexible and scalable, but it requires more effort to develop and manage, and it may introduce additional challenges related to data consistency and security.




