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
      * ![img](../assets/endpoint_security_uefi_secure_boot_process)
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


## Hardening Techniques
### Hardening
### Service Hardening
### Network Hardening
### Default Passwords
### Removing Unnecessary Software

## Operating System Hardening
### Configuration, Standards, and Schemas
### Encryption

## Securing Embedded and Specialized Systems
### Embedded Systems
### SCADA and ICS
### Securing the Internet of Things Communication Considerations
### Security Constraints of Embedded Systems

## Asset Management
