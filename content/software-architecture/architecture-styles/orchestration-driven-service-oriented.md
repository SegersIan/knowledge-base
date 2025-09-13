[<< Back To Overview](./readme.md)

# Architecture Style: Orchestration-Driven Service-Oriented

![Orchestration-Driven Service-Oriented Architecture Style Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1601.png)

## Description

### Topology

* **Business Services**: Sit on top of the architecture and are the entry point. These services did not contain code, just input, output, and sometimes schema information.
    * Examples: `ExecuteTrade`, `PlaceOrder` ("Are we in the business of..." as guiding principle)
* **Enterprise Services**: Fine-grained, shared implementations. Highly specialized atomic building blocks for the coarse-grained business services. These are tied together via the orchestration engine. Given a good collection of reusable enterprise services, one could easily change any business process. Composition was the goal. 
    * Examples: `CreateCustomer`, `CalculateQuote`
    * Concerns: Dynamic nature of reality defies these attempts (Business Components are not static, solutions change, markets change, technologies change)  
* **Application Services**: One-off, single-implementations, a service that would be used only once. So  you don't invest on making it reusable.
    * Examples: `GeoLocationService`
* **Infrastructure Services**: Operational services like monitoring, logging and such.
* **Orchestration Engine**:  Heart of the architecture. Stitching business service implementations together using orchestration of the Enterprise Services basically. The database usually was one shared one. This acts an an integration hub.
* **Message Flow**: All requests flow through the orchestration engine, cause the logic of the architecture lives here.

### Why It's bad

This is a historical **anti-pattern architectural style** which is worth documenting as one might find these in the wild. It helps to understand historically why the emerged, why they were made, and why it made sense at that point in time. We can also draw some insights from this.

This style of service-oriented architecture appeared just as companies were becoming enterprises in the late 1990s: merging with smaller companies, growing at a breakneck pace, and requiring more sophisticated IT to accommodate this growth. Computing resources were scarce, precious, and commercial. Distributed computing had just become possible and necessary, and many companies needed the variable scalability and other beneficial characteristics.

External drivers forced architects towards distributed architects with significant constraints. OSS was not properly accepted by enterprise, OS's and licenses were expensive. Due to the insane pricing, architects were forced to reuse anything. Reuse became the dominant philosophy in this architecture. This extensive reuse philosophy and technical partitioning results in strong coupling which made change excruciating over time.

When a team builds a system primarily around reuse, they also incur a huge amount of coupling between components. By reusing and centralizing everything, domains became bloated. A "entity-driven-design" approach emerged, where the `CustomerProfile`  service would contains also the `DrivingLicenseInfo` while 9/10 the business services would not care about such information. However this `DrivingLicenseInfo` exposed to all other services. So the size and the technical nature of partitioning cause strong coupling across the entire architecture.

[Reuse Example 1](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1603.png)
[Reuse Example 2](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1604.png)

**This architecture thought us, that a extreme focus on technical partitioning and reuse does not scale.**

## When To Use

Never

## When NOT To Use

This always applies, do not use it.

## Considerations

## Characteristics

| Characteristic    | Rating       |
| ---               | ---          |
| Partitioning Type | Technical    |
| Number of quanta  | 1            |
| Deployability     | ⭐           |
| Elasticity        | ⭐⭐⭐           |
| Evolutionary      | ⭐           |
| Fault Tolerance   | ⭐⭐⭐           |
| Modularity        | ⭐⭐⭐           |
| Overall cost      | ⭐ |
| Performance       | ⭐⭐        |
| Reliability       | ⭐⭐      |
| Scalability       | ⭐⭐⭐⭐           |
| Simplicity        | ⭐ |
| Testability       | ⭐        |

## Resources

None