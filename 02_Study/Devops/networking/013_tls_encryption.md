---
share_link: https://share.note.sx/0cyvlaoa#jW2RVK60BnqM99z7pOYlSUu2HiELg6/yh5gkFle7Wz8
share_updated: 2024-09-25T12:32:41+05:30
---
### TLS Encryption

**Transport Layer Security (TLS)** is a cryptographic protocol designed to provide secure communication over a computer network. It ensures three main security properties:

1. **Confidentiality**: Encrypts data to prevent unauthorized access.
2. **Integrity**: Ensures data has not been tampered with during transmission.
3. **Authentication**: Verifies the identities of the communicating parties.

### How TLS Works

1. **Handshake**: The client and server exchange messages to agree on encryption algorithms and establish a secure session key.
2. **Session Key Generation**: Both parties generate a shared session key used for encrypting the data.
3. **Data Transfer**: Data is encrypted and decrypted using the session key, ensuring secure communication.

[TLS is widely used to secure web traffic (HTTPS), email, and other internet communications](https://en.wikipedia.org/wiki/Transport_Layer_Security)[3](https://en.wikipedia.org/wiki/Transport_Layer_Security)[4](https://www.comparitech.com/blog/information-security/tls-encryption/)

---

# How secure transmission happens

Secure data transmission in TCP/IP involves several steps, combining the reliability of TCP with the encryption provided by TLS (Transport Layer Security). Here’s a step-by-step breakdown:

### 1. Establishing a TCP Connection (Three-Way Handshake)

1. **SYN (Synchronize)**: The client sends a SYN packet to the server to initiate a connection.
2. **SYN-ACK (Synchronize-Acknowledge)**: The server responds with a SYN-ACK packet, acknowledging the client’s request.
3. **ACK (Acknowledge)**: The client sends an ACK packet back to the server, confirming the connection is established.

### 2. Initiating TLS Handshake

1. **Client Hello**: The client sends a “Client Hello” message to the server, which includes supported cipher suites and the client’s random number.
2. **Server Hello**: The server responds with a “Server Hello” message, selecting a cipher suite and sending its own random number.
3. **Server Certificate**: The server sends its digital certificate to the client for authentication.
4. **Server Key Exchange (if needed)**: The server may send a key exchange message if the chosen cipher suite requires it.
5. **Server Hello Done**: The server signals the end of its hello messages.

### 3. Client Key Exchange

1. **Client Key Exchange**: The client generates a pre-master secret, encrypts it with the server’s public key (from the server’s certificate), and sends it to the server.
2. **Change Cipher Spec**: The client sends a “Change Cipher Spec” message to indicate that subsequent messages will be encrypted.
3. **Client Finished**: The client sends a “Finished” message, encrypted with the session key derived from the pre-master secret.

### 4. Server Key Exchange

1. **Change Cipher Spec**: The server sends a “Change Cipher Spec” message to indicate that subsequent messages will be encrypted.
2. **Server Finished**: The server sends a “Finished” message, encrypted with the session key.

### 5. Secure Data Transmission

1. **Data Transfer**: Both the client and server use the session key to encrypt and decrypt the data they exchange.
2. **Integrity Check**: Each message includes a Message Authentication Code (MAC) to ensure data integrity.

### 6. Closing the Connection

1. **Client Close Notify**: The client sends a “Close Notify” message to indicate it wants to close the connection.
2. **Server Close Notify**: The server responds with a “Close Notify” message, confirming the closure.

[This process ensures that data is transmitted securely, maintaining confidentiality, integrity, and authenticity throughout the communication](https://www.avg.com/en/signal/what-is-tcp-ip)[1](https://www.avg.com/en/signal/what-is-tcp-ip)[2](https://network-guides.com/tcp-ip-basics/).

If you have any more questions or need further details, feel free to ask! 😊

[](https://www.avg.com/en/signal/what-is-tcp-ip)[1](https://www.avg.com/en/signal/what-is-tcp-ip): [](https://www.avg.com/en/signal/what-is-tcp-ip)[2](https://network-guides.com/tcp-ip-basics/):