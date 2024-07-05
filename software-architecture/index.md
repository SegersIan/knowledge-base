# The (Software) Architect Handbook

Written and compiled by Ian Segers as personal guide for his job as Solution Architect.
In case you are reading this directly on [GitHub](https://github.com/SegersIan/architecture-handbook), you can read this Markdown rendered on the [GitHub Page](https://segersian.github.io/architecture-handbook/). This is a static website which gets easily cached. To make sure to have the latests contents, do a hard refresh (CTRL + SHIFT + R for chrome/brave/edge).

## What Is Software Architecture?

*Many definitions exists out there, but I like to inspire my definition on Systems, from the field of [Systems Thinking](topics/systems-thinking.md).*

**Software architecture is everything that matters about the architecture and design of information systems. whatever that might be.** 

Before we further explain what that exactly might entail, it is important to first understand what are **systems**.

## Systems

> A "system" in systems thinking is a set of interconnected elements, which can be subsystems in their own right, organized within defined boundaries. These elements function cohesively to achieve a common purpose or produce specific outcomes, influenced by the system's structure and internal interactions.

[Here can find a detailed breakdown](topics/systems-thinking.md) of the definition.

### A Systems Analogy

A system can be as simple as a bathtub. The bathtub holds water, there is a faucet that allows to regulate inflow of water, and there is a drainage pipe that allows for outflow of water. There are interconnected elements, and they produce a specific outcome (e.g. fill up the bath tub) based on the systems's structure and internal interactions (open the faucet, close the drainage).

An example op an adjacent system would be the sewage system. The bathtub system and sewage system are inter-connected. The defined boundary of the bathtub system is the faucet, tub, and drainage pipe. The defined boundary of the sewage starts from the drainage pipe and ends at the sewage filtering station. 

The bathtub system and sewage system are both part of a larger overarching system called the water supply and sanitation system. Making the bathtub system and the sewage systems subsystems of the  water supply and sanitation system.

Yet again, the bathtub system itself can have multiple subsystems. The faucet for example can be examined more closely, and be considered as a (sub)system in its own right again, detailing the internal workings of the faucet. 

Notice that a system is not just about how it is structured. There is also a time aspect to this, how does the system behave over time? How does that behavior change as we interact with the system? (e.g. close the faucet, open the drainage, ...) This is what we mean with "these elements ... produce specific outcomes".

### A Software System

With Information Systems we can look at it in the exact same way. An organization can be seen as one large IT system - with each component in it - being a system in its own right (e.g. a webserver), producing specific outcomes and behavior. This comes with a defined boundary (e.g. all the on-prem systems of the organization). All these systems are interconnected, facilitating communication between and within (sub)systems. Data being the content that is communicated over these interconnections or lives within components.

This means that one can "zoom in" on any component of an information system and look at it's internals, exposing potential another subsystem. However, for ease of reasoning about a system diagram, we don't expose the details of any subsystems, based on what the diagram tries to communicate.

Information systems also have a time aspect, it's not a static snapshot, the system over time produces certain outcomes.

### Boundaries and Domains

A system has defined boundaries, and that's what we do also with information systems. An information system has defined boundaries, detailed what components are part of it, some might use "scope". These boundaries or scope usually encompass a "domain". A domain is a name or term that indicates on what premise the scope or boundaries of the system are defined. This could be a business domain (e.g. Marketing) or a technical domain (e.g. Database Layer). In this handbook we refer to this as Technical and Domain partitioning, telling on how we define our boundaries of our systems(s).

[Domain-Driven-Design (DDD)](topics/domain-driven-design.md) has a concept of "Bounded Context" that is meant to aid in defining your domain, which should indicate how the boundaries are defined.

### Some Clarifications

* Elements in Systems Thinking are Components in Software Systems.
* Many Components in a Software Systems can be software systems in their own right.
* Components are interconnected - meaning - they can communicate.
* The (software) domain *usually* refers to a system's specified boundary.
* The pattern or philosophy that a system software is structured
* Software systems and information systems will be used interchangeably.

## Architecture Properties

* [**Architecture Style**](architecture-styles/readme.md) is the overarching philosophy that:
    * Guides the structuring and partitioning of the software system and its components.
    * Guides the preferred integration (architecture) patterns between the components of the software system.
    * Guides the preferred integration (architecture) patterns between the software system and other external software systems.
    * Targets certain architecture characteristics.
* [**Architecture Characteristics**](architecture-characteristics/readme.md): describes entire software system's behavior. One would aim to target a specific set of desired characteristics that accommodates your system's needs.

## Architecture Fields

* [**Application Architecture**](application-architecture/readme.md) focuses on designing and deciding upon the individual components of the system.
* [**Integration Architecture**](integration-architecture/readme.md) focuses on the flows and communication between these components.
* [**Data Architecture**](data-architecture/readme.md) focuses on the content residing within these components and the information that moves through the system's flows and communications.
* [**Evolutionary Architecture**](topics/evolutionary-architecture.md) focuses on how the constant changes over time to a software system can be best handled, without eroding your architecture and desired architecture characteristics.

## Laws Of Architecture

[See Topic: Laws Of Software Architecture](topics/laws-of-software-architecture.md)

## Doing Architecture

When "doing architecture" as a software architect you should:
1. **Understand the current architecture**, which current architecture style(s) it has, and its current architecture characteristics.
2. **Understand the future goals of the organization** and its information system(s).
3. **Define a clear target state of the architecture**, which target architecture style(s) it should have, and its desired architecture characteristics that accommodate the future goals of the organization.
4. **Define a roadmap** from the current to target architecture.
5. **Govern the transition/process** from the current to the target architecture.
    * Use [**Architectural Decisions**](topics/architecture-decisions.md) for implementation rules.
    * Use [**Design Principles**](topics/design-principles.md) for implementation guidance.
    * [Make Development Teams Effective](topics/make-effective-teams.md)
6. **Obtain feedback** during the transition/process **and refine** your roadmap and target architecture as you learn.
7. **Coach and mentor people** on the transition/process journey.

## Topics

* [Anti-Patterns](topics/anti-patterns.md)
* [Architectural Thinking](topics/architectural-thinking.md)
* [Architecture Decisions](topics/architecture-decisions.md)
* [Architecture Risk](topics/architecture-risk.md)
* [Best Practices](topics/best-practices.md)
* [Components](topics/components.md)
* [Conways Law](topics/conway-law.md)
* [Domain-Driven-Design](topics/domain-driven-design.md)
* [Diagramming and Presenting Architecture](topics/diagrams-and-presentations.md)
* [Evolutionary Architecture](topics/evolutionary-architecture.md)
* [Feature Toggles](topics/feature-toggles.md)
* [How To Do...](topics/how-to-do.md)
* [Making Development Teams Effective](topics/make-effective-teams.md)
* [Negotiation and Leadership Skill](topics/negotiation-and-leadership-skills.md)
* [Laws Of Software Architecture](topics/laws-of-software-architecture.md)
* [Modules](topics/modules.md)
* [Software Architect Role](topics/software-architect-role.md)
* [Systems Thinking](topics/systems-thinking.md)
* [Team Topologies](topics/team-topologies.md)

## Useful

* [Resources](resources.md)
* [Thought Leaders](thought-leaders.md)
* [Nuggets Of Wisdom](./nuggets-of-wisdom.md) that contain some good wisdom.

## Copyright

This handbook is from my experience and many materials that I have read. My intention is to clarify on every topic I cover my sources that I have used, it can be in my own words, it can be sometimes copied from any of my sources. My apologies if I failed to do so, please contact me (via a PR on this GitHub Repo, great for transparency) if I did fail to do so. I obviously don't take credit for when I quote source material and you should proceed with caution if you want to reuse these.

## Todo

Here you can find my [raw todo notes](./todo.md) on all topics that I plan to address in this handbook.