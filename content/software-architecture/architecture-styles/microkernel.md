[<< Back To Overview](./readme.md)

# Architecture Style: Microkernel

![Microkernel Architecture Style Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1201.png)

*Alternative names: plug-in architecture*

## Description

A natural fit for product applications that one can download and install as a single (monolithic) installation, but also used in many non-product business applications. Some programming frameworks or programming tools tend to use this also.

There are 2 components, the **core system** and the **plug-in** components. All application logic is divided between independent plug-in components and the basic core system, providing extensibility, adaptability, and isolation of application features and custom processing logic.

A good example is the Visual Studio Code IDE, a core system that delivers basic functionality, but can be extended with various plugins. The idea is to have a system that delivers a basic functionality, but it can be extended, while keeping the core clean. In modern media it might be referred to as a "clean core".

Plug-ins can be shipped, modified, released at another release frequency than the core system and those plug-ins can be developed, maintained, and published by the end user itself or 3th parties. Logic is Nicely isolated in plugins which allows for a nice separation of concern. 

### Core System

This contains the minimum functionality to run the system. Or one could also call it "the happy path" through the application without any customer or special logic. The Core System naturally can use another architectural style for its internal structure. Usually a layered style architecture.

[Core System Design Examples](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1202.png)

### User Interface

The presentation layer can be embedded in the core system or implemented as a separate layer, or have a microkernel architecture on it's own.

[Presentation Layer Design Examples](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1203.png)

### Plug-in Components

Standalone, independent components containing specialized processing, additional features, and custom code to enhance or extend the core system. Highly volatile code can be separately developed, designed, tested, and released without touching the core system. 

**Ideally, plug-ins are independent from each other.**

Plugins can be distributed as JAR, DLL, or similar artifacts based on the technology used for the core system. Based on desired characteristics, plug-ins are compile-based or runtime-based. Other alternatives are possible like REST or messaging as communication channel between the plug-in and core system.

However, when opting for REST/messaging, you are looking more at a distributed architecture, therefore you might want to consider other distributed architecture styles for your solution.

[Plug-in Example 1](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1204.png)
[Plug-in Example 2](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1205.png)
[Plug-in Rest Example](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1206.png)

### Data Storage

It is not common, and maybe also not desirable for plug-ins to use the core system database for storage. Else a strong coupling between the core system and the plug-in would emerge. A plug-in, to respect its independence and isolation, should have it's own data store.

[Data Store Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1207.png)

### Registry

The core system needs to know which plug-in components are available and how to get to them. Hence, the core system must have some "registry" that keeps track of these things.

### Contracts

Clear contracts are required for being able to communicate between the core system and the plug-ins. These can be implemented as XML, JSON, or actual objects. Keep data contract evolution in consideration. Meaning, in case these contracts change over time as the core system might change to support new features or deprecate old.

## When To Use

* When creating software, or development tools that have a need for high extendability.
    * IDE's, Build Tools, Jenkins, Jira, Frameworks, browsers
* When creating a product-based software that want's to allow an ecosystem of 3th party developers to extend your product or tool. 
* Large Business applications could benefit also from this, see ERP software.
    * E.g. special plugins when you need to comply with special regulation, etc.

## When NOT To Use

Focus on the few areas where this is applicable. If not of the above meet your use cased or has similarities, you probably don't want to consider this architectural style.

## Considerations

None

## Characteristics

| Characteristic    | Rating       |
| ---               | ---          |
| Partitioning Type | Domain & Technical    |
| Number of quanta  | 1            |
| Deployability     | ⭐⭐⭐      |
| Elasticity        | ⭐           |
| Evolutionary      | ⭐⭐⭐      |
| Fault Tolerance   | ⭐           |
| Modularity        | ⭐⭐⭐      |
| Overall cost      | ⭐⭐⭐⭐⭐ |
| Performance       | ⭐⭐⭐      |
| Reliability       | ⭐⭐⭐      |
| Scalability       | ⭐           |
| Simplicity        | ⭐⭐⭐⭐ |
| Testability       | ⭐⭐⭐        |

## Resources

None