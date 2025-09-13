# Security Assesment and Testing

## Vulnerability Management

Definition: Identify, prioritize and remediate vulnerabilities in your environment(s).

### Identify Scan Targets
  * The scope depends, it can be all systems or depending on some critercia:
    * What is the data classification of the information at-rest/in-transit/in-use by the system?
    * Is the system publicly exposed?
    * What services are running on the system?
    * Is it dev/staging/prod?
  * Key goal: Build an asset inventory and then decide to which subset the scope reaches.
  * ASV: Approved Scan Vendor (in case of PCI DSS compliance)
### Determin Scan Frequency
  * How often should they run?
  * Influenced by
    * Risk appetite
    * Regulatory Requirements - Like PCI DSS or FISMA that dictate a minimum frequency
    * Technical Constraints - If a test takes 12h, you can only run 2/day.
    * Business Constraints - Scans might cause disruptions that are not acceptable.
    * Licensing limitations
  * TIP: Start Small and increase based on needs, feedback and experience.
  * Examples: Nesus
### Configuring Vulnerability Scans
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
### Scanner Maintenance
  * Make sure that vulnerability feeds are up-to-date
### Scanner software
  * Make sure to patch the scanner software itself, for vulnerabilities.
### Vulnerability Plug-In Feeds
  * Automatically and regularrly auto download new plugs related to new vulnerabilities.
  * *Security Content Automation Protocol (SCAP)* - by NIST, Standerized way of communicating security-related information
    * Common Configuration Enumeration (CGE) - discuss system config issues
    * Common Platform Enumeration (CGE) - describe product names and versions
    * Common Vulnerabilities and Exposures (CVE) - describe security-related software flaws (before: Common Vulnerability Enumeration)
    * Common Vulnerability Scoring System (CVSS) - describe severity of CVE's
    * Common Configuration Checklist Description Format (XCCDF) - describe checklists and reporting results of said checklists
    * Open Vulnerability and Assesment Language (OVAL) - describe low level testing procedures by said checklists
### Vulnerability Scanning Tools
  * *Network Vulnerability scanners* - Tenable's Nessus, Qualy, Rapid7's Nexpose, OpenVAS
  * *Application Vulnerability Scanners* - Static Testing (the code), Dynamic Testing (runtime), Interactive Testing (combining both)
  * *Web Application Vulnerability Scanners* - Niko, Arachimi, Acunetix and Zed Attach Proxy (ZAP)
    * Specialized in WEB applications and their typical vulnerabilities
      * Cross-Site Scripting (XSS)
      * Cross-Site Forgery (XSF)
      * SQL Injection
      * Etc
### Understanding CVSS (v3.1)
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
### Confirmation of Scan Results
  * When a vulnerability is present: Possitive report
  * When a vulnerability is not present: Negative report
  * A positive or negative report can be "false" if an error occurd and the opposite is true
  * Don't trust only the results, do supplementary research and verifications with sources like
    * Log files
    * Security Information and Event Management (SIEM) - corrolate log files from different sources
    * Configuration Management Systems - provide info on systems and what's installed on them

## Vulnerability Classification

### Patch Management - Often ignored due to lack of resources or "Fear" of change/instability
### Legacy Platforms - Discontinued products, Often ignored due to lack of resources or "Fear" of change/instability
### Weak Configurations
  * Use of default config (admin/setup page still exposed)
  * Default credentials or unsecured accounts
  * Open service ports (but unused)
  * Permissions that violate the least privilege
### Error Messages - Descriptive error messages, useful to the attacker, especially if debug mode is still on
### Insecure Protocols - Discontinued or old protocol versions
### Weak Encryption
  * Most important:
    * The algorithm
    * The key that goes with it

## Penetration Testing

### Adopting the Hacker Mindset - Instead of defending against everything, you just need to find one little crack, you only need to win once
  * Taking an adversary mindset
### Reasons for Penetration Testing
  * Complentary to all other efforts, and brings another angle.
### Benefits of Penetration Testing
  * Benchmark: someone with the skillset of this pen tester can or cannot get in
  * Get remediation tips and insights
  * Get step by step insights on how to reproduce vulnerabilities
  ### Threat Hunting is also using a hacker mindset, but you don't test against the live system,
    * They imagine on how a hacker might have getting around a security control, what evidence they might leave behind and then search for proof (IoCs).
    * THis outputs usually different results.
    * If they find compromise, go incident handling mode, and create postmortem.
### Penetration Test Types
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
### Rules Of Engagement (RoE)
  * Timeline - When, how long?
  * Scop - Inclide/exclude locations, systems, applications, or other potential targets
  * Data Handling requirements - How to handle an information that got disclosed during the pentest
  * Target Expected Behavior - What behavior to expect from the target
  * Commited Resources - Time commitment of certain personal during the testing
  * Legal concerns
  * When and how communications happen - regular updates? What if a critical issue is found ? etc...
  * Permission: Make sure to have a signed permission, your free out of jail card when getting caught or things go south.
### Reconnaissance
  * Even in white box, reconnaissance is done to supplement.
  * Passive reconnaisance - gather info without interacting with the target or organization
  * Active reconnaisance - directly engage, like port scanning etc...
    * Footprinting: Scanning which servers are used and versions
  * War Driving/Flying - Drive/Fly by office with high-end antennas and attempt to eavesdrop or connect to WIFI.
### Running the test - Key phases
  * Initial Access - when attacker exploits a vulberability to gain access to the organization's network.
  * Privilege Escalation - using hacking techniques to elevate from initial access.
  * Pivot/lateral move - hacker gains access to other systems from the initial compromised system
  * Establish persistance - Installing backdoors  and other techniques that allows to regain access at a later stage.
  * [Metasploit](https://www.metasploit.com/)
### Cleaning Up
   * Present results
   * Cleanup traves of their work
   * Remove any tools or malware they might have installed

## Audits and Assesments

### Security Tests - Verify that a control is functioning properly
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
  ### Responsible Disclosure Programs
    * Allows security researchers to securily info about vulnerabilities in a product with the vendor.
    * Bug bounties is a form of this
### Security Assesments - Comprehesive review of the security of a give scope
  * Perform risk assesment of a said scope
### Security Audits - External/impartial people who test the security controls
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

## Vulnerability Life Cycle

### Vulnerability Identification
  * Potential Sources: Vulnerability scans, pentration tests, Responisble disclosure, Audits
### Vulnerability Analysis
  * Validate if it exists
  * Prioritize and categorize using CVE and CVSS
  * Supplement with external analysis
### Vulnerability Response and Remediation
  * Based on scoring, we can guide which are most in need of remediation
  * Some examples how Cybersecurity specialists deal with it:
    * Patching
    * Network segmentation to decrease the risk
    * Implement other compensating controls (Firewalls, IPS,...)
    * Purchase insurance to transfer risk
    * Formally accept risk
### Vulnerability of Remediation
  * Test by rescanning or reproducing
  * Might need to be done by external auditors
### Reporting
  * Communicate findings, action taken, lessons learned to relevant stakeholders. Make sure decisions makers are informed.
  * May include:
    * Identified, analyzed and remediated vulnberabilities with CVE/CVSS
    * Details on remediation steps
    * Highlight trends, conclusions, insights
    * Offer recommendations for improvement
