---
title: "Architecture For Flow"
---

# Architecture For Flow

This is a interpretation of the talk on architectuure for flow.

## The Elevator Pitch

* **Goal** - How to build adaptive, socio-technical systems optimized for continuous change and feedback? Cause we know changes are constant.
* **How** - The way to do that is, to be **efficient** (building systems well, be good at building) and to be **effective** (building the right system, solving the actual problems and providing value). For that we need to *align Tech Strategy, Architecture, and Team boundaries*.
* **What** - 
    * There are **3 tools** introduced to help implement this efficiency and effectivity. 
        * *Wardley Maps* - To understand and map you value chain
        * *Domain Driven Design* - To understand your boundaries, oppertunity to reuse (modulerize) and choose appropiate investment strategy (Build, buy, outsource).
        * *Team Topologies* - To properly design the organization and the team's boundaries.
    * She introduces the **Architecture For Flow Canvas** where she designs an opionated approach that combines these 3 tools to reach the stated goal.

## The Tools

### Warley Maps

* A 2 dimensional graph with
    * The **x-axe** being **Evolution** (With the main areas *Genesis, Custom-Builtm, Product/Rental, Commodity*)
    * The **y-axe** being **Value Chain** (with the scale from *Invisible* to *Visible* to the end user)
* The idea is that you draw from the top, the most visible part (for your end user) of the value chain.
    * This can start with a certain functionality, using application X, hosted on platform Y, running on infrastructure Z, ending with the physical datacenter China (the least visible to the end user).
    * As you have drawn the value chain, you can move each item horizontally given component, module, feature, capability based on their evolution. 
        * Is this commodity? (like a virtual machine) - Put it all the way right.
        * Is this genesis? (Like your IP, value proposition, unique) - Put it all the way left.
* Note that over time the position on the x-axe (evolution) is expected to evolve over time. It's the evolution dimension after all. New things need to be custom built if it's a differentiator, but as the landscape matures and available tools, given capability could be switch from custom-built to COTS.

### Domain Driven Design

See also [Domain Driven Design]({{< relref "/software-architecture/topics/domain-driven-design.md" >}}), but a quick overview of what is relevant for this talk:

* A business has a **Business Domain**.
* The busininess domain exists out of **subdomains types** (*Core, Supporting, Generic*)
* based on the  **subdomains types**, you might make an investment strategy (Core subdomain you build as it's a differnetiatior, generic should be outsourced...)
* Any subdomain can be broken down in one or more **Bounded Contexts**.
* The Business Domain describes your **Problem Space** and your Subdomains your **Solution Space**.
* A bounded context can identify reusable / modular parts of the domain.

### Team Toplogies

We are covering [Team Topologies]({{< relref "/team-topologies" >}}) already extensively.

## Architecture For Flow Canvas

Through **7 steps**, the canvas helps you map **the as-is** of your organization and then the **to-be** state.

### 1. Analyzing Current Teams

* [Slide Step 1](../assets/architect_for_flow_canvas_step_1.png)
* Analyze:
    * How are teams currently structured (size, boundaries types, ...)?
    * What are the dependencies and interactions between teams.
    * How do these themse work together (Like a seperate Dev and Ops).

### 2. Assessing Flow Of Change

* [Slide Step 2](../assets/architect_for_flow_canvas_step_2.png)
* What is preventing flow of changes? Causes are usually one of the following origins:
    * **Team Dependencies** 
        * Depending on others to do a task or activity
        * Depending on other people's specific expertise
        * Every dependency comes with overhead
        * Constraints slow down overall performance
    * **Team Ownership**
        * Not owning neture e2e flow
        * Lack of ownership clarity
        * Too big of scope
        * High cognitive load
    * **Software Architecture & Quality**
        * Tightly coupled architecture
        * High technical depth
    * **Work Management**
        * Lack of clear priorities
        * High WIP
        * Many interuptions and context switches

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

### 5. Modulerizing Solution Space

* [Slide Step 5](../assets/architect_for_flow_canvas_step_5.png)
* Modulerize everything in your **Solution Space** by decomposing into **bounded contexts**:
    * Group related behavior together
    * Enforce high cohesion and modularity
    * Serve as well-defined owernship boundaries
* Available techniques: Event Storming, Domain Storytelling, Example mapping, Userstory Mapping, ...

### 6. Visualizing Future Landsape

* [Slide Step 6](../assets/architect_for_flow_canvas_step_6.png)
* Analyze the modularizied solution spaces and bounded contexs and move components/context accross the evolution axe accordingly.
    * Focus major development investments on differentiators
    * Close efficiency gaps by using standerized commodoties (e.g. Cloud)
    * Modular, well-encapsulate, loosely coupled architecture.

### 7. Defining Future Team Organization

* Now you have designed your solution space to a TO BE state. 
* Use the Team Topologies and the reverse conway manouver to **design an organization that fits the defined future landscape**.
    * *Value Stream Teams* - [Slide Step 7_1](../assets/architect_for_flow_canvas_step_7_1_value-stream-teams.png)
    * *Platform Teams* - [Slide Step 7_2_1](../assets/architect_for_flow_canvas_step_7_2_1-platform-teams.png)
* ![Slide Step 7_2_2](../assets/architect_for_flow_canvas_step_7_2_2-platform-value-chain.png)
* ![Slide Step 7_3](../assets/architect_for_flow_canvas_step_7_3_enabling-teams.png)
* ![Slide Step 7_4](../assets/architect_for_flow_canvas_step_7_4_wins_vs_big_ball_of_mud.png)

## Critique / Remarks


## Resources

* The Talk: https://www.youtube.com/watch?v=PK-y-iG5VnE
* The Book: https://architectureforflow.com/
