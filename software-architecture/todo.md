## Topics to cover - AKA THE TODO
* What is Software Enterprise Architecture
* How to do Enterprise Architecture 
    * Understand the perceived role of IT
    * Translate the business Strategy into IT strategy
    * Create Transparancy
    * Define the target picture
    * Create a roadmap to get from the current to target picture
    * Govern/Harmonize the exection of the plan
    * Obtain process about the process and refine
    * Coach and mentor the people on the journey/road
    * Somewhere side track from this steps in also things like Business capabilities and such.
* How to get "TRUST" from the engineering team, and how to measure it (doing surveys for example)
* How to get architecture in the "AGILE" or "SAFE" ecosystem ?
* How to get architecture adapted all together
* What are architectural styles and can they co-exist ?
* Where/how does "clean Architecture" fit in ?
* Make a good split and difference between architecture and enterprise architecture
* What is the difference between architecture and design, or "systen design".
    * See Clean Architecture first chapter ?
* Consider on how to discuss the points of Software Architecture and the hard parts book
* Consider how the architect elevator fits the big picture.
* Discuss the architectural styles
* Evolutionary Architecture - Go deeper with the fitness function and such. Circle back to "Defining charachteristics".
    * https://martinfowler.com/articles/evodb.html evolutionary database change
    * See "Build microservices" book of sam newmann, which has "Evolutionary Architect" 
* Discuss managed evolution, but go deeper, what it solves or does. Like, IT allignment. Circle that back to the enterprise architecture and understand how the role of IT is perceived and the relation.
* Discuss evolutionary psychology
* Emphasize how 'data' and *'relations/connections* impact architecture.
* The concepts of "lenses/views" and how they can be used. Which are they, and when to use which ones?
* Role of conways law in architecture
    * See "Build microservices" book of sam newmann, which has "Evolutionary Architect" 
* Operational aspects of architects
    * Architectural Decision Records
    * Record exceptions
    * Exceptions are ok, just measure how many you make.
* Look at managed evolution KPIs
* Make a throrough list of fitness function examples
* Make a reference list of all the -ilities that we can think off.
* Domain Events, Event Driven Architecure, Even Sourcing...
    * https://martinfowler.com/articles/201701-event-driven.html
* "Emerging design/architecture"
* Add also something about all the database reading models, like eventual consistency and such. Cause this is very important when architecting or designing stuff, and the what you should take in consideration.
    * https://www.microsoft.com/en-us/research/wp-content/uploads/2011/10/ConsistencyAndBaseballReport.pdf
    * Also see the Data instensive applications
* Nuggets of wisdom list
    * Don't split services/domains on "entity", entity driven design I call it. Cause where goes to the entity independent, or aggregate of enttities business logic?
    * Your thoughts on the DRY principle, and using the rule of 3. You want to apply DRY for code that changes at the same time, for the same actor/end user. (e.g. a logic for a user vs admin that seems similar at first).
    * Clean architecture book page 62
        * v1: A module should be responsible to one, and only one, user ornstakeholder
        * v2 (better): A module should be responsible to one, and only one, actor.
            * Note: module can be a small as a single source file, so maybe it is not really DRY specific, but more a guide.
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

* DDD - I (IAN) would label it as a data/scope modelling tool, not an "structuring" tool.

### (Anti) Patterns

*This section might be moved to a page of it's own, listing all (anti) patterns.

* Big Ball of Mud (Anti Pattern)
    * Absence of architecture, or absence of architecture governance (making sure the vision is followed).
    * No real structure
    * [Orignal Whitepaper](https://www.researchgate.net/publication/2938621_Big_Ball_of_Mud)
* Unitary Architecture (Pattern)
    * System lives on one piece of hardware, no integrations or such.
    * e.g. Embedded systems
* Client/Server (Pattern)
    * Desktop + database server
    * Browser + web server
    * Three-Tier 
* Architecture by implication (Anti Pattern)
* Accident Architecture (Anti Pattern)


## Managed Evolution Notes

* Architecture domains/domains/fields
    * Application Architecture
    * Integration Architecture
    * Infrastructure Architecture

## Framework thinking

These notes are intended to help "framework thinking" on this topic

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

* Think of guides or methodologies for several use cases
    * When greenfield (Define new characteristics)
    * When replacing systems (review desire characteritics, and current once, etc...)
        * Did something change meanwhile ? Like stakeholders ? Or pure replace.
    * When ...
    * Tips of questions and concerns

# Next Chapters for main page:

## 5. Concepts

### Evolutionary Architecture

That change is constant, is a fundamental fact for many areas of life. This is no different for software systems and software architecture. 

Architecture will have to evolve, if the systems wants to survive over a long time. A system is like a biological organism, it must adapt and change to survive. Survival of the fittest is a law that also exists for organisations and the systems that support them.

> Survival of the fittest... suggestes that organisms best adjusted to their environment are the most successful in surviving and reproducing.

In [Building Evolutionary Architectures](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/) the authors build further on the concept of Evolutionary Architectures.

**As an architect, you should take this in consideration. Try to define your architecture in a way that allows and expect change over time. Business and its requirements change constantly, as the technologies and platforms that support them.**

### Understanding Needs

To do good architecture, one must really try to understand the **needs of all the stakeholders** involved, and **understand their priorities**. **All your architectural decisions should be guided by the this**.

### Foundations

#### Architectural Thinking

*based on [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/)*

#### Modularity

*based on [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/)*

#### Architectura Characteristics

*based on [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/)*

#### Component Based Thinking

*based on [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/)*

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
