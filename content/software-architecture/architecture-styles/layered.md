[<< Back To Overview](./readme.md)

# Architecture Style: Layered

![Layered Architecture Style Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1001.png)

*Alternative names: n-tier architecture*

## Description

When we talk about "A monolith" most people will be referring to the layered architecture style. Although not entirely wrong, there are some other architectural styles which are categorized as monolith. See the [architectural styles overview](./readme.md) for more.

The layered approach is perfect for small, simple applications like web applications. Code is partitioned from a technical view. All code of the presentation layer goes into the presentation layer, disregarding the domain or entity it relates to.

Components within the layered architecture style are organized logical horizontal layers, each layer performing a specific role within the application. The amount of layers is not fixed, but 3 or 4 tiers are most common. It is important that each boundary of each layer is respected. Each layer has a distinct responsibility and role. Following the separation of concerns.

### Open/Closed Layers

As a request travels through the system and its layers, each layer can be either **open** or **closed**:
* The request cannot skip **Closed** layers.
    * See [Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1003.png)
* The request can skip **Open** layers.
    * See [Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1005.png)

If you want to avoid open layers, you can move shared components in the relevant layer. So the top layer can then call any component or shared component in that underlying layer ([Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1004.png))

### Physical Separation

Layers can be physically separated (separated binaries, DLLs, JARs) but don't have to. The physically separations can be done in various combinations (e.g. Business Layer placed in the same DLL as the Persistence Layer). However a phsyicall group should only contain layers which are adjacent to each other. You would never put the Presentation Layer and Database Layer in one physical component while putting the Business and Persistence Layer outside.
[Examples of different Physical seperation](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1002.png)

## When To Use

* Starting point when its not known yet which architectural style eventually will be used.
* Very tight budget or time constraints.
* Use it for a service or (web) application that has a very narrow and clear domain or responsibility.
* A micro-service style architecture could use the layered style within each individual micro-service.
* Many developers are familiar with it.

## When NOT To Use

* When the domain of the system is very wide in scope.

## Considerations

* Physical layering can exist in numerous combinations.
* Each layer has a distinct responsibility and role. Following the separation of concerns.
* A layer can only call the next layer underneath itself. No skipping layers. A request travels from top to bottom the response the other way up.
* Layers of isolation, changes in a single layer should have no impact or little on the other layers.

### Anti-Pattern: Architecture Sinkhole

When a request travels through all the layers and back up without any additional business logic. Let's say you want to fetch a user profile, the request travels through all the 4 layers to the database, fetches the user profile and just returns that model all the way up without business logic, transformation, aggregate, or calculation. This anti-pattern will manifest a few times, but should not grow out of control. Reason why this can be bad, is that it might result in unnecessary memory and compute resources. **Therefore, one can consider opening up all layers. Trade-off of that is that change will be harder to manage.**

**TIP: Use 80/20, only 20% of request should pass through sinkhole, if 80% of request pass through the sinkhole, maybe consider another architecture style.**

## Characteristics

| Characteristic    | Rating       |
| ---               | ---          |
| Monolithic/Distributed | Monolithic    | 
| Partitioning Type | Technical    |
| Number of quanta  | 1            |
| Deployability     | ⭐           |
| Elasticity        | ⭐           |
| Evolutionary      | ⭐           |
| Fault Tolerance   | ⭐           |
| Modularity        | ⭐           |
| Overall cost      | ⭐⭐⭐⭐⭐ |
| Performance       | ⭐⭐        |
| Reliability       | ⭐⭐⭐      |
| Scalability       | ⭐           |
| Simplicity        | ⭐⭐⭐⭐⭐ |
| Testability       | ⭐⭐        |

## Resources

None