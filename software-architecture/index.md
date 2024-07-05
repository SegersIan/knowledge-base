# The Archtecture Handbook

Written and compiled by Ian Segers as personal guide for his job as Solution Architect.
In case you are reading this directly on [GitHub](https://github.com/SegersIan/architecture-handbook), you can read this Markdown rendered on the [GitHub Page](https://segersian.github.io/architecture-handbook/).

This is a static website which gets easily cached. To make sure to have the latests contents, do a hard refresh (CTRL + SHIFT + R for windows).

## 1. Systems

Before we dive into Software Architecture, we must talk about Systems.

For a System we can find a definition like:

> a set of things working together as parts of a mechanism or an interconnecting network; a complex whole.

Or more specifically for Software Systems:

> System software is a set of generalized programs that manage the resources of the computer, such as the central processing unit, communication links, and peripheral devices

However, as you will read further about *Evolutionary Architecture* you might understand why I personally like to keep the following definitio.:

> a group of body organs that together perform one or more vital functions

Lastly, if we look at physics, we can also see the usage of the term:

> The law of conservation of energy states that energy can neither be created nor destroyed - only converted from one form of energy to another. This means that a system always has the same amount of energy, unless it's added from the outside.

Either way, a **System** is a concept, far more general than software/IT systems. There is a field of [Systems Thinking](https://en.wikipedia.org/wiki/Systems_thinking). If you want to read more about it, I suggest [Thinking in Systems: A Primer](https://en.wikipedia.org/wiki/Thinking_In_Systems:_A_Primer).

Keep in mind, a system can exist out of smaller systems or be a part of a bigger system. Usually a system has also adjacent systems. Deciding on what parts you consider to include in your "view" of the system is important and challenging.

## 2. Domain

Deciding on the "boundries" and the "scope" of your system is challenging. We call this "domain modelling", the domain being the definition of your system boundries and its scope. A "domain" refers to a system in our field, usually they're used interchangeably. A domain is a system, but not every system is a (software) domain. In software term "domain" is more popular than "system". It is common to use "system" in softwware architecure, when we talk about a technical componnent, like "the IBM Mainframe". As you might have guessed, the "IBM Mainframe" in itself can be broken down in sub systems and such.

## 3. System Architecture 

It the field of IT, architects exist at every level of a large system. The largest system would be "the enterprise", at this level we would talk about a "Enterprise Architect". When we divide our system in smaller sub systems, we might find Domain Architects, Solution Architects, or the sub system where a lot of other systems are running on, the infrastructure architects. Infrastructure once again can be divided in small sub systems like Network Architect, Datacenter Architect, Cloud Architect, and the list goes on.

**The architecture of any given system**, high or low level, would have the following **4 pillars** (or do well to have these 4) which guides in defining an architecture:

1. The (actual/desired) **structure** of the system
2. The (actual/desired) **characteristics** of the system.
3. The **architecture decisions** for the system.
4. The **design principles** for the system.

> The structure of a system, with all of its components/sub-systems and their relations manifest in a certain set of characteristics. The Architecture decisions and design principles are intended to guide the **evolution of the system** over time while maintaining the current characteristics or working towards the desired characteristics of the system. All while keeping the implementors and maintainers of the sysem from excercissing **needles** creativity.

We will discuss later **Evolutionary Architecture** which is a great concept for helping to guide the **evolution of the system**.

Ath the time of writing, this architecture handbook focuses primarily on "Software Architecture" and touch a bit on "Enterprise Architecture".

## 4. Software Architecture

Software Architecture focuses on any systems/domains defined in software. Usually these domains (I will start to use 'domain' more than system from now on) are mapped to business domains and capabilities. 

Software architecture followes *the 4 pillars** of architecture (see 3.). Let's have a look how the 4 pillars are implemented for software architecture.

#### 4.1. Structure of the system

> Refers to the [**architectural style(s)**](architecture-styles/readme.md) the system is implemented in. 
> When we talk about an micro-service architecture, we're talking about the structure of the system, not the architecture, cause the architecture also describes the characteristics, decisions, and design principles.

[Structure Of the System Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0103.png)

#### 4.2. Characteristics of the system

> Describes basically **how we want the system to behave**. See [the characteristics list](architecture-characteristics.md) for an detailed list of examples. The *desired* behaviour and other charactericis vary widely per system.

[Characteristics Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0104.png)

#### 4.3. Architecture Decisions

>Describes the **rules** for how a system should be constructed. These form the **constraints of the system** and **informs the developers on what they can and cannot do**.
>Exceptions to these rules can happen, such a exception is also called a *variance*. Based on the size of an organization, an Architecture Decision Board (ADB) or an indivdual architect can grant such exceptions. This is very common, as there are always exceptions to the rule. An exception is usually only for a given part of the system. It doesn not hurt to measure the amount of exceptions that are granted.

Example: The presentation layer is not allowed to call the database layer directly.

These **Architectural decisions are about:**:
* **Making the right trade-offs** for your system. There is no perfect architecture, so we need to be explicit and consious about which trade-offs we make. It's about **Fit For Purpose**.
    * Note that the [Software Architecture: The Hard Parts](https://architecturethehardparts.com/) books uses the following subtitle:
        > Modern Trade-Off analyses for Distributed Architectures.  
* **Keeping your options open** of your system in the future. 
    * Try to minimize the number of early and irreverisble decisions. What we do is "defer" as many decisions as possible. When talking to business you could compare these "deferred decisions" to "options" in the finance.
    * Examples: Choosing a platform agnostic programming language, allow for horizontal scaling so the sizing decisions can be postponed (elasticity).
    * As Gregor Hohpe puts it: [Architecture is about selling options](https://architectelevator.com/architecture/architecture-options/).



[Architecture Decisions Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0105.png)

#### 4.4. Design Principles

>Describes the **guidelines** for how a system should be constructed. Instead of a hard rule, like the architecture decisions, the guideliness are intended to "guide".

Example: "Wherever possible, leverage async communication for decoupling"

[Design Principles Image](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0106.png)


### Noteworthy alternative definitions

A second common style of definition for architecture is that it's “the design decisions that need to be made early in a project”, but Ralph complained about this too, saying that it was more like the decisions you wish you could get right early in a project. His conclusion was that “Architecture is about the important stuff. Whatever that is” - *([Martin fowler](https://martinfowler.com/architecture/))*

> Note that "what is important" means that (expert) developers decide what is important, a simple webapp, the DB could be important, but for a medical imaging app, a detail.


## 4. What is a Software Architect?

*based on [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/)*

*Architectural wisdom and ideas can very specific for their time they were documented. As technology constantly changes, many aspects regarding architecture will change along with that. An example would be the introduction of tools like Kubernetes, which made the restructuring of any software topology cheap, which allows for a more evolving topology. A decade ago, such decisions were costly, so mostly final, once they were made.*

The core responisbilities that we discuss here are relevant for all type of architects (including infrastructure).

### Core Responsibilities
1. Make **architecture decisions**
    * Designs and design principles must **guide technology decisions** not dictate them.
    * You can instruct to use "reactive-based framework for web development" but not which one.
2. Continually **analyze the architecture**
    * Analyze the current architecture and technology environment and recommend solutions for improvement.
    * "How viable is the artchitecture from a few years ago, today? Given the changes in both business and technology"
    * This includes test/release environments, which allows for agility. Remind DevOps principles and practices.
3. **Keep current with latest** technology and industry **trends**
4. Actively **ensure compliance** with decisions
5. **Technical breadth over technical depth**
    * Seek aggresively experience or exposure to multiple languages, platforms, and technologies.
6. Have **business domain knowledge**
    * Important for good communication, you do need to align with business needs.
7. Possess **interpersonal skills**
    * Teamwork, facilitation, and leadership.
8. Understand and **navigate politics**
    * Must understand the political climate and be able to navigate the politics.

In addition to these core expectations, there are many more and this will change as technology and scale changes.

Note that (7) and (8) are cruccial for the ability of the architect to have effective impact and to execute change.

## Useful

* [Thought Leaders](thought-leaders.md)
* [Resources](resources.md)

## Copyright

This handbook is based on existing materials that I have read, combined with my own experience. Due to this, some text here can be close to the words of any of the materials I've read. For that reason I do my best to be transparent and share the relevant [resources](resources.md). I don't take credit for any of the wisdom to be found here.

## Todo

Here you can find my [raw todo](./todo.md) for all topics that I plan to address or needs modifications.