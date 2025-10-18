---
title: "Data Exfiltration Techniques"
---
# 🕵️‍♂️ Data Exfiltration Techniques — One-Page Overview

## 🌐 Network / Protocol Channels

| Technique                                       | Description                                                         | Key Mitigations                                                                                 |
| ----------------------------------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **DNS tunneling**                               | Encodes data into DNS queries/subdomains to attacker DNS.           | Egress DNS only via internal resolvers, monitor high-entropy queries, block suspicious domains. |
| **HTTP(S) exfiltration**                        | Sends data via POST/GET requests or WebSockets to external servers. | Proxy inspection, CASB, DLP, block unknown domains.                                             |
| **DoH / DoT abuse**                             | Uses encrypted DNS to bypass DNS monitoring.                        | Allow DoH only to corporate resolvers, block public DoH.                                        |
| **Email exfiltration**                          | Sends sensitive files via SMTP or webmail.                          | Email DLP, restrict external recipients.                                                        |
| **FTP / SFTP / SCP**                            | Uploads data to external file servers.                              | Block outbound file transfer protocols, proxy inspection.                                       |
| **Cloud storage abuse (Dropbox, GDrive, etc.)** | Uploads data to personal cloud accounts.                            | CASB, DLP, restrict unsanctioned apps.                                                          |
| **VPN / SSH / Reverse shell**                   | Creates encrypted tunnels to attacker infrastructure.               | Egress filtering, detect long-lived tunnels, block unauthorized ports.                          |
| **ICMP / UDP / TCP covert channels**            | Hides data in packet payloads or headers.                           | Restrict ICMP/UDP, IDS/IPS signatures.                                                          |
| **P2P / Torrent**                               | Uses P2P protocols to share data.                                   | Block P2P, monitor for protocol signatures.                                                     |

---

## ⚙️ Application / Database Techniques

| Technique                           | Description                                            | Key Mitigations                                 |
| ----------------------------------- | ------------------------------------------------------ | ----------------------------------------------- |
| **SQL injection**                   | Exfiltrates DB data through injected queries.          | Parameterized queries, WAF.                     |
| **API abuse / parameter tampering** | Legitimate API used to extract excessive data.         | Rate limits, authZ checks, API gateway logging. |
| **SSRF**                            | Server requests internal resources and leaks data out. | Validate URLs, restrict outbound requests.      |
| **Verbose error / log leaks**       | Sensitive data exposed via logs or debug messages.     | Sanitize logs and error messages.               |

---

## 💻 Host / Endpoint Techniques

| Technique                            | Description                            | Key Mitigations                           |
| ------------------------------------ | -------------------------------------- | ----------------------------------------- |
| **Removable media (USB, SD)**        | Copies data to external drives.        | Disable/whitelist USB, endpoint DLP.      |
| **Screenshots / clipboard / camera** | Captures and exports visible data.     | MDM restrictions, EDR monitoring.         |
| **Steganography**                    | Hides data in images, audio, or video. | DLP, content inspection.                  |
| **Compressed / encrypted archives**  | Packs data into small encrypted files. | Behavioral analytics, sandbox inspection. |

---

## 🕳️ Covert / Side-Channel Methods

| Technique                        | Description                                     | Key Mitigations                                  |
| -------------------------------- | ----------------------------------------------- | ------------------------------------------------ |
| **Timing / traffic patterns**    | Encodes data via request timing.                | Anomaly detection, traffic analysis.             |
| **Optical / acoustic / thermal** | Uses LEDs, speakers, or heat emissions.         | Physical controls, disable unused peripherals.   |
| **Air-gap bridging**             | Moves data via infected USBs or nearby devices. | Strict physical controls, media handling policy. |

---

## 👥 Social / Insider Channels

| Technique                          | Description                                          | Key Mitigations                               |
| ---------------------------------- | ---------------------------------------------------- | --------------------------------------------- |
| **Phishing or social engineering** | Tricking users to upload or share sensitive data.    | Awareness training, DLP.                      |
| **Insider exfiltration**           | Malicious or careless employee copies data.          | Least privilege, UEBA, auditing.              |
| **Third-party/vendor misuse**      | Vendor or partner exfiltrates via authorized access. | Vendor monitoring, contract security clauses. |

---

## 🔍 Common Indicators

* Outbound traffic to unknown or rare domains/IPs
* High-entropy DNS queries or large DNS volume
* Unusual HTTP POSTs or uploads
* Large email attachments or bulk DB exports
* Frequent connections to cloud storage or new APIs
* Off-hours or geo-anomalous activity

---

## 🛡️ Core Mitigation Stack

* **Egress filtering & proxy logging**
* **DNS monitoring and allowlists**
* **DLP (email, web, cloud)**
* **CASB for SaaS control**
* **Endpoint DLP + EDR + MDM**
* **Strong auth & least privilege**
* **UEBA + SIEM monitoring**
* **Patch vulnerable apps & DBs**

---

**In short:**

> Data exfiltration hides sensitive data in *normal-looking traffic, files, or behaviors*.
> Layer controls: monitor egress, limit channels, detect anomalies, and enforce least privilege.
