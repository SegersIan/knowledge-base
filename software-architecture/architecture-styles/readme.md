# Architecture Styles

Architecture styles can be use for the architecture of a whole system, but these styles can be also combined. One does not exclude the use of others.

As per usual, you need to select the style(s) based on your needs. Remember, as an architect, you must understand your needs for the system.

## Monolithic vs Distributed Architectures

Neither is better than the other, each answers a specific set of needs. The fundamental decision rests on how many [quanta](../architecture-characteristics/readme.md#architectural-quanta) the architect discovers during the design process. If the system can manage with a single quantum (in other words, one set or architecture characteristics), then a monolithic architecture offers many advantages. On the other hand, differing architecture characteristics for components requires distributed architecture to accommodate the differing architecture characteristics.

The ability to determine a fundamental design characteristic of architecture (monolith vs distributed) early in the design process highlights one of the advantages of using the architecture quantum as a way of analyzing architecture characteristics scope and coupling.

Read about [components](../topics/components.md) that can assist in the thought process in identifying your components and what architectural style might be more suitable. You can't understand architectural styles without understanding [Architecture Characteristics](../architecture-characteristics/readme.md) and [components](../topics/components.md).

## Distributed Architecture Considerations

[Wiki Page](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing)

The 8 Fallacies:
1. The Network Is Reliable ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0902.png))
2. Latency Is Zero ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0903.png))
3. Bandwidth Is Infinite ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0904.png))
4. The Network Is Secure ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0905.png))
5. The Topology Never Changes ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0906.png))
6. There Is Only One Administrator ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0907.png))
7. Transport Cost Is Zero ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0908.png))
8. The Network Is Homogenous ([Illustration](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0909.png))

Other considerations:
* Distributed logging
* Distributed transactions
* Contract maintenance and versioning (evolution)

## Physical units vs Logical Components

A logical component is a grouping of responsibilities (namespace), the physical units refers to units of deployability (e.g. JARs or DLLs). Physical units can still co-exist on the same host. They don't need to be distributed over different hosts.

## Styles Comparison

| Characteristic/Name    | [Ball Of Mud](ball-of-mud.md) | [Layered](layered.md)  |[Pipeline](pipeline.md)   |[Microkernel](microkernel.md)    |[Service-Based](./service-based)|  [Event-Driven](event-driven.md)|  [Space-Based](space-based.md)    |  [Orchestration-Driven Service-Oriented](orchestration-driven-service-oriented.md)|  [Microservices](microservices.md) |
| ---                    | ---           | ---          |---            |---                | ---             | ---              | ---                 | ---                                       | ---                |
| Monolithic/Distributed | Monolithic    | Monolithic   | Monolithic    |Monolithic         | Distributed     | Distributed      | Distributed         | Distributed                               | Distributed        |
| Partitioning Type      | None             | Technical      | Domain & Technical| Domain          | Technical         | Domain & Technical | Technical                                 | Domain             | Domain |
| Number of quanta       | 1             | 1            | 1             |1                  |1 to many        | 1 to many         | 1                  | 1                                          | One to many       |
| Deployability          | ⭐           | ⭐           | ⭐⭐        | ⭐⭐⭐           | ⭐⭐⭐⭐      |  ⭐⭐⭐          | ⭐⭐⭐           | ⭐                                        | ⭐⭐⭐⭐         |
| Elasticity             | ⭐           | ⭐           | ⭐           | ⭐                | ⭐⭐           | ⭐⭐⭐          | ⭐⭐⭐⭐⭐       | ⭐⭐⭐                                  | ⭐⭐⭐⭐⭐       |
| Evolutionary           | ⭐           | ⭐           | ⭐⭐⭐      | ⭐⭐⭐           | ⭐⭐⭐         | ⭐⭐⭐⭐⭐     | ⭐⭐⭐           | ⭐                                        | ⭐⭐⭐⭐⭐       |
| Fault Tolerance        | ⭐           | ⭐           | ⭐           | ⭐                | ⭐⭐⭐⭐      |  ⭐⭐⭐⭐⭐    | ⭐⭐⭐            | ⭐⭐⭐                                   | ⭐⭐⭐⭐         |
| Modularity             | ⭐           | ⭐           | ⭐⭐⭐      | ⭐⭐⭐           | ⭐⭐⭐⭐      | ⭐⭐⭐⭐        | ⭐⭐⭐            | ⭐⭐⭐                                  | ⭐⭐⭐⭐⭐       |
| Overall cost           | ⭐           | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐      | ⭐⭐⭐⭐      | ⭐⭐⭐          | ⭐⭐               | ⭐                                       | ⭐                 |
| Performance            | ⭐           | ⭐⭐         | ⭐⭐        | ⭐⭐⭐           | ⭐⭐⭐        | ⭐⭐⭐⭐⭐      | ⭐⭐⭐⭐⭐       | ⭐⭐                                     | ⭐⭐              |
| Reliability            | ⭐           | ⭐⭐⭐      | ⭐⭐⭐      | ⭐⭐⭐           | ⭐⭐⭐⭐      | ⭐⭐⭐          | ⭐⭐⭐⭐          | ⭐⭐                                     | ⭐⭐⭐⭐         |
| Scalability            | ⭐           | ⭐           | ⭐           | ⭐                | ⭐⭐⭐         | ⭐⭐⭐⭐⭐     | ⭐⭐⭐⭐⭐       | ⭐⭐⭐⭐                                | ⭐⭐⭐⭐⭐       |
| Simplicity             | ⭐           | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐         | ⭐⭐⭐        | ⭐               | ⭐                 | ⭐                                        | ⭐                 |
| Testability            | ⭐           | ⭐⭐        | ⭐⭐⭐      | ⭐⭐⭐            |⭐⭐⭐⭐       | ⭐⭐            | ⭐                 | ⭐                                        | ⭐⭐⭐⭐          |

## Shifting fashion in architecture

Preferred styles shift over time, driven by following factors:
* **Observations from the past**: Experience and observations of the past usually guides architects on finding solutions to these deficiencies that they experience.
* **Changes in the ecosystem**: These changes can remove/ease existing paint points or introduce new challenges. The introduction of Kubernetes allowed for lots of automation of automation.
* **New Capabilities**: Usually small and hidden new capabilities that shift radically what is possible or how things can work. Containers might have seemed just a natural evolution on virtual machines, but it had an enormous impact on the industry.
* **Acceleration**: Change is constant, but the velocity is always increasing of changes in the ecosystem. Resulting in new tools, engineering practices, with new design and capabilities.
* **Domain Changes**: The business changes, and its domain which developers constantly adapt to. Like mergers in companies.
* **Technology Changes**: Organizations try to follow some of the technological changes for their obvious benefits.
* **External Factors**: Maybe a design is just perfectly fine, but the licensing might change or the sun setting of vendor products, regulation, and conformity with standards can demand changes.
Always have an understanding of current industry trends and on how they make sense.

## Decide on a style

As we might have expected **IT DEPENDS** which one we choose an various factors like characteristics and which trade-off we are prepared to make. This section is some general advise.

### 1. Factors to be comfortable with

* **The Domain**: Understand important aspects of the domain, especially those affection operational architecture characteristics. No need to be subject experts, but have a good understanding of the major aspects.
* **Architecture characteristics that impact structure**: Discover and clarify the architecture characteristics needed to support the domain and external factors.
* **Data Architecture**: Data architecture is a specialization of its own. However, architects must understand the impact that data design might have on their design, particularly if the new system must interact with an older/existing data architecture.
* **Organizational Factors**: Budgets can influence the design, or vendor selection (licenses), or plans for merger & acquisitions might desired open solutions and integration architectures.
* **Knowledge of process, teams, and operational concerns**: Conway's Law, maturity in engineering practices, how teams are build will have an influence. A monolith is much harder with 10 squads than maybe one.
* **Domain/Architecture isomorphism**: Some problem domains match the topology of the architectural style, or be ill-suited for given style.

### 2. Determinations to be made

* **Monolith vs Distributed**: Will a single set of architectural characteristics suffice ? Monolith will suffice. If different parts of the system needs different architectural characteristics, distributed is most likely the answer.
* **Where should data live?**: In monolith, all data lives in one or few databases. In distributed, one must determine where data is persisted, and how it will flow. This means you must consider structure and behavior when designing an architecture. Don't be fearful of iterating. We call this also data partitioning.
* **What communication styles? (Sync vs Async)**: Once data partitioning is determined, what are the communication styles that we prefer? Synchronous communication presents fewer design, implementation, and debugging challenge. ***Default to synchronous when possible and use asynchronous when necessary.***