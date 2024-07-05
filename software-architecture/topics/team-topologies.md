# Team Topologies

    Although Team Topologies is strictly not about architecture, it has a huge impact and connection on how we structure team ownership and our architecture according to Conways law. Therefore, I felt this made sense to cover in the Architecture Handbook.

## What is Team Topologies?

> An *adaptive model* to organization design.

"Team Topologies" is a [book](https://teamtopologies.com/book) that provides a framework for organizing and optimizing software development teams within an organization. The book emphasizes the importance of adapting team structures and interactions to the specific context of the organization and its technological landscape. This is all based on the [Reverse Conway Maneuver](https://martinfowler.com/bliki/ConwaysLaw.html). By embracing Conways Law, this framework tries to help create efficient teams that will also result in your desired architecture. As always, frameworks come with their fair share of criticism, but it doesn't make it worth covering and using as input in your decision process. 

> Team topologies is a framework that gives you the tools, concepts, and patterns that help you reason and navigate the challenges of organizational design, with Conway's law in view.

## Why Team Topologies?

> Organization not only need to strive for autonomous teams, they also need to continuously think about and evolve themselves in order to deliver value quickly to the customers.

## Key Concepts

These concepts are used as building blocks on how to reason and think of structuring teams ownership and responsibilities.

### Conway Law

Taking [Conways Law](conways-law.md) in consideration, we can use this to our advantage to create teams that result in the architecture/system that we want, while making the teams also more efficient.

### Flow Of Change

Refers to how changes in software and systems are managed and how they flow through an organization's structure of teams.

[Image: Visual Representation](../attachments/img_team_topologies_flow_of_change.png)

### Team Types

* **Stream-aligned team** aligned to a flow of work from (usually) a segment of the business domain. These are “You Built It, You Run It” teams. No hand-offs to other teams for any purpose.
    * *Primary team type*
* **Enabling team** helps a Stream-aligned team to overcome obstacles. Also detects missing capabilities.
    * *Reduce load for stream-aligned teams, by acting as service providers (e.g learn new things while retaining focus).*
* **Complicated Subsystem team** where significant mathematics/calculation/technical expertise is needed.
    * *Reduce load for stream-aligned teams, where stream-aligned teams are the internal customer of the subsystem.*
* **Platform team** a grouping of other team types that provide a compelling internal product to accelerate delivery by Stream-aligned teams.
    * *Reduce load for stream-aligned teams, where stream-aligned teams are the internal customer of the platform.*
> The goal of the these team types, is to manage cognitive load for teams by defining clear responsibilities and boundaries.

[Image: Visual Representation](../attachments/img_team_topologies_team_types.png)

### Interaction Modes

There are only three ways in which team should interact:

* **Collaboration**: working together for a defined period of time to discover new things (APIs, practices, technologies, etc.) 
* **X-as-a-Service**: one team provides and one team consumes something “as a Service”
* **Facilitation**: one team helps and mentors another team

[Image: Visual Representation](../attachments/img_team_topologies_interaction_modes.png)

## Relation To Systems Thinking

Notice that we recognize the key parts of any generic "system" from [Systems Thinking](./systems-thinking.md).

* **The Organization**: The top level system we view.
* **Team Types**: Are the "Components" or "Elements" that our system is made of up and what their boundaries are.
* **Interaction Modes**: How Components/Elements of a system are interconnected with each other.

## Conway's Law & Reverse Conway Maneuver

*Part I (Teams as the means of Delivery) of the [Team Topologies Book](https://teamtopologies.com/book)*

### The Issue with Traditional, top-down approach to team organization (Org Charts)

> 1. Conway's law suggest major gains from designing software architecture and team interactions together, since they are similar forces.
> 2. Team Topologies clarifies team purpose and responsibilities, increasing the effectiveness of their interrelationships.
> 3. Team Topologies takes a humanistic approach to building software systems while setting up the organizations for strategic adaptability.

### Conway's Law and Why It Matters

> 1. Organizations are constrained to produce designs that reflect communication paths.
> 2. The design of the organization constrains the "solution search space" limiting possible software designs.
> 3. Requiring everyone to communicate with everyone else is a recipe for a mess.
> 4. **Choose Software Architectures that encourage team-scoped flow.**
> 5. Limiting communication paths to well-defined team interactions produces modular, decoupled systems.

### Team-First Thinking

> 1. The team is the most effective means of software delivery, not individuals.
> 2. Limit the size of multi-team groupings within the organization based on dunbars number.
> 3. Restrict team responsibilities to match te maximum team cognitive load.
> 4. Establish clear boundaries of responsibilities for teams.
> 5. Change the team working environment to help teams succeed.

## Team Patterns 

*Part II (Team Topologies that work for flow) of the [Team Topologies Book](https://teamtopologies.com/book)*

### Static Team Topologies

> 1. Ad hoc or constant changing team design slows down software delivery.
> 2. There is no single definitive team topology but several inadequate topologies for any one organization.
> 3. Technical and cultural maturity, org scale, and engineering discipline are critical aspects when considering which topology to adopt.
> 4. In particular, the feature-team/product-team is powerful but only works with a supportive surrounding environment.
> 5. Splitting a team's responsibilities can break down silos and empower other teams.

### The 4 Fundamental Team Topologies

> 1. The 4 fundamental team topologies simplify modern software team interactions.
> 2. Mapping common industry team types to the fundamental topologies sets up organizations for success, removing gray areas of ownership and overloaded/underloaded teams.
> 3. The main topology is (business domain) stream-aligned; all other topologies support this type.
> 4. The other topologies are enabling, complicated-subsystems, and platform.
> 5. The topologies are often "fractal" (self-similar) at large scale: teams of teams.

### Choose Team-First Boundaries

> 1. Choose software boundaries using the team-first approach.
> 2. Beware of hidden monoliths and coupling in the software-delivery chain.
> 3. Use software boundaries defined by business-domain bounded contexts.
> 4. Consider alternative software boundaries when necessary and suitable.

## Evolving The Organization Design

*Part III (Evolving team interactions for innovation and rapid delivery) of the [Team Topologies Book](https://teamtopologies.com/book)*

### Team Interaction Modes

> 1. Choose specific team interaction modes to enhance software delivery.
> 2. Choose between 3 interaction modes - collaboration, X-as-a-Service, and facilitating - to help teams provide and evolve services to other teams.
> 3. Collaboration can be a powerful driver for innovation but can also reduce flow.
> 4. X-as-a-Service can help other teams deliver quickly but only if the boundary is suitable.
> 5. Facilitating helps to avoid cross-team challenges and detects problems.

### Evolve Team Structures With Organizational Sensing

> 1. Use different team topologies simultaneously for strategic advantage.
> 2. Change team topologies and interactions to accelerate adoption of new approaches.
> 3. Differentiate between explore, exploit, sustain, retire phases using team topologies.
> 4. Expect multiple, simultaneous team topologies to meet different needs.
> 5. Recognize triggers or organizational change.
> 6. Treat operations as high-fidelity sensory input for self-steering.

### Conclusion: The Next-Generation Digital Operating Model

> 1. Combine a team-first approach with Conway's law, the 4 fundamental topologies, team interaction modes, topology evolution, and organizational sensing.
> 2. Get Started: begin with the team, identify streams, identify the thinnest viable platform, identify capability gaps, and practice team interactions.

## Resources

* [Team Topologies Book](https://teamtopologies.com/book)
* [Team Topologies Website](https://teamtopologies.com/)
* [Talk - Architect for FLow  - DDD & Team Topologies](https://youtu.be/Lfzph_5wb9c?si=01k_bK6HJD7qMYfP) by [Susanne Kaiser](https://www.susannekaiser.net/)
* [Business Harvard - A Leader’s Framework for Decision Making](https://hbr.org/2007/11/a-leaders-framework-for-decision-making)
