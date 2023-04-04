# System Design

 ## Vertical VS Horizontal Scaling
 `Scablity` : The scalability of an application can be measured by the number of requests it can effectively support simultaneously. The point at which an application can no longer handle additional requests effectively is the limit of its scalability. This limit is reached when a critical hardware resource runs out, requiring different or more machines.

 Scaling horizontally and scaling vertically are similar in that they both involve adding computing resources to your infrastructure. There are distinct differences between the two in terms of implementation and performance.

 `Horizontal scaling` means scaling by adding more machines to your pool of resources (also described as “scaling out”), whereas `vertical scaling` refers to scaling by adding more power (e.g. CPU, RAM) to an existing machine (also described as “scaling up”).

 One of the fundamental differences between the two is that horizontal scaling requires breaking a sequential piece of logic into smaller pieces so that they can be executed in parallel across multiple machines. In many respects, vertical scaling is easier because the logic really doesn’t need to change. Rather, you’re just running the same code on higher-spec machines. However, there are many other factors to consider when determining the appropriate approach.

// @todo : add image here

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