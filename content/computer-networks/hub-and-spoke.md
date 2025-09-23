# Hub-and-Spoke Network Topology

## **Concept:**
- **Central hub**: One primary connection point (router, switch, server)
- **Spokes**: Individual connections from hub to end devices/networks
- **All traffic flows through the hub**: No direct spoke-to-spoke communication

## **Structure:**
```
    Device A
       |
Device D ←→ [HUB] ←→ Device B
       |
    Device C
```

## **Characteristics:**
- **Centralized control**: Hub manages all communications
- **Simplified management**: Single point for policies, monitoring, security
- **Single point of failure**: If hub fails, entire network goes down
- **Efficient for centralized services**: File servers, internet access, authentication

## **Common Examples:**
- **Wi-Fi networks**: Access point (hub) + client devices (spokes)
- **WAN architectures**: Corporate HQ (hub) + branch offices (spokes)
- **VPN networks**: VPN concentrator (hub) + remote users (spokes)
- **Traditional Ethernet**: Switch (hub) + connected devices (spokes)

## **Trade-offs:**
- **Pros**: Simple management, centralized security, cost-effective
- **Cons**: Single point of failure, potential bottleneck at hub, limited scalability

**Bottom line:** Hub-and-spoke centralizes network traffic through one primary node for simplified management at the cost of resilience.
