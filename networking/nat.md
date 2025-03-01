# Network Address Translation (NAT) Explained

This document dives into how **Network Address Translation (NAT)** works, using a simple home setup: a PC connected to a modem via an Ethernet cable. NAT is a critical process in modern networking, allowing devices like your PC to communicate with the internet efficiently, especially under IPv4 constraints.

## What Is NAT?
NAT is a technique implemented in routers (or modem/router combos) to map private IP addresses to a public IP address, enabling multiple devices to share a single internet-facing address. It operates at the **network layer (Layer 3)**, modifying IP packet headers, and often pairs with **Port Address Translation (PAT)**—the most common form in homes.

## Your Home Setup
Imagine your room:
- **PC**: Connected to your modem via an Ethernet cable.
- **Private IP**: Your PC gets an address like `192.168.1.10` (from the RFC 1918 private range `192.168.0.0/16`).
- **Modem/Router**: Assigned a public IP by your ISP, e.g., `203.0.113.5`.
- **NAT**: Handled by the modem/router, translating between these IPs.

## How NAT Works: Step-by-Step
Let’s say your PC wants to visit `example.com` (IP: `93.184.216.34`, port 80). Here’s the technical breakdown:

### 1. Packet Creation (Outbound)
Your PC generates a packet:
- **Source**: `192.168.1.10:49152` (ephemeral port)
- **Destination**: `93.184.216.34:80` (web server)
- This travels over the Ethernet cable to your modem.

### 2. NAT Translation (Outbound)
The modem/router:
- Replaces the source IP and port:
  - Old: `192.168.1.10:49152`
  - New: `203.0.113.5:50001` (new port assigned)
- Updates the packet’s checksums.
- Logs the mapping in its **NAT table**:

| Private IP:Port       | Public IP:Port     | Protocol | Destination       | Timeout |
|-----------------------|--------------------|----------|-------------------|---------|
| 192.168.1.10:49152   | 203.0.113.5:50001 | TCP      | 93.184.216.34:80  | 300s    |

- Sends the packet to the internet.

### 3. Packet Delivery
The web server sees the packet as coming from `203.0.113.5:50001` and responds:
- **Source**: `93.184.216.34:80`
- **Destination**: `203.0.113.5:50001`

### 4. Reverse Translation (Inbound)
The modem/router:
- Checks its NAT table.
- Rewrites the destination:
- Old: `203.0.113.5:50001`
- New: `192.168.1.10:49152`
- Forwards the packet to your PC via the cable.

### 5. Session Tracking
The NAT table entry is temporary, expiring after a timeout (e.g., 30s for UDP, longer for TCP).

## Technical Details
- **PAT (Overload)**: Your setup uses PAT, where many private IPs share one public IP via port mappings.
- **Stateful**: NAT remembers active connections to reverse-translate replies.
- **Ports**: Ephemeral ports (e.g., 49152-65535) are used for outbound connections.
- **Checksums**: Adjusted to maintain packet integrity post-translation.

## Why NAT Matters
1. **IPv4 Conservation**: Your PC and other devices (e.g., `192.168.1.11`) share `203.0.113.5`, stretching the limited IPv4 space.
2. **Security**: Private IPs aren’t directly reachable from the internet.
3. **Scalability**: Add devices without needing more public IPs.

## Further Reading
- [RFC 1918](https://tools.ietf.org/html/rfc1918) - Private IP ranges
- [NAT on Wikipedia](https://en.wikipedia.org/wiki/Network_address_translation)

## Animated youtube video
- [NAT Explained](https://www.youtube.com/watch?v=FTUV0t6JaDA)

---
