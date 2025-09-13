# Nuggets Of Wisdom

> When a team builds a system primarily around reuse, they also incur a huge amount of coupling between components.
* Source: [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 16, p241

> When an architect designs a system that favors reuse, they also favor coupling to achieve that reuse, either by inheritance or composition.
> However; if the architect's goal requires high degrees of decoupling,then they favor duplication over reuse.
* Source: [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 17, p246

> Don't try to find the *best* design in software architecture; instead, strive for the *least worst* combination of trade-offs.
* Source: [Software Architecture: The Hard Parts](https://architecturethehardparts.com/) - Chapter 1, p2

> Data is a precious thing and will last longer than the systems themselves.
* Source: [Software Architecture: The Hard Parts](https://architecturethehardparts.com/) - Chapter 1, p4

> There are no right or wrong answers in architecture - only trade-offs
* Source: [Software Architecture: The Hard Parts](https://architecturethehardparts.com/) - Chapter 2, 30

> A second common style of definition for architecture is that it's “the design decisions that need to be made early in a project”, but Ralph complained about this too, saying that it was more like the decisions you wish you could get right early in a project. His conclusion was that “Architecture is about the important stuff. Whatever that is” - *([Martin fowler](https://martinfowler.com/architecture/))*
> Note that "what is important" means that (expert) developers decide what is important, a simple webapp, the DB could be important, but for a medical imaging app, a detail.

> There are no wrong answers in architecture, only expensive ones
* Source: [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 5, p74

> Developers are drawn to complexity like months to a flame, frequently with the same result.
* Neal Ford

> Since hindsight no longer leads to foresight after a shift in context, a corresponding change in management style may be called for.
* [HBR - A leaders framework for decision making](https://hbr.org/2007/11/a-leaders-framework-for-decision-making)

> Conway's law suggest major gains from designing software architecture and team interactions together, since they are similar forces.
* Source: [Team Topologies Book](https://teamtopologies.com/book)

> Promote software to a profit center, and demand strategic innovations as the only acceptable result.
* Source: [Strategic Monoliths and Microservices - Driving Innovation Using Purposeful Architecture](https://learning.oreilly.com/library/view/strategic-monoliths-and/9780137355600/)

## TODO

* Nuggets of wisdom list
    * Don't split services/domains on "entity", entity driven design I call it. Cause where goes to the entity independent, or aggregate of enttities business logic?
    * Your thoughts on the DRY principle, and using the rule of 3. You want to apply DRY for code that changes at the same time, for the same actor/end user. (e.g. a logic for a user vs admin that seems similar at first).
    * Clean architecture book page 62
        * v1: A module should be responsible to one, and only one, user ornstakeholder
        * v2 (better): A module should be responsible to one, and only one, actor.
            * Note: module can be a small as a single source file, so maybe it is not really DRY specific, but more a guide.