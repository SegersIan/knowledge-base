[<< Back To Overview](./readme.md)

# Architecture Style: Microservices 

![Microservices Architecture Style Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1701.png)

## Description

Was named and use popularized by [a blog post from Martin Fowler and James Lewis](https://martinfowler.com/articles/microservices.html). The microservices style is heavily inspired on Domain-Driven-Design (DDD). The concept of **Bounded Context** (from DDD) was a decisive inspiration, which represents a decoupling style. The goal of microservices is high decoupling, physically modeling the logical notion of bounded context.

**The driving philosophy of microservices is the notion of bounded context: each service models a domain or a workflow.**

### Topology

We create single-purpose services that implement a bounded context. Each service is expected to include all necessary parts to operate independently, including databases and other dependent components.

### Distributed

* Each service runs its own process, originally implying its own hardware. Virtualization, Containers and infrastructure automation made it possible to separate these much further compared to a single application server (e.g Websphere, Tomcat, ...) that struggles with multi-tenancy concerns for bigger organizations, like improper isolation between shared applications. Each services having its own process solves the issues introduced by shared application servers.
* Microservice style would not have been realistic without trust in OSS (low cost), introduction of virtualization, containers and infrastructure automation tools.

### Granularity

* Finding the correct granularity for services is a core challenge. Making them too small, results often in communication (coupling) with many other services to do useful work. Some developers might take the term "microservices" as a commandment. As Martin Fowler said "**The term microservice is a label, not a description**".
* **Guidelines** to help find appropriate boundaries:
    * **Purpose**: Ideally each microservice should be extremely functionally cohesive, contributing one significant behavior on behalf of the overall application.
    * **Transactions**: Bounded contexts are business workflows, and often the entities that need to cooperate in a transaction show architects a good service boundary. Transactions cause problems in distributed architectures, so if you can design your system to avoid transactions across services, you'll generate better designs.
    * **Choreography**: If you build services with excellent domain isolation, yet require extensive communication to function, consider bundling these services back int a larger service to avoid the communication overhead. This keeps microservices from becoming unnecessary small.
    * **Data Isolation**: See ["Data Isolation"](####-Data-Isolation).
* **Iteration is key**, iteration is the only way to ensure good service design. Refine!

### Data Isolation

* Bounded contexts drive isolation, including the data. Microservices kills any coupling via shared databases or shared schemas used for integration.
* Don't model based on the "Entity", known as the "Entity Trap", but I personally like to name it entity-driven-design. 
* There are no various sources, each with their source of truth of a certain domain. In microservices, joining data of their respective source of truths is challenging, as all the data might not live in the same bounded context. Solve this either via
    * Communicating with various bounded contexts to retrieve the data.
    * Data replication or caching to distribute information.
* This isolation can create headaches to aggregate information, but the trade off is freedom in being able to chose the right tool, based on type of storage and related factors (Document database, Graph Database, ...) while other teams are not affected.

### API Layer

* The API layer is optional, but sits between the Consumers of the system, which is a good location for lots of operational logic/tasks.
* The API layer should not be used for mediator/orchestration, that belongs in the bounded context! Mediators is "technical" partitioning, remember, it's all about bounded contexts here.

### Operational Reuse

Microservices prefer duplication over reuse, to avoid coupling. However, some parts, like operational components (e.g. monitoring, logging, circuit breakers,...) could really benefit from coupling. Even when using distinct bounded contexts, there will be similarities, especially from operational aspect.

The **Sidecar Pattern** offers a solution to this problem. Reusable components can be located in this sidecar and independently maintained by other teams (e.g. Infrastructure Teams). This pattern is very popular in **service mesh**. This patterns creates a consistent operational interface across all microservices. This is a part of thinking about creating a "platform".

[Sidecar Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1702.png)

### Frontends

It is common to see a single (monolithic) user interface that talks to a microservice architecture. However, ideally the frontend is follows also the same design philosophy of microservices and we would expect to see micro frontends. Micro frontends exist, however due to practicalities and the novelty of the concept it is not so mainstream. However, we do expect further adoption.

* [Monolithic Frontend Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1705.png)
* [Micro Frontend Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1706.png)

### Communication

Finding the correct communication channel helps keeping services decoupled, yet coordinated in a useful way. 

* **Synchronous**: Caller waits for the response from the callee. Microservices typically uses **protocol-aware heterogeneous interoperability**:
    * *Protocol Aware*: There is no centralized integration hub to avoid strong coupling, but standardize how which protocols are used.
    * *Heterogenous*: Every service can be in an entire different technology, so the protocol must support polyglot environments.
    * *Interoperability*: Services calling one another.
* **Asynchronous**: Caller doesn't wait for the response from the callee, but might come back at a later point. Common to use messaging and events. Event-driven architecture style is very often combined with microservices style to accommodate asynchronous communication. 

#### Choreography and Orchestration

* Since we can use the event-driven style in conjunction with the microservices style, we can use the Broker/Choreography pattern as natural fit, cause of it's highly decoupled nature. Allowing for decoupling between services. 
*  When there is a need for mediator/orchestration pattern, you can create a microservice with the sole responsibility to act as a mediator for the given bounded context. To be clear, you should not make a "mediator" microservices that is reused as "the mediator microservice" for any need for a mediator. 
* Note that in microservices we can have **choreography** and **orchestration** using request-based and event-based communication. But many of the same principles, challenges, and benefits for each pattern apply for request-based and event-based implementations. Examples being  error handling, workflow control, visibility, testing and recoverability.

Diagrams:
* [Choreography Simple Example](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1707.png)
* [Choreography Complex Example](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1709.png)
* [Orchestration Simple Example](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1708.png)
* [Orchestration Complex Example](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1710.png)

#### Transactions and sages

Don't do transactions in microservices, fix granularity instead! See the ["Granularity"](####-Granularity). 
However, exceptions do exist, when they do, **patterns exists with serious trade-offs**.

A popular distributed transactional pattern in microservices is the **saga pattern**. In this pattern a service acts a service using the mediator/orchestration pattern. The drawback on this is, when a single step in the transaction fails, all previous steps must be informed to cancel the step or execute a compensating action. 

This style of transactional coordination is called **Compensating Transaction Framework**. The complexity of this and all challenges to implement this (especially undo actions) makes it less than desirable. Where possible, try to avoid cross service transactions all together and rethink your bounded contexts.

Diagrams:
* [Saga Default](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_17011.png)
* [Saga Compensating Transactions](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_12.png)

## Nuggets Of Wisdom
> The best way to think about microservices is not by defining the size, but rather by determining the purpose.
* Source: [Strategic Monoliths and Microservices - Driving Innovation Using Purposeful Architecture](https://learning.oreilly.com/library/view/strategic-monoliths-and/9780137355600/)

## When To Use

* When you desired high decoupling, so teams can move independently, at their own pace.
* Works well for really large organizations, where it is important to scale, make it reliable, but maintain speed of delivery.

## When NOT To Use

* When cost is a serious concern for skills, engineers, and infrastructure.
* When performance is key.

## Considerations

* Performance is often a negative side effect of the distributed nature. Network calls take longer, security verification at multiple points.
* Use of transactions across service boundaries is advised against. Determining the granularity of services is the key to success.
* New developments in automation and operations constantly reduce the overall cost for operating and hosting a microservice architecture. However, for smaller engineering teams usually is not reasonable.

## Characteristics

| Characteristic    | Rating              |
| ---               | ---                 |
| Partitioning Type | Domain              |
| Number of quanta  | One to many         |
| Deployability     | ⭐⭐⭐⭐          |
| Elasticity        | ⭐⭐⭐⭐⭐        |
| Evolutionary      | ⭐⭐⭐⭐⭐        |
| Fault Tolerance   | ⭐⭐⭐⭐          |
| Modularity        | ⭐⭐⭐⭐⭐        |
| Overall cost      | ⭐                  |
| Performance       | ⭐⭐               |
| Reliability       | ⭐⭐⭐⭐           |
| Scalability       | ⭐⭐⭐⭐⭐        |
| Simplicity        | ⭐                  |
| Testability       | ⭐⭐⭐⭐           |

## Resources

* [How To Choose Microservice boundaries](https://www.linkedin.com/pulse/how-choose-microservices-boundaries-denis-baltor/)
* [Martin Fowler on Microservices](https://martinfowler.com/microservices/)
* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/)