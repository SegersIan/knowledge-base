---
title: "Architecture For Flow"
---

# Architecture For Flow

This is a interpretation of the talk on architecture for flow.

## The Elevator Pitch

* **Goal** - How to build adaptive, socio-technical systems optimized for continuous change and feedback? Cause we know changes are constant.
* **How** - The way to do that is, to be **efficient** (building systems well, be good at building) and to be **effective** (building the right system, solving the actual problems and providing value). For that we need to *align Tech Strategy, Architecture, and Team boundaries*.
* **What** - 
    * There are **3 tools** introduced to help implement this efficiency and effectivity. 
        * *Wardley Maps* - To understand and map you value chain
        * *Domain Driven Design* - To understand your boundaries, opportunity to reuse (modularize) and choose appropriate investment strategy (Build, buy, outsource).
        * *Team Topologies* - To properly design the organization and the team's boundaries.
    * She introduces the **Architecture For Flow Canvas** where she designs an opinionated approach that combines these 3 tools to reach the stated goal.
* In general
    * Optimize for of sustainable value
    * Enable fast and constant feedback
    * Be adaptive to rapid changes.

## The Tools

### Warley Maps

* A 2 dimensional graph with
    * The **x-axe** being **Evolution** (With the main areas *Genesis, Custom-Built, Product/Rental, Commodity*)
    * The **y-axe** being **Value Chain** (with the scale from *Invisible* to *Visible* to the end user)
* The idea is that you draw from the top, the most visible part (for your end user) of the value chain.
    * This can start with a certain functionality, using application X, hosted on platform Y, running on infrastructure Z, ending with the physical data-center China (the least visible to the end user).
    * As you have drawn the value chain, you can move each item horizontally given component, module, feature, capability based on their evolution. 
        * Is this commodity? (like a virtual machine) - Put it all the way right.
        * Is this genesis? (Like your IP, value proposition, unique) - Put it all the way left.
* Note that over time the position on the x-axe (evolution) is expected to evolve over time. It's the evolution dimension after all. New things need to be custom built if it's a differentiator, but as the landscape matures and available tools, given capability could be switch from custom-built to COTS.

### Domain Driven Design

See also [Domain Driven Design]({{< relref "/software-architecture/topics/domain-driven-design.md" >}}), but a quick overview of what is relevant for this talk:

* A business has a **Business Domain**.
* The business domain exists out of **subdomains types** (*Core, Supporting, Generic*)
* based on the  **subdomains types**, you might make an investment strategy (Core subdomain you build as it's a differentiator, generic should be outsourced...)
* Any subdomain can be broken down in one or more **Bounded Contexts**.
* The Business Domain describes your **Problem Space** and your Subdomains your **Solution Space**.
* A bounded context can identify reusable / modular parts of the domain.

### Team Topologies

We are covering [Team Topologies]({{< relref "/team-topologies" >}}) already extensively.

## Architecture For Flow Canvas

Through **7 steps**, the canvas helps you map **the as-is** of your organization and then the **to-be** state.

### 1. Analyzing Current Teams

* [Slide Step 1](../assets/architect_for_flow_canvas_step_1.png)
* Analyze:
    * How are teams currently structured (size, boundaries types, ...)?
    * What are the dependencies and interactions between teams.
    * How do these teams work together (Like a separate Dev and Ops).

### 2. Assessing Flow Of Change

* [Slide Step 2](../assets/architect_for_flow_canvas_step_2.png)
* What is preventing flow of changes? Causes are usually one of the following origins:
    * **Team Dependencies** 
        * Depending on others to do a task or activity
        * Depending on other people's specific expertise
        * Every dependency comes with overhead
        * Constraints slow down overall performance
    * **Team Ownership**
        * Not owning entire e2e flow
        * Lack of ownership clarity
        * Too big of scope
        * High cognitive load
    * **Software Architecture & Quality**
        * Tightly coupled architecture
        * High technical depth
    * **Work Management**
        * Lack of clear priorities
        * High WIP
        * Many interruptions and context switches

### 3. Visualizing Current Landscape

* [Slide Step 3](../assets/architect_for_flow_canvas_step_3.png)
* Note: Here we introduce ***Wardley Mapping** for the first time.
* Mapping the current landscape using **Wardley Mapping**
    * Start on top with the **Problem Space**, the suggested approach to articulate this is using the [Jobs To Be Done](https://strategyn.com/jobs-to-be-done/) (but other methodologies exist).
        * This makes sense, cause the Jobs To Be Done are the most visible part to the end user.
    * Now follow up with the **Solution Space**, where you describe all components/systems that implements these Jobs to Be Done. This will be further down cause this becomes more invisible to the end user.
    * Eventually located the components/systems accordingly on the evolution axe.
* Now ask yourself:
    * What to invest in? (Should something be more custom-built, or COTS)
    * What to evolve? (Can this be a COTS or else internal reusable component?)

### 4. Categorizing Problem Space

* [Slide Step 4](../assets/architect_for_flow_canvas_step_4.png)
* Note: Here we introduce ***Domain Driven Design** for the first time.
* Categorize everything in your **Problem Space** to either a *Core, Supporting, or Generic* subdomain.
    * Based on this you can decide if given area should be build (differentiating), Buy/Use or outsourced (e.g. accounting).

### 5. Modularizing Solution Space

* [Slide Step 5](../assets/architect_for_flow_canvas_step_5.png)
* Modularize everything in your **Solution Space** by decomposing into **bounded contexts**:
    * Group related behavior together
    * Enforce high cohesion and modularity
    * Serve as well-defined ownership boundaries
* Available techniques: Event Storming, Domain Storytelling, Example mapping, User story Mapping, ...

### 6. Visualizing Future Landscape

* [Slide Step 6](../assets/architect_for_flow_canvas_step_6.png)
* Analyze the modularized solution spaces and bounded contexts and move components/context across the evolution axe accordingly.
    * Focus major development investments on differentiators
    * Close efficiency gaps by using standardized commodities (e.g. Cloud)
    * Modular, well-encapsulate, loosely coupled architecture.

### 7. Defining Future Team Organization

* Now you have designed your solution space to a TO BE state. 
* Use the Team Topologies and the reverse conway maneuver to **design an organization that fits the defined future landscape**.
    * *Value Stream Teams* - [Slide Step 7_1](../assets/architect_for_flow_canvas_step_7_1_value-stream-teams.png)
        * Find suitable team boundaries aligned to customer-facing streams of changes.
        * Bounded contexts as team boundaries for stream aligned teams.
        * Optimize for team cognitive load
        * Create clear ownership boundaries
        * Limit number, type, size of components per team (scope).
    * *Platform Teams* - [Slide Step 7_2_1](../assets/architect_for_flow_canvas_step_7_2_1-platform-teams.png)
        * They support stream aligned teams to have a fast flow of change
        * Identify services needed to support reliable flow of change
        * Providing self-service capabilities (x-as-a-service)
        * You can use the same Wardley Map to analyze how to create platforms. Here the end user is the value stream team instead of the customer.
            * [Slide Step 7_2_2](../assets/architect_for_flow_canvas_step_7_2_2-platform-value-chain.png)
    * *Enabling Teams* - [Slide Step 7_3](../assets/architect_for_flow_canvas_step_7_3_enabling-teams.png)
        * Help Value Stream and Platform teams to upskill on missing capabilities. This unblocks teams to wait on someone with a certain expertise.
        * Examples
            * Software Development
            * UX & Accessability 
            * Software design & architecture
            * Testing & Q&A
            * DevOps Practices
            * AppSec
            * Data and analytics
            * Product management
            * Effective communication
            * Documentation
            * Platform engineering
            * DevEx
            * Infra management
            * Cost Management
            * ...
* Unlocking blockers to flow, in summary a bit - [Slide Step 7_4](../assets/architect_for_flow_canvas_step_7_4_wins_vs_big_ball_of_mud.png)
    * Modular well encapsulated, loosely coupled architecture with bounded context.
    * Focus major development investments on differentiators with discovered subdomain types.
    * Closing efficiency gaps by using standardized commodities.
    * Bounded-contexts serve as well defined ownership boundaries.
    * Optimize for team cognitive load.
    * Cross-functional, autonomous, stream-aligned teams & platform teams providing self-services.
    * Enabling teams as internal mentor, coaches to upskill teams

## Critique / Remarks

This seems to take in account a single learning loop. So it allows to get better and more efficient towards a given product and end goal. But what about the changing needs for customers? Changes is business and domain ? How do you innovate on a larger scale here? Something that goes across existing bounded contexts and subdomains. The second learning loop is at least not explained here.

## Resources

* The Talk: https://www.youtube.com/watch?v=PK-y-iG5VnE
* The Book: https://architectureforflow.com/
