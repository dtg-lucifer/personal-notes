---
share_link: https://share.note.sx/ki8mw3ek#c5H5pW8TL60joIfuP7fDKnLMGi7bZqFA1g5nbH9jNEI
share_updated: 2024-09-17T13:50:11+05:30
---

# What is subnet? 

Subnet is a way to break a big network into smaller pieces of network of devices or hosts, just like we have our home network.

Refer to - [[005_tcp_ip_model#What is Subnet?]]

---
# Classful and classless ip addressing

**Classful IP addressing** and **classless IP addressing** are two different methods used to allocate and manage IP addresses within a network.

### Classful IP Addressing

[Classful addressing divides the IP address space into fixed classes (A, B, C, D, E), each with predefined ranges and subnet masks](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[1](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[2](https://www.networkstraining.com/classful-vs-classless-ip-addressing/). Here are the main characteristics:

- **Class A**: 1.0.0.0 to 126.0.0.0, with a default subnet mask of 255.0.0.0.
- **Class B**: 128.0.0.0 to 191.255.0.0, with a default subnet mask of 255.255.0.0.
- **Class C**: 192.0.0.0 to 223.255.255.0, with a default subnet mask of 255.255.255.0.
- **Class D**: 224.0.0.0 to 239.255.255.255, used for multicast.
- **Class E**: 240.0.0.0 to 255.255.255.255, reserved for future use.

[Classful addressing was simple but inefficient, as it often led to wasted IP addresses due to its rigid structure](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[1](https://www.geeksforgeeks.org/classful-vs-classless-addressing/).

### Classless IP Addressing

[Classless addressing, also known as **Classless Inter-Domain Routing (CIDR)**, offers more flexibility by allowing IP addresses to be allocated based on need rather than fixed classes](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[1](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[2](https://www.networkstraining.com/classful-vs-classless-ip-addressing/). Key features include:

- **Variable-Length Subnet Mask (VLSM)**: Allows for more efficient use of IP address space by enabling subnets of varying sizes.
- **CIDR Notation**: Uses a suffix to indicate the number of bits in the subnet mask (e.g., 192.168.1.0/24).

[This method helps optimize address allocation and supports the growth of the internet by efficiently managing IP address resources](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[2](https://www.networkstraining.com/classful-vs-classless-ip-addressing/).

If you have more questions or need further details, feel free to ask!

[](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[1](https://www.geeksforgeeks.org/classful-vs-classless-addressing/): [](https://www.geeksforgeeks.org/classful-vs-classless-addressing/)[2](https://www.networkstraining.com/classful-vs-classless-ip-addressing/):

---
# Classes of IP addresses

IPv4 addresses are divided into five classes: A, B, C, D, and E. Each class has a specific range and purpose:

1. **Class A**:
    
    - **Range**: 1.0.0.0 to 126.0.0.0
    - **Default Subnet Mask**: 255.0.0.0
    - **Usage**: Large networks with many devices (e.g., large organizations).
2. **Class B**:
    
    - **Range**: 128.0.0.0 to 191.255.0.0
    - **Default Subnet Mask**: 255.255.0.0
    - **Usage**: Medium-sized networks (e.g., universities, multinational companies).
3. **Class C**:
    
    - **Range**: 192.0.0.0 to 223.255.255.0
    - **Default Subnet Mask**: 255.255.255.0
    - **Usage**: Small networks (e.g., small businesses, home networks).
4. **Class D**:
    
    - **Range**: 224.0.0.0 to 239.255.255.255
    - **Usage**: Multicast groups (used for one-to-many communication).
5. **Class E**:
    
    - **Range**: 240.0.0.0 to 255.255.255.255
    - **Usage**: Experimental purposes (reserved for future use).

[Additionally, there are private IP address ranges within these classes that are used for internal networks and are not routable on the internet](https://www.meridianoutpost.com/resources/articles/IP-classes.php)[1](https://www.meridianoutpost.com/resources/articles/IP-classes.php)[2](https://www.computernetworkingnotes.com/networking-tutorials/ip-address-classes-explained-with-examples.html).

[If you have any more questions or need further details, feel free to ask!](https://www.meridianoutpost.com/resources/articles/IP-classes.php) [1](https://www.meridianoutpost.com/resources/articles/IP-classes.php): [](https://www.meridianoutpost.com/resources/articles/IP-classes.php)[2](https://www.computernetworkingnotes.com/networking-tutorials/ip-address-classes-explained-with-examples.html):

---

# RFC 1918

RFC 1918, titled “Address Allocation for Private Internets,” was introduced to address the issue of IPv4 address exhaustion. As the number of devices connected to the internet grew, the pool of available public IP addresses began to deplete. To mitigate this, RFC 1918 reserved specific IP address ranges for private use within local networks, which do not require globally unique IP addresses.

### Private IP Ranges According to RFC 1918

RFC 1918 defines three blocks of IP addresses for private use, corresponding to different classes:

- **Class A**: 10.0.0.0 to 10.255.255.255 (10/8 prefix)
- **Class B**: 172.16.0.0 to 172.31.255.255 (172.16/12 prefix)
- [**Class C**: 192.168.0.0 to 192.168.255.255 (192.168/16 prefix)](https://usercomp.com/news/1188080/rfc1918-private-ip-addresses) [1](https://usercomp.com/news/1188080/rfc1918-private-ip-addresses)[2](https://fixflux.com/rfc1918/)

### How It Solved IP Exhaustion

By using these private IP ranges, organizations can assign IP addresses within their internal networks without consuming public IP addresses. Devices within these private networks communicate with the internet through a process called Network Address Translation (NAT), which translates private IP addresses to a public IP address when accessing external networks. This approach significantly reduces the demand for public IP addresses and helps manage the limited IPv4 address space more efficiently.

If you have any more questions about networking or need further details, feel free to ask!

---
# How to subnet a network ?

To break down the network `192.168.1.0/24` into 4 different subnets, you need to perform subnetting. Here’s a step-by-step guide to achieve this:
### Step-by-Step Subnetting
1. **Determine the Number of Subnets Needed**:
    - You need 4 subnets.
2. **Calculate the Number of Bits to Borrow**:
    - To create 4 subnets, you need to borrow 2 bits from the host portion because (2^2 = 4).
3. **New Subnet Mask**:
    - Original subnet mask: `255.255.255.0` (or `/24` in CIDR notation).
    - Borrowing 2 bits for subnetting changes the subnet mask to `255.255.255.192` (or `/26` in CIDR notation).
4. **Calculate the Subnet Addresses**:
    - Each subnet will have (2^{6} = 64) addresses (since 6 bits are left for hosts).
### Subnet Calculation
- **Subnet 1**:
    - Network Address: `192.168.1.0`
    - First Usable IP: `192.168.1.1`
    - Last Usable IP: `192.168.1.62`
    - Broadcast Address: `192.168.1.63`
- **Subnet 2**:
    - Network Address: `192.168.1.64`
    - First Usable IP: `192.168.1.65`
    - Last Usable IP: `192.168.1.126`
    - Broadcast Address: `192.168.1.127`
- **Subnet 3**:
    - Network Address: `192.168.1.128`
    - First Usable IP: `192.168.1.129`
    - Last Usable IP: `192.168.1.190`
    - Broadcast Address: `192.168.1.191`
- **Subnet 4**:
    - Network Address: `192.168.1.192`
    - First Usable IP: `192.168.1.193`
    - Last Usable IP: `192.168.1.254`
    - Broadcast Address: `192.168.1.255`
### Summary
- **Subnet Mask**: `255.255.255.192`
- **CIDR Notation**: `/26`
- **Number of Subnets**: 4
- **Number of Hosts per Subnet**: 62 usable IP addresses (64 total, minus 2 for network and broadcast addresses)
This approach ensures that you have 4 subnets, each with 62 usable IP addresses. If you have any more questions or need further clarification, feel free to ask!

---

# Let's subnet *48.25.24.71/21*

To determine the network address, broadcast address, and network range for the subnet `48.25.24.71/21`, let’s break it down step-by-step.
### Step-by-Step Calculation
1. **Identify the Subnet Mask**:
    - A `/21` subnet mask in CIDR notation corresponds to `255.255.248.0`.
2. **Convert the IP Address to Binary**:
    - IP Address: `48.25.24.71`
    - Binary: `00110000.00011001.00011000.01000111`
3. **Apply the Subnet Mask**:
    - Subnet Mask: `255.255.248.0`
    - Binary: `11111111.11111111.11111000.00000000`
4. **Calculate the Network Address**:
    - Perform a bitwise AND operation between the IP address and the subnet mask.
    - Network Address: `48.25.24.0`
    - Binary: `00110000.00011001.00011000.00000000`
5. **Calculate the Broadcast Address**:
    - Invert the subnet mask to get the wildcard mask: `0.0.7.255`
    - Binary: `00000000.00000000.00000111.11111111`
    - Perform a bitwise OR operation between the network address and the wildcard mask.
    - Broadcast Address: `48.25.31.255`
    - Binary: `00110000.00011001.00011111.11111111`

### Network Range
- **Network Address**: `48.25.24.0`
- **First Usable IP**: `48.25.24.1`
- **Last Usable IP**: `48.25.31.254`
- **Broadcast Address**: `48.25.31.255`

### Summary
- **Network Address**: `48.25.24.0`
- **Broadcast Address**: `48.25.31.255`
- **Network Range**: `48.25.24.0 - 48.25.31.255`

This subnet provides a range of IP addresses from `48.25.24.0` to `48.25.31.255`, with `48.25.24.0` as the network address and `48.25.31.255` as the broadcast address. The usable IP addresses range from `48.25.24.1` to `48.25.31.254`.

If you have any more questions or need further clarification, feel free to ask!