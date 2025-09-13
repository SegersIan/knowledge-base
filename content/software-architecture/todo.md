## Topics to cover - AKA THE TODO
* What is Software Enterprise Architecture
* How to get "TRUST" from the engineering team, and how to measure it (doing surveys for example)
* How to get architecture in the "AGILE" or "SAFE" ecosystem ?
* How to get architecture adapted all together
* Where/how does "clean Architecture" fit in ?
* Make a good split and difference between architecture and enterprise architecture
* Consider on how to discuss the points of Software Architecture and the hard parts book
* Consider how the architect elevator fits the big picture.
* Discuss managed evolution, but go deeper, what it solves or does. Like, IT allignment. Circle that back to the enterprise architecture and understand how the role of IT is perceived and the relation.
* Emphasize how 'data' and *'relations/connections* impact architecture.
* The concepts of "lenses/views" and how they can be used. Which are they, and when to use which ones?

* Look at managed evolution KPIs
* Make a throrough list of fitness function examples
* Domain Events, Event Driven Architecure, Even Sourcing...
    * https://martinfowler.com/articles/201701-event-driven.html
* "Emerging design/architecture"
* Add also something about all the database reading models, like eventual consistency and such. Cause this is very important when architecting or designing stuff, and the what you should take in consideration.
    * https://www.microsoft.com/en-us/research/wp-content/uploads/2011/10/ConsistencyAndBaseballReport.pdf
    * Also see the Data instensive applications
* Technology radar and application radar
* SAGA Pattern
    * Choreography (is basically event driven choreography, while orchestration is more SAGA as you would know it. I would do research if "SAGA Choreography" is really SAGA all together, read back the original whitepaper to validate.)
    * https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/saga/saga
    * Orchestration 
* Hexagonal Architecture

* ". I think that one of an architect’s most important tasks is to remove
architecture by finding ways to eliminate irreversibility in software designs." martin fowler

* "Software is not limited by physics, like
buildings are. It is limited by imagination, by design, by organization. In
short, it is limited by properties of people, not by properties of the world. “We
have met the enemy, and he is us.” - ralph johnson

* Architecture domains/domains/fields
    * Application Architecture
    * Integration Architecture
    * Infrastructure Architecture

## Architecture over time - patterns
Discuss patterns or techniques which allow to gradually migrate from todays architecture/design to the target architecture/design.

* Parallel Run
* Dark launching
* Feature toggles
* Strangler pattern
* Granualar roll out 
* Feedback channels
* ...

## Others

### Understanding Needs

To do good architecture, one must really try to understand the **needs of all the stakeholders** involved, and **understand their priorities**. **All your architectural decisions should be guided by the this**.

### Component Principles

### Component Chesion

*based on [Clean Architecture](https://www.amazon.com/dp/0134494164)*

### Component Coupling

*based on [Clean Architecture](https://www.amazon.com/dp/0134494164)*

### X is a Detail

*based on [Clean Architecture](https://www.amazon.com/dp/0134494164)*

- Add your thoughts on how this element is relevant in larger architectures, and about microservices , where if the service is small enough, it might be less "important". I think it's still relevant, to follow this,  but on a smaller scale. Cause it has a solid point to avoid "bleeding in" of external concepts/ideas/or such.

### Techniques and Soft Skills

* BASE
* ACID
    * What they mean, and how they related to architectures (monolith vs distributed etc...)
* emergent design and intentional architecture 

## Modelling
    * Go deeper on domain modelling techniques and approaches.

### Data 
* Draw the comparison with your blog on cloud services.
* Operational vs Anlytical data
* Data mesh
* Look at data intensive applications book to see 
* Data vs Application architecture might be a more mainstream approach.

### Concurrency Models
* What is covered in the book

### 7 databases in 7 weeks
* ANy thoughts from there

## Architecture Katas

## The role of patterns in architecture + a list of patterns (might be the parent placeholder for things like the SAGA.)

## Secure By Design

## Privacy By Design

## Technology Radar

## Application Radar

## Talk about emergent design, usually design emerges from the path of least resistance (technically or from organization, like, which team had the least bandwith or knows the stakeholder best?, they get to implement features). Also identify what other "forces" impact systems or emergent design more specific.

ChatGPT input:


When discussing emergent design or architecture in IT systems, especially in the absence of intentional design, several forces or "laws" akin to the law of the "path of least resistance" can be observed. These forces collectively influence the system's evolution and characteristics:

1. **Conway's Law**: This principle states that system designs are constrained to mimic the communication structures of the organization that creates them. In other words, the system's architecture will mirror the organizational structure.

2. **Accidental Complexity**: This refers to complexity that arises from the chosen tools, languages, or approaches rather than from the inherent complexity of the system itself. Over time, this accidental complexity can shape the system in unforeseen ways.

3. **Technical Debt**: As shortcuts are taken or temporary solutions are implemented, technical debt accumulates. This debt can guide future development choices, often leading to more complex and less optimal solutions.

4. **Survivorship Bias**: The systems or components that endure are often those that are good enough, not necessarily the best. This bias can guide the evolution of a system based on what works adequately under certain conditions, rather than what might be optimal in a different context.

5. **Erosion of Design**: Over time, the original design of a system can erode due to multiple incremental changes, leading to a structure that no longer resembles the intended design. This erosion shapes the emergent design.

6. **Resource Limitation**: The availability of resources (time, budget, skills) heavily influences system design. Constraints in these areas can lead to simpler, more pragmatic solutions.

7. **Feedback Loops**: The responses and feedback from a system's users or environment can significantly influence its evolution. Positive feedback may lead to the reinforcement of certain features or designs, while negative feedback may prompt changes.

8. **Evolutionary Design**: The system evolves over time through a process of natural selection, where the most successful features or components survive and less successful ones are discarded or modified.

9. **Market and User Demand**: Market trends and user needs can greatly influence the direction of a system's development, often pushing it in directions not initially anticipated.

10. **Regulatory and Compliance Forces**: Legal and compliance requirements can impose constraints on a system's design, often leading to architectures that prioritize compliance over other aspects.

These forces often interact with each other, leading to complex dynamics that shape the emergent design of IT systems. Understanding these forces can help in managing and guiding the evolution of such systems.

The list of ten forces shaping emergent IT system design was a curated selection, not an exhaustive one. There are indeed additional factors that can influence system architecture in the absence of intentional design:

11. **Technology Lock-In**: The initial choice of technology (like a programming language or platform) can constrain future development, leading to a path dependency where changing technologies becomes increasingly difficult and costly.

12. **Security Considerations**: Security needs can profoundly shape system architecture, often resulting in trade-offs with usability, performance, or cost.

13. **Scalability Needs**: The necessity to scale a system to handle increased load can lead to significant architectural changes, often emphasizing distributed systems, cloud computing, or microservices.

14. **Legacy Systems Integration**: The need to integrate with or build upon legacy systems can significantly influence architecture, often leading to more complex and less ideal solutions.

15. **Performance Optimization**: The drive to optimize for performance can lead to specific architectural choices, such as the use of certain algorithms, data structures, or hardware optimizations.

16. **Cultural and Social Factors**: The cultural and social context in which a system is developed can subtly influence design choices, especially in terms of user interface and experience.

17. **Environmental Impact and Sustainability**: Increasingly, considerations about a system's environmental impact and sustainability can influence architectural decisions, such as energy-efficient computing or reduced electronic waste.

18. **Knowledge and Experience of the Development Team**: The collective knowledge, experience, and biases of the development team can greatly influence the architecture, often leading to a preference for familiar technologies and patterns.

19. **Data Gravity**: The concept that data and applications tend to move towards the largest data pools. Large datasets can influence the architecture by necessitating processing and analytics to be close to where the data resides.

20. **User Feedback and Behavior**: The way users interact with a system and their feedback can lead to iterative changes in the system, shaping its design over time.

These additional forces, along with the initial ten, highlight the multifaceted and complex nature of system design in IT, especially when there's no intentional architecture or design in place. The emergent design is often a product of these varied, sometimes conflicting, influences.