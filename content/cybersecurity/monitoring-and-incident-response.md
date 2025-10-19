---
title: "Monitoring And Incident Response"
---
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

![img](../assets/incident_response_process.jpg)

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
* Others
  * [Diamond Model](https://apps.dtic.mil/sti/pdfs/ADA586960.pdf)
  * [Lockheed Martin's Cyber Kill Chain](https://www.lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/Gaining_the_Advantage_Cyber_Kill_Chain.pdf)

## Incident Response Data and Tools

### Monitoring Computing Resources
* **Systems** - system logs, system health and performance.
* **Appllication** - Application logs, performance
* **Infrastructure** - SNMP, Syslogs, ...

### Security Information and Event Management Systems (SIEM)
> The central security monitoring tool that collects and aggregates logs from variety of sources to perform correlation and analysis activities.
> As you got all these logs, you can create reports, alerts, ...

* **Sources**: Network devices, network packets, applications, IDS, IPS, ...
* **Dashboards**: of the most relevant SIEM collected data/insights
* **Sensors**: Software/hardware agents to agather additional data. Might send the original data or preprocess if desireable.
* **Sensitivity and Thresholds** - adjust correctly for alerts to avoid fatigue and false positives.
* **Trends** can also indicate issues and give more context.

### Alerts and Alarms
* **Alert Tuning** - modify alerts to omly alarm on important events (avoid alert fatigue)
  * Remember, attackers can use alert fatigue on purpose
  * Might cause actual incidents to dismissed

### Log Aggregation, Correlation, and Analysis Rules
#### Rules
One can configure rules to trigger actions on.
#### Log Files
Commong logs used during incident response:
* **Firewall Logs** including, NGFW, WAF, UTM,
* **Application Logs**
* **Endpoint logs**
* **OS specific security Logs**
  * Linux `/var/log/auth.log` and `/var/log/secure`
* **IDS/IPS logs**
* **Network Logs**

* **Tools**
  * `grep`, `tail`
  * Network flows: Uses sampling!
    * Determine what traffix sas sent on your network, where it went, where it came from.

#### Logging Protocols and Tools

##### **Local Syslog (Traditional):**
* **On Linux machines:**
  - **syslogd daemon**: Collects logs from applications/kernel
  - **Local storage**: Writes to `/var/log/` files (messages, auth.log, kern.log)
  - **Log rotation**: logrotate manages file sizes/retention
  - **Local analysis**: Logs stay on the machine that generated them

##### **Network Syslog (Centralized):**
* **Syslog Protocol (RFC 3164/5424):**
  - **UDP port 514**: Standard syslog transmission
  - **Client → Server**: Devices send logs to central syslog server
  - **Structured format**: Timestamp, facility, severity, message

##### **Modern Implementations:**
* **rsyslog (most common):**
  - **Enhanced syslog**: Supports TCP, TLS, databases, filtering
  - **Both roles**: Can be local daemon AND central server
  - **Configuration**: `/etc/rsyslog.conf`
* **syslog-ng:**
  - **Next generation**: Advanced filtering, parsing, routing
  - **Enterprise features**: Better performance, more destinations

#### Going Beyond Logs: Using metadata
* **Examples**
  * *Email Metadata* (e.g Header)
  * *Mobile Metadata* Call logs, SMS, data Usage, GPS tracking, Cellular tower...
    * Powerful for geospatial stuff
  * *Web Metadata* meta tags, headers, cookies, ...
  * *File Metadata* when modifed, who modifed, Geotag (photos), camera used, size, hash...
* Very useful for forensics.
#### Other Data Sources
* *Examples*
  * Vulnerability scans
  * Packet captures
  * Automated reports etc
  * Dashboards
* These can be read by agents or else just fed to the logging infrastructue, making it agentless then.

### Benchmarks and Logging
* We know benchmarks for hardening, but in these hardening benchmarks there are often tips/instructions on configuring pproper logging.

### Reporting and Archiving
> After logging, you must report and archive.

* *Reporting* is part of the identification process step, looking at trends, changes and sio.
* *Archiving* finally of the logs, keep size manageable, do retenetion based in your documents, polcies, compliance and such. Keep privacy compliance also in mind.

## Mitigation and Recovery
### Secure Orchestration, Automation, and Response (SOAR)
**Platforms that automate repetitive security tasks and coordinate incident response across multiple security tools.**

#### **The Core Problem SOAR Solves:**
- **Alert fatigue**: Security teams drowning in thousands of daily alerts
- **Manual processes**: Analysts spending hours on repetitive investigation tasks
- **Tool silos**: Security tools don't communicate with each other
- **Slow response**: Manual processes delay incident response

#### **What SOAR Does:**

**Orchestration:**
- **Connects disparate tools**: SIEM, firewalls, endpoint tools, threat intel feeds
- **Unified workflow**: Single pane of glass for incident management

**Automation:**
- **Playbooks**: Automated response workflows for common scenarios
- **Enrichment**: Automatically gathers context (IP reputation, user info, file analysis)
- **Response actions**: Block IPs, isolate endpoints, create tickets - automatically

**Response:**
- **Incident management**: Tracks cases from detection to resolution
- **Collaboration**: Team communication and task assignment
- **Reporting**: Metrics on response times, effectivenes

### Containment, Mitigation, and Recovery Techniques
* First mitigation is often quickly blocking the cause of an incident.
  * This means reconfigure endpoint security solutions:
* Examples:
  * *Application Allow List*
  * *Application Deny List*
  * *Isolation/Quarantine* - place files in a safe zone or sytems in safe network
  * *Monitoring* - VALIDATE IF your mitigation effors are effective nad working and don't create unintended side
  effects.
  * *Configuration Change* - These need to be tracked carefully for later rollback, diagnostics, etc...
* Quarantine vs Delete
  * Antimalware can default to quarantine or deleting after identification,
    * Quarantine is good, cause it doesn't blindly all files, imagine if you're having a false positive!
* Remediation Actions
  * Modify firewall changes (add, remove, update rules)
  * Mobile Device Management (MDM) changes
  * Data Loss Prevention (DLP) changes
  * Content filter changes
  * Updateding/revoking certificates.
* Network containment techniques
  * *Isolation* - move a sustem into protected space/network, away from other systems.
    * Remove from network, move it to isolation vlan, security rules
  * *Containment* - leave system in place, but find other ways to contain
    * Firewall rules on the system itself
    * Be catious to shut down the system, might cause issues for later forensics.
  * *Segmentation* - create seperate security levels and segemtns, but this is before an incident happens

### Root Cause Analysis (RCA)
> Identify the underlying cause of for an issue or compromise
> Identify how to fix the problem

* **Techniques**
  * 5 whys
  * Event analise
  * Diagramming cause and effect
