---
share_link: https://share.note.sx/vainksu0#BirMyEU2vdMMs0qLnsf8SizF9yCeSZhaEcaoZoQQUUw
share_updated: 2024-08-29T00:11:33+05:30
---
# What is the OSI model?


![OSI model](https://www.bing.com/th?id=OSK.HEROv_MZsEKcfuN21wq0UFQh61feieKNC8Km3Wjc6fPN2Nk&pid=cdx&w=320&h=189&c=7)

Certainly! The **Open Systems Interconnection (OSI) model** is a conceptual framework that standardizes how computer networks function. [It divides network communication into **seven distinct layers**, each with specific protocols and functions](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)[1](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)[2](https://www.fortinet.com/resources/cyberglossary/osi-model)[3](https://builtin.com/articles/osi-model-layers)[4](https://networkengineering101.com/understanding-the-osi-model-for-effective-networking/)[5](https://www.geeksforgeeks.org/open-systems-interconnection-model-osi/):

1. **Physical Layer**: Deals with physical connections (cables, switches, etc.). It transmits raw bits over the network.
2. **Data Link Layer**: Ensures reliable communication between directly connected nodes. It handles framing, addressing, and error detection.
3. **Network Layer**: Manages routing and forwarding of data packets. IP addresses and routing protocols operate here.
4. **Transport Layer**: Provides end-to-end communication. Segments data, handles flow control, and ensures reliable delivery (e.g., TCP).
5. **Session Layer**: Establishes, maintains, and terminates communication sessions between applications.
6. **Presentation Layer**: Translates data formats between applications. Encryption, compression, and data conversion occur here.
7. **Application Layer**: Represents user applications (e.g., HTTP, SMTP). It interacts directly with end-user software.

Remember, the OSI model isn’t a strict set of rules; it’s a tool for understanding network functionality. Feel free to ask if you need more details! 😊

### Best way to remember all the layers
- **Please** | Physical Layer - Frames are converted into bits and transmitted physically.
- **Do** | Data Link Layer -  Packets are framed and sent to the next device.
- **Not** | Network Layer - Segments are packaged into packets and routed.
- **Tell** (the) | Transport Layer - Data is broken into segments for reliable delivery.
- **Secret** | Session Layer - Connections are established and managed.
- **Password** (to) | Presentation Layer -  Data is formatted and encrypted.
- **Anyone** | Application Layer - Applications create the data.
---
# Application Layer
It is implemented in the software mainly. The application which will access the internet through the othe layers.

Application Layer is the topmost layer in the Open System Interconnection (OSI) model. This layer provides several ways for manipulating the data (information) which actually enables any type of user to access network with ease. This layer also makes a request to its bottom layer, which is presentation layer for receiving various types of information from it.

The Application Layer interface directly interacts with application and provides common web application services. This layer is basically highest level of open system, which provides services directly for application process.
- Application Layer provides a facility by which users can forward several emails and it also provides a storage facility.
- This layer allows users to access, retrieve and manage files in a remote computer.
- It allows users to log on as a remote host.
- This layer provides access to global information about various services.
- This layer provides services which include: e-mail, transferring files, distributing results to the user, directory services, network resources and so on.
- It provides protocols that allow software to send and receive information and present meaningful data to users.
- It handles issues such as network transparency, resource allocation and so on.
- This layer serves as a window for users and application processes to access network services.
- Application Layer is basically not a function, but it performs application layer functions.
- The application layer is actually an abstraction layer that specifies the shared protocols and interface methods used by hosts in a communication network.
- Application Layer helps us to identify communication partners, and synchronizing communication.
- This layer allows users to interact with other software applications.
- In this layer, data is in visual form, which makes users truly understand data rather than remembering or visualize the data in the binary format (0’s or 1’s).
- This application layer basically interacts with Operating System (OS) and thus further preserves the data in a suitable manner.
- This layer also receives and preserves data from it’s previous layer, which is Presentation Layer (which carries in itself the syntax and semantics of the information transmitted).
- The protocols which are used in this application layer depend upon what information users wish to send or receive.
- This application layer, in general, performs host initialization followed by remote login to hosts.
##### Application Layer Protocols
The application layer provides several protocols which allow any software to easily send and receive information and present meaningful data to its users. The following are some of the [application layer protocols](https://www.geeksforgeeks.org/protocols-application-layer/).

- ****TELNET:**** [Telnet](https://www.geeksforgeeks.org/introduction-to-telnet/) stands for Telecommunications Network. This protocol is used for managing files over the Internet. It allows the Telnet clients to access the resources of Telnet server. Telnet uses port number 23.
- [****DNS:****](https://www.geeksforgeeks.org/domain-name-system-dns-in-application-layer/) DNS stands for Domain Name System. The DNS service translates the domain name (selected by user) into the corresponding IP address. For example- If you choose the domain name as www.abcd.com, then DNS must translate it as 192.36.20.8 (random IP address written just for understanding purposes). DNS protocol uses the port number 53.
- [****DHCP:****](https://www.geeksforgeeks.org/dynamic-host-configuration-protocol-dhcp/) DHCP stands for Dynamic Host Configuration Protocol. It provides IP addresses to hosts. Whenever a host tries to register for an IP address with the DHCP server, DHCP server provides lots of information to the corresponding host. DHCP uses port numbers 67 and 68.
- [****FTP:****](https://www.geeksforgeeks.org/file-transfer-protocol-ftp-in-application-layer/) FTP stands for File Transfer Protocol. This protocol helps to transfer different files from one device to another. FTP promotes sharing of files via remote computer devices with reliable, efficient data transfer. FTP uses port number 20 for data access and port number 21 for data control.
- [****SMTP:****](https://www.geeksforgeeks.org/simple-mail-transfer-protocol-smtp/) SMTP stands for Simple Mail Transfer Protocol. It is used to transfer electronic mail from one user to another user. SMTP is used by end users to send emails with ease. SMTP uses port numbers 25 and 587.
- [****HTTP:****](https://www.geeksforgeeks.org/http-full-form/) HTTP stands for Hyper Text Transfer Protocol. It is the foundation of the World Wide Web (WWW). HTTP works on the client server model. This protocol is used for transmitting hypermedia documents like HTML. This protocol was designed particularly for the communications between the web browsers and web servers, but this protocol can also be used for several other purposes. HTTP is a stateless protocol (network protocol in which a client sends requests to server and server responses back as per the given state), which means the server is not responsible for maintaining the previous client’s requests. HTTP uses port number 80.
- [****NFS:****](https://www.geeksforgeeks.org/network-file-system-nfs/) NFS stands for Network File System. This protocol allows remote hosts to mount files over a network and interact with those file systems as though they are mounted locally. NFS uses the port number 2049.
- [****SNMP:****](https://www.geeksforgeeks.org/simple-network-management-protocol-snmp/) SNMP stands for Simple Network Management Protocol. This protocol gathers data by polling the devices from the network to the management station at fixed or random intervals, requiring them to disclose certain information. SNMP uses port numbers 161 (TCP) and 162 (UDP).

---
# Presentation Layer
This layer mainly takes the data to be transfered from the application layer and translates that to the machine readable data from the ASCII format

The presentation layer is also called the ****Translation layer****. The data from the application layer is extracted here and manipulated as per the required format to transmit over the network. 
- Presentation layer format and encrypts data to be sent across the network.
- This layer takes care that the data is sent in such a way that the receiver will understand the information (data) and will be able to use the data efficiently and effectively.
- This layer manages the abstract data structures and allows high-level data structures (example- banking records), which are to be defined or exchanged.
- This layer carries out the encryption at the transmitter and decryption at the receiver.
- This layer carries out data compression to reduce the bandwidth of the data to be transmitted (the primary goal of data compression is to reduce the number of bits which is to be transmitted).
- This layer is responsible for interoperability (ability of computers to exchange and make use of information) between encoding methods as different computers use different encoding methods.
- This layer basically deals with the presentation part of the data.
- Presentation layer, carries out the data compression (number of bits reduction while transmission), which in return improves the data throughput.
- This layer also deals with the issues of string representation.
- The presentation layer is also responsible for integrating all the formats into a standardized format for efficient and effective communication.
- This layer encodes the message from the user-dependent format to the common format and vice-versa for communication between dissimilar systems.
- This layer deals with the syntax and semantics of the messages.
- This layer also ensures that the messages which are to be presented to the upper as well as the lower layer should be standardized as well as in an accurate format too.
- Presentation layer is also responsible for translation, formatting, and delivery of information for processing or display.
- This layer also performs serialization (process of translating a data structure or an object into a format that can be stored or transmitted easily).

###### **Presentation Layer Protocols :**  
Presentation layer being the 6th layer, but the most important layer in the OSI model performs several types of functionalities, which makes sure that data which is being transferred or received should be accurate or clear to all the devices which are there in a closed network.  
Presentation Layer, for performing translations or other specified functions, needs to use certain protocols which are defined below –

- [**Apple Filing Protocol (AFP):**](https://www.geeksforgeeks.org/afp-fullform/) Apple Filing Protocol is the proprietary network protocol (communications protocol) that offers services to macOS or the classic macOS. This is basically the network file control protocol specifically designed for Mac-based platforms.
- **Lightweight Presentation Protocol (LPP):** Lightweight Presentation Protocol is that protocol which is used to provide ISO presentation services on the top of TCP/IP based protocol stacks.
- [**NetWare Core Protocol (NCP):**](https://www.geeksforgeeks.org/introduction-of-novell-netware/) NetWare Core Protocol is the network protocol which is used to access file, print, directory, clock synchronization, messaging, remote command execution and other network service functions.
- **Network Data Representation (NDR):** Network Data Representation is basically the implementation of the presentation layer in the OSI model, which provides or defines various primitive data types, constructed data types and also several types of data representations.
- **External Data Representation (XDR):** External Data Representation (XDR) is the standard for the description and encoding of data. It is useful for transferring data between computer architectures and has been used to communicate data between very diverse machines. Converting from local representation to XDR is called encoding, whereas converting XDR into local representation is called decoding.
- [**Secure Socket Layer (SSL):**](https://www.geeksforgeeks.org/secure-socket-layer-ssl/) The Secure Socket Layer protocol provides security to the data that is being transferred between the web browser and the server. SSL encrypts the link between a web server and a browser, which ensures that all data passed between them remains private and free from attacks.

###### Functions of the Presentation Layer
- ****Translation:**** For example, [ASCII to EBCDIC](https://www.geeksforgeeks.org/difference-between-ascii-and-ebcdic).
- ****Encryption/ Decryption:**** Data encryption translates the data into another form or code. The encrypted data is known as the ciphertext and the decrypted data is known as plain text. A key value is used for encrypting as well as decrypting data.
- ****Compression:**** Reduces the number of bits that need to be transmitted on the network.

Note: ****Device or Protocol Use:****  JPEG, MPEG, GIF.

---
# Session Layer
**Working of Session Layer :**  
Session Layer, which is the 5th layer in the OSI model, uses the services provided by The transport layer, enables applications to establish and maintain sessions and to synchronize the sessions.   
Now, in order to establish a session connection, several things should be followed.

First thing is we should map the session address to the shipping address. The second thing is that we need to select the required transport quality of service (also referred as QoS) parameters. Next thing is we need to take care of the negotiations which should happen between session parameters. Then we further need to transmit limited transparent user data. Then at last, we need to monitor Data Transfer phase properly. The ability to send larger amount of data files is extremely important and a necessary thing too.

**Functions of Session Layer :**  
The session layer being the fifth layer in the OSI model performs several different as well as important functions which are need for establishing as well as maintaining a safe and secure connection.

- Session Layer works as a dialog controller through which it allows systems to communicate in either half-duplex mode or full duplex mode of communication.
- This layer is also responsible for token management, through which it prevents two users to simultaneously access or attempting the same critical operation.
- This layer allows synchronization by allowing the process of adding checkpoints, which are considered as synchronization points to the streams of data.
- This layer is also responsible for session checkpointing and recovery.
- This layer basically provides a mechanism of opening, closing and managing a session between the end-user application processes.
- The services offered by Session Layer are generally implemented in application environments using remote procedure calls (RPCs).
- The Session Layer is also responsible for synchronizing information from different sources.
- This layer also controls single or multiple connections for each-end user application and directly communicates with both Presentation and transport layers.
- Session Layer creates procedures for checkpointing followed by adjournment, restart and termination.
- Session Layer uses checkpoints to enable communication sessions which are to be resumed from that particular checkpoint at which communication failure has occurred.
- The session Layer is responsible for fetching or receiving data information from its previous layer (transport layer) and further sends data to the layer after it (presentation layer).
###### **Session Layer Protocols :**  
Session Layer uses some protocols which are required for safe, secure and accurate communication which exists between two-ender user applications.  
Following are some of the protocols provided or used by the Session Layer –

- [**AppleTalk Data Stream Protocol (ADSP):**](https://www.geeksforgeeks.org/adsp-fullform/) ADSP is that type of protocol which was developed by Apple Inc. and it includes a number of features that allow local area networks to be connected with no prior setup. This protocol was released in 1985.   
    This protocol rigorously followed the OSI model of protocol layering. ADSP itself has two protocols named: AppleTalk Address Resolution Protocol (AARP) and Name Binding Protocol (NBP), both aimed at making system self-configuring.
- [**Real-time Transport Control Protocol (RTCP):**](https://www.geeksforgeeks.org/real-time-transport-control-protocol-rtcp/) RTCP is a protocol which provides out-of-band statistics and control information for an RTP (Real-time Transport Protocol) session. RTCP’s primary function is to provide feedback on the quality of service (QoS) in media distribution by periodically sending statistical information such as transmitted octet and packet counts or packet loss to the participants in the streaming multimedia session.
- [**Point-to-Point Tunneling Protocol (PPTP):**](https://www.geeksforgeeks.org/pptp-full-form/) PPTP is a protocol which provides a method for implementing virtual private networks. PPTP uses a TCP control channel and a Generic Routing Encapsulation tunnel to encapsulate PPP (Point-to-Point Protocol) packets This protocol provides security levels and remote access levels comparable with typical VPN (Virtual Private Network) products.
- [**Password Authentication Protocol (PAP):**](https://www.geeksforgeeks.org/password-authentication-protocol-pap/) Password Authentication Protocol is a password-based authentication protocol used by Point to Point Protocol (PPP) to validate users. Almost all network operating systems, remote servers support PAP. PAP authentication is done at the time of the initial link establishment and verifies the identity of the client using a two-way handshake (Client-sends data and server in return sends Authentication-ACK (Acknowledgement) after the data sent by client is verified completely).
- [**Remote Procedure Call Protocol (RPCP):**](https://www.geeksforgeeks.org/remote-procedure-call-rpc-in-operating-system/) Remote Procedure Call Protocol (RPCP) is a protocol that is used when a computer program causes a procedure (or a sub-routine) to execute in a different address space without the programmer explicitly coding the details for the remote interaction. This is basically the form of client-server interaction, typically implemented via a request-response message-passing system.
- **Sockets Direct Protocol (SDP):** Sockets Direct Protocol (SDP) is a protocol that supports streams of sockets over Remote Direct Memory Access (RDMA) network fabrics.  
    The purpose of SDP is to provide an RDMA-accelerated alternative to the TCP protocol. The primary goal is to perform one particular thing in such a manner which is transparent to the application.

---

# Transport Layer
The transport layer provides services to the application layer and takes services from the network layer. The data in the transport layer is referred to as __Segments__. It is responsible for the end-to-end delivery of the complete message. The transport layer also provides the acknowledgment of the successful data transmission and re-transmits the data if an error is found.

****At the sender’s side:**** The transport layer receives the formatted data from the upper layers, performs ****Segmentation****, and also implements ****Flow and error control**** to ensure proper data transmission. It also adds Source and Destination [port number](https://www.geeksforgeeks.org/what-is-ports-in-networking)s in its header and forwards the segmented data to the Network Layer. 

> ****Note:**** The sender needs to know the port number associated with the receiver’s application. 
> 
> Generally, this destination port number is configured, either by default or manually. For example, when a web application requests a web server, it typically uses port number 80, because this is the default port assigned to web applications. Many applications have default ports assigned. 

****At the receiver’s side:**** Transport Layer reads the port number from its header and forwards the Data which it has received to the respective application. It also performs sequencing and reassembling of the segmented data. 

###### Functions of the Transport Layer 

- ****Segmentation and Reassembly:**** This layer accepts the message from the (session) layer, and breaks the message into smaller units. Each of the segments produced has a header associated with it. The transport layer at the destination station reassembles the message.
- ****Service Point Addressing:**** To deliver the message to the correct process, the transport layer header includes a type of address called service point address or port address. Thus by specifying this address, the transport layer makes sure that the message is delivered to the correct process.

###### Services Provided by Transport Layer 

- [Connection-Oriented Service](https://www.geeksforgeeks.org/connection-oriented-service)
- [Connectionless Service](https://www.geeksforgeeks.org/connection-less-service)

****1. Connection-Oriented Service:**** It is a three-phase process that includes:

- Connection Establishment
- Data Transfer
- Termination/disconnection

In this type of transmission, the receiving device sends an acknowledgment, back to the source after a packet or group of packets is received. This type of transmission is reliable and secure.

****2. Connectionless service:**** It is a one-phase process and includes Data Transfer. In this type of transmission, the receiver does not acknowledge receipt of a packet. This approach allows for much faster communication between devices. Connection-oriented service is more reliable than connectionless Service.

> ***Note:***
> 
> - Data in the Transport Layer is called ****Segments****. 
> - Transport layer is operated by the Operating System. It is a part of the OS and communicates with the Application Layer by making system calls. 
> - The transport layer is called as ****Heart of the OSI**** model. 
> - ****Device or Protocol Use :**** TCP, UDP  NetBIOS, PPTP

---
# Network Layer
The [network layer](https://www.cloudflare.com/learning/network-layer/what-is-the-network-layer/) is responsible for facilitating data transfer between two different networks. If the two devices communicating are on the same network, then the network layer is unnecessary. The network layer breaks up segments from the transport layer into smaller units, called [packets](https://www.cloudflare.com/learning/network-layer/what-is-a-packet/), on the sender’s device, and reassembling these packets on the receiving device. The network layer also finds the best physical path for the data to reach its destination; this is known as [routing](https://www.cloudflare.com/learning/network-layer/what-is-routing/).

Network layer protocols include IP, the [Internet Control Message Protocol (ICMP)](https://www.cloudflare.com/learning/ddos/glossary/internet-control-message-protocol-icmp/), the [Internet Group Message Protocol (IGMP)](https://www.cloudflare.com/learning/network-layer/what-is-igmp/), and the [IPsec](https://www.cloudflare.com/learning/network-layer/what-is-ipsec/) suite.

###### Function of the network layer
**Logical addressing:** Breaking down everything in form of **data packets** and sending that over another network using **IP addressing**, which is called logical addressing. These types of data packets are called **IP PACKETS**, which contains both the sender and also the receivers IP.


---
# Data Link Layer
The data link layer is very similar to the network layer, except the data link layer facilitates data transfer between two devices on the _same_ network. The data link layer takes packets from the network layer and breaks them into smaller pieces called frames. Like the network layer, the data link layer is also responsible for flow control and error control in intra-network communication (The transport layer only does flow control and error control for inter-network communications).

---
# Physical Layer
This layer includes the physical equipment involved in the data transfer, such as the cables and [switches](https://www.cloudflare.com/learning/network-layer/what-is-a-network-switch/). This is also the layer where the data gets converted into a bit stream, which is a string of 1s and 0s. The physical layer of both devices must also agree on a signal convention so that the 1s can be distinguished from the 0s on both devices.

---

# How the network traffic actually works

So basically lets assume we want to send a data to another machine, then the execution order will be as the same of below

```bash
Your Machine (Starts here, TO down)    Other Machine
     |                                       |
Application                            Application
	  |                                       |
Presentaion                            Presentation
	  |                                       |
Session                                  Session
     |                                       |
Transport                                Transport
     |                                       | 
Network                                    Network
     |                                       |
Data-link                                 Data-link
     |                                       |
Physical  ------------>>>------------  Physical (from here, To top)
 
```

So it looks like a loop.




