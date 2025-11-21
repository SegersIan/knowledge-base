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

![ing](../assets/threat_modeling_meastro_1.png)

Each layer has a clear, distint purpose and abstracting complexity from the layers above. The threat model basically lists a set of threats for each layer in that reference architecture. In addition, there are a few cross-layer threats.

Here are the **“A. Layer-Specific Threat Modeling”** items from the article reformulated into lay-terms (only the “Threat Landscape” bullet items for each layer):

#### Layer 7: Agent Ecosystem

* **Compromised Agents**: Bad actors sneak in fake or malicious AI agents into the marketplace.
* **Agent Impersonation**: Malicious agents pretend to be legitimate ones and fool users or other agents.
* **Agent Identity Attack**: Attackers break the identity/authentication of an agent, gaining unauthorized control.
* **Agent Tool Misuse**: Agents are tricked into using their tools in improper ways, causing unintended harm.
* **Agent Goal Manipulation**: Attackers change an agent’s goal so it starts doing something other than its original purpose (often harmful).
* **Marketplace Manipulation**: Fake reviews/ratings or recommendation tampering used to promote malicious agents or hurt good ones.
* **Integration Risks**: Weaknesses in APIs/SDKs used to plug agents into systems allow compromise in interactions.
* **Horizontal/Vertical Solution Vulnerabilities**: Attackers exploit weaknesses specific to industry- or function-specific agents.
* **Repudiation**: Agents deny operations they performed, making it hard to trace actions back to them.
* **Compromised Agent Registry**: The registry of agents is tampered with to inject bad listings or alter existing ones.
* **Malicious Agent Discovery**: The mechanism that shows available agents is manipulated so bad agents are hidden or good ones overlooked.
* **Agent Pricing Model Manipulation**: Attackers exploit or change how agents are priced to cause financial loss or unfair advantage.
* **Inaccurate Agent Capability Description**: Agents advertise misleading capabilities, causing users to misuse them or rely on them wrongly.

#### Layer 6: Security and Compliance (Vertical Layer)

* **Security Agent Data Poisoning**: Attackers tamper with the data used by security agents, so the agents mis-identify threats or raise false alarms.
* **Evasion of Security AI Agents**: Malicious actors trick security agents so that the agents fail to detect or respond to threats.
* **Compromised Security AI Agents**: Attackers take over security agents, making them do malicious work or disabling protections.
* **Regulatory Non-Compliance by AI Security Agents**: Security agents operate in ways that break privacy or compliance rules (often due to bad configuration/training).
* **Bias in Security AI Agents**: Security agents treat some systems unfairly (e.g., under-protecting certain systems) because of inherent bias.
* **Lack of Explainability in Security AI Agents**: The security agent’s decisions aren’t transparent, making auditing and root-cause analysis hard.
* **Model Extraction of AI Security Agents**: Attackers reverse-engineer the security agent’s model by querying it, and use that to bypass defenses.

#### Layer 5: Evaluation and Observability

* **Manipulation of Evaluation Metrics**: Adversaries tamper with test/benchmark data to make a given agent look better than it is.
* **Compromised Observability Tools**: Monitoring tools are hijacked so that attackers can hide malicious activity or leak sensitive data.
* **Denial of Service on Evaluation Infrastructure**: Evaluation systems are overwhelmed or broken so that compromised agents go undetected.
* **Evasion of Detection**: Agents are designed to avoid triggering monitoring systems or alerts, hiding their real behaviour.
* **Data Leakage through Observability**: Logs or dashboards expose sensitive information because of mis-configuration or oversight.
* **Poisoning Observability Data**: The monitoring data (feeds, logs) are corrupted so attackers can mask malicious behavior from defenders.

#### Layer 4: Deployment and Infrastructure

* **Compromised Container Images**: Malicious code is embedded into the container images that run AI agents, infecting production.
* **Orchestration Attacks**: Vulnerabilities in platforms like Kubernetes are used to gain control of the AI deployment system.
* **Infrastructure-as-Code (IaC) Manipulation**: Attackers tamper with deployment scripts (like Terraform, CloudFormation) so insecure infrastructure is built.
* **Denial of Service (DoS) Attacks**: The infrastructure supporting agents is overloaded/attacked so legitimate AI services fail.
* **Resource Hijacking**: Attackers use your compromised infrastructure (e.g., compute nodes meant for AI agents) for crypto-mining or other illicit use.
* **Lateral Movement**: Once inside one part of the infrastructure, attackers move sideways to compromise other systems tied to the AI ecosystem.

#### Layer 3: Agent Frameworks

* **Compromised Framework Components**: Libraries or modules in the AI-agent framework contain malicious or defective code, compromising agents built on them.
* **Backdoor Attacks**: Hidden malicious features in the framework are used by attackers to gain unauthorized access/control over agents.
* **Input Validation Attacks**: Poor handling of user inputs in the framework allows code injection or system compromise of the agent setup.
* **Supply Chain Attacks**: Attackers compromise dependencies of the framework before distribution, leading to compromised agent software.
* **Denial of Service on Framework APIs**: Flooding or abusing the agent framework’s API so agents cannot function properly.
* **Framework Evasion**: Agents are specifically built to bypass or hide from the framework’s built-in security controls and perform unauthorized actions.

#### Layer 2: Data Operations

* **Data Poisoning**: Attackers manipulate training or operational data so the agent learns bad behavior or makes wrong decisions.
* **Data Exfiltration**: Sensitive data used by or stored for the AI agent is stolen, leaking private or proprietary information.
* **Denial of Service on Data Infrastructure**: Data storage or pipelines are disrupted so agents lose access to needed data and can’t function.
* **Data Tampering**: Data in transit or at rest is modified, leading to incorrect agent behavior or inaccurate results.
* **Compromised RAG Pipelines**: In systems that integrate retrieval-augmented generation (RAG) or similar workflows, malicious code/data is injected into those pipelines, causing bad or malicious agent behavior.

#### Layer 1: Foundation Models

* **Adversarial Examples**: Inputs are specially crafted to deceive the core model into making wrong predictions or acting badly.
* **Model Stealing**: Attackers query the model and replicate it—stealing intellectual property, reducing competitive advantage.
* **Backdoor Attacks**: The model has hidden triggers planted in it that make it behave maliciously when activated.
* **Membership Inference Attacks**: Attackers figure out whether a particular data point was used in training the model—exposing private/training data.
* **Data Poisoning (Training Phase)**: During training, malicious data is injected so the model learns biased or faulty behavior.
* **Reprogramming Attacks**: The model is repurposed for a malicious use that it was not intended for.
* **Denial of Service (DoS) Attacks**: Attackers overload the model (e.g., with expensive queries) to degrade performance, reduce availability, or disrupt its service.

#### Cross-Layer Threats

* **Supply Chain Attacks**: A weakness in one part of the stack (for example a library) is compromised and that breach affects other layers too. ([Cloud Security Alliance][1])
* **Lateral Movement**: An attacker breaks into one layer (e.g., infrastructure) and then moves sideways to access and exploit other layers (e.g., data operations). ([Cloud Security Alliance][1])
* **Privilege Escalation**: Someone or something gains higher-level permissions in one layer and uses that elevated access to interfere with other layers in the system. ([Cloud Security Alliance][1])
* **Data Leakage**: Sensitive information belonging to one layer gets exposed or accessed through another layer due to an interaction or gap between them. ([Cloud Security Alliance][1])
* **Goal Misalignment Cascades**: A mis-set or manipulated goal in one agent or layer propagates through the ecosystem, causing other agents/layers to “go off script” and do unintended harmful things. ([Cloud Security Alliance][1])

Here are the **“C. Mitigation Strategies”** and **“D. Using MAESTRO: A Step-by-Step Approach”** sections from the article, reformulated into accessible layman-terms and formatted in markdown:

### Mitigation Strategies

* **Adversarial Training**: Train your AI models and agents with tricky or malicious inputs so they learn to handle them safely. ([Cloud Security Alliance][1])
* **Formal Verification**: Use rigorous checks (math/model-proofs) to ensure agents behave as intended, aligned with goals. ([arXiv][2])
* **Explainable AI (XAI)**: Make sure the AI agents’ decisions can be understood, audited and traced by humans (so you can check “why did it do that?”). ([Cloud Security Alliance][1])
* **Red Teaming**: Regularly simulate attacks or adversarial behaviours against your AI agents to find weak spots before real attackers do. ([toreon.com][3])
* **Safety Monitoring & Runtime Controls**: Keep watching what your agents actually do in real time (logs, dashboards, alerts), so you can catch unsafe behaviour early. ([Cloud Security Alliance][1])
* **Defense in Depth**: Use multiple layers of protection (infrastructure, models, data, agents) rather than relying on a single security control. ([Cloud Security Alliance][1])

### Using MAESTRO: A Step-by-Step Approach

* **1. System Decomposition**: Break down your AI-agent system into components using the 7-layer MAESTRO architecture (foundation models, data ops, frameworks, infra, evaluation, security/compliance, agent ecosystem). ([Cloud Security Alliance][1])
* **2. Layer-Specific Threat Modeling**: For each of those seven layers, use the “Threat Landscape” lists to identify what specific threats apply in your system. ([Cloud Security Alliance][1])
* **3. Cross-Layer Threat Identification**: Look for risks that hop between layers (for example: a weakness in infrastructure enabling a model attack). ([arXiv][2])
* **4. Risk Assessment**: For every identified threat, estimate how likely it is and how bad the impact could be — then prioritise. ([Cloud Security Alliance][1])
* **5. Mitigation Planning**: Choose the most relevant mitigation strategies (from section C) and map them to the highest-priority threats. ([Cloud Security Alliance][1])
* **6. Implementation & Monitoring**: Put the mitigations into practice, keep monitoring, and update the threat model as your agents evolve. ([Cloud Security Alliance][1])



## Resources

* [MAESTRO - Threat model framework for agentic AI](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro)
* [7 Layered Agentic AI Reference Architecture](https://kenhuangus.medium.com/7-layered-agentic-ai-reference-architecture-20276f83b7ee)
[1]: https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro?utm_source=chatgpt.com "Agentic AI Threat Modeling Framework: MAESTRO | CSA"
[2]: https://arxiv.org/html/2508.10043v1?utm_source=chatgpt.com "Securing Agentic AI: Threat Modeling and Risk Analysis for ..."
[3]: https://www.toreon.com/threat-modeling-insider-june-2025/?utm_source=chatgpt.com "Threat Modeling Insider - June 2025"