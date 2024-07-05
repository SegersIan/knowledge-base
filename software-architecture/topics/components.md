# Components

Components are the physical manifestation of a module and group artifacts together. Nothing requires you to use components, it just happens to be that its useful to have a higher level of modularity. Components form the fundamental modular building blocks in architecture.

Typically the architect defines, refines, manages, and governs components. Architecture is independent of the development process. Generally tne component is the lowest level of the software system an architect directly interacts with. Architects must identify components as one of the first task of a new project. But before an architect can identify components, they must know how to partition architecture.

## Component Scope

The scope of a component can manifest/decided in various ways:

* The simplest component wraps code at higher level of [modularity](../topics/modules.md) than classes. This is often called a library, libraries are usually compile-time dependencies (DLL notable exception).
* Components also appear as subsystems or layers in architecture as deployable units of work. Another type of component, a service, tends to run in its own address spaces and communicates via low-level networking protocols like TCP/IP or higher-level formats like REST or message queues, forming stand-alone, deployable units in architectures like microservices.

Scope directly impacts the granularity of the component which is one of the bigger challenges that architects face. 

* [Diagram: Varieties of components](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0801.png)
* [Diagram: Microservice might not require components if is small enough](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0802.png)

## Technical vs Domain Partitioning

Systems are decomposed/partitioned in one or more components by doing top-level partitioning. There are 2 approaches on how to approach this partitioning of components. *The top-level partitioning is of particular interest to architects because it defines the fundamental architectural style and way of partitioning code. As always, each partitioning approach has trade-offs. **Choosing technical or domain partitioning approach is one of the first decisions an architect must make**.

* **Technical Partitioning**: Organizing architecture based on technical capabilities like the layered architecture. 
    * The organizing principles of this architecture is separation fo technical concerns.
    * This separation enables developers to find certain categories of the code base quickly, as its organized by capabilities.
    * However, most realistic software systems require workflows that cut across technical capabilities.
    * Emphasizes reuse, redundancy should be less tolerated. Might result in stronger coupling.
* **Domain Partitioning**: Organizing architecture by (workflow and/or business) domain rather than technical capabilities.
    * Domains better reflects the kind of changes that most often occur on projects.
    * Reuse is less desirable, redundancy should be more tolerated.
    * [See DDD](domain-driven-design.md) as a methodology on defining domains. Should result in less coupling.

Diagrams
* [Diagram: 2 types of top-level architecture: layered and modular](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0803.png)
* [Diagram: Technical vs Domain partitioning](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0804.png)

### Comparison

| | Domain Partitioning | Technical Partitioning |
| --- | --- | --- |
| Advantages | - Models closely toward how the business functions rather than the implementation detail<br>- Easier to utilize the Inverse Conway Maneuver to build cross-functional teams around domains<br>- Align more closely to the modular monolith and microservices architecture styles.<br>- Message flows matches the problem domain<br>- Easy to migrate data and components to distributed architecture. | - Clearly separates customization code.<br>- Aligns more closely to the layered architecture pattern. |
| Disadvantage | - Redundancy of some else, reusable logic. | - Higher degree of global coupling.<br>- Developers may have to duplicate domain concepts in different layers<br>- Typically higher coupling at the data level. Meaning application and data architects must collaborate closely |

## Identifying Components

Have a look at the [Component Identification Flow/Cycle Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0808.png) to see how the individual steps related. Component identification works best as an iterative process, producing candidates and refinements through feedback.

1. **Identify Initial Components**: Must somehow determine that top-level components to begin with, based on the top-level partitioning approach (Technical vs Domain). The likelihood of achieve a good design from this initial set components is near to 0.
2. **Assign Requirements To Components**: Align requirements (or user stories) to those components to see how well they fit. This may entail creating new components, consolidating existing ones, or breaking components apart.
3. **Analyze Roles and Responsibilities**: Look at the roles and responsibilities elucidated during the requirements to make sure that the granularity matches, finding the correct granularity is one of the greater challenges. Therefore, think about both the roles and behaviors the application must support that allows the architect to align the component and domain granularity.
4. **Analyze Architecture Characteristics**: Look at the architecture characteristics discovered earlier in order to think about how they might impact component division and granularity. For example, while two parts of a system might deal with user input, the part that deals with hundreds of concurrent users will need different architecture characteristics than another part that needs to support only a few. Thus, while a purely functional view of component design might yield a single component to handle user interaction, analyzing the architecture characteristics will lead to a subdivision.
5. **Restructure Components**: Feedback is critical,  so continually iterate on their component design with developers. An iterative approach is key. As the architects and developers delve more deeply into building the application, they gain more nuanced understanding of where behavior and roles should lie.

## Component Granularity

Finding proper granularity is one of the most difficult tasks for an architect. 

* Too fine-grained component design leads to too much communication between components to achieve a result. 
* Too coarse-grained component design leads to difficulties in deployability and testability + [modularity](modules.md) related negative effects.

## Component Design

The goal is an initial design that partitions the problems space in coarse chunks that take into account different architecture characteristics. There are different approaches in identifying components.

* [**[Anti-Pattern] Entity Trap**](anti-patterns.md#anti-pattern-entity-trap)
* **Actor/Actions Approach**: Popular way to map requirements to components. Originally in the Rational Unified Process (RUP), architects identify who performs activities with the application and the actions those actors might perform. 
    * Works well for monolithic and distributed systems.
    * Works well for technical and domain partitioning.
* [**Event Storming Approach**](domain-driven-design.md): Polar with microservices, the architect assumes the project will use messages and/or events to communicate between various components.
    * Works well for distributed systems with messages/events.
    * Works well for domain partitioning.
* **Workflow Approach**: Models the components around workflows, much like event-storming, but without the explicit constraints of building a message-based system. A workflow approach identifies key roles, determines the kind of workflows these roles engage in, and builds components around the identified activities.
    * An alternative to Event Storming, more generic for those wo are not using DDD or messaging.
    * Works well for distributed systems with messages/events.
    * Works well for domain partitioning.
    

None of these techniques is superior to the others; all offer a different set of trade-offs.  When using waterfall, the Actor/Action approach works well. When doing DD and distributed styles, event storming might be a good fit.

## Choosing Between Monolithic vs Distributed Architectures

Read [Architecture Styles](../architecture-styles/readme.md#monolithic-vs-distributed-architectures)

## Resources

* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 8
