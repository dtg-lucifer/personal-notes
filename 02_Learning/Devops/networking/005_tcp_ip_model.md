---
share_link: https://share.note.sx/lr8wejkv#TNspbZp+Gwrec4wm4AgPrGH5FEdS0uq1heXK8mIyyOc
share_updated: 2024-09-17T13:53:33+05:30
---

---
# The INTERNET PROTOCOL SUITE

Unlike the OSI Model this model simply divides the networking into 5 layers
- [[#Application layer]]
- [[#Transport layer]]
- [[#Network layer]]
- [[#Data link layer]]
- [[#Physical layer]]

The OSI Model was mainly based on the theoritical implementation and where as this one is actually used in the real life practically.


# Application layer
It contains the main layer with which users interact with. 
Such as **Browsers and applications**
It relies on the physical devices

###### Protocols

**TCP/IP**: 
- **HTTP** - basic data flow in the internet
- **DHCP** - dynamically allocates the IP address to the data packets
- **FTP** - how the file tranfers
- **SMTP** - simple mail transfer protocol
- **POP3 & IMAC** - receive emails
- **SSH** - secure shell

**TELNET**: Port 23, this is the terminal emulation which allows to connect remote devices over TELNET

**UDP**: stateless connection



---
# Transport layer
- **Function**: Handles **process-to-process communication** (or port-to-port communication).
- **Responsibilities**:
    - **Segmentation and Reassembly**: Breaks data into smaller segments for transmission and reassembles them at the destination.
    - **Flow Control**: Ensures efficient data flow between sender and receiver.
    - **Error Detection and Correction**: Detects and corrects errors in data transmission.
    - **Port Addressing**: Adds a **port number** to the header of the data.
- **Protocols**: Common protocols at this layer include **TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)**.
- It has **Multiplexer** and **De-Multiplexer** for the passong and receiving packets accross various ports and applications
- Checksum - This is basically a unique number. Using which something can be calculated. The checksum is attached to the data packets sent over the network to make sure that the data is same or not to determine whether the data is safe or not.
- Timers - These are to make sure that the packet is been received to the other peer or not (Re transmission timers)
---
# Network layer
1. **Network Layer** (also known as the **Internet Layer**):
    
    - **Function**: Deals with **host-to-host communication**.
    - **Responsibilities**:
        - **Logical Addressing**: Adds an **IP address** (Internet Protocol address) to the packet if it crosses network boundaries.
        - **Routing**: Determines the best path for data packets to reach their destination.
        - **Packet Forwarding**: Moves packets from one network to another.
    - **Protocols**: The primary protocol at this layer is **IP (Internet Protocol)**.
---
# Data link layer

 

---
# Physical layer


---

# What is Subnet? 
A **subnet** (short for **subnetwork**) is a logical subdivision of an IP network. Subnetting is the process of dividing a large network into smaller, more manageable sub-networks. Subnets are used to improve network performance, security, and organization.
- **IP Address**: An IP address consists of two parts: the **network** portion and the **host** portion. For example, in the IP address `192.168.1.10` with a subnet mask of `255.255.255.0`, `192.168.1` represents the network, and `.10` represents the host within that network.
- **Subnet Mask**: The subnet mask determines how the IP address is divided into the network and host portions. A subnet mask like `255.255.255.0` means the first three octets (192.168.1) are the network portion, and the last octet (.10) is the host portion.

- **Purpose of Subnetting**:
    
    - **Network Organization**: Subnets help organize a large network into smaller groups, making it easier to manage and troubleshoot.
    - **Improved Performance**: By limiting the number of devices in each subnet, you can reduce broadcast traffic, which improves network performance.
    - **Enhanced Security**: Subnetting can isolate segments of a network, preventing devices on different subnets from directly communicating unless through a router or firewall, which can be configured to enforce security policies.
    - **Efficient IP Address Usage**: Subnetting allows for more efficient use of IP addresses, especially in large organizations where different departments or floors may need their own subnets.
- **CIDR Notation**:
    
    - **CIDR (Classless Inter-Domain Routing)** notation is often used to specify a subnet mask. It is written as an IP address followed by a slash and the number of bits in the network portion. For example, `192.168.1.0/24` represents a subnet with a 24-bit subnet mask (`255.255.255.0`).
- **Subnets in Action**:
    
    - Imagine a company with an IP network `192.168.0.0/16`. Instead of having all devices in a single large network, the company could create subnets like `192.168.1.0/24`, `192.168.2.0/24`, and so on, with each subnet serving a different department or office location.

### Example:

Let’s say you have an IP address `192.168.1.25` and a subnet mask of `255.255.255.0`:

- The network portion is `192.168.1`.
- The host portion is `25`. This means the IP address belongs to the subnet `192.168.1.0/24`, which can accommodate 254 hosts (from `192.168.1.1` to `192.168.1.254`).

### Summary:

A **subnet** is a logical subdivision of an IP network, created to improve network organization, performance, security, and efficient IP address utilization. Subnetting is done using a subnet mask that divides the IP address into network and host portions.