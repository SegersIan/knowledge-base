# Digital Forensics

> Used for various situations:
> - Incident Response
> - Court order/holds like electronic discovery
> - Internal investigations
> - Intelligence/counterintelligence

## Digital Forensic Concepts
* **Acquisition and analysis of digital forensic data**
  * Drives, files, copies of live memory, network capture,...
  * Crucial to have a complete and intact picture of what occured.
* **Document the process**
  * What you have observed, what conclusions can be made from data, what evidence exists to support those conclusions.
  * Timelines, sequence of events, cues as what occured and why, use timestaqmps, file metadata, evengt logs and many clues.
* **Human Side**
  * Interview individuals involve in the activity, can't always be merely a technical expert.

### Legal Holds and e-Discovery
* **Legal/Litigation Hold** - a notice that informs an organization that they must preserve data amd records that might be destroyed or modified in the course of their normal operations.
  * Meaning: Backups, paper documents, electronic files and such.
* **Spoilation of Evidence** Intentionally, reckless,y or negliglenty altering, destroying, fabricating, hiding, or withholding evidence relevant to legal matters.
* **electronic discovery / e-discovery**
  * Legal hold is often the first part of this bigger process.
  * Can also be part of "Freedom of Information Act" requests and other investigations.
  * Process where each side of the legal case obtain evidence of the other side.
* **Electronic Discover Renference Model (EDRM)** is a framework for e-discovery
  * **9 Stages** (for the discovery process)
    1. *Information Governance* from before the "fact/act" to asses
      * WHat data exists ? Allowing to scope and control what data needs to be provided.
    2. *Identify the info* to know what you have and where.
    3. *Preserve the info* to ensure it's not changed/destroyed
      * One of the most _difficult_ and _important_ parts
    4. *Collect the info* for processing
    5. *Process the data* remove unneeded/irrelevant info and format/collate it.
    6. *Review the data* that only necessary is included, so nothing that should not be shared is shared.
    7. *Analyse the data* for key elements like topics, terms, individuals and organizations
    8. *Produce the data* to provide info to 3th parties or those involved.
    9. *Present the data* for testimony or further analysis with expers/involved parties.
  * [Visit EDRM website](https://edrm.net/)
* **Cloud makes ediscovery more complex** often don't permit legal holds of their services/data cause they serve also other customers (a challenge with multitenancy).
* **Chain Of Custody**
  * **Digital-Specific Documentation:**
  - **System information**: Computer name, IP address, OS version, time zone
  - **Hash values**: MD5/SHA-256 of original drives and forensic images
  - **Imaging details**: Tools used (dd, FTK Imager, EnCase), write-blocker serial numbers
  - **Network isolation**: How system was disconnected from network

  * **Digital Evidence Handling:**

  * **Acquisition:**
  - **Write-blocker usage**: Hardware device prevents accidental writes to evidence
  - **Forensic imaging**: Bit-for-bit copy, not just file copy
  - **Hash verification**: Before and after imaging to prove integrity
  - **Multiple copies**: Working copy for analysis, pristine copy for court

  * **Documentation Requirements:**
  - **Drive serial numbers**: Physical identifiers of storage devices
  - **System state**: Running processes, network connections at time of seizure
  - **Imaging software**: Version numbers, settings used
  - **Analysis timeline**: What forensic tools touched the evidence when

  * **Critical Digital Chain Elements:**
  - **Image integrity**: Cryptographic hashes prove no modification
  - **Tool validation**: Using accepted forensic tools (not just cp/xcopy)
  - **Working vs. original**: Never analyze original evidence directly
  - **Time synchronization**: NTP timestamps for all forensic activities

  * **Security+ Context:**
  - **Legal admissibility**: Digital evidence needs stricter controls than physical
  - **Technical proof**: Hash values, write-blockers show technical competence
  - **Tool reliability**: Using forensically sound tools and procedures

  * **Bottom line:** Digital chain of custody emphasizes cryptographic integrity, proper imaging tools, and technical documentation that courts can understand.

## Conducting Digital Forensics
### Acquiring Forensic Data
### Acquisition Tools
### Validating Forensic Data Integrity
### Data Recovery
### Forensic Suites and a Forensic Case Example

## Reporting

## Digital Forensics and Intelligence
