---
title: "Digital Forensics"
---
# Digital Forensics

> Used for various situations:
> - Incident Response
> - Court order/holds like electronic discovery
> - Internal investigations
> - Intelligence/counterintelligence

## Digital Forensic Concepts
* **Acquisition and analysis of digital forensic data**
  * Drives, files, copies of live memory, network capture,...
  * Crucial to have a complete and intact picture of what occurred.
* **Document the process**
  * What you have observed, what conclusions can be made from data, what evidence exists to support those conclusions.
  * Timelines, sequence of events, cues as what occurred and why, use timestamps, file metadata, event logs and many clues.
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

## Conducting Digital Forensics

### Acquiring Forensic Dat
* **Order of Volatility** - [See Visual](../assets/order_of_volatility.jpeg)
  * From top (most volitale) to bottom (least volitale). You start collecting the most volatile data and then work your way down, as it has the highest risk getting lost.
  * 1. *CPU cache and registers* - ephemeral
    * Least likely to be useful or be collected, it's just too ephemeral.
  * 2. *Routing table, ARP Cache, process table, kernel statistics* - ephemeral
    * Most likely already changed compared to when an incident occured, be aware, it's jsut the state from when you snap it
  * 3. *System Memory - RAM* - ephemeral
    * Can contain encryption keys, ephemeral data from apps, ...
  * 4. *Temporary Files and Swap Space* - ephemeral
    * Might be persisten based on how the system was shut down.
  * 5. *Data on the Hard Disk* - persistent
    * Capture entire disk, so you can also find "deleted" files
  * 6. *Remote logs* - persistent
    * Windows registry is a common target for analysis.
  * 7. *Backups* - persistent
**Other systems to target**
  * Smartphones, tablets, IoT, Embedded, Specialized Systems
  * Firmware -> was it modified?
    * Often available for cloning via direct usb, memory forensics or serial cable.
  * Snapshots from VMs.
  * Network traffic and logs.
  * Devices, printouts, media
* **Prevent malicious USB cloning and data acquisition**
  * Data blockers can block USB sticks from transfering signals, but still able to charge.
* **Chain-Of-Custody** - Documentation of the chain of custody of the evidence.
  * This document is linked to a single artifact.
  * You record every time the custody changes (from who to who?, where, when)
  * Who, when and how copies were made.
  * You want to document/audit each "Access", "transfer" or "otherwise handled" event of a given disk, device or drive.
  * Allows to document if the evidence can be legally submitted.
* **Admissable evidence** must be
  * Relevant and reliable
  * legally obtained
  * Authentic
  * Must be the best evidence available
  * The process and procedures should stand up to challenges in court.
* **Admisibility**
  * Data must be intact
  * Data must be unaltered
  * Data must be provably unaltered before and after forensic process.
  * Forensic Analysits must be able to demonstraite appropiate skills, riight tools and techniques and have documented their actions in reliable, testable way via auditble trail. So their effors and findings must be repeatable by a 3th party if necessary.
* For **Cloud Forensics**, consider
  * *Right-to-audit clauses* in contract with cloud service provider (CSP). with small companies it might not be in the contract, but you should take it in consideration, So either you can make the audit or a 3th party. Many providers do regular audits and just update the findings regularly to find a more "Reasonable" approach to them.
  * *Regulatory and jurisdictions*
    * Regulatory requiremments might differ from the location the cloud service operatates and where it headquarters.
    * Local jurisdiction can claim access to your data of a given location. Worry about where you are based, the HQ of your CSP and the location of your datacenters used.
  * *Data Breach Notification Laws* also vary from country to country or state to state.

### Acquisition Tools
#### Forensic Drive Data
* **Forensic Copy Of Drive** requires complete bit-for-bit copy of a drive.
* **dd** Linux CLI that allows to create images for forensic or other purposes.
  * Example: `dd if=/dev/sda of=example.img conv=noerror,sync`
    `if` - input file
    `of` - output file
    `conv=noerror,sync` - copy, despite errors
  * Other settings are mostly useful for performance, like block size.
  * TIP: Also make a MD5sum hash of the image itself, by tracking that one also in chain of custody, one can verify if the image was tampered with since its creation.
    * Example `dd if=... | tee outputfile.img | md5sum > example.md5`
    * The hash of the drive and of the image should match!!!
* **FTK Imager** free windows tool for forensic imagess
  * Supported formats:
    * `raw` (like `dd` does)
    * `SMART` (ASR Data's format)
    * `E01` (EnCase)
    * `AFF` (Advanced Forensics Format)
  * Sources: Phsycial drives, logical drives, image files, folders, CD, DVD
  * Extra: Can capture live memoery from a system.
    * Target format `AD1`, native to FTK.
* **WinHex** windows disk editing tool
  * Can also make disk images in `raw` (like `dd`) format.
  * Used to directly read and modify data from drive, memoery, RAID arrays and other file systems

#### Forensive Network Data
* By default network data is barely captured, unless it's setup in advance,
* Forensic artifacts like firewall logs, IDS and IPS logs, email server logs, authentication logs and other secondary sources may provide the information you need.
* If they do capcture network, will be Wireshark like tools.
* Can be a lot of data that network capturing

#### Forensive Data from Other SOurces
* **Virtual Machines** - Risky, cause there is a virtualization layer underneat, a restart or shut down might move data to other hardware. Make a SNAPSHOT and that should be satisfying forensic demands.,
* **Containers** - Needs specialized tools due to the nature of shared resources and such.

### Validating Forensic Data Integrity
* Document the provenance/origin of the data and ensure the data + process cannot be repudiated.
* Best way: Hash the original file/disk/source and the forensic copy, they should match.
  * Hashes will be a part of the chain-of-custody
* MD5 and SHA1 hashes are outmoded where hackers are involved, but for forensics, it's ok, apparently ?
* **Forensic vs Logical Copies**
  * "normal" copying a file, folder, drvie is a logical copy. Data is preserved but not the same state of the drive or device it was copied from.
  * Remember, on bit level is what matters.
* **Write Blockers** (hardware/sofrware) - ensure their worl doesn't alter the drives/images they work with
  * Basically makes a drive or image readonly, making sure nothing is written to it.

### Data Recovery
* Aside of forensic analysis, these techniques might be used to **recover data** due to accidental deletion or system errors.
* usually file deletion is just removing the "file index".
* When a file is partially overwrriten, fragemments can be still recovered.
* This `open space` on a disk, is called `slack space` => `slack space analysis`
* **SSDs**
  * SSDs might move data to "less worn" cells and stop using the "really worn cells". These worn cells still retain their latest data, and you don't have access anymore to it, so you can't overwrite it, but you might be able to read it with forensics, USe FulL Device Encryption to protect this when you get rid of old SSDs as organization.
### Forensic Suites and a Forensic Case Example
* [EnCase](https://www.opentext.com/products/forensic)
* [Autopsy](https://www.autopsy.com/)
  * Can show timelines of when files were changed and such, allowing to find further corolations.
  * This timeline stuff is insanely useful
  * However!!! Incorret time settings can cause problems or confusion when analyzing. Always verify the time settings before getting to conclusions.
* [Learn hands on forensics with CFReDS](https://cfreds.nist.gov/)
* Other features
  * Distributed cracking of encryption
  * hash cracking
  * steganographic encoding detection
  * Etc..

## Reporting
* The report is sharing the findings from the forensic analysis.
* Must be relevant and useful witout too deep technical nuance.
* **Typical report**
  * Summary of the forensic investgation and findings
  * outline of the forensic process, including tools and any assumptiomns that were made about the tool or process.
  * Series of sections detailing the findings for each drive or devic. Accuracy is critical when findings are shared, and conclusions must be backed up with evidence and appropiate detail.
  * Recommendations or conclusions in more detail than the summary included.
