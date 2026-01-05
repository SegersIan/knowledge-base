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
* ![Slide Step 1](../assets/architect_for_flow_canvas_step_1.png)
### 2. Assessing Flow Of Change
* ![Slide Step 2](../assets/architect_for_flow_canvas_step_2.png)
### 3. Visualizing Current Landscape
* ![Slide Step 3](../assets/architect_for_flow_canvas_step_3.png)
### 4. Categorizing Problem Space
* ![Slide Step 4](../assets/architect_for_flow_canvas_step_4.png)
### 5. Modulerizing Solution Space
* ![Slide Step 5](../assets/architect_for_flow_canvas_step_5.png)
### 6. Visualizing Future Landsape
* [Slide Step 6](../assets/architect_for_flow_canvas_step_6.png)
### 7. Defining Future Team Organization
* ![Slide Step 7_1](../assets/architect_for_flow_canvas_step_7_1_value-stream-teams.png)
* ![Slide Step 7_2_1](../assets/architect_for_flow_canvas_step_7_2_1-platform-teams.png)
* ![Slide Step 7_2_2(assets/architect_for_flow_canvas_step_7_2_2-platform-value-chain.png)
* ![Slide Step 7_3](../assets/architect_for_flow_canvas_step_7_3_enabling-teams.png)
* ![Slide Step 7_4](../assets/architect_for_flow_canvas_step_7_4_wins_vs_big_ball_of_mud.png)



## Critique / Remarks


## Resources

* The Talk: https://www.youtube.com/watch?v=PK-y-iG5VnE
* The Book: https://architectureforflow.com/
