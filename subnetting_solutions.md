# Part 2: Basic Networking & Subnetting

## Section A: Theory Questions

### Q1. Define the following terms

**IP Address**  
An IP address is a unique logical address assigned to a device on a network so it can be identified and communicate with other devices.  
Example: `192.168.1.10`

**Subnet Mask**  
A subnet mask is used to separate the network portion of an IP address from the host portion. It helps devices know whether another device is on the same network or a different one.  
Example: `255.255.255.0`

**Default Gateway**  
A default gateway is the router address that a device uses to send traffic to other networks, such as the internet.  
Example: `192.168.1.1`

**CIDR Notation**  
CIDR notation is a shorter way of writing the subnet mask by showing how many bits belong to the network portion.  
Example: `/24` means 24 bits are for the network.

**Broadcast Address**  
A broadcast address is the last address in a subnet. It is used to send data to all devices in that subnet.  
Example: for `192.168.1.0/24`, the broadcast address is `192.168.1.255`

---

### Q2. Classify the following IP addresses

| IP Address  | Class | Public/Private      |
| ----------- | ----- | ------------------- |
| 10.0.0.1    | A     | Private             |
| 172.16.5.10 | B     | Private             |
| 192.168.1.1 | C     | Private             |
| 8.8.8.8     | A     | Public              |
| 224.0.0.1   | D     | Special / Multicast |

**Notes:**

- Class A private range: `10.0.0.0 – 10.255.255.255`
- Class B private range: `172.16.0.0 – 172.31.255.255`
- Class C private range: `192.168.0.0 – 192.168.255.255`
- Class D is used for multicast, so it is not treated as normal public/private addressing.

---

### Q3. Explain the difference between

**IPv4 vs IPv6**

- IPv4 uses 32 bits and is written like `192.168.1.1`
- IPv6 uses 128 bits and is written like `2001:0db8::1`
- IPv6 provides a much larger number of addresses than IPv4
- IPv4 is still more common, but IPv6 is the newer standard

**TCP vs UDP**

- TCP is connection-oriented, reliable, and checks that data arrives correctly
- UDP is connectionless, faster, but does not guarantee delivery
- TCP is used for things like web pages, email, and file transfer
- UDP is used for things like streaming, gaming, and voice calls

**Static IP vs Dynamic IP (DHCP)**

- A static IP stays fixed and does not change
- A dynamic IP is assigned automatically by DHCP and may change over time
- Static IPs are often used for servers and printers
- Dynamic IPs are common for normal user devices

---

## Section B: Subnetting Exercises

### Exercise 1: Basic Subnetting

Given network: `192.168.10.0/24`  
Need: **4 equal subnets**

To create 4 subnets from `/24`, we borrow **2 bits**:

- Original: `/24`
- New: `/26`

A `/26` subnet mask is:

`255.255.255.192`

Each subnet has:

- Total addresses = `2^(32-26) = 64`
- Usable hosts = `64 - 2 = 62`

Subnet increment in the last octet:

`256 - 192 = 64`

So the subnets are:

- `192.168.10.0`
- `192.168.10.64`
- `192.168.10.128`
- `192.168.10.192`

| Subnet # | Network Address | First Usable IP | Last Usable IP | Broadcast Address | Subnet Mask     | CIDR |
| -------- | --------------- | --------------- | -------------- | ----------------- | --------------- | ---- |
| 1        | 192.168.10.0    | 192.168.10.1    | 192.168.10.62  | 192.168.10.63     | 255.255.255.192 | /26  |
| 2        | 192.168.10.64   | 192.168.10.65   | 192.168.10.126 | 192.168.10.127    | 255.255.255.192 | /26  |
| 3        | 192.168.10.128  | 192.168.10.129  | 192.168.10.190 | 192.168.10.191    | 255.255.255.192 | /26  |
| 4        | 192.168.10.192  | 192.168.10.193  | 192.168.10.254 | 192.168.10.255    | 255.255.255.192 | /26  |

#### Show your work / calculations

- Starting network: `192.168.10.0/24`
- Number of needed subnets = `4`
- Borrowed bits = `2` because `2^2 = 4`
- New prefix = `/26`
- New subnet mask = `255.255.255.192`
- Block size = `64`
- Subnet ranges increase by `64`

---

### Exercise 2: Intermediate Subnetting

Given network: `172.16.0.0/16`

We will use VLSM and assign the largest departments first.

#### 1) Engineering needs 200 hosts

Need at least 200 usable hosts.

- `/25` gives 128 total, 126 usable → not enough
- `/24` gives 256 total, 254 usable → enough

So:

- Subnet mask = `255.255.255.0`
- CIDR = `/24`

Assign:

- Network address = `172.16.0.0`
- Usable range = `172.16.0.1 - 172.16.0.254`
- Broadcast = `172.16.0.255`
- Wasted usable addresses = `254 - 200 = 54`

#### 2) HR needs 50 hosts

Need at least 50 usable hosts.

- `/27` gives 32 total, 30 usable → not enough
- `/26` gives 64 total, 62 usable → enough

So:

- Subnet mask = `255.255.255.192`
- CIDR = `/26`

Assign next available block:

- Network address = `172.16.1.0`
- Usable range = `172.16.1.1 - 172.16.1.62`
- Broadcast = `172.16.1.63`
- Wasted usable addresses = `62 - 50 = 12`

#### 3) Sales needs 25 hosts

Need at least 25 usable hosts.

- `/28` gives 16 total, 14 usable → not enough
- `/27` gives 32 total, 30 usable → enough

So:

- Subnet mask = `255.255.255.224`
- CIDR = `/27`

Assign next available block:

- Network address = `172.16.1.64`
- Usable range = `172.16.1.65 - 172.16.1.94`
- Broadcast = `172.16.1.95`
- Wasted usable addresses = `30 - 25 = 5`

#### 4) Management needs 10 hosts

Need at least 10 usable hosts.

- `/29` gives 8 total, 6 usable → not enough
- `/28` gives 16 total, 14 usable → enough

So:

- Subnet mask = `255.255.255.240`
- CIDR = `/28`

Assign next available block:

- Network address = `172.16.1.96`
- Usable range = `172.16.1.97 - 172.16.1.110`
- Broadcast = `172.16.1.111`
- Wasted usable addresses = `14 - 10 = 4`

#### Final table

| Department  | Required Hosts | Subnet Mask     | CIDR | Network Address | Usable IP Range            | Broadcast Address | Wasted Addresses |
| ----------- | -------------: | --------------- | ---- | --------------- | -------------------------- | ----------------- | ---------------: |
| Engineering |            200 | 255.255.255.0   | /24  | 172.16.0.0      | 172.16.0.1 - 172.16.0.254  | 172.16.0.255      |               54 |
| HR          |             50 | 255.255.255.192 | /26  | 172.16.1.0      | 172.16.1.1 - 172.16.1.62   | 172.16.1.63       |               12 |
| Sales       |             25 | 255.255.255.224 | /27  | 172.16.1.64     | 172.16.1.65 - 172.16.1.94  | 172.16.1.95       |                5 |
| Management  |             10 | 255.255.255.240 | /28  | 172.16.1.96     | 172.16.1.97 - 172.16.1.110 | 172.16.1.111      |                4 |

---

### Exercise 3: Troubleshooting Scenario

Given:

- IP Address: `192.168.1.150`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `192.168.1.1`

The subnet mask `255.255.255.192` is `/26`.

A `/26` subnet has blocks of 64:

- `192.168.1.0 - 192.168.1.63`
- `192.168.1.64 - 192.168.1.127`
- `192.168.1.128 - 192.168.1.191`
- `192.168.1.192 - 192.168.1.255`

The IP `192.168.1.150` falls in the subnet:

`192.168.1.128/26`

#### 1. What subnet does this computer belong to?

The computer belongs to subnet:

`192.168.1.128/26`

#### 2. What is the valid host range for this subnet?

- Network address = `192.168.1.128`
- First usable IP = `192.168.1.129`
- Last usable IP = `192.168.1.190`
- Broadcast address = `192.168.1.191`

So the valid host range is:

`192.168.1.129 - 192.168.1.190`

#### 3. Can this computer communicate with the default gateway? Why or why not?

No, it cannot communicate correctly with the default gateway.

Why:

- The computer is in subnet `192.168.1.128/26`
- The default gateway `192.168.1.1` is in subnet `192.168.1.0/26`

They are in different subnets, so the gateway is not in the same local network as the computer.

#### 4. What should be changed to fix the connectivity issue?

The default gateway should be changed to an address in the same subnet as the computer.

A correct example would be:

`192.168.1.129`

or any other valid usable IP in subnet `192.168.1.128/26` that is configured as the router interface.

---

## Summary

In this part, we learned:

- basic IP addressing concepts
- address classes
- public vs private IPs
- differences between important networking technologies
- subnetting a network into equal parts
- VLSM subnetting for departments with different host needs
- troubleshooting subnet and gateway configuration issues
