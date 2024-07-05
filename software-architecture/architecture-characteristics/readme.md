# Architecture Characteristics

The software development process has many techniques for (functional) requirement gathering. Mostly functional. As architect, one must consider many other factors in addition to those requirements that are not directly related to the domain functionality.

## Description

The important aspects of the system, independent of the problem domain.

Characteristics describe our desired behavior of a system across different dimensions. it is important to understand the desired characteristics and to make an explicit commitment to them. A system must not comply or concern itself about all the possible Architecture Characteristics that we can think of, cause for each system, this will differ.

What is important, is that a conscious and explicit decision is made of what Architecture Characteristics are important for given system. In addition these decisions must be clear and preferably quantifiable so it is easy to asses of the system complies with desired characteristics or not.

*Characteristics are often interconnected*. This means it can be often challenging to accommodate various characteristics as they might oppose each other in design. Hence, why it is important to be picky and limited in the preferred characteristics that you prioritize. As always, it's a trade-off.

> *Note: Non-Functional requirements are the same, but not considered a good name.*

## Criteria Of A Characteristic

[See Criteria Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0402.png)

* **Criteria 1: Specifies a non domain design consideration**
    * Explicit - Usually/might appear in requirement documents
    * Specify operational and design criteria for success, concerning how to implement the requirements and why certain choices were made.
    * Example: Performance never appears in requirements documents, but we need to specify which level of performance is desired.
* **Criteria 2: Influences some structural aspect of the design**
    * Implicit: Usually don't appear in requirement documents
    * Does this characteristic require special structural considerations to succeed?
    * Example: Security is baseline requirement, but when you need to facilitate payment, if you use a third-party payment processor or in-application payment processing, you might reconsider how to structure this. This characteristic will have impact on the architecture if you do in-application and security is a concern
* **Criteria 3: Is critical or important to application success**
    * Support for each characteristic adds complexity to the design. Therefore, the least characteristics the better.

## Categories

Everyone might create their own interpretation of these terms, but we commonly separate them into 3 categories.

* **Operational**: Overlap heavily with operations and DevOps concern.
* **Structural**: Code quality concerns, such as modularity, coupling between components, code quality and such.
* **Cross-Cutting**: When the category is less clear or has overlap.

## List Of Characteristics

A universal list doesn't seem feasible, there are various variations and interpretations of possible characteristics. Ideally you make a list with definitions for your organization to align around the names, definitions, and their scope. 

However, below is a list of examples to help you get started. You can also see the [ISO 25010 list](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010) for inspiration.

| Term | Category | Definition/Example |
| ---  | ---      | ---        |
| Availability | Operational | How long does the system need to be available ? (e.g. 99.9% up) |
| Continuity | Operational | Disaster Recovery capability |
| Performance | Operational | Response time |
| Recoverability | Operational | Business continuity requirements (e.g. ISO27001) |
| Reliability | Operational | Fail-safe? Mission critical in a way that it affects lives |
| Robustness | Operational | Ability to handle errors and boundary conditions while running if the internet connection drops |
| Scalability | Operational |  Ability of the system to perform and operate as the number of users/requests increases |
| Configurability | Structural | Ability for end users to change aspects of the software configuration |
| Extensability | Structural | How important is it to plug new pieces of functionality in |
| Installability | Structural | Ease of system installation on all necessary platforms |
| Reuse | Structural | Ability to reuse common components across multiple products |
| Localization | Structural | Support for multiple (human) languages |
| Maintainability | Structural | How easy to apply changes and enhance the system |
| Portability | Structural | Does the system need to run on more than one platform? |
| Supportability | Structural |  What level of technical support is needed by the application ? |
| Upgradeability | Structural |  Ability to easily upgrade from previous versions |
| Accessability | Cross-Cutting | Access to all your users, including those with disabilities |
| Archivability | Cross-Cutting | Will the data need to be archived or deleted after some time ? |
| Authentication | Cross-Cutting | Security requirements to ensure users are who they say they are |
| Authorization | Cross-Cutting | Ensure users can access only what they are allowed to access |
| Legal | Cross-Cutting | GPDR ? Data protection ? |
| Privacy | Cross-Cutting | Ability to hide transactions from internal company employees. |
| Security | Cross-Cutting |  Does the data need to be encrypted at-rest or in-transport ? |
| Usability | Cross-Cutting | Level of training required for users to achieve their goals |

## Identifying Characteristics

The aforementioned list is mostly about implicit architecture characteristics, there are at least 2 more ways to uncover architecture characteristics:

### Extract From Domain Concerns

Listen well to domain/business stakeholders and understand their concerns. Don't mistake a single concern as one characteristic.

| Domain Concern Example | Architecture Characteristics |
| ---                    | ---                          |
| Merges & Acquisitions  | Interoperability, Scalability, adaptability, extensibility |
| Time To Market         | Agility, Testability, Deployability |
| User Satisfaction      | Performance, availability, Fault tolerance, testability, deployability, agility, security |
| Competitive Advantage  | Agility, testability, deployability, scalability, availability, fault tolerance |
| Time and Budget        | Simplicity, feasibility |

### Extract From Requirements

Sometimes there are explicit requirements (e.g. min/max amount of users) or just from having a lot of domain knowledge. If you have a class registration system that is once per year used, for 24h, all students will need to use it. You probably only need to deal with a small peak, and further not worry about availability.

## Measuring Characteristics (Governance)

Common problems around the definition of architectural characteristics:
* They aren't physics: Many characteristics have vague meanings.
* Wildly varying definitions: Within same organization, departments may disagree on the definition.
* Too Composite: Many characteristics comprise many other at smaller scale (e.g. agility => modularity, deployability, testability)

There are 3 types of measurements:
* **Operational**: Many characteristics have direct measurements. However many nuanced interpretations. The average response time can be for one team good enough, for the others the 1% that take 10 times longer are relevant to care about.
* **Structural**: Comprehensive metrics for internal code quality don't yet exists. Some metrics and common tools do allow architects to address some critical aspects of code structure, albeit along narrow dimensions. A good example is [cyclomatic complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity).
* **Process**: Some characteristics interest with software development processes. Agility may decompose into features as testability and deployability. Testability is measurable through code coverage tools.

Governance is an important role of an Architect, negligence can lead to disastrous quality problems. [Fitness functions](../topics/evolutionary-architecture.md#fitness-functions) are excellent to help with this.

## Scope of Characteristics

When architects talk about scalability, generally that discussion is around the scalability of the entire system. That was a safe assumption a decade ago when everything was monolithic. With the advent of new architectural styles like microservices, the scope of architecture characteristics has narrowed considerably. When evaluating many operational architecture characteristics, an architect must consider dependent components outside the code based that will impact those characteristics.

In modern systems, architects define architecture characteristics at the *quantum level* rather than system level.

### Architectural Quanta

To successfully design, analyze, and evolve software, developers must consider all the *coupling points that could break*. To identify these coupling points, consider the architecture quantum boundaries. So what is an architecture boundary?

> An independently deployable artifact with high functional cohesion and synchronous connascence.

* **Independently Deployable**: Includes necessary components to function independently from other parts of the architecture. A database used by an application, is a part of the quantum, because without the database, the application wont work.
* **High Functional Cohesion**: How well the contained code is unified in purpose. This implies that an architecture quantum does something purposeful. The [bounded context from DDD](../topics/domain-driven-design.md) is a good example of high functional cohesion.
* **Synchronous Connascence**: Implies synchronous communication within an application context or between distributed services tha form this architecture quantum. [Connascence is a indication of modularity](../topics/modularity.md).

## Resources

* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) | Chapters 4, 5, 6, 7
* [Tolerance for Imperfection](https://deviq.com/principles/tolerance-for-imperfection)