[<< Back To Overview](./readme.md)
 
# Architecture Style: Event-Driven

![Event-Driven Architecture Style Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1401.png)

## Description

Made up of decoupled event processing components that asynchronously receive and process events.
This architectural style can be used standalone or embedded with other architectural styles.

> There is a difference between the architectural style of pure "Event-Driven" and events and event sourcing in general. Therefore, for more information specific to events and not the specific architectural style. See [Integration Architecture > events](../integration-architecture/events/readme.md).

### Request-Based & Event-Based
Majority of processes in any architectural style are request-driven, using the request-based model. 
In the event-based model, systems **react** to an event that happens. We are inverting the responsibility for systems to act accordingly.

If we think about it, the event-model is all around us in nature and physics. When you throw a ball against the wall, the ball moves through the air as reaction to the event of force being exercised on the ball. 
We could mistake the idea that we "tell the ball" what to do, but rather through our understanding of physics (or experience) we know that the ball will respond with flying through the air, if we put pressure on it.
Actually, in nature there is little that is genuinely "request-based", even a "response" is a reaction to an event that indicated a "request". The philosophical part aside, the request-based model demands a synchronous interaction, event-based is intentionally asynchronous.

### Topologies

Most common topologies are **Broker** and **Mediator** topology. They architecture characteristics and implementation strategy differs between these topologies, therefore it is important to understand the difference between them.

#### Broker Topology (Choreography Pattern)

This is also known as **The Choreography Pattern**.

> Used when you require a high degree of responsiveness and dynamic control over the processing of an event.

This topology has no central event mediator,  messages flow across the event processor components in a chain-like broadcasting fashion. Works great when you have relative simple event processing flow that doesn't require event orchestration and coordination There are [**4 primary architecture components**](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1403.png):

* **Initiating Event**: Event that starts the entire flow. This event gets send to the Event Broker.
    * Example: An order was placed advertised with "PlaceOrder" event.
* **Event Broker**: Receives events and forwards these events based on if any Event Processors are listening and interested for the given even (e,g. through pub/sub).
    * Example: "OrderPlaced" event forwarded to "OrderPlacement"
    * Technology examples: RabbitMQ, ActiveMQ, HornetQ
* **Event Processor**: Accepts an incoming event that it cares about and performs actions/business logic specific to that event. Once the processing is done, the results/output/actions are advertised asynchronously with a Processing Event. Event processors are highly decoupled and independent of each other.
    * Example: "OrderPlacement" processes PlaceOrder event into an order.
* **Processing Event**: 
    * Example: "order-created"

> Event Processors advertise to the rest of the system the results of their processing as Processing events.

[See Example Flow Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1404.png)

##### Challenges

* No control over the overall workflow associated with the initiating event. Everything is dynamic, based on various conditions, no one in the system really knows when the entire Business activity has been completed or not.
* Error Handling is hard, there is no implicit monitoring if a business activity has failed, or if a failure has occurred. Other event processes or not aware of a crash in a certain part of the system.
* The ability to restart a business transaction (recoverability) is also something not supported with this topology. Requiring often manual intervention.

#### Mediator Topology (Orchestration Pattern)

This is also known as **The Orchestration Pattern**.

> Used when you require control over the workflow of an event process. Partially addresses the shortcomings of the broker topology.

There are [**5 primary architecture components**](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1405.png):
* **Initiating Event**: Event that starts the entire flow. This is sent to an event queue.
* **Event Queue**: This queue keeps track of all the initiating events. Ready for the Event Mediator to consume.
* **Event Mediator**: The central component in this topology/pattern. This accepts events from the initial event queue. The event mediator **only knows the steps involved in processing the event and therefore generates corresponding processing events that are sent to dedicated event channels.**
* **Event Channels**: Dedicated event channels (usually queues) in a point-to-point fashion between the event mediator and the event processors.
* **Event Processors**: Event processor listens to dedicated event channels, processes the event, and usually will respond back to the mediator to inform failure/success.

> Event Processors **do not** advertise to the rest of the system, and only communicates back to the event mediator. Therefore "events" in this topology are more like "commands".

It is common that there are multiple event mediators, each event mediator scoped to a specific domain, business process, or other logical grouping.

##### Event Mediator Types

[Mediator Delegation Model](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1406.png): One advice is to use a simple event mediator, and based on the contents of the event, it might forward this to a more complex event mediator if warranted. Therefore one must understand well the types of events being processed to choose the right type of event mediator. 

* Simple Event Mediator: Simple error handling + orchestration: Apache Camel, Mule ESB, Spring Integration, or self written
* Hard Event Mediator: Complex conditional processing and multiple dynamic paths with complex error handling: Apache ODE, Oracle BPEL (Business Process Execution Language)
* Complex Event Mediator: Long running transactions that required manual (human) interaction: BPM (Business Process Management) engine such as jBPM

**Examples**
* [Example of combined mediators types: Overview](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1407.png)
* [Example of combined mediators types: Step 1](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1408.png)
* [Example of combined mediators types: Step 2](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1409.png)
* [Example of combined mediators types: Step 3](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1410.png)
* [Example of combined mediators types: Step 4](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1411.png)
* [Example of combined mediators types: Step 5](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1412.png)

##### Challenges

* It is very difficult to declaratively model the dynamic processing that occurs within a complex event flow. THerefore many workflows within the mediator only handle the general processing, **a hybrid model combining mediator and broker topology is used to address the dynamic nature** of complex event processing.
* Event processors can easily be scaled, the event meditator less so, occasionally causing bottleneck problems.
* Event processors care not as highly decoupled compared to the broker topology.
* Performance is not as good due to the mediator controlling nature.

#### Comparison

Trade off between workflow control and error handling capability versus high performance and scalability. Performance and scalability are good in general for event-driven architecture, the broker topology does is slightly better than the mediator topology.

|                    | Broker/Choreography | Mediator/Orchestration |
| ---                | ---                 | ---                    |
| **Advantages**     | Highly decoupled events processors<br>High scalability<br>High Responsiveness<br>High Performance<br>High fault tolerance |  Workflow control<br>Error handling<br>Recoverability<br>Restart capabilities<br>Better data consistency |
| **Disadvantages** | Workflow control<br>Error handling<br>Recoverability<br>Restart capabilities<br>Data inconsistency | More coupling of event processors<br>Lower Scalability<br>Lower performance<br>Lower fault tolerance<br>Modeling complex workflows |

## When (NOT) To Use

A key question that emerges is using "event-driven" versus "request-reply" based models.

* Event-Driven: Recommended for flexible, action-based events that require high levels of responsiveness and scale, with complex and dynamic user processing.
* Request-Based: Recommended for well-structured, data-driven (e.g. fetch user profile) requests when certainty and control over the workflow is needed.

* Advantages over request-based
    * Better response to dynamic user content
    * Better scalability and elasticity
    * Better agility and change management
    * Better adaptability and extensibility
    * Better responsiveness and performance
    * Better real-time decision making
    * Better reaction of situational awareness
* Trade-offs
    * Only supports eventual consistency
    * Less control over processing flow
    * Less certainty over outcome of event flow
    * Difficult to test and debugs

## Considerations

Changes to a particular domain usually impact many event processors, mediators, and other messaging artifacts, hence why event-driven architecture is not domain partitioned.

### Async Error Handling
A key characteristic is the asynchronous nature of event-driven architectures. With a simple "acknowledgement" one can create a responsive experience to the end user without having to fix the performant nature if it was request-based. Working asynchronous does come with a challenge, which is **error handling**. Error handling in an async environment is more challenging thant with request-based. Cause if an error happens, how do you get back to the end user to inform them and take proper action?

**[The Workflow Event Pattern](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1414.png)** (see [Reactive Architecture](https://www.reactiveprinciples.org/)) is one way to address error handling in asynchronous setting which addresses *resiliency* and *responsiveness* concerns. It works like the following:
* An Event Product sends an initiating event to the Event channel.
* Initiating event is accepted by the Event Consumer. 
* The Event Consumer spots an error/issue/excepton with the event and forwards without thinking much about it to the event channel that directs events to the workflow processor.
* THe Workflow processor can accept the faulty event and then use either some logic/AI to modify the event and sends it back to the original event channel for re-processing.
* Alternatively the Workflow processor can send the event to a dashboard operated by end user or internal user for manual review/modifications. Once modified, the event can be channeled back to the original event channel for re-processing.
* **IMPORTANT**: This pattern will result in some out-of-order events. Take necessary design/implementation considerations to deal with this. See [Building Event-Driven Microservices: Chapter 6 Deterministic Streeam Processing](https://www.oreilly.com/library/view/building-event-driven-microservices/9781492057888/)

### Preventing Data Loss

Data loss is when a message is dropped or never makes it to its final destination. In a [typical scenario](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1416.png) there are 3 areas of potential data loss.
* Issue 1: An Event Processor fails to get a message to the queue/event channel.
    * Solution: Use *persistent message queues* and *synchronous send*. Also known as guaranteed delivery.
* Issue 2: An Event Processor de-queues the next message and crashes before processing it.
    * Solution: Use *client acknowledgement mode* instead of *auto acknowledge mode* which dictates that the client must first acknowledge that it was received before dropping the message.
* Issue 3: An Event Processor is unable to persist some data related to a message to a database.
    * Solution: Use ACID properties for DB communication and *Last Participant Support (LPS)* for removing the message from the persisted queue by acknowledging that the processing has been completed.

[Solution Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1417.png)

### Broadcast Capabilities

Another unique characteristic of event-driven architecture style is the ability to broadcast knowledge/events/messages without the need to know who is listening which is great for decoupling.

[Solution Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1418.png)

### Request-Reply

Sometimes synchronous communication is required which requires request-reply patterns. This is accomplished with *request-reply messaging (aka psydosynchronous communication)*. Note that there 2 popular ways to implement this by using *[Correlation ID](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1420.png)* or *[temporary queues](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1421.png)*.

[Solution Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1419.png)

### Hybrid Event-Driven Architectures

Event-driven architectural style can be used in conjunction with other architectural styles. Adding event-driven to any architectural style helps remove bottlenecks, provides a back pressure point in the event requests getting backed up, and provides a level of user responsiveness not found in other architectural styles.

Examples:
* Event-Driven + Microservices
    * Leverages Event-Driven for data pumps, async data sending, programmatic scalability
* Event-Driven + Space-Based
    * * Leverages Event-Driven for data pumps, async data sending, programmatic scalability (processing units)
* Event-Driven + Microkernel
* Event-Driven + Pipeline

## Versioning

[See Versioning](../topics/events/versioning.md)

## Characteristics

| Characteristic    | Rating       |
| ---               | ---          |
| Partitioning Type | Technical    |
| Number of quanta  | 1 to many    |
| Deployability     | ⭐⭐⭐      |
| Elasticity        | ⭐⭐⭐      |
| Evolutionary      | ⭐⭐⭐⭐⭐ |
| Fault Tolerance   | ⭐⭐⭐⭐⭐ |
| Modularity        | ⭐⭐⭐⭐    |
| Overall cost      | ⭐⭐⭐      |
| Performance       | ⭐⭐⭐⭐⭐ |
| Reliability       | ⭐⭐⭐      |
| Scalability       | ⭐⭐⭐⭐⭐ |
| Simplicity        | ⭐           |
| Testability       | ⭐⭐         |

## Resources

* [Building Event-Driven Microservices: Leveraging Organizational Data at Scale](https://www.oreilly.com/library/view/building-event-driven-microservices/9781492057888/)
* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/)
* [Reactive Manifesto](https://www.reactivemanifesto.org/)