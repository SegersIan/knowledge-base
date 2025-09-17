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
  * Most common authentication, authorization and accounting (AAA) system for network devices.
    * Accounting refers to resource utilization like time, bandwith or CPU
  * Operates over UDP and TCP as client-server model.
  * How It Works
    * RADIUS sends passwords obfuscated by shared secret + MD5 hash.
    * Traffic between RADIUS Network Server and RADUI server encrypted in IPSec tunnels usaully.
* **Terminal Access Controller Acees Control Systgem Plus (TACACS+)**
  * Proviedes AAA services
  * By Cisco
  * Operates over TCP
* **Kerberos**
  * Authentication Protocol
  * Between trusted hosts across an untrusted network (e.g. the internet)
  * Uses authentication to shield its authentication traffiix
  * Kerberos users have
    * The primairy (e.g. username)
    * The instance (to help differentiate similar primaries)
    * The Realms (groups of users) seperated by trust boundries
  * ![img](assets/identity_and_access_mgmt_kerberos.jpg)
#### Single Sign-On (SSO)
* Single identity to access multiple services/systems without reuathentication.
* Lightweight Directory Access Protocol (LDAP)
  * Offer hierarchical organized information about the organization.
    * `ou` organizational unit
    * `cn` common name
  * ![img](assets/identity_and_access_mgmt_ldap_hierarchy.jpg)
* Kerberos can be also used for SSO.
* **Core Technologies for authN & authZ to implement SSO**
  * **Security Assertion Markup Language (SAML)**
    * `xml` based to exchange AuthN/AuthZ infromation
    * So if all Identity providers follow SAML, then any service/application that wants to implement SSO, support SAML and you'll be able to integrate with various Idenity Providers.
  * **OpenID**
    * *Open standard for (decentralized) authentication.*
    * Example `Login with Google` or `Login with Facebook`
    * You login to a OpenId IDentity Provider (IdP) as external identity provider to your service/application.
    * The standard tells how this "dance" between Identity Provider and your service goes.
  * **OAuth**
    * *Open standard for authorization*
    * Method to specify "what information to provide a third-part application and sites without sharing credentials.
    * Concept of scopes, etc...
#### Federation
* The core problem Federation solves - You work at Company A, but need to access a partner application at Company B. Without federation, Company B would need to create and manage a separate account for you.
* Key Terms/topics
  * The `principal`, typically the user.
  * The `Identity Providers (IdO)` who provide identity and authentication services via `attestation` process.
  * The `Service Providers (SP) / Relying Party (RP)` who offer a service/application that the `principal` tries to access after their identity was `attested`
  * Trust relationship between `Identity Provider` and `Service Provider` must be pre established.
* Authorization is not in this process, authorization is configered on Service provider side.
  * Sometimes the SP would assign authorization rules/roles based on Identity related attibutes (like organizational unit).
  * But still, this is configured and set on the SP side.
* OpenID and SAML are often used to implement the entire Federation process.
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
