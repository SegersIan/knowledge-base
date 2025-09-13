# General Anti-Patterns

A general set of anti-patterns that might not immediately find place or belong to a specific topic.

## Anti-Pattern: Architecture By Implication

Developers make design decisions implicitly rather than explicitly, which can lead to a poorly defined and chaotic architecture. This anti-pattern often emerges when teams lack experience, proper communication, or sufficient design documentation, causing developers to assume that their colleagues share their understanding of the system's design.

## Anti-Pattern: Distributed Monolith

> A distributed monolith is the result of splitting a monolith into multiple services, that are heavily dependent on each other, without adopting the patterns needed for distributed systems. In practice, it's the result of splitting a monolith into separate services, but keeping them tightly coupled. That means, they still rely heavily on each other. In this context, you lose the simplicity that comes with a monolithic architecture, but don't enjoy the benefits of independent microservices.

[Source](https://dev.to/morintd/understand-the-difference-between-monolith-microservices-and-distributed-monolith-39kb#:~:text=A%20distributed%20monolith%20is%20the,but%20keeping%20them%20tightly%20coupled.)

## Anti-Pattern: Entity Trap

The architect takes each entity identified in the requirements and does almost a 1:1 mapping between each component and entity (e.g. AuctionManager, ItemManager, BidManager). This is not architecture, but component-relational mapping of a framework to a database. This anti-pattern arises when an architect incorrectly identifies the database relationships as workflows in the application, a correspondence that rarely manifests in the real world.

## Anti-Pattern: Frozen Cavemen

An architect who always reverts back to their pet irrational concern for every architecture. Manifests in architects who have been burned in the past by a poor decision or unexpected occurrence, making them particularly cautious in the future. Risk assessment is important, but should be realistic as well.


## Resources

* [DeviIQ Anti-patterns](https://deviq.com/antipatterns)

### TODO

* Accident Architecture (Anti Pattern)