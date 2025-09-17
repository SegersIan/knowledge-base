# Identity and Access Management
* **Subject** - People, applications, devices, systems, organization, entities basically
  * Most common "individual"


## Identity
* **Identity** A set of claims about such a `subject`.
    * Typically linked to information about the subject, important to the use of the identity.
    * Attribute Examples: Name, age, location, title, phyisical attributes, ...
* **Use of Identity** - If a `subject` wants to use their identity, it can claim so with:
  * `Usernames` - just identity, not an authentication in itself
  * `Certificates` - often used to identify systems and individuals.
  * `Tokens` - means to present a certificate
    * USually via a physical device
  * `SSH Keys` - Cryptographic representation replacing `username` and `password`.
  * `Smartcards` with embedded chip, often cary key pairs.
* **Lost Key Pairs**
  * Typical flaws: Uploaded private keys, no password on ssh certificates, poor passphrase mgmt.

## Authentication and Authorization
* Authentication - AuthN - Ensure the subject is who they claim to be
* Authorization - AuthZ - Verfies what you have access to.

### Authentication and Authorization Technologies
* **Extensible Authentication Protocol (EAP)**
  * Authentication framework for Wifi.
  * Implementations EAP-TLS, LEAP, EAP-TTLS...
* **Challenge Handshake Authentication Protocol (CHAP)**
  * Authentication framework
  * Encrypted challenge + 3-way handshake
  * ![img](assets/identity_and_access_mgmt_chap.jpg)
* **802.1XX**
  * Authentication framework
  * IEEE standard for devices that want to connect to network
    * Network Access Control (NAC)
  * How It works
    * Device sent authentication request to authenticators/controllers (switches, AP,...)
    * Controllers connect to authentication server, typically via RADIUS
    * RADIUS might use LDAP or Active Directory as data source for Identity information.
  * ![img](assets/identity_and_access_mgmt_8021x.jpg)
* **Remote Authentication Dial-In User Service (RADIUS)**
  * Most common authentication, authorization and account (AAA) system for network devices.
  * Operates over UDP and TCP as client-server model.
  * How It Works
    * RADIUS sends passwords obfuscated by shared secret + MD5 hash.
    * Traffic between RADIUS Network Server and RADUI server encrypted in IPSec tunnels usaully.
* **Kerberos**
  * ![img](assets/identity_and_access_mgmt_kerberos.jpg)
* **Single Sign-On**
  * ![img](assets/identity_and_access_mgmt_ldap_hierarchy.jpg)
## Authentication Methods
### Passwords
### Multifactor Authentication
### One-Time Passwords
### Biometrics

## Accounts
### Account Types
### Provisioning and Deprovisioning Accounts

## Access Control Schemes
### Filesystem Permissions
