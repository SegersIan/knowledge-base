# Monitoring and Incident Response

## Incident Response (IR)

### The Incident Response Process/Cycle

> The process is not linear, you might go back and forth based on findings and learnings.

* 1. **Preparation** - build tools, processes, and procedures to respond to an incident.
  * Includes: Build team, train, conduct exercises, document, configure tools.
* 2. **Detection** Reviewing events to identify incidents
  * [IoCs](<malware-types#indicators-of-compromise-iocs>), loge analysis and security monitoring + awareness and reporting program for staf.
* 3. **Analysis** - An event is indentified, identify other related events and their targer/impact.
* 4. **Containment**  - Contain the incident from furher escalation
  * Not always clear what to do, quarantine (move a system to an isolated network) is an method,
* 5. **Eradication** - Remove the artificats related to the incident
  * Restore systems, rebuild systems, restore backups, and verify its clean
* 6. **Recovery** - Restore back to normal
  * Move a system out of quarantine, go back online, fixes to remediate the chance of immediatly reoccring
  * Make sure to update a backlog for improvememts based on past incidents.
* 7. \[Optional\] **Post Mortem** - Lessons learned, reflect.
* **Back to 1** - so repeat, as you can now prepare again better

#### Prepering for Incident Response

* **Incident Response Team Members**
  * Member of management/organizational leadership.
    * Takes decisions & communictates to senior management, should have the permission to take decisions.
  * Information Security Staff
  * Technnical Experts
    * System admins, developers, ...
  * Communications and PR staff
  * Legal and HR if staff may be involved
  * Law enforcement in some cases
* **Excercices**
  * *Tabletop* - talk through the process regarding a hpyothetical situation
    * Lowest learning quality, but least impact also to operations
  * *Similations* - Similate parts of a plan or entire plans
    * Higher learning quality, but requires more resources and people must be informed.
    * Every commumucation should pretext with `This is an excercise`
* **Building Incident Response Plans**
  * Must be reviewed reguraly
  * Must be tested reguraly
  * May contain various subplans, like
    * Communication plan - who talks to who and how
    * Stakeholder management plan - Who are the stakeholders and how do we involve them
    * Business Continuity (BC) plans - how do we continue business process in case of failure
      * e.g. do everything with pen or paper, use another system,...
    * Disaster Recovery (DR) plans - focuses on estoration or continuation dispise a natural/human disaster

#### Policies
> Formal statements about the intent of an organization. This means it does not talk about the implementation.
> Explains the WHY, not the HOW

Makes sense to `Incident Response Policies` that are used to guide the incident response implementation.

### Training
* Training if the plans
* General trainings through certifications and such
* [CISA Incident Response Training](https://www.cisa.gov/resources-tools/programs/Incident-Response-Training)

### Threat Hunting
> Part of the "Detection" and "Analysis" steps of the Incident Response Process.
> You look for incidents, compromises, IoCs

* **Indicator Examples**
  * *Account Lockout* - Sign of brute-force attempts
  * *Concurrent Session Usage* - If the same user is using concurrent connections from different devices, especially if one of the devices is new/unknown or in another geographical location.
  * *Blocked Content* - Any attempts of accessing blocked content
  * *Impossible Travel* - When a user connects from 2 different locations that was impossible to travel between so fast
  * *Resource Consumption* - Especially if unusal patterns, but this is used often in addition to other indicators.
  * *Out-Of-Cycle logging* - events that happen outside of their usual time/schedule (a job running an another moment, a user at 2 AM)
  * *Missing Logs*- an absence of logs where there should be, might indicate someone cleaned their tracks.
  * *published/documented* - discovered/published indicators, distributed via threat feeds.

### Understanding Attacks and Incidents

* **Attack Frameworks** are used to understand adversaries, document techniques and categorize tactis in a shared language and terminology.
* **MITRE ATT&CK** is such a attack framework
  * `Adversarial Tactis, Techniques, and Common Knowledge knowledgebase of adversary tactics and techniques`
  * [FInd there the knowledgebase](https://attack.mitre.org/)
  * This knowledgebase can be also used for Threat Modeling.
## Incident Response Data and Tools
### Monitoring Computing Resources
### Security Information and Event Management Systems
### Alerts and Alarms
### Log Aggregation, Correlation, and Analysis Rules
### Benchmarks and Logging Reporting and Archiving

## Mitigation and Recovery
### Secure Orchestration, Automation, and Response (SOAR)
### Containment, Mitigation, and Recovery Techniques
### Root Cause Analysis
