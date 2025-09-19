# Endpoint Security

## Operating System Vulnerability Types

* **Vulnerabilities in the OS itself**
* **Default passwords & Insecure (Default) Settings**
* **Insecure configurations**
* **Misconfiguration**

## Hardware Vulnerability Types
Note: Often hard to deal directly with, so compensating controls are key.

* **Firmware** - embedded software of devices
  * Not always possible to update
  * Requires sometimes *manual* updates, and not part of automated updates.
  * Attacks: Via any way that allows access to the firmware itself
    * Examples: executable updates, user download malicious firmware and network enabled updates that provide remote-acces to firmware and management.
    * Reintalling the OS wouldn't change a thing
  * Defenses
    * Firmware validation!
* **End-Of-Life or Legacy hardware** - means no moe support or patches from cendor
  * Tips/watch for
    * End-Of-Sales: Last day the device will be sold (might be still in supply chain via resellers for a grace period)
    * End-Of-Life: Not sold anymore, but still supported, should get rid of it though.
    * End-Of-Support: Last day that vendor will provide support/updates/patches.
    * Legacy: Unsupported.

## Protecting Endpoints

* **Endoint** - They're at the endpoint of a network (wired & wireless)
  * Examples: Servers, mobiles, laptops, desktops,

### Preserving Boot Integrity

* Protection of the endpoint starts already at bootup.
* If untrusted/malicious code is inserted into the boot process, the system can't be protected.
* **Unifued Extensible Firmware Interface (UEFI)** (replacement of BIOS)
  * Has 2 security techniques
    * 1. **Secure Boot** ensure that the system boots omly software that the Original Equipment Manufacturer (OEM) trusts.
      * HOW: UEFI uses signature database `db` and revoked signature database `dbx` with all signatures of trusted and revoked boot software/firmware.
        * Signature Databases are validate with platform public key (platform = the motherboard, installed on manufacturing)
          * The `platform private key` is at the manufacturer, for signing the database updates (not actual firmware/updates).
        * If a violation is found, attempt to restore to original trusted firmware, so you depend on the logic/decision of the boot process on how to deal with an untrusted signature.
      * ![img](../assets/endpoint_security_uefi_secure_boot_process.jpg)
    * 2. **Measured Boot** - Boot proceses that measure each component
      * UEFI measures (hashes) each component as it loads
      * Stores measurements in TPM (Trusted Plaform Module) Platform Configuration Registers (PCRs)
      * Does NOT compare against expected values
      * Does NOT stop boot if something is different
      * Just creates a tamper-evident log
      * This allows a remote server to maie decisions.
* **Boot Integrity** starts with the hardware root of trust comntaining the cryptographic keys that secure the boot process. This usually lives in the TPM (Trusted Plaform Module).
  * There is an unconditional, implicit trust in the hardware root, or more specific the TPM.
* **Trusted Plaform Module (TPM)** frequently used for built-in encryption
  * 3 major functions
    * 1. **Remote Attestation** - allowing hardware & software configs to be verified
    * 2. **Binding** - encrypts data
    * 3. **Sealing** - encrypts data + set requirements for the state of the TPM chip before decrypting
* **Phsycially Unclonable Functions (PUFs)** - unique to the specific hardware.
* **Apple's secure enclave** dedicated secure system for hardware key management.
  * Full processor - ARM-based coprocessor with its own OS
  * Active computation - runs security-sensitive operations itself
  * Isolated execution - processes cryptographic operations in hardware isolation
  * Real-time operations - handles Touch ID, Face ID, payment processing
  * Application processor - can run complex security applications
  * Fare more advance than the TPM.
* **Key Management Services** used to store keys and certificates and maange them centreally.

#### Summary
* TPM -> Used for system securty
* HSM -> to create, store and manage keys for multiple systems
* KMS -> a servuce for managung secrets

### Endpoint Security Tools

* **Antivirus and Antimalware** - Still useful
  * Detection methods
    * *Signature-Based* Hash/patterns recogintion of known virus/malware (IoC)
    * *Heuristic or Behavior-based* looks for similar behavior as known malware's behavior
    * *AI/ML* Use large datasets to build signature and behavior based signatures.
    * *Sandboxing* Let run malicious code run in a sandbox and analyze it.
      * Sandboxing having an isolated environment.
      * Some malware tries to identify if they're in a sandbox, so they don't behave as usual.
      * [Cuckoo Sandbox GitHub](https://github.com/cuckoosandbox) and [Docs](https://cuckoo.readthedocs.io/en/latest/introduction/what/) which is an automated malware analysis tool.
  * Last line of defence on an endpoint, so strongly recommended, but not sufficient.
  * When consider using it... ask:
    * **What are threats are you likely to face?** in some organizations it's mostly workstations and email, so have antimalware that focuses on those areas.
    * **Integration with other security tools** do you need monitoring/reporting of malware solutions into another tool?
    * **Detection capabilities you use** and how likely will you catch stuff? Using more than one antimalware technology might further decrease risk.
* **Allow/White Lists and Deny/Black/Block Lists**
  * Control what software can be installed
  * Allow lists good for highest secure environments
  * Deny lists good when there should be more flexibility for unknown software.
  * Maintaining the lists is time consuming.
* **(Endpoint Detection and Response (EDR)**
  * Offer monitoring of Endpoints using an agent/client
    * Focus on: Network monitor and log analysis => To Correlate/analyze events
    * Able to search and explore all collected data for investigations + detection of suspicious data.
    * Search for anomalies and IoCs
    * Magic is in the detection and reporting.
  * XDR (THe extended version of EDR) - takes broader perspective
    * Ingest from a broader perspect logs and such to aim the same goals as EDR.
* **Data Loss Prevention (DLP)**
  * Protect against intentional and accidental data loss/exfiltration.
  * Feature: Able to classify data - data labeling, tagging, soyou know what to treat different or apply policies.
  * Feature: Encrypt data when sent outside certain trust boundry - or use other techniques like tokenization, etc...
  * Feature: Map organizational data and apply policies
* **Network Defenses**
  * **Host-Based Firewall** are firewalls installed or part of the host. Don't allow analyzing traffic.
  * **Host-based Intrusion Prevention System (HIPS)** - Analyzes traffic before it "enters" the host.
    * This can decide on its own logic to block traffic (unlike the firwall that has fixed clear rules), so comes with caution!
      * Example: A new OS update caused a new behavior, but the HIPS itself was not not updated yet to know about this new update's behavior, BLOCK.
  * **Host-based Intrusion Detection System** - Can only detect, but not take action.
    * Ideal to combine with the Host-Based firewall, so you have fixed clear rules, but you can also analyze the traffic, without unpredictable behavior.

## Hardening Techniques
### Hardening
Changing the settings to increase its overall level fo security and reduce its vulnerability.

* **Hardening guidelines** for various OS, software, ...
  * [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
  * [NIST Repositoryu](http://ncp.nist.gov/repository)

### Service Hardening
* **Reduce number of `open ports` and `protocols`**
  * If a port is closed, its hard to exploit remotly
  * Port scanners are usually used to seek for first vulnerabilities
  * Rule of thumb: Only ports and services that must be available to provide necessary services should be open. Those that are open should be limited to the networks and services that use them.
* Most common
  * 22/TCP - SSH (Linux)
  * 53/TCP and UDP - DNS (Linux & Windows)
  * 80/TCP - HTTP (Linux & Windows)
  * 125-129/TCP and UDP - NetBIOS (Linux & Windows)
  * 389/TCP and UDP - LDAP  (Linux & Windows)
  * 443/TCP - HTTPS (Linux & Windows)
  * 3389TCP and UDP - RDP (Windows)
* **Block ports AND STOP services**
  * Stop SSH `systemd` or RDP `services.msc` services.

### Network Hardening
* Use **VLAN** or **subnets** (VPCs) to segment the network. Create trust boundries.
  * Example: Use guest networks

### Default Passwords
* [Password Advice](passwords#Advice)

### Removing Unnecessary Software
* Less patching, maintenance, no risk of them running by accident
* Kill bloatware

## Operating System Hardening
Again, check [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks) for hardening.
CIS Benchmark example for Windows
```
* Set password history to 24 or more
* Max password age to 1 year or les, but not 0.
* Min password length 0f 12
* Require password complexity
* Disable password storage with reversible encryption
```
It's a long list! Just remember to use tools to automate this.

* **Hardening the windows registry**
  * Configure the permission for the registry
  * Block remore registry access
* **Windows Group Policy and Hardening**
  * Group Policy Objects allow to stricten permissions to key thigs (min password, guest account enablement)
* **Hardening Linux: Security Enhanced Linux (SELinux)**
  * Security module om top of existing linux distrubtions
  * [Wiki](https://en.wikipedia.org/wiki/Security-Enhanced_Linux)
  * Capabilities like:
    * [Mandatory Access Control](<identity-and-access-management#Access Control Schemes>)
  * See also [AppArmor](https://apparmor.net/) for security hardening
### Configuration, Standards, and Schemas

* **Patching and Patch Management**
### Encryption

## Securing Embedded and Specialized Systems
### Embedded Systems
### SCADA and ICS
### Securing the Internet of Things Communication Considerations
### Security Constraints of Embedded Systems

## Asset Management
