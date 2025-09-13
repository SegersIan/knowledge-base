# Events and Event Sourcing

> This section goes deeper into events, event-sourcing, and related topics. If you want to know more about the architectural style "Event-Driven" that strongly leans on events, see the [Event-Driven Architectural Style](../../architecture-styles/event-driven.md)

## Events vs Event Sourcing

Events are used as a method of communication between different parts of a system. An event is a significant change in state or an important occurrence that other parts of the system might need to know about. Event sourcing is a design pattern where the state of a business entity is persisted as a sequence of state-changing events. Whenever the state of a business entity changes, a new event is appended to the list of events.

Event's primary goal is to enable loose coupling between different components or services.

Event Sourcing's primary goal is to ensure complete traceability and auditability of all changes made to the entity's state. It allows the system to reconstruct past states by replaying the events.

## Topics

* [Event Versioning](./versioning.md)
* [TODO] Event Modeling
* [TODO] Event Stores/Sourcing ?
* ...

## Resources

* [What Is Event Modeling](https://eventmodeling.org/posts/what-is-event-modeling/)
