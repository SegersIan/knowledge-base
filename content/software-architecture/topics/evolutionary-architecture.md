# Evolutionary Architecture

## Introduction

All architectures evolve, they have to, every system changes over time due to internal factors (technology changes, new use cases) and external factors (the industry changes, new markets, ...).
It only makes sense to look at your architecture as something that evolves over time for various reasons.

Evolutionary architecture defines the concept of a **fitness function** to measure certain architectural characteristics over time. By collecting this data from fitness functions, one can see how architectural characteristics are affected as the architecture evolves over time.
With this data to your disposal, you can observe if changes negatively or positively affected your architecture. This observability of your architecture allows you to react and adjust accordingly the development of your architecture in a way that desired characteristics are conserved.

Fitness functions overlap many existing verification mechanisms, depending on the way they are used (as metrics, monitors, unit test libraries, chaos engineering, and so on.).

[More on architectural characteristics](../architecture-characteristics/readme.md)

> Remember: Change is constant, so might as well accept that and plan for it

## Fitness Functions

> Fitness Function: Any mechanism that performs an objective integrity assessment of some architecture characteristic or combination of architecture characteristics.

* ***Any mechanism***: Wide variety of tools to implement fitness functions.
* ***Objective integrity Assessment***: Objective definitions for architecture characteristics.
* ***some architecture characteristic or combination of architecture characteristics***: There are 2 scopes for fitness functions
    * *Atomic*: Validates a single architecture characteristic
    * *Holistic*: Validates a combination of architecture characteristics. Exercises a combination of interlocking architecture characteristics to ensure that the combined effect won't negatively affect the architecture.

One implements fitness functions to build protections around unexpected change in architecture characteristics.
The separation between fitness functions and unit tests provide a good scoping guideline for architects. Fitness functions validate architecture characteristics, not domain criteria; unit tests are the opposite.

***You can decided wether a fitness function or unit test is needed by asking the question:***

> Is any domain knowledge required to execute this test? If "yes", then a unit/function/user acceptance test is appropriate; if "no", then a fitness function is needed.

### Automated vs Manual

Fitness functions are ideally automated, although in some occasions, manual work might be required.

### When to run?

Automated fitness functions certainly qualify well be a part of your continuous integration pipeline. Manual fitness functions depend on the use case an scope, but probably at some integration or user acceptance phase. Do what makes most sense to you.

### Examples

* **Cyclic Dependencies Between Components**: Create an automated test (e.g. with jDepend) to detect any cyclic dependencies between components. 
* **Respect Layered Architecture**: Create an automated test to detect if the set rules for your layered architecture are respected (nowhere are closed layers skipped).
* **Distance from the main sequence**: This is characteristic regarding [modularity](../topics/modularity.md)

### Tools

* [jDepend](https://github.com/clarkware/jdepend)
* [ArchUnit](https://www.archunit.org/)
* [NetArchTest](https://github.com/BenMorris/NetArchTest)
* [SonarQube](https://www.sonarsource.com/)

## Architectural Coupling

Todo...

## Evolutionary Data

Todo...

## Building Evolvable Architectures

Todo...

## Pitfalls and Anti-Patterns

Todo...

## In Practice

Todo...

## Todo...

...mention that by doing the right decoupling and layers within a component or overal architecture, it allows to change things over time with a limited blast radius (e.g. swap out the database).

## Resources

* [Building Evolutionary Architectures: Support Constant Change](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/)
* [Software Architecture: The Hard Parts](https://architecturethehardparts.com/)