# NETWORKING LAB 01
# End Device Configuration, Hub Connectivity and Switch Configuration

**Platform:** Cisco Packet Tracer  
**Switch Model:** Cisco Catalyst 2960-24TT  
**Network Type:** Local Area Network (LAN)  
**Subnet Mask:** 255.255.255.0 (/24)  
**Status:** Initial configuration and testing completed; troubleshooting findings documented.

---

## 1. Introduction

This practical exercise focused on building a Local Area Network (LAN) using Cisco Packet Tracer.

The objective was to gain hands-on experience connecting end devices through Ethernet hubs and a central network switch, configuring IPv4 addresses, managing a Cisco switch through its Command Line Interface (CLI), and testing connectivity between devices.

The exercise also provided an opportunity to identify and understand network communication problems, particularly the importance of IP addressing and routing between different networks.

## 2. Objectives

The objectives of this lab were to:

1. Understand how end devices connect within a LAN.
2. Learn how Ethernet hubs and switches operate.
3. Build a network topology using Cisco Packet Tracer.
4. Configure IPv4 addresses on PCs and laptops.
5. Access and configure a Cisco 2960 switch through its CLI.
6. Test connectivity between end devices using the ping command.
7. Identify and troubleshoot network connectivity problems.
8. Understand the difference between Layer 2 switching and Layer 3 routing.

## 3. Network Topology

The network was designed with one central Cisco Catalyst 2960-24TT switch connected to three Ethernet hubs.

The hubs provided additional Ethernet connections for the end devices.

### Network segments

**Segment A**
- Hub0
- PC0
- Laptop0

**Segment B**
- Hub1
- PC6
- Laptop

**Segment C**
- Hub3
- PC2

All three hubs were connected to the central switch.
<img width="684" height="302" alt="Screenshot 2026-11-01 140653" src="https://github.com/user-attachments/assets/69a79d96-9370-4b16-a62d-a491eb5ef5a8" />


## 4. Devices and Equipment Used

| Device | Quantity | Function |
|---|---:|---|
| Cisco 2960-24TT Switch | 1 | Connects network segments and forwards Ethernet frames |
| Ethernet Hub | 3 | Repeats incoming signals to connected ports |
| Desktop PC | 3 | End-user network devices |
| Laptop | 2 | End-user network devices |
| **Total** | **9** | |

## 5. IP Addressing Configuration

The five end devices were manually configured with IPv4 addresses.

The subnet mask used was:

`255.255.255.0`

This is equivalent to `/24`.

### IP addressing table

| Segment | Device | IPv4 Address | Subnet Mask |
|---|---|---|---|
| A | PC0 | 192.168.11.4 | 255.255.255.0 |
| A | Laptop0 | 192.160.11.5 | 255.255.255.0 |
| B | PC6 | 192.160.11.7 | 255.255.255.0 |
| B | Laptop | 192.160.11.8 | 255.255.255.0 |
| C | PC2 | 192.160.11.13 | 255.255.255.0 |

**Note:** The IP addresses above reflect the actual configuration reported during the exercise. The default gateway and DNS settings have not yet been verified.

### Network identification

Based on the configured IP addresses and subnet mask, the devices belong to same ip

| Network | Network address | Devices |
|---|---|---|
| Network 1 | 192.160.11.0/24 | Laptop0, PC0, PC6, Laptop and PC2 |

This means the topology contains three physical hub-connected segments .

## 6. Configuration Process

The following activities were performed during the practical exercise:

1. Opened Cisco Packet Tracer.
2. Added one Cisco Catalyst 2960-24TT switch to the workspace.
3. Added three Ethernet hubs.
4. Added three desktop PCs and two laptops.
5. Connected the hubs to the central switch.
6. Connected the end devices to their respective hubs.
7. Configured IPv4 addresses on all five end devices.
8. Used the subnet mask `255.255.255.0`.
9. Accessed the Cisco switch through its CLI.
10. Performed switch configuration using the command-line interface.
11. Used the ping command to test connectivity between network devices.

**Configuration evidence:**


<img width="485" height="470" alt="Screenshot 2026-11-01 140654" src="https://github.com/user-attachments/assets/ed725e56-a743-48cf-a8e7-4f94466eb56d" />


<img width="479" height="458" alt="Screenshot 2026-11-01 141128" src="https://github.com/user-attachments/assets/690a68de-3a21-4cd4-be17-efa8bd5d8b67" />

<img width="476" height="476" alt="Screenshot 2026-11-01 143230" src="https://github.com/user-attachments/assets/0dd1b97a-9920-4645-aa6a-63a05f635a03" />


<img width="340" height="413" alt="Screenshot 2026-11-01 144528" src="https://github.com/user-attachments/assets/0f3d77dc-79f9-4feb-87fa-53d360a92b23" />









## 7. Testing and Verification

After configuring the end devices and switch, connectivity testing was performed.

### Test 1: Communication between Segment A and Segment B

**Source:** Device in Segment A.

**Destination:** Device in Segment B.

**Testing tool:** Command Prompt.

**Protocol:** Internet Control Message Protocol (ICMP).

**Command used:*ping 192.160.11.7*

`ping 19.160.11.7`

**Expected result:**

The destination device should respond to ICMP Echo Requests if the network configuration and routing are correct.

**Actual result:**

The ping test failed.
<img width="340" height="413" alt="Screenshot 2026-11-01 144528" src="https://github.com/user-attachments/assets/ae5b3f55-d199-40d0-a2ab-2d2ee84f5285" />


## 8. Problems Encountered

### Problem 1: Failed Communication Between Different IP Networks

**Description**

During the connectivity test, I attempted to ping a device in Segment B from a device in Segment A. The ping test was unsuccessful.

**Investigation**

I examined the IPv4 addresses assigned to the end devices and discovered that they were configured with different network addresses.

PC0 was assigned:

`192.168.10.4`

The other four devices were assigned addresses within:

`192.160.11.0/24`

All devices used the subnet mask:

`255.255.255.0`


**Root cause**

The topology did not have a configured Layer 3 routing device to provide communication .

**Technical explanation**

A Layer 2 switch forwards Ethernet frames using MAC addresses. It does not perform IP routing between different networks.

When a device wants to communicate with a destination outside its local subnet, it needs to send the traffic to its default gateway.

A router or Layer 3 switch is required to route traffic between the different IP networks.

**Proposed solution**

Introduce a router or Layer 3 switch and configure the necessary network interfaces, IP addresses and default gateways.

**Verification**

After configuring the routing device, repeat the ping test and confirm that both networks can communicate.

**Status:** Root cause identified from the addressing configuration. Router configuration and successful verification are pending.

## 9. Troubleshooting Commands

The following commands are useful for investigating this type of connectivity problem.

### End-device commands

| Command | Purpose |
|---|---|
| `ipconfig` | Displays IP configuration |
| `ping` | Tests connectivity |
| `tracert` | Traces the network path |

### Cisco switch commands

| Command | Purpose |
|---|---|
| `show running-config` | Displays the current configuration |
| `show interfaces status` | Displays switch port status |
| `show vlan brief` | Displays VLAN information |
| `show mac address-table` | Displays learned MAC addresses |
| `show ip interface brief` | Displays interface IP information and status |

## 10. Lessons Learned

Through this exercise, I learned the following:

1. How to connect multiple end devices through Ethernet hubs and a central switch.
2. How to configure IPv4 addresses and subnet masks on end devices.
3. How to access and configure a Cisco switch through its CLI.
4. The difference between a hub and a network switch.
5. How Layer 2 switches use MAC addresses to forward Ethernet frames.
6. How subnet masks help determine whether devices belong to the same IP network.
7. Why routers are necessary for communication between different IP networks.
8. Why default gateways are important when communicating with remote networks.
9. The importance of testing network connectivity and documenting problems encountered during configuration.

## 11. Future Improvements

To improve this practical exercise, I plan to:

1. Correct the IP addressing scheme and use private IPv4 addresses consistently.
2. Configure a router to enable communication between different IP networks.
3. Configure the appropriate default gateways on all end devices.
4. Perform additional ping tests within and between networks.
5. Investigate VLAN configuration and network segmentation.
6. Practise switch management and additional Cisco CLI commands.
7. Document the router configuration and troubleshooting results in a follow-up lab.

## 12. Conclusion

This lab provided practical experience building a LAN using end devices, Ethernet hubs and a Cisco Catalyst 2960 switch.

It also helped me understand the relationship between IP addressing, subnet masks, Layer 2 switching and Layer 3 routing.

One important lesson from this exercise was that connecting devices physically does not automatically guarantee communication between different IP networks. Appropriate addressing and routing configurations are essential.

Documenting the connectivity failure helped me identify an important networking concept and understand the role of routers in connecting different networks.

---

**Project:** Networking Lab 01  
**Author:** SamTech  
**Tools:** Cisco Packet Tracer  
**Next practical:** Configuring a router to enable communication between different IP networks.
