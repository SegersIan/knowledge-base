# Architectural Thinking

An architect sees things differently from a developer. Like a meteorologist might see clouds different from an artists point of view. Many architects believe that **architectural thinking** is simply "thinking about architecture", but its more.

There are 4 main aspects of thinking like an architect: *Architecture vs Design*, *Technical breadth vs Depth*, *Analyzing Trade-offs*, and *Understanding Business Drivers*.

## Architecture vs Design

Software architecture refers to the high-level structuring of a software system, outlining the system's main components, their relationships, and their interactions, serving as a blueprint for the system. Software design, on the other hand, delves deeper into the details, focusing on the realization of that architecture by specifying how each component or module will function, including algorithms, data structures, and interfaces, to achieve the system's overall objectives. While architecture provides a holistic view and establishes the foundational framework, design is concerned with the nitty-gritty aspects that bring this framework to life. That's why there are "Architectural Decisions" and "Designing Guidelines". Architects makes decisions about the architecture, but will only give "guidance" or "advise" or design level, where the developer can take their own decisions. 

To make architecture work, both the physical and virtual barriers between architects and developers must be broken down. Allowing for a bidirectional relationship. 

* [See Traditional Relationship Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0201.png)
* [See Bidirectional Relationship Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0202.png)

## Technical breath vs depth

Unlike developers, architects need technical breath, not depth. Developers meed more depth, less breath. Architects must make decisions that match capabilities to technical constraints, a broad understanding of a wide variety of solutions is valuable.

As many developers evolve into the architect role, they will face the some challenges:
* The architect tries to maintain expertise in wide variety of areas.
* The architect has stale expertise, the mistaken sensation that your outdated information is still cutting edge.

Once transitioning into the architecture role, may have to change the way they view knowledge acquisition. But it's also about properly balancing. You must maintain some level of technical depth.

* [See Knowledge Pyramid Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0205.png)
* [See Knowledge Pyramid Anti-Pattern Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0205.png)

## Analyzing Trade-Offs

Everything in architecture is a trade-off. So you need to make a trade-off analysis for every solution that you consider. Being able to understand which is the most optimal trade-off for your goals is key. Cause all solutions starts with "it depends", there are not cookie-cut solutions that fit all, or best practices, analyzing trade-offs are the best approach to compare and decide on a various set of solutions.

> There are no right or wrong answers in architecture - only trade-offs

## Understanding Business Drivers

Understanding the business drivers tha are required for the success of the system and translating those requirements int architecture characteristics (which allows you to do trade-off analysis). This requires the architect to have some level of business domain knowledge and healthy, collaborative relationships with key business stakeholders.

## Balancing Architecture and Hands-On Coding

A software architect ideally codes to maintain a certain level of technical depth. Therefore is is advised to do hands-on coding if possible. However, some tips are in place to achieve this:

* Don't take ownership of code within the critical path of the project, cause you might become the bottleneck, as you got many other responsibilities, so don't become the bottleneck.
* Consider doing frequent proof-of-concepts. Consider making it production quality, as often POCs go straight in production (unfortunately, might as wel prepare for this).
* Consider tackling technical debit or architecture stories.
* Consider working on bug fixes.
* Consider helping to optimize how developers work, with tools, automation, creating fitness functions, and such.
* Consider doing frequent code reviews.

## Resources

* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 2