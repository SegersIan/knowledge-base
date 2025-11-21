---
title: "Theat Modeling"
tags: ["Cybersecurity", "AI", "Agentic AI"]
---
# Threat Modeling

| Framework | Core Focus           | Notes |
|-----------|----------------------| ---    |
| STRIDE    | General Security     | To Add |
| PASTA     | Risk-Centric         |        |
| LINDDUN   | Privacy              |        |
| OCTAVE    | Organizational Risk  |        |
| Trike     | System Modeling      |        |
| VAST      | Agile Development    | To Investigate|
| MAESTRO   | Agentic AI           |        |

# Threat Modeling - Systems and Applications

... To do, one day, got an entire book on it

# Threat Modeling - Agentic AI

## MAESTRO

CEO and Chief AI officer Ken Huan at DistributedApps.ai came up with the **MAESTRO** threat modeling framework for agentic AI. The MAESTRO is an abbreviation for **M**ulti-**A**gent **E**nvironment, **S**ecurity, **T**hreat, **R**isk, and **O**utcome.

### Principles
* **Extended Security Categories**: They're expanding traditional categories like STRIDE, PASTA, and LINDDUN with AI-specific considerations. For example:
* **Multi-Agent and Environment Focus**: Explicitly considering the interactions between agents and their environment. A self-driving car must be aware of other cars, objects, and weather conditions.
* **Layered Security**: Security isn't a single layer, but a property that must be built into each layer of the agentic architecture.
* **AI-Specific Threats**: Addressing threats arising from AI, especially adversarial ML and autonomy-related risks.
* **Risk-Based Approach**: Prioritizing threats based on likelihood and impact within the agent's context.
* **Continuous Monitoring and Adaptation**: Ongoing monitoring, threat intelligence, and model updates to address the evolving nature of AI and threats.

### Elements

Meastro base itself on the [7 Layered Agentic AI Reference Architecture](https://kenhuangus.medium.com/7-layered-agentic-ai-reference-architecture-20276f83b7ee) by the same author, which is visualized here.

This layered approach decomposes the complex AI agent ecosystem into distinct functional layers: from Foundation Models that provide core AI capabilities, through Data Operations and Agent Frameworks that manage information and development tools, to Deployment Infrastructure and Security layers that ensure reliable and safe operations, culminating in the Agent Ecosystem where business applications deliver value to end-users. Each layer serves a specific purpose while abstracting complexity from the layers above it, enabling modular development, clear separation of concerns, and systematic implementation of AI agent systems across organizations.

![ing](../assets/threat_modeling_meastro_1.png)



## Resources

* [MAESTRO - Threat model framework for agentic AI](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro)
* [7 Layered Agentic AI Reference Architecture](https://kenhuangus.medium.com/7-layered-agentic-ai-reference-architecture-20276f83b7ee)
