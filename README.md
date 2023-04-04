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


