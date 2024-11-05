---
share_link: https://share.note.sx/rpys1z29#nVjSlvWCuxQznYqC626w//GWjj1hkG4i4CC5Ihjga9s
share_updated: 2024-09-17T13:53:21+05:30
---
# Network HOP
Trip a piece of data takes to go from one internet node to another on the way to its destination.

A **network hop** refers to the journey a data packet takes from one network device to another as it travels from its source to its destination. [Each hop represents a single step in this journey, typically involving routers or switches](https://en.wikipedia.org/wiki/Hop_%28networking%29)[1](https://en.wikipedia.org/wiki/Hop_%28networking%29)[2](https://networkencyclopedia.com/hop-networking/).

For example, if a data packet travels from your computer to a server on the internet, it might pass through several routers. Each time the packet moves from one router to the next, it counts as a hop. [The total number of hops can affect the speed and reliability of the data transmission](https://en.wikipedia.org/wiki/Hop_%28networking%29)[2](https://networkencyclopedia.com/hop-networking/).

If you have any more questions about networking or need further clarification, feel free to ask!

# Three way handshake
Three-step method employed by TCP to establish a secure client-server connection. Data packets with the flags SYN , SYN-ACK, and ACK are exchanged). This method is executed before any exchange of data occurs.

***Step 1. SYN:** Client Sends a message to the Server to that it would like to begin a message exchange.*
***Step 2. SYN + ACK:** Server sends a message to the client that it has received the request is ready to receive data.*
***Step 3. ACK:** The client sends a data packet indicating it is about to send data. A connection has been established.*

# DNS(Domain naming system)
**(DNS) domain name system:** A hierarchical naming system used for translating a human-readable domain name into an IP Address. A DNS server will take the domain name a client sends to it and returns the IP Address for that server.

---

**==Socket==:** A logical communication endpoint for an application formed when combining the IP address and port number.Example: 66.249.75.195:83
**==Port==:** Logical endpoint for data to be sent within a device. Port numbers are associated with web browsers and other internet-communicating web applications.

---
# TLS Handshake
**TLS handshake:** Method in which a client and server:

- Agree on the TLS version to use
- Agree on the _ciphers_ to use within a _cipher suite_
- Exchange keys for symmetric encryption
- Verify the validity of a host’s certificate

**Cipher**: Set(s) of steps for performing encryption and decryption

**Cipher Suite**: A set of ciphers

This method performs the following steps:

- Step 1. `ClientHello`: Client specifies the TLS version and cipher suites it supports, and then sends to the server.
- Step 2. `ServerHello`: Server verifies it can use the specified TLS version and cipher suite. It provides its certificate and public key, and then sends `ServerHelloDone`.
- Step 3. `Key exchange`: The client and the server exchange key data for symmetric encryption.

---
# MAC Addresses

- **MAC Address (Media Access Control Address)**:
    - A unique identifier assigned to **network interface cards (NICs)** at the **data link layer** (Layer 2) of the OSI model.
    - Composed of **48 bits** (usually represented as 12 hexadecimal digits).
    - Written in the format `XX:XX:XX:XX:XX:XX`, where each `X` represents a hexadecimal digit (0-9, A-F).
    - **Purpose**:
        - **Uniqueness**: Every NIC worldwide has a distinct MAC address.
        - **Local Network Communication**: Used for communication within a local network (e.g., Ethernet LAN).
    - **How It Works**:
        - When a device sends data, it includes its own MAC address as the **source address**.
        - Routers and switches use MAC addresses to forward data to the correct destination.
        - **ARP (Address Resolution Protocol)** maps IP addresses to MAC addresses.
    - **Types**:
        - **Unicast**: Sent to a specific NIC (one-to-one communication).
        - **Multicast**: Sent to a group of NICs (e.g., multicast groups).
        - **Broadcast**: Sent to all devices on the network (e.g., ARP requests).
    - **Changing MAC Addresses**:
        - Some devices allow users to modify their MAC addresses (e.g., for privacy or security).
        - Useful in virtualization (e.g., creating multiple VMs with unique MACs).
    - **Example**:
        - Suppose your NIC has the MAC address `00:1A:2B:3C:4D:5E`.
        - When you send data, it includes this address as the source.
        - Routers and switches use it to route the data to the correct destination.
MAC addresses are essential for local network communication.
