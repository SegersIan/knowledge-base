---
title: "DoS Attack Comparison"
---
# DoS / DDoS — quick taxonomy

1. **Volumetric (bandwidth) attacks** — saturate link capacity.
2. **Protocol (state-exhaustion) attacks** — exhaust network / protocol resources (tables, connections).
3. **Application-layer attacks** — exhaust app resources by appearing as legitimate traffic.

# Table: attack types, what they do, indicators, mitigations

| Attack Type                                       |                                                                                            What it does | Typical indicators                                                               | Effective mitigations                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------: | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **SYN flood (TCP handshake abuse)**               |                              Sends lots of SYNs, never completes handshake → exhausts connection table. | Many half-open connections, rising SYN count, high % SYN vs ACK.                 | SYN cookies, connection limits, stateful firewall tuning, load balancer, upstream scrubbing. |
| **UDP flood**                                     |                                 Sends massive UDP packets to random/target ports to saturate bandwidth. | Sudden high UDP traffic volume, high bandwidth utilization.                      | Rate limiting, drop/refuse UDP to unused services, CDN/ISP scrubbing, Anycast.               |
| **ICMP flood (ping flood / smurf)**               |                                                Massive ICMP echo requests to overload network or hosts. | High ICMP traffic, ping replies from many hosts.                                 | Block/limit ICMP, network ACLs, anti-spoofing.                                               |
| **HTTP(s) flood (Layer 7)**                       |                          Many legitimate-looking HTTP requests (e.g., GET/POST) to exhaust app servers. | High requests/s with normal headers, slow response times, increased backend CPU. | WAF, rate limiting, caching, CDNs, challenge pages (CAPTCHA), autoscaling + scrubbing.       |
| **Slowloris / RUDY (slow HTTP)**                  |                         Opens many connections and sends data very slowly to keep connections occupied. | Many long-lived HTTP sessions, low traffic volume but high connection count.     | Connection timeouts, max concurrent connections, reverse proxy, load balancer.               |
| **DNS amplification (reflection)**                | Attacker spoofs victim IP, queries open DNS resolver for large responses → amplifies traffic to victim. | High UDP traffic from many resolvers, specific source ports.                     | Disable open resolvers, DNS rate limiting, BCP38, ISP filtering, scrubbing.                  |
| **NTP / SSDP / Chargen amplification**            |                                    Same reflection/amplification pattern using NTP, SSDP, Chargen, etc. | High volume UDP, many sources replying.                                          | Patch/disable services, close UDP, ISP scrubbing, ingress filtering.                         |
| **HTTP slow POST / slow body (RUDY)**             |                                                 Sends POST bodies very slowly to keep server resources. | Long POSTs, many open connections, low throughput.                               | Tighten request body timeouts, WAF rules, reverse proxies.                                   |
| **TCP/UDP fragmentation (teardrop)**              |                                                Sends fragmented packets that overload reassembly logic. | Fragmented packet spikes, reassembly errors.                                     | Patch OS, drop malformed fragments, IDS/IPS signatures.                                      |
| **TCP connection exhaustion (connection flood)**  |                                 Exhausts server's max concurrent connections (e.g., SSL handshake CPU). | Maxed connection counts, increased CPU for handshake.                            | TLS offload, rate limiting, connection limits, SYN cookies.                                  |
| **Application logic abuse (slow business logic)** |                 Exploits expensive operations (search, reports) to exhaust resources with few requests. | High CPU for specific endpoints, few requests trigger heavy work.                | Rate limit heavy endpoints, require auth, implement caching, circuit breakers.               |
| **Botnet-driven DDoS**                            |                                                    Thousands/millions of infected devices send traffic. | Distributed sources (geo), massive scale.                                        | CDN/Anycast, scrubbing services, ISP partnership, blackholing for extreme cases.             |
| **Reflection + amplification hybrid**             |                                                      Combines spoofing + amplifiers for massive volume. | Very high pps and Gbps, many distinct source IPs (reflectors).                   | ISP scrubbing, BCP38 ingress filtering, close open services.                                 |
| **Resource exhaustion via API abuse**             |                                                 High frequency of valid API calls to exhaust DB or CPU. | Elevated API call rate, slow DB, application errors.                             | API rate limiting, quotas, auth, caching, per-user throttling.                               |

# High-level indicators to monitor

* Sudden spike in bandwidth (Gbps) or packets/sec (pps).
* Explosive increase in new connections, half-open TCP sessions.
* Many requests to the same endpoint or many slow/long connections.
* Increased error rates (502/503), queue depths, CPU/memory exhaustion.
* Traffic from many spoofed source IPs or unusual geographies.

# Mitigation layers (defense in depth)

1. **Network perimeter / ISP**: BCP38 anti-spoofing, ISP DDoS protection, blackholing (targeted).
2. **Edge / CDN / Anycast**: Absorb volumetric attacks, caching, distribute load globally.
3. **DDoS scrubbing services**: Clean traffic in the cloud, drop malicious flows.
4. **Network devices**: Rate limits, ACLs, SYN cookies, connection limits.
5. **WAF & Application**: Block Layer 7 attacks, challenge suspicious clients, tune rules.
6. **Autoscaling + circuit breakers**: Scale safely and shed load on overload.
7. **App hardening**: Timeouts, request size limits, CPU-cost caps on endpoints.
8. **Monitoring & runbooks**: Telemetry, playbooks, contact with upstream ISP/scrubbers.

# Best practices & operational notes

* **Classify attacks**: volumetric vs protocol vs app — response differs.
* **Have contracts with ISP / scrubbing provider** before an incident.
* **Implement BCP38 / ingress filtering** at edge to prevent reflection use of your network.
* **Close/patch open amplifiers** (misconfigured DNS, NTP, SSDP) on your infrastructure.
* **Use CDNs / Anycast** where possible — they’re first line for volume absorption.
* **Instrument metrics**: bandwidth, pps, new connections, request latency, error rates.
* **Practice DDoS runbooks** and test failover/cutover workflows (don’t improvise during attack).

# Quick cheat-sheet (what to do when hit)

1. Identify type (bandwidth vs connection vs app).
2. Contact upstream ISP / DDoS provider.
3. Enable rate limits, SYN cookies, and stricter timeouts.
4. Divert to scrubbing center if volumetric > your link.
5. Apply WAF rules or CAPTCHA for suspicious Layer-7 traffic.
6. Monitor, preserve logs, and communicate with stakeholders.