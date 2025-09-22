# Network Security

## Designing Secure Networks
* Different security controls usually operate on a distinct [ISO Model Layer](<../../computer-networks#the-7-layers>)
  * Most popular: Application Layer (7); Transport Layer (4) ; and Network Layer (3)

### Infrastructure Considerations
* **Attack Surface** - Points at which an unauthorized user could gain access.
* **Device Placement** - Physical placement are impact by needs, features and prefered topology and security design
  * Examplex: create VLANs, ...
* **Security Zones** - Network segments (physical/virtual)
  * For many reasons
  * Exampoles: Guest networks, internet facing networks (DMZ), management networks, higher clearance level, more sensitive data.
* **Connectivity Considerations** how connectivity is implemented (wifi, optics, cable, ...) and necessary throughput
  * Also multiple ISPs/failover connections are part of this
* **Failure Modes** - What if a security device fails ? Depends on business requirements
  * `fail-closed` - block any traffic during failure
  * `fail-open` - do't interfere with traffic during failure
* **Network Taps** to monitor traffic
  * `active` powered
  * `passive` not powered (removes los off power failure mode)

### Network Design Concepts
* **Physical Isolation** - requires physical presence to move data between air-gapped systems.
  * aka **Air-Gapped**`
  * Known hack: Malware that copied itself to USB sticks.
* **Logical Segmentation** - Virtual/software level isolation of networks
  * Often on Layer 2,3
  * aka VLANs, Subnets, ...
  * Packets move with VLAN tags.
  * Attacks focust on devices/systems that seperate/enforce this.
* **High Availability (HA)** to handle the `Availability` goal
* **Implementing Secure Protocols** - ensure that services/communication is secure
  * E.g. HTTPS over HTTP; SSH over Telnet
  * Mind the Protocol versions! (downgrade attacks)
  * Using an alternate port NOT a security control (Just obscurity)
* **Reputation Services** - feeds that track IP addresses, domains, and hosts known to engage in malicious activity.
  * Often combined with threat feeds.
* **Software-Defined Networking (SDN)** software-based network configuration.
  * Relies on controllers that managed network devices and configurations.
  * Flexibile, can be changed based on metrics/insights.
  * You can configure security zones and such (like security groups in AWS).
  * Often on Layer 2,3 and sometimes 4.
* **Software-Defined Wide Area Network (SD-WAN)**
  * Used more for availability, connecting various internet providers in a transparent way.
* **Scure Access Service Edge (SASE)**
  * Pronounced "Sassy"
  * Combines: **VLAN**, **SDN-WAN**, **firewalls**, **Cloud Access Security Brokers (CASB)**
  * USed to
    * make endpoints secure.
    * in-transit data is secure
    * policy-based security enforcement
  * **Cloud Access Security Brokers (CASB)** - policy enforcement point between service providers and service customers to allow organizations to enforce their policies for cloud resources.

### Network Segmentation
* **VLAN** is oneof the many technologies to implement segmentation.
  * Sets up a broadcast domain that is segmented at Data Link Layer (Layer 2).
  * Netowkrk devices enforce these packet forward based on the VLAN "tag".
  * The tag is assigned by the network devices as they receive traffic from an endpoint, the endpoint itself doesn't tag the data.
* **Segementation Designs**
  * Demilitarizewd Zones (DMZ)/Screened Subnets - Exposed to less trusted areas (public internet)
    * Mostly used for public facing devices. But internally in networks this could also be necessary.
  * Intranets - Like only for employees
  * Extranets - For external access
* **North-South Traffic**
  * Traffic between internal systems and the outside world (clients, internet, external networks).
  * Think: in/out of the datacenter or cloud.
* **East-West Traffic** - traffic flow in datacenter
  * Traffic within a datacenter, cloud, or enterprise network, i.e., between internal systems.
  * Think: side-to-side, lateral movement inside the environment.

### Zero Trust
* Never trust, always verify.
* See also [General Concepts](<general-concepts#Zero Trust>)
* ![img](assets/zero_trust_architecture.png)
  * [Source - NIST Zero Trust Architecture (NIST SP 800-207)](https://csrc.nist.gov/pubs/sp/800/207/final)
  * *Subjct*: The actors
  * *Policy Engines*: Are the decision/rule engines"
  * *Policy Administrators*: Enforce the decisions
  * *Policy Enforcement Points*: Where enforcement happens
    * Commonly deployed as a local agent
  * *Control Plane*
    * *Adaptive Identity/Authentication* - use context-based authN
      * based on: location subject, device of subject, does device meet security, ...
      * Can request additional validation for AuthN if necesary
    * *Threat Scope Reduction (limited blast radius)*
      * `least privilege` + `identity based network segmentation`
        * meaning, based on your identity, the scope for network segmentation is set for the subject.
    * *Policy-Driven Access Control* - the policy check
    * *Policy Administrator* - who enforces
  * *Data Plane*
    * *Implicit trust zones*  - where can subject move once authenticated
    * *Subjects and systems* - users/systems that seek access
    * *Policy Enforcement Points* - Where its enforced

### Network Access Control (NAC)
> Is a system/device/endpoint alllwed to connect to given network?

* Implementation types
  * Agent
    * Agent based: Installed agent on endpoint to perform security checks.
      * Can go very deep based on OS, version, patches, detailed endpoint intelligence.
      * More control but more effort to install/maintain
    * Agentless
      * less control but easier/cheaper
  * Admission Checks
    * preadmission - before connecting
    * postadmission - after connecting
* If violations happen, endpoint can be put in quarantine so it can be fixed.
* **802.1X** - authN standard for endpoints on WIRED & WIRELESS networks.
  * `Supplicant` - the subject
  * Post authentication/connecting, then segmentation happens if applied.
  * [See also](<identity-and-access-management#Authentication and Authorization Technologies>)
  * Also used for `port-authentication`, being the `physical port`.
    * So even when you connect physically to a port, a `supplicant` has to be provided and a AuthN process must find place.

### Port Security and Port-Level Protections
> Again, we are reffering here to the physical ports.
* **Port Security** - Allow list `mac addresses` for a specific port (or max amount of mac addresses)
  * Prevents MAC spoofing, content-addresable memory (CAM) table overfflows, plug in extra network devices
* **Content-addresable memory (CAM) table**
  * Maps `mac` addresses to `ip` addreses.
  * Poisining the **CAM** could allow attackers to "escape" certain limitations.
  * **CAM Table Overflow Attack**
    * Overflow the CAM table (usually fixed size) by spamming thousands of frames with random different mac addresses
    * Once full, no new mac addresses can b learned, so it falls back to HUB (broadcast anything you get)
    * Result: Attack reveives now all traffic on their port
* **Mac Spoofing** might not be hard, port security can still be that extra layer of challenge.
* **Port-Level Protections**
  * **General Concepts**
      * *Bridge Protocol Data Unit (BPDU)* - Messages to coordinate the Spanning Tree.
      * *Spanning Tree* - Loop-free path layout that Spanning Tree Protocol (STP) creates across your switched network.
  * **Protections***
    * *Loop Prevention* - Detect and stop loops (e.g. connect 2 ports on the same switch)
      * Spanning Tree Protocol (STP) is used for this, using BPDUs.
    * *Broadcast storm prevention* - Prevent broadcast packets from being amplified and traverse the network.
    * *DPU Guard* - Block ports from sending BPDU messages that shouldn't. Usually ports with endpoints connecting to them.
    * *Dynamic Host Configuration Protocol (DHCP) SNOOPING* - Prevent rogue/random DHCP servers of handing out IP addresses.
      * If DHCP message is not from a "trust list" and/or "expected mac list", drop the message.
      * If DHCP message resonse to "offer an IP address" does not come from the same port as it was requested
        * Why did you come from the left door? I send my request through the right door.

### Virtual Private Networks (VPNs) and Remote Access
> Allows to act as 2 endpoints are on the same network over a public network.

* **Important**: A VPN tunnel is not by definition encrypted!
* **The Major VPN technologies**
  * *IPSec VPNs*
    * Mostly for
      * `site-to-site` connections
      * Need to transport more than just web/app traffic.
    * level 3 (network layer)
    * Require a client
    * 2 Modes
      * `tunnel` - Entire packets of data sent over the connection are protected.
        * Network devices route based on original IP addresses
      * `transport` - IP header is unprotected, but IP payload is encrypted.
        * Network devices route based on tunnel endpoint IP addresses
        * Important if you still need routing/network visibility (That's why `site-to-site` works great)
  * *SSL VPNs**
    * Actually uses TLS obviously
    * Either
      * Portal-Based approach : Users acces via web page and access services through the connection
      * `tunnel` mode like IPSec.: Entirely encrypted data, but don't require the client!
    * Don't requirce a client.
    * Allows to segment application access, so more granualar access without too much complexity.
* **Deciding VPN Type**
  * Do you need
    * `site-to-site` (always-on)
    * `remote access` (as-needed) - for traveling/remote employees
* **Tunneling**


### Network Appliances and Security Tools
* **TODO**

### Deception and Disruption Technology
* **TODO**

### Network Security, Services, and Management
* **TODO**

## Secure Protocols
### Using Secure Protocols
* **TODO**

### Secure Protocols
* **TODO**

## Network Attacks
### On-Path Attacks
* **TODO**

### Domain Name System Attacks
* **TODO**

### Credential Replay Attacks
* **TODO**

### Malicious Code
* **TODO**

### Distributed Denial-of-Service Attacks
* **TODO**
