# Modules    

Different platforms offer different reuse mechanisms for code, but all support some way of grouping related code together in *modules*. This concept of *modules* is proven slippery to define. Therefore, we will use a definition from the [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 3 book. 

Modularity is an organizing principle. IF an architect designs a system without paying attention to how the pieces wire together, a myriad of difficulties might be presented. Good modularity exemplifies the definition of an implicit architectural characteristic. No project features a requirement that asks the architect to ensure good modular distinction and communication, yet sustainable code bases require order and consistency.

## Definition

Modularity describes a logical grouping of related code, which could be a group of classes in a OO language or functions in a functional language. This grouping does't imply a physical separation, merely a logical one. 

When it comes to restructuring the architecture, the coupling encouraged by louse partitioning becomes an impediment to breaking the monolith apart. Thus, it is useful to talk about modularity as a concept separate from the physical separation forced or implied by a particular platform. **Components** *are the physical manifestation of modules*. Note that component can contain one ore more modules.

## Measuring

Given its importance, there are a variety of language-agnostic metrics to help measure modularity. There are 3 key concepts: *cohesion, coupling, and connascence*.

### NOTE!

> This measuring techniques come from the structured programming field. Some of it might also apply to OO and Functional paradigms, however, these metrics are originally targeting structured code bases.

### Cohesion

Refers to what extent the parts of a module should be contained within the same module. Measuring how relates parts are to each other. Ideally a cohesive module is one where all the parts should be packaged together. Attempting to divide a cohesive module would only result in increased coupling, and decreased readability.

* [Types of Cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)) - From best to worst:
    * *Functional Cohesion*
    * *Sequential Cohesion*
    * *Communication Cohesion*
    * *Procedural Cohesion*
    * *Temporal Cohesion*
    * *Logical Cohesion*
    * *Coincidental Cohesion*
* The [Chidamber and Kemerer Object-oriented metrics suite](https://en.wikipedia.org/wiki/Programming_complexity) are a well known set of metrics that allows to measure the "Lack of Cohesion", also known as the LCOM (Lack of Cohesion of Methods) formula. 
    * LCOM: The sum of sets ofg methods not shared via sharing fields.
    * Useful to analyze code base in order to move from one architectural style to another.
    * Only measures *structural* lack of cohesion; not to determine logically if particular pieces fit together. It tells us **HOW** but not **WHY**.

### Coupling

A basic measuring method would be by just measuring afferent and efferent coupling:
* *Afferent* Coupling: Incoming connections/dependencies to a code artifact. (ingress/incoming)
* *Efferent* Coupling: Outgoing connections/dependencies to a code artifact. (egress/outgoing)

The following approach allows for a deeper evaluation than the basic afferent/efferent measurements.

* **Abstractness**: The ratio of abstract artifacts (abstract classes, interfaces, ...) to concrete artifacts (implementation).
* **Instability**: The ratio of efferent coupling to the cum of both efferent and afferent coupling.
    * Determines the volatility of a code base. A code base that has high instability breaks more easily because of the high coupling. If a class calls to many other classes to delegate work, the calling class shows high sensitivity to breakage if one or more of the called methods change.
* **Distance from Main Sequence**: `Distance = | Abstractness + Instability - 1 |`
    * This is a derived metric from Abstractness and Instability.
    * This metric imagines an ideal relationship between abstractness and instability; classes that fall near this idealized line exhibit a health mixture of these two competing concepts.
    * [Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0303.png)
    * There are [2 zones](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0303.png) where a code artifact can fall
        * *Zone of uselessness*: Code that is too abstract becomes difficult to use.
        * *Zone of pain*: Code with too much implementation and not enough abstraction becomes brittle and hard to maintain.
 
### Connascence

A refinement of the afferent/efferent measures towards OO.

> Two components are connascence if a change in one would require the other to be modified in order to maintain the overall correctness of the system.

#### Static Connascence

This is analyzed at build/source code level.

Source-code-level coupling, the degree to which something is coupled, either afferent or efferent:

* **Connascence of Name (CoN)**: Multiple components must agree on the *name of an entity*.
    * Example: `createUser()` and then `updatePerson()` when it's about the same entity.
* **Connascence of Type (CoT)**: Multiple components must agree on the *type of an entity*.
    * Example: Using the same language type for the same entity.
* **Connascence of Meaning (CoM) or Connascence of Convention (CoC)**: Multiple components must agree on the *meaning of particular values*.
    * Example: `int TRUE = 1; int FALSE = 0`,  imagine someone changing that around.
* **Connascence of Position (CoP)**: Multiple entities must agree on the *order of values*.
    * Example: `createUser(string name, string surname) vs updateUser(string surname, string name)`
* **Connascence of Algorithm (CoA)**: Multiple components must agree on a *particular algorithm*.
    * Example: If a certain hashing algorithm is chosen, 2 related components must use the same.

#### Dynamic Connascence

This is analyzed at runtime.

* **Connascence of Execution (CoE)**: The order of execution of multiple components is important.
    * Example: You must call code in certain precedence/order to work. You can't do `article.publish()` while `article.setTile()` should be called first.
* **Connascence of Timing (CoT)**: The timing of the execution of multiple components is important.
    * Example: Race condition challenges
* **Connascence of Values (CoV)**: Occurs when several values relate on one another and must change together.
    * Example: You can not change any of the coordinates of a `square` data structure without changing the other coordinates to adhere to the requirements of a square (each side must be equal, corners 90 degrees, etc...). 
    * You can see how this can relate to "transactions" and especially in "distributed" systems. All values must change or not at all, in an (if possible) atomic approach. You try to keep redundant data in sync sort to say.
    * **CoV is about agreeing on a value. If any part of the system decides to change the value, all other parts must be updated to stay consistent.** 
* **Connascence of Identity (CoI)**: Occurs when several values relate on one another and must change together.
    * Example: Sounds similar to CoV, but there is a difference. This is about the "SAME IDENTITY" that multiple components refer to. 
    * **CoI is about agreeing on a specific instance. It's not about the value itself but about the specific identity or reference to an object/resource.**

#### Connascence Properties

Connascence is an analysis tool for architects and developers, some properties of Connascence help developers use it wisely.

* **Strength**: The ease which one can refactor that type of coupling. One can improve the coupling characteristics of the code by refactoring towards better types of connascence.
    * [See strength Diagram](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0305.png) that is an excellent refactoring guide. The strongest (dynamic)Connascence types are at the bottom, and you want to start your refactoring focus there and then work your way up to the more weaker ones (Static).
* **Locality**: Proximity between the modules. Proximal code (in same module) typically has more and higher forms of connascence than more separated code (different modules).
    * One must consider **strength** and **locality** together. Strong forms of connascence in the same module are less troublesome than between separate modules.
* **Degree**: Size of impact, does it impact a few or many classes? A strong connascence is ok if the degree/impact is low. Like not having many components, but code bases grow...

#### How to use connascence to improve modularity

1. Minimize overall connascence by breaking the system unto encapsulated elements.
2. Minimize any remaining connascence that crosses encapsulation boundaries.
3. Maximize the connascence within encapsulation boundaries.


## Conclusions

* Coupling originates mostly from structured programming, connascence goes deeper and questions *how* things are coupled together. Naturally there [is some overlap here](https://fundamentalsofsoftwarearchitecture.com/images/book/fosa_0305.png).
* As architect you care more on ***HOW*** things modules are coupled, not the degree.
* These metrics were designed in a time when distributed architectures were not mainstream yet, so they work well for code bases, but there are challenges on a higher level.
* See [Architectural Characteristics](./architecture-characteristics/readme.md) on how to thing more about connascence on higher architectural level.

## Resources

* [Clean Architecture](https://www.amazon.com/dp/0134494164)
* [Fundamentals of Software Architecture](https://fundamentalsofsoftwarearchitecture.com/) - Chapter 3
