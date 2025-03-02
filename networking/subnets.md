# Understanding IP Subnetting

Subnetting is a fundamental concept in networking that divides an IP address space into smaller, manageable segments. This guide covers how IPs are split, subnet structures, IP classes, network/broadcast addresses, and the benefits of subnetting.

## How an IP is Split into Network and Hosts

An IP address (e.g., `192.168.1.10`) is a 32-bit binary number, typically written in dotted-decimal notation. It’s divided into two parts:

- **Network Portion**: Identifies the network a device belongs to.
- **Host Portion**: Identifies a specific device within that network.

The split is determined by a **subnet mask**, which is also 32 bits long. For example:
- Subnet mask: `255.255.255.0` (or `/24` in CIDR notation) means the first 24 bits are for the network, leaving 8 bits for hosts.
- In binary: `11111111.11111111.11111111.00000000`.

For `192.168.1.10/24`:
- Network: `192.168.1.0` (first 24 bits define the network).
- Host: `.10` (last 8 bits identify the host).

The number of host bits determines how many devices can exist in the subnet (2ⁿ - 2, where n is the number of host bits, subtracting 2 for network and broadcast addresses).

## What the Subnet Looks Like

A subnet is a range of IP addresses defined by the network address and subnet mask. For example:
- IP: `192.168.1.10`
- Subnet Mask: `255.255.255.0` (`/24`)
- Subnet Range: `192.168.1.0` to `192.168.1.255`
  - `192.168.1.0` = Network address (unusable by hosts).
  - `192.168.1.255` = Broadcast address (unusable by hosts).
  - Usable hosts: `192.168.1.1` to `192.168.1.254` (254 devices).

Smaller subnets can be created by "borrowing" host bits. For instance, `/26` (255.255.255.192) splits the `/24` into 4 subnets, each with 62 usable IPs.

## IP Classes (A, B, C)

Originally, IP addresses were divided into classes based on the first octet. Subnet masks were implied:

- **Class A**:
  - Range: `1.0.0.0` to `126.0.0.0`
  - Default Mask: `255.0.0.0` (`/8`)
  - Network Bits: 8, Host Bits: 24
  - Hosts per network: ~16.7 million (2²⁴ - 2)
  - Example: `10.1.2.3`

- **Class B**:
  - Range: `128.0.0.0` to `191.255.0.0`
  - Default Mask: `255.255.0.0` (`/16`)
  - Network Bits: 16, Host Bits: 16
  - Hosts per network: ~65,534 (2¹⁶ - 2)
  - Example: `172.16.1.2`

- **Class C**:
  - Range: `192.0.0.0` to `223.255.255.0`
  - Default Mask: `255.255.255.0` (`/24`)
  - Network Bits: 24, Host Bits: 8
  - Hosts per network: 254 (2⁸ - 2)
  - Example: `192.168.1.10`

*Note*: Classful addressing is largely replaced by CIDR (Classless Inter-Domain Routing), allowing flexible subnet masks.

## Network and Broadcast IPs Within a Subnet

Every subnet reserves two special addresses:
- **Network Address**: The first IP in the range, used to identify the subnet itself (e.g., `192.168.1.0` in a `/24`).
- **Broadcast Address**: The last IP, used to send data to all devices in the subnet (e.g., `192.168.1.255` in a `/24`).

For a `/26` subnet like `192.168.1.64 - 192.168.1.127`:
- Network: `192.168.1.64`
- Broadcast: `192.168.1.127`
- Usable IPs: `192.168.1.65` to `192.168.1.126`

## Advantages of Subnetting

1. **Efficient IP Usage**: Divides large IP blocks into smaller segments, reducing waste.
2. **Improved Security**: Isolates network segments, limiting unauthorized access or attack spread.
3. **Better Performance**: Reduces broadcast traffic by confining it to smaller subnets.
4. **Simplified Management**: Organizes networks logically (e.g., by department or location).
5. **Scalability**: Allows networks to grow without requiring massive readdressing.

## Animated youtube video
- [Subnet Mask Explained](https://www.youtube.com/watch?v=s_Ntt6eTn94)
