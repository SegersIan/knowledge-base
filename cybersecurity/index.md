# Cybsersecurity

## Links

* [Resources](resources.md)

## General Concepts

### The 3 Cybersecurity Objectives

* **CIA** Triad == The 3 Objectives/goals
  * **Confidentiality** - No unauthorized individual is able to access sensitive information.
  * **Integrity** - No unauthorized changes to systems or data.
  * **Availability** - Informations and systems are ready to meet the needs of legitimate users at the time those users request them.
* 1 Additional goal/objective
  * **Nonrepudiation** - Someone who performs some action, cannot later deny having taken that action.

### Security Incident

* When there is a breach of any of the CIA Triad goals.
  * Tip: Security therefore is not only about dangerous individuals, but also events like an earthquake.

### The 3 Cybersecurity Threats

* **DAD** Triad
  * Disclosure (aka data loss) <-> Confidentiality violation
    * Data exfiltration (the act of moving data outside the intended organization/boundaries)
  * Alteration <-> Integrity violation
  * Denial <-> Availability violation

### Breach Impact

Types of impact/risks when a security incident happens. Many risks cover multiple types.

* **Financial** - Equipment broken, new datacenter, loss of revenue, ...
* **Reputational** - Negative publicity
* **Strategic** - IP that allows competition to act faster, outsmart you, copy you, ...
* **Operational** - inability to do day-to-day functions, slow down business processes, ...
* **Compliance** - violating a legal or regulatory requirement (e.g. HIPAA)

### Security Controls

* **Control Objectives**: Statements of desired security state (requirements).
* **Security Controls**: Speciifc measures, the implementation of the objectives/requirements.
* **Gap analysis**: Analyse gap between the Control Objectives and the Security Controls.
  * Here we do actually Security Assesment and Testing.
* **Security Control *Categories***:
  * Technical - digital implementations (firewall rules, access control, ...)
  * Operational - processes (access reviews, log monitoring, ...)
  * Managerial - procedural mechanisms (periodic risk assesment, security planning excerices, ...)
  * Physical - physical implementation (locks, fences, ...)
** Security Control *Types***
  * Preventive - Stop before it occurs (Firewalls, ...)
  * Detterent - Prevent from attempting to violate the security policy (guarddogs, ...)
  * Detective - Identify security events/issues that already have happened (Intrusion Detection Systems IDS, ...)
  * Corrective - Remeditate a security issue that has happened (restore from backup, ...)
  * Compensating - Mitigates the risk with alternative methods if the original control requirement.
  * Directive - Inform employees and others what they should do to implement security objectives.

### Data Protection

* 3 States of data
  * Data-at-rest
  * Data-in-transit
  * Data-in-use
* **Data Loss Pevention (DLP)**
  * Information handling policies and procedures to prevent data loss and theft.
  * 2 Environments
    * Agent-based DLP - Installed as agents on a system to scan/monitor for senstive information, system config or actions.
    * Agentless/network-based DLP - Monitors network traffic for risk or proof of data loss. Mostly to pick up on unencrypted content.
  * DLP can take actions
    * Pattern matching - find Social Security number formats, sensitive terms etc and trigger on that.
    * Watermarking - tag sensitive documents, and the DLP scans all those tagged documments to find unencrypted data
* **Data Minimization** - minimaize the amount of senstive data
  * Best: Destroy data once not required anymore
  * Data deintification - remove possibility to link data back to an individual
  * Data obfuscation - impossible to retrieve original data
    * Hashing - senstive to *raindbow table attack*
      * Raindbow Table Attack: If someone knows the hashing algoritm, they can hash all the IDs and use it later to reverse lookup.
    * Tokenization - Use an intermediate ID between data and indivudal and secure that (like different IDs per user)
    * Masking - Partial redacting (like credit card **** **** 0321)
* **Access Restrisctions**
  * Limit ability of individuals/systems
  * 2 Types
    * Geographical: Limit based on geography of individual/system
    * Permission: Limit based by role or level of authorization
* **Segementation and Isolation**
  * Segmentation - Allows systems only to talk to each other within the same segment or limited access to other segments.
  * Isolation - Enirely isolates a system from talking to others
