---
share_link: https://share.note.sx/01cgw2ig#ABAIY+HcXrwMILS3cFXExcWpvHa4Qro0/BhDm3FxJUw
share_updated: 2024-09-17T13:53:41+05:30
---
# What is it??

The three-way handshake is a method used in TCP (Transmission Control Protocol) to establish a connection between a client and a server. It ensures that both parties are ready to communicate and agree on the initial sequence numbers used for the data exchange. Here's how it works:

### Steps of a Three-Way Handshake

1. **SYN (Synchronize)**
   - The client initiates the connection by sending a SYN packet to the server. This packet contains a sequence number (let's say `Seq=100`) which the client intends to use in its data transmission.

2. **SYN-ACK (Synchronize-Acknowledge)**
   - The server responds to the client's SYN packet with a SYN-ACK packet. This packet acknowledges the client's sequence number by setting the acknowledgment number to `Ack=101` (which is `Seq+1`), and also includes its own sequence number (say `Seq=200`) for the data it will send.

3. **ACK (Acknowledge)**
   - The client sends an ACK packet back to the server. This packet acknowledges the server's sequence number by setting the acknowledgment number to `Ack=201` (which is `Seq+1`). This completes the handshake, and the connection is established.

### Why is the Three-Way Handshake Important?

- **Reliability**: It ensures that both the client and the server agree on the initial sequence numbers and are ready for data transmission, making the communication reliable.
- **Synchronization**: It allows both parties to synchronize their sequence numbers and buffer sizes before the actual data transmission begins.
- **Connection Establishment**: The handshake confirms that both sides are ready and able to communicate, preventing half-open or corrupted connections.

This process is fundamental to the TCP protocol and is essential for ensuring reliable communication over a network.