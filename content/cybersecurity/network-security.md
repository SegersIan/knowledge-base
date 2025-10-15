---
title: "Network Security"
---
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
  * Replacement for Multiprotocol Label Switching (MPLS)
  * **SD-WAN and MPLS are alternative WAN technologies that often compete or complement each other:*
  *  **Key Relationship:**
    * **MPLS = Traditional approach:**
      - **Hardware-centric**: Dedicated circuits, fixed paths
      - **Service provider managed**: Limited customer control
      - **Expensive**: Premium pricing for guaranteed performance
      - **Predictable**: Consistent performance, SLAs
    * **SD-WAN = Modern approach:**
      - **Software-defined**: Centralized policy management
      - **Internet-based**: Uses broadband, LTE, etc. (cheaper links)
      - **Customer controlled**: Dynamic path selection, policies
      - **Flexible**: Adapts to real-time network conditions
* **Secure Access Service Edge (SASE)**
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
  * *Split-Tunnel* - Only send traffic intended for the secure other side of the tunnel.
    * Example: Public internet via usual connetion, but intranet storage via Tunnel.
  * *Full-Tunnel*  - Send all network traffic through VPN tunnel
    * Example: When you are in a coffeeshop and you can't trust even the local network, you might then want to direct ALL traffic through the tunnel.

### Network Appliances and Security Tools
* **Jump Servers/Boxes** - Securely operate in security zones with different security levels.
  * Lives in the target security level
  * Accessed often via SSH, RDP, ...
  * Should be configured for a secure audit trail, with the audit trail living also somewhere else securely.
* **Load Balancing**
  * *Modes*
      * `Active/Active` distribute equally across backend systems
      * `Acive/Passive` bring backup backend systems online when an active system fails.
  * *Algorithms*
    * `round robin`
    * `Least connection` - send to backend with least connections
    * `agent based` - based on reporting of agents installed on the backend systems.
    * `Source IP hashing` - randomized algorithm using the IP address of the coient
    * `weighed least connection` -  `least connection` + `weights` to influence prefereence
    * `fixed weights` - just fixed weights set per backend system.
    * `weighted response times` - backend's response time + `weights` to influence prefereence
  * *Sticky Sessions* - Let a client stick to a distinct backend for entire session,
  * *Network Level*
    * Layer 4: Transport level based load balancing - Is dummer
      * Less overhead, but limited to protocol, port, IP address, etc...
    * Layer 7: Application level load balancing - Can do smart stuff based on request level (e.g. inspect headers)
      * more overhead, cpu, etc... has performance penalty

* **Proxy Servers**
  * Forward requests
  * Due to centraliztions of forwarding requests, you can take actions on these request or responses.
  * Actions
    * Filter
    * modify
    * cache
    * Restrictions
  * *Forward Proxy* between clients and servers
    * Forward requests to servers.
    * This hides original IP, so this is how you can get around geoblocking for example or other blocking based on source IP.
  * *Reverse Proxy* between servers and clients
    * Can act as load balancer and cache for static content.
    * Features are quite broad
* **WebFilters**
  * aka **Content Filters**
  * Centralized proxies or agent based tools to allow/block traffic based on consent rules.
    * Content categorization allows for having various categories with different rules.
* **Data Protection**
  * Use Data Loss Protection (DLP) to avoid exfiltration points.
    * Can send notifications, block traffic, encrypt data, ...
* **Intrusion Detection (IDSs) and Intrustion Prevention Systems (IPSs)**
  * To either detect and/or block threats.
  * Methods
    * `Signature-Based` detection rely on known Hash/signatures of threats
    * `Anomaly-Bases` detection rely on having a baseline and then spot anomalies.
  * An IPS in passive mode, just monitors and takes no action, acting as a IDS essentially.
  * `Active/Inline` mode - All traffic flows THROUGH the IDS/IPS
    * Network dependency: If IDS fails, network traffic stops, although SOME have a `fail open` possibility.
  * `Passive/Tap` mode - IDS/IPS receives COPY of network traffic
    * No network impact: If IDS fails, network traffic continues normally
* **Firewalls**
  * *Next-Generation Firewalls (NGFW)* can interact on level 4 (transport) and level 7 (application) of the network layers.
    * Can be called `all-in-one` network security devices.
      * Can do IDS/IPS, deep inspectiom, antivirus/malware detections, overlap a bit with UTM, but typically faster cause it's still a bit more focussed.
      * More configuration and expertise required.
  * *Uniform Threat Management (UTM)* - firwall, IDS/IPS, antimalwaree, URL + Email filtering, DLP, VPN, Security and analytics capabilities. EVERYHTING.
    * "Out of the box"
    * Deployed at network boundires.
  * `Stateless` - Just apply the filter rules, very basic.
  * `Statefull` - They keep the state of flow, so they can make more overarching decisions.
    * Example: They can "recognize" a message that's an agress response from a previously approved ingress request.
  * *Web Application Firewals (WAF)*
    * Works only on level 7 (application) and does even stuff like XSS/SQL injection and other scanning, so this is more specialized for distinct application. So firewall + IPS without other fancies.
  * **Screened Subnets**
    * So firewwalls allow creation of screend subnets. For example `public internet <-> Firewall <-> DMZ`, the firewall made this seperation possible.
  * Example Rules `ALLOW TCP port ANY from 10.0.10.0/24 to 10.1.1.68/32 to TCP port 80`
* **Access Control Lists (ACLs)**
  * Simple rules: Often close to firewall rules, applied by any network device.
  * Advanced rules: Advanced ACLS, time-based, dynamic, or other ACLs including conditionals.
  * Example Cisco Rules `access-list 100 permit tcp any host 10.10.10.1 eq http`
  * Often used in cloud a security groups and stuff.

### Deception and Disruption Technology
* **Goal**: Capture info about attackers + techniques they're using => So you can disrupt ongoing attacks.
* **Major Types**
  * *Honeypots* - Intentionally configured to appear vulnerable, but heavily instrumented and monitored systems, documenting everything an attacker does while keeping copies of every file and command used.
    * **GOAL: Adversial Research**
  * *Honeynets* - A group of honey pots to be even more tempting and more details on an attacker.
    * Gives more insight on network attacks.
    * **GOAL: Adversial Research**
  * *Honeyfile* - Intentionally attractive file (With unique detectible data, fingerprinted), for if the attacker succeeds.
    * **GOAL: Intrusion Detection**
    * If you notice this data leaving the network or is found later outside the network, you know you've been breached.
    * Have a DLP detect it would be awesone.
  * *Honeytokens* - Intentionally attractive data but specificllay to allow for tracking data.
    * **GOAL: Intrusion Detection**
    * E.g. entries in database, files, directorictes,...
    * IDS, IPS, DLP or other systems then watch for those data.
* See [HoneyNet Project](https://www.honeynet.org/)

### Network Security, Services, and Management
* **Out-Of-Band Management** - another way of accessing the admin interface
  * Physical seperate port or vlan for the admin pannel of some device.
  * Physical access itself is also option, but often far less realistic for frequent access.
* **DNS** - Can be poisoned, so attacker can "impersonate"
  * **DNSSEC**
    * Provides authentication of DNS data
  * *Proper configuration*
    * Disable zone transfers
    * DNS logging
    * Requests to malicious DNS domains blocked
  * *DNS Filtering* blocks mailicious domians
    * Often fed through threat, reputation and deeny lists feeds.
* **Email Security**
  * *Domain Keys Identified Maiul (DKIM)* - Public DNS record lists Public Key which van be used to verify all the emails from a given domain. All those email bodies and headers are signed with corrolated Private Key.
    * TL;DR; Signing of emails
    * This helps those reveive your emails.
  * *Sender Policy Framework (SPF)* - List all the allowed senders/servers where emails can be sent from
    * Can be your on premise email servers and then the 3th party service that you want to sent emails on your behalf
    * TL;DR; Is the sender allowed to send for given domain?
    * This helps those reveive your emails.
  * *Domain Based Message Authentication Reporting and Conformance (DMARC)* - If not authentic, what do I do ?
    * TL;DR; Gives hints/tips/directions on what to do when DKIM/SPF fails.
    * This helps those reveive your emails.
  * *Email Security Gateways (SEG)* - filter inbound/outbound emails
    * Phising protection, email protection, URL analysis, threat feed integration and all the checking of DKIM, SPF and DMARC above.
* **Secure Socket Layer (SSL)/Transport Layer Security(TLS)**
  * *TLS* used ephemeral keys, so a key per session.
    * First there is a `diffie-helman` key exchange which estabilished then a connection specific "session key".
* **Simple Network Mangement Protocol (SNMP)** monitor and manage network devices.
  * [Detailed Description](https://www.manageengine.com/network-monitoring/what-is-snmp.html)
  * When a deviced (configured to use SNMP) has a failure or error, it sends a `snmp trap` message to the centralized `snmp` managwer.
  * events like `coldStart`, `warmStart`, `linkDown`, `linkUp`, `authenticationFailure`, and `egpNeighborLoss`.
* **Monitoring Servicers & Systems** - health checks in essence
  * Is a port responding?
  * Is the service on the port responding correctly?
* **File Integrity Monitors** monitor important files against changess (e.g config files)
  * Example: Tripwire
  * Createe signagtures/fingerprints of files and then watches for any changes.
* **Hardening Network Devices**
  * Same as endpoint hardening, follow Center for Internet Security (CIS) benchmarks for hardening guides.
  * Protect the management console - use isolated vlan/network/jump server or VPMN.

## Secure Protocols
### Using Secure Protocols
* **Scenario:** Video/Voice/Videoconferencing (initially HTTP, SIP, RTP)
  * *Secure Protocol(s)/Alternatives:* HTTPS, Session Initiation Protocol over TLS (SIPS), Secure Real Time Transport Protocol (SRTP)
* **Scenario** Network Time Prococol (NTP)
  * *Secure Protocol(s)/Alternatives:* NTS (relies on TLS), does not protect the data, but provides authN and integrity reinsurrance. Not widely adopted tho.
* **Scenario** Email Web traffic
  * *Secure Protocol(s)/Alternatives:* HTTPS, IMAPS, DMARK, DKIM, SPF
* **Scenario** FTP
  * *Secure Protocol(s)/Alternatives:* HTTP, SFTP or FTPS
* **Scenario** LDAP
  * *Secure Protocol(s)/Alternatives:*: LDAPS
* **Scenario:** Remote Access (Tetlnet)
  * *Secure Protocol(s)/Alternatives:* SSH, RDS, HTTPS
* **Scenario:**  Routing and switching protcol security - Border Gateway Protocol (BGP)
  * *Secure Protocol(s)/Alternatives:* No secure alternative
* **Scenario:** Domain Name Resolution (DNS)
  * *Secure Protocol(s)/Alternatives:* DNSSEC and DNS Reputation lists
* **Scenario:** Network Addres allocation (DHCP)
  * *Secure Protocol(s)/Alternatives:* no alternative, relie on detection and response instead of detterent
* **Scenario:** Subscription Servicees and cloud toold (HTTPS)
  * *Secure Protocol(s)/Alternatives:* N/A

### Secure Protocols
> Note: Understand when you would recommend:
>   - To switch to the secure protocol
>   - If both protocols might coexist
>   - Other factors to take in account when implementing

| Unsecure protocol | Original port   | Secure protocol option(s) | Secure port   | Notes |
|-------------------|-----------------|---------------------------|---------------| --- |
| DNS   | UDP/TCP 53      | DNSSEC   | UDP/TCP 53                                       | |
| FTP   | TCP 21 (and 20) | FTPS     | TCP 21 (explicit mode) / TCP 990 (implicit mode) |  Using TLS |
| FTP   | TCP 21 (and 20) | SFTP     | TCP 22 (SSH)                                     | Using SSH |
| HTTP  | TCP 80          | HTTPS    | TCP 443                                          | Using TLS |
| IMAP  | TCP 143         | IMAPS    | TCP 993                                          | Using TLS, Fetching emails from server, stay in sync. |
| LDAP  | UDP/TCP 389     | LDAPS    | TCP 636                                          | Using TLS |
| POP3  | TCP 110         | POPS     | TCP 995 — Secure POP3                            | Using TLS, Fetching emails and delete on server |
| RTP   | UDP 16384–32767 | SRTP     | UDP 5004                                        | Real Time Protocol |
| SNMP  | UDP 161 and 162 | SNMPv3   | UDP 161 and 162                                 | Simple Network Management Protocol |
| Telnet | TCP 23          | SSH      | TCP 22                                         | Remote Access |
| SMPT   | TCP 25          | SMTPS over TLS | TCP 465                                  | Sending of emails |
* `DNSSEC` uses digital signatures for authentication and integrity.
* `SNMPv3` improves with authentication, integrity validation and encruptions.
  * You can still run this on a lower security level, if you don't use `authPriv`, then it's insecure, even `v3`
* `ssh` is also used as tunneling protoctol or `sftp`.
  * If you don't use a password for the `ssh keys`, it's still less ecure.
* `SRPT` uses encryption and authentication
  * pairs with `Secure Real Time Control Protocol (SRTCP)` that monitors the `QoS`
* `LDAPS` is a TLS version of LDAP.

* **Email Related Protocols**
  * `Secure Multipurpose Internet Mail Extension (S/MIME)` allowsto encrypt and sign `mime` data, the format for email attachments.
    * Integrity, non-repudiation, confideniality, Authentication
    * used less frequently cause you need certificate for each user from own KPI or CA.
  * SMPT has no Secure option
* **File Transfer Protocols**
  * `FTPS` => `FTP` over `HTTPS` => as it uses might require extra ports.
  * `SFTP` => `FTP` over `SSH` => as it re-uses the SSH port, its often easer to set up
* **Internet Protocol Security (IPSec)** used to encrypt and authenticate IP traffic
  * More than jus a single protocol
  * *Authentication Header (AH)*: hashing + shared key to ensure integrity and authentication (like HMAC)
  * *Encapsualting Security Payload (ESP)* like with VPNs:
    * `tunnel` mode: integrity + authentication for entire packet (headers + payload).
    * `transport` mode: integrity + authentication for payload alone.
  *  *Security Associations (SA)*: Provide parameters for AH and ESP to operate
  * [IPSec wiki](https://en.wikipedia.org/wiki/IPsec)

## Network Attacks
### On-Path Attacks
* aka **Man-In-The-middle**
* Attacker forces traffic to go through him, allowing for eavesdropping and/or altering the communication.
* **SSL Stripping** for when someone is "on-path"
  * How its done
    1. Victim types: https://bank.com
    2. Attacker intercepts, serves HTTP version of login page (forces downgrade)
    3. Victim submits credentials over HTTP (thinking it's secure)
    4. Attacker captures plaintext credentials
    5. Attacker forwards request over HTTPS to real bank.com
    6. Attacker relays response back to victim (still over HTTP)
  * Protection: `HTTP Strict Tansport Security (HSTS)` - forces browsers to connect only via HTTPS using TLS
    * IMPORTANT: Only works after the user has visited the site AT LEAST ONCE (where the attack can already happen).
    * Browsers and plugins can "force" any request to go over https, even if http was requested. (HTTPS Anywhere).
    * Certificate pinning
* **Browser-based on-path attack** Relies on Trojan in the user's browser.
  * Trojan can access bypass TLS encryption, it just needs to intercept requests/responsed before encrypting or after decrypting, so it can be modified, or injected with content [see injection attacks](<application-security#Code Injection Attacks>)

### Domain Name System Attacks
* **Domain Hijacking** - Stealing the domain, so they can be pointed to malicious systems
  * By Social Engineering
  * Technical Means
  * People forgetting to renew
* **DNS Poisining**
  * Method 1: On-Path attack where attacker supplies a altered DNS query with a destination to a malicious system.\
  * Method 2: Poison thee DNS cache on a system (like the local OS/Browser cache)
* **URL Redirection**
  * Popular Method: Insert alternate IP in hosts file.
    * Can be scanned and checked for changes by antimalware tools.
* **Domain Reputation** can be also used to our benefit.

### Credential Replay Attacks
* Requires attacker to capture valid networkd data and re-send or delay.
* Usuallt on-path
* IoC: Modified gatwats or routes

### Malicious Code
* [See Malware Types](malware-types)
* See IoC's per type.

### Distributed Denial-of-Service (DDoS) Attacks

* **Network DDoS** - Most common form of DDoS
  * Often uses botnets to conduct these attacks or commercial services for testing purposes.
  * *Protection(s)*
    * ISP might provide protection service.
    * Your network border security devices.
  * *Categories of DDoS techniques*
    * `Volume-Based` - Just sheer volume of traffic
      * Some use *amplification techiques* that leverage flaws/features in protocols to generate more traffic than the attack sends.
        * `UDP Floods` - UDP doesn't use 3way handshake like TCP, so the host will just try to process it. UDP is also not rate limited.
          * Can be detected with IDS and IPS, or with a packet analyzer manually.
        * `ICMP Floods` - Sends many `ping` messages, ICMP is ratelimited in modern systems
            * Many OS/Systems/network devices disable `ping/icmp` support by default.
      * `Amplified Denial-of-service attack` - Use protocols that allow a small query to return large sets of data (e.g. DNS, NTP, SNMP, ...)
        * Again, if you spoof the sender address (change it to your target), all these DNS resuls will be sent to the target.
      * `Reflected Denial-of-service attack` this is more specificly about the spoofing, so the sender spoofs the sender IP to the target's IP, which makes it also hard to dstop and track down.
      * Could be still same size requests.
    * `Protocol-Based`
      * TCP Based - they do use a 3 way handshake, process being `SYN > SYN/ACK > ACK`.
        * `SYN flood` sends `SYN` messages to server, server respond with `SYN/ACK` but then the attacker never responds with the final `ACK`  so the server meanwhile keeps waiting and blocking resources, hoping to receive the `ACK`, eventually timing out. But this allows for many of these handshakes to open up but not close, causing a lot fo resources on the server side.
        * MOST COMMON
      * Older
        * `Ping of Death` - Ping packet too large to handle
        * `Smurf attacks` - Send a spoofed ping packet, and systems would respond back to this spoofed target address, overwelhmin it.
        * `Xmas/Christmas tree attack` - Packets with  all their TCP flags on

## Others

### IPv6
* **Basic format:**
  * 128-bit addresses (vs IPv4's 32-bit)
  * Hexadecimal notation: 2001:db8::1
  * Address shortening: :: represents consecutive zeros
* **Security implications:**
  * Larger attack surface: Huge address space makes scanning harder but networks more complex
  * Dual-stack risks: Running IPv4 and IPv6 simultaneously creates more attack vectors
  * Tunneling protocols: 6to4, Teredo can bypass security controls
  * ICMPv6: More critical than ICMPv4 - blocking it breaks IPv6 functionality

### Quality Of Service (QoS)
- **Prioritizes network traffic** based on importance/type
- **Bandwidth allocation** and **latency management**
- **Traffic shaping** - controls data flow rates

**Security implications (the important part):**
  **QoS bypasses:**
  - **Attackers can mark traffic** as high priority to bypass security controls
  - **DDoS amplification**: Flood high-priority queues to impact critical services
  - **Covert channels**: Hide data in QoS headers/markings

  **Network security integration:**
  - **Firewall QoS rules** - ensure security traffic gets priority
  - **VPN QoS**: Critical security traffic shouldn't be deprioritized
  - **Security tool performance**: IDS/IPS need adequate bandwidth allocation

  **Basic mechanisms (just awareness level):**
  - **DSCP marking**: How traffic gets tagged for priority
  - **Traffic classes**: Voice, video, data, background
  - **Bandwidth guarantee vs limiting**

**Real-world security context:**
- **VoIP security**: Voice traffic prioritization can impact security monitoring
- **Critical system access**: Ensure management traffic has QoS priority
- **Incident response**: Security tools need guaranteed bandwidth during attacks
